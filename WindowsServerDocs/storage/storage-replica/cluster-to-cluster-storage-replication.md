---
title: Réplication du stockage de cluster à cluster
ms.prod: windows-server
manager: siroy
ms.author: nedpyle
ms.technology: storage-replica
ms.topic: get-started-article
ms.assetid: 834e8542-a67a-4ba0-9841-8a57727ef876
author: nedpyle
ms.date: 04/26/2019
description: Comment utiliser le réplica de stockage pour répliquer des volumes d’un cluster vers un autre cluster exécutant Windows Server.
ms.openlocfilehash: 81c1357ba3d37fcecc0aeb59a92472044bb9ce3b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71393791"
---
# <a name="cluster-to-cluster-storage-replication"></a>Réplication du stockage de cluster à cluster

> S'applique à : Windows Server 2019, Windows Server 2016, Windows Server (canal semi-annuel)

Le réplica de stockage peut répliquer des volumes entre les clusters, y compris la réplication de clusters à l’aide de espaces de stockage direct. La gestion et la configuration sont similaires à la réplication de serveur à serveur.  

Vous allez configurer ces ordinateurs et ce stockage dans une configuration de cluster à cluster, où un seul cluster réplique son propre ensemble de stockage avec un autre cluster et son ensemble de stockage. Ces nœuds et leur stockage doivent se trouver sur des sites physiques distincts, même si cela n’est pas obligatoire.  

> [!IMPORTANT]
> Dans ce test, quatre serveurs sont pris comme exemple. Vous pouvez utiliser un nombre quelconque de serveurs pris en charge par Microsoft dans chaque cluster, qui est actuellement 8 pour un cluster espaces de stockage direct et 64 pour un cluster de stockage partagé.  
>   
> Ce guide ne couvre pas la configuration des espaces de stockage direct. Pour plus d’informations sur la configuration de espaces de stockage direct, consultez [espaces de stockage direct vue d’ensemble](../storage-spaces/storage-spaces-direct-overview.md).  

Cette procédure pas à pas utilise l’environnement suivant comme exemple :  

-   Deux serveurs membres, nommés **SR-SRV01** et **SR-SRV02** qui sont intégrés ultérieurement dans un cluster nommé **SR-SRVCLUSA**.  

-   Deux serveurs membres, nommés **SR-SRV03** et **SR-SRV04** qui sont intégrés ultérieurement dans un cluster nommé **SR-SRVCLUSB**.  

-   Une paire de sites logiques qui représentent deux centres de données différents, l’un étant nommé **Redmond** et l’autre **Bellevue**.  

![Diagramme montrant un exemple d’environnement avec un cluster du site de Redmond qui se réplique sur un cluster du site de Bellevue](./media/Cluster-to-Cluster-Storage-Replication/SR_ClustertoCluster.png)  

**FIGURE 1 : réplication de cluster à cluster**  

## <a name="prerequisites"></a>Conditions préalables  

* Forêt de services de domaine Active Directory (exécution de Windows Server 2016 non nécessaire).  
* 4-128 serveurs (deux clusters de 2-64 serveurs) exécutant Windows Server 2019 ou Windows Server 2016, Datacenter Edition. Si vous exécutez Windows Server 2019, vous pouvez à la place utiliser l’édition standard si vous ne répliquez qu’un seul volume, avec une taille maximale de 2 to.  
* Deux ensembles de stockage avec JBOD SAS, SAN Fibre Channel, VHDX partagé, espaces de stockage direct ou cible iSCSI. Le stockage doit contenir un mélange de disques durs HDD et SSD. Nous allons rendre chaque ensemble de stockage disponible uniquement pour chacun des clusters, sans aucun accès partagé entre les clusters.  
* Chaque ensemble de stockage doit autoriser la création d’au moins deux disques virtuels, un pour les données répliquées et un autre pour les journaux. Le stockage physique doit avoir la même taille de secteur sur tous les disques de données. Le stockage physique doit avoir la même taille de secteur sur tous les disques de journal.  
* Au moins une connexion Ethernet/TCP sur chaque serveur pour la réplication synchrone, mais de préférence RDMA.   
* Les règles de pare-feu et de routeur appropriés pour autoriser le trafic bidirectionnel ICMP, SMB (port 445, ainsi que 5445 pour SMB Direct) et WS-MAN (port 5985) entre tous les nœuds.  
* Un réseau entre les serveurs avec une bande passante suffisante pour contenir votre charge de travail d’écriture d’E/S et une latence moyenne de parcours circulaire égale à 5 ms pour la réplication synchrone. La réplication asynchrone ne présente pas de recommandation en matière de latence.  
* Impossible de localiser le stockage répliqué sur le lecteur contenant le dossier du système d’exploitation Windows.
* Il existe des considérations importantes & limitations pour la réplication espaces de stockage direct. consultez les informations détaillées ci-dessous.

La plupart de ces exigences peuvent être déterminées à l’aide de l’applet de commande `Test-SRTopology`. Vous pouvez accéder à cet outil si vous installez un réplica de stockage ou les fonctionnalités des outils de gestion des réplicas de stockage sur au moins un serveur. Il n’est pas nécessaire de configurer de réplica de stockage pour utiliser cet outil, mais vous devez installer l’applet de commande. Vous trouverez plus d’informations dans la procédure ci-dessous.  

## <a name="step-1-provision-operating-system-features-roles-storage-and-network"></a>Étape 1 : configurer le système d’exploitation, les fonctionnalités, les rôles, le stockage et le réseau

1.  Installez Windows Server sur les quatre nœuds de serveur avec le type d’installation Windows Server **(expérience utilisateur)** . 

2.  Ajoutez des informations réseau et joignez-les au domaine, puis redémarrez-les.  

    > [!IMPORTANT]  
    > À partir de ce stade, connectez-vous toujours en tant qu’utilisateur de domaine membre du groupe Administrateurs intégré sur tous les serveurs. Pensez toujours à élever vos invites CMD et Windows PowerShell à l’avenir lors de l’exécution sur une installation de serveur graphique ou sur un ordinateur Windows 10.  

3.  Connectez le premier ensemble de boîtiers de stockage JBOD, la cible iSCSI, le SAN FC ou le stockage sur disque fixe local (DAS) au serveur du site **Redmond**.  

4.  Connectez le deuxième ensemble de stockage au serveur du site **Bellevue**.  

5.  Installez si nécessaire les derniers pilotes et microprogrammes de stockage et de boîtier du fournisseur, les derniers pilotes du fournisseur HBA, le dernier microprogramme du fournisseur de BIOS/UEFI, les derniers pilotes réseau du fournisseur et les derniers pilotes de carte mère sur les quatre nœuds. Redémarrez les nœuds si besoin.  

    > [!NOTE]  
    > Consultez la documentation de votre fournisseur de matériel pour la configuration du stockage partagé et du matériel réseau.  

6.  Vérifiez que les paramètres BIOS/UEFI des serveurs permettent de hautes performances, par exemple avec la désactivation de C-State, la définition de la vitesse de QPI, l’activation de NUMA et la définition de la fréquence mémoire la plus élevée. Vérifiez que la gestion de l’alimentation dans Windows Server est définie pour favoriser de hautes performances. Redémarrez si nécessaire.  

7.  Configurez les rôles comme suit :  

    -   **Méthode graphique**  

        1.  Exécutez **ServerManager.exe** et créez un groupe de serveurs, en ajoutant tous les nœuds de serveur.  

        2.  Installez les rôles et fonctionnalités **Serveur de fichiers** et **Réplica de stockage** sur chacun des nœuds et redémarrez-les.  

    -   **Méthode Windows PowerShell**  

        Sur SR-SRV04 ou un ordinateur de gestion à distance, exécutez la commande suivante dans une console Windows PowerShell pour installer les fonctionnalités et rôles requis pour un cluster étendu sur les quatre nœuds et redémarrez-les :  

        ```PowerShell
        $Servers = 'SR-SRV01','SR-SRV02','SR-SRV03','SR-SRV04'  

        $Servers | ForEach { Install-WindowsFeature -ComputerName $_ -Name Storage-Replica,Failover-Clustering,FS-FileServer -IncludeManagementTools -restart }  
        ```  

        Pour plus d’informations sur ces étapes, voir [Installer ou désinstaller des rôles, services de rôle ou fonctionnalités](../../administration/server-manager/install-or-uninstall-roles-role-services-or-features.md).  

9. Configurez le stockage comme suit :  

    > [!IMPORTANT]  
    > -   Vous devez créer deux volumes sur chacun des boîtiers : un pour les données et l’autre pour les journaux.  
    > -   Les disques de données et de journaux doivent être initialisés en tant que **GPT**, et non **MBR**.  
    > -   Les deux volumes de données doivent être de la même taille.  
    > -   Les deux volumes de journaux doivent être de la même taille.  
    > -   Tous les disques de données répliqués doivent avoir la même taille de secteur.  
    > -   Tous les disques de journaux doivent avoir la même taille de secteur.  
    > -   Les volumes de journaux doivent utiliser un stockage flash, comme les disques SSD.  Microsoft recommande que le stockage de journaux soit plus rapide que le stockage de données. Les volumes de journaux ne doivent jamais être utilisés pour d’autres charges de travail.
    > -   Les disques de données peuvent utiliser des disques HDD, des disques SSD ou une combinaison hiérarchisée et utiliser des espaces de parité ou en miroir, ou RAID1 ou10, ou RAID5 ou RAID50.  
    > -   Le volume du journal doit être au moins de 8 Go par défaut et peut être plus grand ou plus petit en fonction des exigences du journal.
    > -   Lors de l’utilisation de espaces de stockage direct (espaces de stockage direct) avec un cache NVME ou SSD, vous constatez une augmentation de la latence plus élevée que prévu lors de la configuration de la réplication du réplica de stockage entre les clusters espaces de stockage direct. La modification de la latence est proportionnellement plus élevée que lorsque vous utilisez NVME et SSD dans une configuration des performances et des capacités, et pas de niveau de disque dur ni de niveau de capacité.

    Ce problème se produit en raison de limitations architecturales dans le mécanisme de journalisation de SR, combinées à la latence extrêmement faible de NVME par rapport aux supports plus lents. Lorsque vous utilisez espaces de stockage direct cache espaces de stockage direct, toutes les e/s des journaux SR, ainsi que toutes les e/s de lecture/écriture récentes des applications, sont exécutées dans le cache et jamais sur les niveaux de performance ou de capacité. Cela signifie que toutes les activités SR se produisent sur le même support de vitesse : cette configuration n’est pas prise en charge non recommandée (voir https://aka.ms/srfaq pour obtenir des recommandations pour les journaux). 

    Lorsque vous utilisez espaces de stockage direct avec des disques durs, vous ne pouvez pas désactiver ou éviter le cache. En guise de solution de contournement, si vous utilisez uniquement SSD et NVME, vous pouvez configurer uniquement les niveaux de performances et de capacité. Si vous utilisez cette configuration et que vous placez les journaux SR sur le niveau de performance uniquement avec les volumes de données qu’ils utilisent uniquement sur le niveau de capacité, vous évitez le problème de latence élevée décrit ci-dessus. La même opération peut être effectuée avec une combinaison de SSD plus rapide et plus lente et aucun NVME.

    Cette solution de contournement n’est bien sûr pas idéale et certains clients peuvent ne pas être en mesure de les utiliser. L’équipe SR travaille sur des optimisations et un mécanisme de journalisation mis à jour à l’avenir pour réduire les goulots d’étranglement artificiels qui se produisent. Il n’y a pas d’ATE pour cela, mais lorsqu’il est possible de cliquer sur clients à des fins de test, cette FAQ sera mise à jour. 

-   **Pour les boîtiers JBOD :**  

1. Assurez-vous que chaque cluster peut voir uniquement les boîtiers de stockage de ce site et que les connexions SAS sont correctement configurées.  

2. Approvisionnez le stockage à l’aide d’espaces de stockage en suivant les **étapes 1 à 3** indiquées dans [Déployer des espaces de stockage sur un serveur autonome](../storage-spaces/deploy-standalone-storage-spaces.md) à l’aide de Windows PowerShell ou du Gestionnaire de serveur.  

-   **Pour le stockage cible iSCSI :**  

1. Assurez-vous que chaque cluster peut voir uniquement les boîtiers de stockage de ce site. Vous devez utiliser plusieurs cartes réseau si vous utilisez iSCSI.  

2. Configurez le stockage à l’aide de la documentation de votre fournisseur. Si vous utilisez le ciblage iSCSI basé sur Windows, voir [Stockage par blocs de cibles iSCSI, procédure](../iscsi/iscsi-target-server.md).  

-   **Pour le stockage SAN FC :**  

1. Assurez-vous que chaque cluster peut voir uniquement les boîtiers de stockage de ce site et que vous avez correctement segmenté les hôtes.  

2. Configurez le stockage à l’aide de la documentation de votre fournisseur.  

-   **Pour espaces de stockage direct :**  

1. Vérifiez que chaque cluster peut voir uniquement les boîtiers de stockage de ce site en déployant uniquement des espaces de stockage direct. (https://docs.microsoft.com/windows-server/storage/storage-spaces/hyper-converged-solution-using-storage-spaces-direct) 

2. Assurez-vous que les volumes de journaux SR se trouvent toujours sur le périphérique de stockage flash le plus rapide et les volumes de données sur un périphérique de stockage à haute capacité plus lent.

3. Démarrez Windows PowerShell et utilisez l’applet de commande `Test-SRTopology` pour déterminer si vous répondez à toutes les conditions des réplicas de stockage. Vous pouvez utiliser l’applet de commande dans un mode d’exigences uniquement pour un test rapide ainsi qu’un mode d’évaluation de performances à exécution longue.  
   Par exemple,  

   ```PowerShell
   MD c:\temp

   Test-SRTopology -SourceComputerName SR-SRV01 -SourceVolumeName f: -SourceLogVolumeName g: -DestinationComputerName SR-SRV03 -DestinationVolumeName f: -DestinationLogVolumeName g: -DurationInMinutes 30 -ResultPath c:\temp        
   ```

     > [!IMPORTANT]
     > Lorsque vous utilisez un serveur de test sans aucune écriture de charge d’E/S sur le volume source spécifié pendant la période d’évaluation, envisagez d’ajouter une charge de travail, ou le rapport généré ne sera pas utile. Vous devez effectuer des tests avec des charges de travail de type production afin de voir des nombres réels et les tailles de journal recommandées. Vous pouvez également simplement copier certains fichiers dans le volume source pendant le test ou télécharger et exécuter [DISKSPD](https://gallery.technet.microsoft.com/DiskSpd-a-robust-storage-6cd2f223) pour générer des E/S d’écriture. Par exemple, un échantillon avec une faible charge de travail d’E/S pendant cinq minutes pour le volume D: :  
     > `Diskspd.exe -c1g -d300 -W5 -C5 -b8k -t2 -o2 -r -w5 -h d:\test.dat`  

4. Examinez le rapport **TestSrTopologyReport.html** pour vous assurer que les exigences de réplica de stockage sont satisfaites.  

   ![Capture d’écran montrant les résultats du rapport de topologie de réplication](./media/Cluster-to-Cluster-Storage-Replication/SRTestSRTopologyReport.png)      

## <a name="step-2-configure-two-scale-out-file-server-failover-clusters"></a>Étape 2 : configurer deux clusters de basculement de serveur de fichiers avec montée en charge  
Vous allez maintenant créer deux clusters de basculement normaux. Après la configuration, la validation et le test, vous allez les répliquer à l’aide d’un réplica de stockage. Vous pouvez effectuer toutes les étapes ci-dessous sur les nœuds de cluster directement ou à partir d’un ordinateur de gestion à distance qui contient le Outils d’administration de serveur distant de Windows Server.  

### <a name="graphical-method"></a>Méthode graphique  

1.  Exécutez **cluadmin.msc** sur un nœud dans chaque site.  

2.  Validez le cluster proposé et analysez les résultats pour vérifier que vous pouvez continuer. L’exemple ci-dessous contient **SR-SRVCLUSA** et **SR-SRVCLUSB**.  

3.  Créez deux clusters. Assurez-vous que les noms de cluster font 15 caractères ou moins.  

4.  Configurez un témoin de partage de fichiers ou un témoin cloud.  

    > [!NOTE]  
    > WIndows Server comprend désormais une option pour le témoin Cloud (Azure). Vous pouvez choisir cette option de quorum au lieu du témoin de partage de fichiers.  

    > [!WARNING]  
    > Pour plus d’informations sur la configuration du quorum, consultez la section **configuration du témoin** dans [configurer et gérer le quorum](../../failover-clustering/manage-cluster-quorum.md). Pour plus d’informations sur l’applet de commande `Set-ClusterQuorum`, voir [Set-ClusterQuorum](https://docs.microsoft.com/powershell/module/failoverclusters/set-clusterquorum).  

5.  Ajoutez un disque dans le site **Redmond** sur le cluster CSV. Pour ce faire, cliquez avec le bouton droit sur un disque source dans le nœud **Disques** de la section **Stockage**, puis cliquez sur **Ajouter aux volumes partagés de cluster**.  

6.  Créez les serveurs de fichiers avec montée en charge sur les deux clusters en suivant les instructions de [Configurer un serveur de fichiers avec montée en charge](https://technet.microsoft.com/library/hh831718.aspx)  

### <a name="windows-powershell-method"></a>Méthode basée sur Windows PowerShell  

1.  Testez le cluster proposé et analysez les résultats pour vous assurer que vous pouvez continuer:  

    ```PowerShell
    Test-Cluster SR-SRV01,SR-SRV02  
    Test-Cluster SR-SRV03,SR-SRV04  
    ```  

2.  Créez des clusters (vous devez spécifier vos propres adresses IP statiques pour les clusters). Assurez-vous que chaque nom de cluster fait 15 caractères ou moins :  

    ```PowerShell
    New-Cluster -Name SR-SRVCLUSA -Node SR-SRV01,SR-SRV02 -StaticAddress <your IP here>  
    New-Cluster -Name SR-SRVCLUSB -Node SR-SRV03,SR-SRV04 -StaticAddress <your IP here>  
    ```  

3.  Configurez un témoin de partage de fichiers ou un témoin cloud (Azure) dans chaque cluster qui pointe vers un partage hébergé sur le contrôleur de domaine ou un autre serveur indépendant. Par exemple :  

    ```PowerShell  
    Set-ClusterQuorum -FileShareWitness \\someserver\someshare  
    ```  

    > [!NOTE]  
    > WIndows Server comprend désormais une option pour le témoin Cloud (Azure). Vous pouvez choisir cette option de quorum au lieu du témoin de partage de fichiers.  

    > [!WARNING]  
    > Pour plus d’informations sur la configuration du quorum, consultez la section **configuration du témoin** dans [configurer et gérer le quorum](../../failover-clustering/manage-cluster-quorum.md). Pour plus d’informations sur l’applet de commande `Set-ClusterQuorum`, voir [Set-ClusterQuorum](https://docs.microsoft.com/powershell/module/failoverclusters/set-clusterquorum).  

4.  Créez les serveurs de fichiers avec montée en charge sur les deux clusters en suivant les instructions de [Configurer un serveur de fichiers avec montée en charge](https://technet.microsoft.com/library/hh831718.aspx)  

## <a name="step-3-set-up-cluster-to-cluster-replication-using-windows-powershell"></a>Étape 3 : configurer la réplication de cluster à cluster à l’aide de Windows PowerShell  
Vous allez maintenant configurer la réplication de cluster à cluster à l’aide de Windows PowerShell. Vous pouvez effectuer toutes les étapes ci-dessous sur les nœuds directement ou à partir d’un ordinateur de gestion à distance qui contient Windows Server Outils d’administration de serveur distant  

1. Accordez au premier cluster un accès complet à l’autre cluster en exécutant l’applet de commande **Grant-SRAccess** sur n’importe quel nœud du premier cluster, ou à distance.  Outils d’administration de serveur distant Windows Server

   ```PowerShell
   Grant-SRAccess -ComputerName SR-SRV01 -Cluster SR-SRVCLUSB  
   ```  

2. Accordez au second cluster un accès complet à l’autre cluster en exécutant l’applet de commande **Grant-SRAccess** sur n’importe quel nœud du deuxième cluster, ou à distance.  

   ```PowerShell
   Grant-SRAccess -ComputerName SR-SRV03 -Cluster SR-SRVCLUSA  
   ```  

3. Configurez la réplication de cluster à cluster, en spécifiant les disques de la source et de la destination, les journaux de la source et de la destination, les noms de cluster de la source et de la destination, et la taille du journal. Vous pouvez exécuter cette commande localement sur le serveur ou à l’aide d’un ordinateur de gestion à distance.  

   ```powershell  
   New-SRPartnership -SourceComputerName SR-SRVCLUSA -SourceRGName rg01 -SourceVolumeName c:\ClusterStorage\Volume2 -SourceLogVolumeName f: -DestinationComputerName SR-SRVCLUSB -DestinationRGName rg02 -DestinationVolumeName c:\ClusterStorage\Volume2 -DestinationLogVolumeName f:  
   ```  

   > [!WARNING]  
   > La taille du journal par défaut est de 8 Go. En fonction des résultats de l’applet de commande **Test-SRTopology**, vous pouvez décider d’utiliser **- LogSizeInBytes** avec une valeur supérieure ou inférieure.  

4. Pour obtenir l’état de réplication de la source et de la destination, utilisez **Get-SRGroup** et **Get-SRPartnership**, comme suit :  

   ```powershell
   Get-SRGroup  
   Get-SRPartnership  
   (Get-SRGroup).replicas  
   ```  

5. Déterminez la progression de la réplication comme suit :  

   1.  Sur le serveur source, exécutez la commande suivante et examinez les événements 5015, 5002, 5004, 1237, 5001 et 2200:
        
       ```PowerShell
       Get-WinEvent -ProviderName Microsoft-Windows-StorageReplica -max 20
       ```
   2.  Sur le serveur de destination, exécutez la commande suivante pour afficher les événements de réplica de stockage qui indiquent la création du partenariat. Cet événement indique le nombre d’octets copiés et la durée de l’opération. Exemple :  
        
       ```powershell
       Get-WinEvent -ProviderName Microsoft-Windows-StorageReplica | Where-Object {$_.ID -eq "1215"} | Format-List
       ```
       Voici un exemple de sortie :
        
       ```
       TimeCreated  : 4/8/2016 4:12:37 PM  
       ProviderName : Microsoft-Windows-StorageReplica  
       Id           : 1215  
       Message      : Block copy completed for replica.  
           ReplicationGroupName: rg02  
           ReplicationGroupId:  
           {616F1E00-5A68-4447-830F-B0B0EFBD359C}  
           ReplicaName: f:\  
           ReplicaId: {00000000-0000-0000-0000-000000000000}  
           End LSN in bitmap:  
           LogGeneration: {00000000-0000-0000-0000-000000000000}  
           LogFileId: 0  
           CLSFLsn: 0xFFFFFFFF  
           Number of Bytes Recovered: 68583161856  
           Elapsed Time (seconds): 117  
       ```
   3. Le groupe de serveurs de destination pour le réplica peut aussi indiquer le nombre d’octets restants à copier à tout moment, et peut être interrogé via PowerShell. Par exemple :

      ```PowerShell
      (Get-SRGroup).Replicas | Select-Object numofbytesremaining
      ```

      Un exemple de progression (qui ne s’interrompt pas) :  

      ```PowerShell
        while($true) {  
        $v = (Get-SRGroup -Name "Replication 2").replicas | Select-Object numofbytesremaining  
        [System.Console]::Write("Number of bytes remaining: {0}`n", $v.numofbytesremaining)  
        Start-Sleep -s 5  
       }
       ```

6. Sur le serveur de destination dans le cluster de destination, exécutez la commande suivante et examinez les événements 5009, 1237, 5001, 5015, 5005 et 2200 pour comprendre la progression du traitement. Il ne doit y avoir aucun avertissement d’erreur dans cette séquence. Il y aura un grand nombre d’événements 1237; ils indiquent la progression.  
    
   ```PowerShell
   Get-WinEvent -ProviderName Microsoft-Windows-StorageReplica | FL  
   ```
   > [!NOTE]
   > Le disque de cluster de destination s’affiche toujours comme étant **En ligne (aucun accès)** lors de la réplication.  

## <a name="step-4-manage-replication"></a>Étape 4 : gérer la réplication

Vous gérez et opérez maintenant votre réplication cluster à cluster. Vous pouvez effectuer toutes les étapes ci-dessous sur les nœuds de cluster directement ou à partir d’un ordinateur de gestion à distance qui contient le Outils d’administration de serveur distant de Windows Server.  

1.  Utilisez **Get-ClusterGroup** ou **Gestionnaire du cluster de basculement** pour déterminer la source et la destination de réplication et leur état actuel.  Outils d’administration de serveur distant Windows Server

2.  Pour mesurer les performances de la réplication, utilisez l’applet de commande **Get-Counter** sur les nœuds source et de destination. Les noms des compteurs sont :  

    -   \Statistiques d’E/S du réplica du système de stockage(*)\Nombre de suspensions du vidage  

    -   \Statistiques d’E/S du réplica du système de stockage(*)\Nombre d’E/S de vidage en attente  

    -   \Statistiques d’E/S du réplica du système de stockage(*)\Nombre de demandes associées à la dernière écriture de journal  

    -   \Statistiques d’E/S du réplica du système de stockage(*)\Longueur moyenne de file d’attente de vidage  

    -   \Statistiques d’E/S du réplica du système de stockage(*)\Longueur de file d’attente de vidage actuelle  

    -   \Statistiques d’E/S du réplica du système de stockage(*)\Nombre de demandes d’écriture d’application  

    -   \Statistiques d’E/S du réplica du système de stockage(*)\Nombre moy. de demandes par écriture de journal  

    -   \Statistiques d’E/S du réplica du système de stockage(*)\Latence moyenne d’écriture d’application  

    -   \Statistiques d’E/S du réplica du système de stockage(*)\Latence moyenne de lecture d’application  

    -   \Statistiques du réplica du système de stockage(*)\RPO cible  

    -   \Statistiques du réplica du système de stockage(*)\RPO actuel  

    -   \Statistiques du réplica du système de stockage(*)\Longueur moyenne de file d’attente de journal  

    -   \Statistiques du réplica du système de stockage(*)\Longueur de file d’attente de journal actuelle  

    -   \Statistiques du réplica du système de stockage(*)\Total des octets reçus  

    -   \Statistiques du réplica du système de stockage(*)\Total des octets envoyés  

    -   \Statistiques du réplica du système de stockage(*)\Latence moyenne d’envoi réseau  

    -   \Statistiques du réplica du système de stockage(*)\État de réplication  

    -   \Statistiques du réplica du système de stockage(*)\Latence moy. de boucle de message  

    -   \Statistiques du réplica du système de stockage(*)\Temps écoulé pour la dernière récupération  

    -   \Statistiques du réplica du système de stockage(*)\Nombre de transactions de récupération vidées  

    -   \Statistiques du réplica du système de stockage(*)\Nombre de transactions de récupération  

    -   \Statistiques du réplica du système de stockage(*)\	Nombre de transactions de réplication vidées  

    -   \Statistiques du réplica du système de stockage(*)\	Nombre de transactions de réplication  

    -   \Statistiques du réplica du système de stockage(*)\Numéro séquentiel dans le journal max.  

    -   \Statistiques du réplica du système de stockage(*)\Nombre de messages reçus  

    -   \Statistiques du réplica du système de stockage(*)\Nombre de messages envoyés  

    Pour plus d’informations sur les compteurs de performances dans Windows PowerShell, consultez [Get-Counter](https://docs.microsoft.com/powershell/module/Microsoft.PowerShell.Diagnostics/Get-Counter).  

3.  Pour déplacer la direction de réplication d’un site, utilisez l’applet de commande **Set-SRPartnership**.  

    ```PowerShell
    Set-SRPartnership -NewSourceComputerName SR-SRVCLUSB -SourceRGName rg02 -DestinationComputerName SR-SRVCLUSA -DestinationRGName rg01  
    ```  

    > [!NOTE]  
    > Windows Server empêche le basculement de rôle lorsque la synchronisation initiale est en cours, car cela peut entraîner une perte de données si vous tentez de basculer avant d’autoriser la réplication initiale. Ne forcez pas les directions de basculement tant que la synchronisation initiale n’est pas terminée.

    Vérifiez les journaux d’événements pour voir la direction du changement de réplication et la survenue du mode de récupération, puis rapprochez. Les E/S d’écriture peuvent alors écrire sur le stockage du nouveau serveur source. Modifier la direction de réplication bloquera les E/S d’écriture sur l’ordinateur source précédent.  

    > [!NOTE]  
    > Le disque de cluster de destination s’affiche toujours comme étant **En ligne (aucun accès)** lors de la réplication.  

4.  Pour modifier la taille du journal par défaut de 8 Go, utilisez **Set-SRGroup** sur les groupes de réplicas de stockage source et de destination.  

    > [!IMPORTANT]  
    > La taille du journal par défaut est de 8 Go. En fonction des résultats de l’applet de commande **Test-SRTopology**, vous pouvez décider d’utiliser -LogSizeInBytes avec une valeur supérieure ou inférieure.  

5.  Pour supprimer la réplication, utilisez **Get-SRGroup**, **Get-SRPartnership**, **Remove-SRGroup**, et **Remove-SRPartnership** dans chaque cluster.  

    ```powershell
    Get-SRPartnership | Remove-SRPartnership  
    Get-SRGroup | Remove-SRGroup  
    ```  

    > [!NOTE]  
    > Le réplica de stockage démonte les volumes de destination. Cela est normal.

## <a name="see-also"></a>Voir également

-   [Vue d’ensemble du réplica de stockage](storage-replica-overview.md) 
-   [Réplication de cluster étendu à l’aide d’un stockage partagé](stretch-cluster-replication-using-shared-storage.md)  
-   [Réplication de stockage de serveur à serveur](server-to-server-storage-replication.md)  
-   [Réplica de stockage : problèmes connus](storage-replica-known-issues.md)  
-   [Réplica de stockage : Forum aux questions](storage-replica-frequently-asked-questions.md)  
-   [espaces de stockage direct dans Windows Server 2016](../storage-spaces/storage-spaces-direct-overview.md)  
