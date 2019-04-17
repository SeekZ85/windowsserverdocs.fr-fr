---
title: "Forum Aux Questions sur le réplica de stockage"
ms.prod: windows-server-threshold
manager: siroy
ms.author: nedpyle
ms.technology: storage-replica
ms.topic: get-started-article
author: nedpyle
ms.date: 07/20/2017
ms.assetid: 12bc8e11-d63c-4aef-8129-f92324b2bf1b
ms.openlocfilehash: f29ca24a39e00f5142fe700e6abb09d1673acf7b
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/17/2017
---
# <a name="frequently-asked-questions-about-storage-replica"></a>Forum Aux Questions sur le réplica de stockage

>S’applique à: WindowsServer (canal semi-annuel), WindowsServer2016

Cette rubrique contient des réponses aux questions fréquemment posées sur le réplica de stockage.

## <a name="FAQ1"></a> Est-ce que le réplica de stockage est pris en charge sur Nano Server?  
Oui.  

> [!NOTE]
> Vous devez utiliser le package Nano Server de **stockage** pendant l’installation. Pour plus d’informations sur le déploiement de Nano Server, voir [Prise en main de Nano Server](https://technet.microsoft.com/library/mt126167.aspx).  

Installez le réplica de stockage sur Nano Server à l’aide de la communication à distance PowerShell comme suit:  

1. Ajoutez Nano Server à votre liste de clients de confiance.  
   > [!NOTE]
   > Cette étape est uniquement nécessaire si l’ordinateur n’est pas un membre d’une forêt des services de domaine Active Directory ou dans une forêt non approuvée. Elle ajoute la prise en charge NTLM à la communication à distance de session PSsession, qui est désactivée par défaut pour des raisons de sécurité. Pour plus d’informations, voir [Éléments à prendre en compte en matière de sécurité de la communication à distance PowerShell](https://msdn.microsoft.com/powershell/scriptiwinrmsecurity).  

   ```  
       Set-Item WSMan:\localhost\Client\TrustedHosts "<computer name of Nano Server>"  
   ```  
2.  Pour installer la fonctionnalité de réplica de stockage, exécutez l’applet de commande suivante à partir d’un ordinateur de gestion:  

    ```  
    Install-windowsfeature -Name storage-replica,RSAT-Storage-Replica -ComputerName <nano server> -Restart -IncludeManagementTools  
    ```  

    L’utilisation de l’applet de commande `Test-SRTopology` avec Nano Server dans Windows Server2016 nécessite l’appel d’un script distant avec CredSSP. Contrairement aux autres applets de commande de réplica de stockage, `Test-SRTopology` doit être exécutée en local sur le serveur source.   
Sur Nano Server (via une session PSsession distante):  

    >[!NOTE]
    >CREDSSP est nécessaire pour la prise en charge du double saut Kerberos dans l’applet de commande `Test-SRTopology`, mais n’est pas requis par les autres applets de commande de réplica de stockage, qui gèrent automatiquement les informations d’identification du système distribué. L’utilisation de CREDSSP n’est pas recommandée dans des circonstances normales. Pour une alternative à CREDSSP, consultez le billet de blog Microsoft suivant: «PowerShell Remoting Kerberos Double Hop Solved Securely» (Résolution sécurisée du double saut Kerberos pour la communication à distance de PowerShell) - https://blogs.technet.microsoft.com/ashleymcglone/2016/08/30/powershell-remoting-kerberos-double-hop-solved-securely/ 

        Enable-WSManCredSSP -role server       

    Sur l’ordinateur de gestion:  

         Enable-WSManCredSSP Client -DelegateComputer <remote server name>  

         $CustomCred = Get-Credential  

         Invoke-Command -ComputerName sr-srv01 -ScriptBlock { Test-SRTopology <commands> } -Authentication Credssp -Credential $CustomCred  

       Copiez ensuite les résultats sur votre ordinateur de gestion ou partagez le chemin. Comme Nano n’a pas les bibliothèques graphiques nécessaires, vous pouvez utiliser Test-SRTopology pour traiter les résultats et vous donner un fichier de rapport avec des graphiques. Par exemple:  

        Test-SRTopology -GenerateReport -DataPath \\sr-srv05\c$\temp  


## <a name="FAQ2"></a> Comment afficher la progression de la réplication pendant la synchronisation initiale?  
Les messages de l’événement1237 affichés dans le journal des événements de l’administrateur de réplica de stockage sur le serveur de destination indiquent le nombre d’octets copiés et restants toutes les 10secondes. Vous pouvez également utiliser le compteur de performance du réplica de stockage sur la destination affichant **\Statistiques du réplica du système de stockage\Total d’octets reçus** pour un ou plusieurs volumes répliqués. Vous pouvez également interroger le groupe de réplication à l’aide de Windows PowerShell. Par exemple, cet exemple de commande obtient le nom des groupes sur la destination, puis interroge un groupe nommé **Replication 2** toutes les 10secondes pour afficher la progression:  

```  
Get-SRGroup

do{
    $r=(Get-SRGroup -Name "Replication 2").replicas
    [System.Console]::Write("Number of remaining bytes {0}`n", $r.NumOfBytesRemaining)
    Start-Sleep 10
}until($r.ReplicationStatus -eq 'ContinuouslyReplicating')
Write-Output "Replica Status: "$r.replicationstatus

```  

## <a name="FAQ3"></a>Puis-je spécifier des interfaces réseau spécifiques à utiliser pour la réplication?  

Oui, avec `Set-SRNetworkConstraint`. Cette applet de commande fonctionne au niveau de la couche d’interface et peut être utilisée dans des situations avec ou sans cluster.  
Par exemple, avec un serveur autonome (sur chaque nœud):  

```  
Get-SRPartnership  

Get-NetIPConfiguration  
```  
Notez les informations de passerelle et d’interface (sur les deux serveurs) et les instructions de partenariat. Ensuite, exécutez:  

```  
Set-SRNetworkConstraint -SourceComputerName sr-srv06 -SourceRGName rg02 -  
SourceNWInterface 2 -DestinationComputerName sr-srv05 -DestinationNWInterface 3 -DestinationRGName rg01  

Get-SRNetworkConstraint  

Update-SmbMultichannelConnection  

```  

Pour configurer des contraintes de réseau sur un cluster étendu:  

    Set-SRNetworkConstraint -SourceComputerName sr-srv01 -SourceRGName group1 -SourceNWInterface "Cluster Network 1","Cluster Network 2" -DestinationComputerName sr-srv03 -DestinationRGName group2 -DestinationNWInterface "Cluster Network 1","Cluster Network 2"  

## <a name="FAQ4"></a> Puis-je configurer une réplication un-à-plusieurs ou une réplication transitive (deA àB àC)?  
Pas dans Windows Server2016. Cette version prend uniquement en charge la réplication un-à-un d’un serveur, cluster ou nœud de cluster étendu. Cela peut changer dans une version ultérieure. Vous pouvez bien sûr configurer la réplication entre différents serveurs d’une paire de volumes spécifique, dans les deux sens. Par exemple, le serveur1 peut répliquer son volumeD sur le serveur2 et son volumeE à partir du serveur3.

## <a name="FAQ5"></a> Puis-je développer ou réduire les volumes répliqués par le réplica de stockage?  
Vous pouvez développer (augmenter) des volumes, mais pas les réduire. Par défaut, le réplica de stockage empêche les administrateurs de développer les volumes répliqués; utilisez l'option `Set-SRGroup -AllowVolumeResize $TRUE` sur le groupe source avant le redimensionnement. Exemple:

1. Utilisez par rapport à l’ordinateur source: `Set-SRGroup -Name YourRG -AllowVolumeResize $TRUE`
2. Augmentez le volume en utilisant la technique de votre choix.
3. Utilisez par rapport à l’ordinateur source: `Set-SRGroup -Name YourRG -AllowVolumeResize $FALSE` 

## <a name="FAQ6"></a>Puis-je mettre en ligne un volume de destination pour l’accès en lecture seule?  
Pas dans Windows Server2016 RTM, également appelé version «RS1». Le réplica de stockage démonte le volume de destination au début de la réplication. 

Toutefois, dans WindowsServer, version1709, il est désormais possible de monter le stockage de destination; cette fonctionnalité est appelée «Test de basculement». Pour ce faire, vous devez disposer d’un volume au format NTFS ou ReFS inutilisé qui ne réplique pas sur la destination actuellement. Ensuite, vous pouvez monter une capture instantanée du stockage répliqué temporairement à des fins de test ou de sauvegarde. 

Par exemple, pour créer un test de basculement dans lequel vous répliquez un volume «D:» dans le groupe de réplication «RG2» sur le serveur de destination «SRV2», avec un lecteur «T:» sur SRV2 qui n’est pas répliqué:

 `Mount-SRDestination -Name RG2 -Computername SRV2 -TemporaryPath T:\`
 
Le volume D: répliqué est désormais accessible sur SRV2. Vous pouvez lire et écrire normalement sur ce volume, copier des fichiers à partir de celui-ci ou exécuter une sauvegarde en ligne que vous enregistrez à un autre emplacement pour la conserver.

Pour supprimer l’instantané de test de basculement et supprimer les modifications:

 `Dismount-SRDestination -Name RG2 -Computername SRV2`
 
Vous devez uniquement utiliser la fonctionnalité de test de basculement pour des opérations temporaires à court terme. Elle n’est pas destinée à être utilisée à long terme. Lors de l’utilisation, la réplication continue sur le volume de destination réel. 

## <a name="FAQ7"></a> Puis-je configurer un serveur de fichiers avec montée en puissance parallèle dans un cluster étendu?  
Bien que techniquement possible, cette configuration n’est pas recommandée dans Windows Server2016, en raison du manque de reconnaissance des sites dans les nœuds de calcul qui contactent le serveur de fichiers avec montée en puissance parallèle. Si vous utilisez une mise en réseau à l’échelle du campus, où les temps de latence sont généralement inférieurs à la milliseconde, cette configuration fonctionne généralement sans problème.   

Si vous configurez une réplication de cluster à cluster, le réplica de stockage prend entièrement en charge les serveurs de fichiers avec montée en puissance parallèle, notamment l’utilisation de espaces de stockage direct, lors de la réplication entre deux clusters.  

## <a name="FAQ8"></a>Puis-je configurer des espaces de stockage direct dans un cluster étendu avec le réplica de stockage?  
Cette configuration n’est pas prise en charge dans Windows Server2016.  Cela peut changer dans une version ultérieure. Si vous configurez une réplication de cluster à cluster, le réplica de stockage prend entièrement en charge les serveurs de fichiers avec montée en puissance parallèle et les serveurs Hyper-V, notamment l’utilisation de espaces de stockage direct.  

## <a name="FAQ9"></a>Comment configurer la réplication asynchrone?  

Spécifiez `New-SRPartnership -ReplicationMode` et indiquez l’argument **Asynchronous**. Par défaut, toute la réplication dans le réplica de stockage est synchrone. Vous pouvez également modifier le mode avec `Set-SRPartnership -ReplicationMode`.  

## <a name="FAQ10"></a>Comment empêcher le basculement automatique d’un cluster étendu?  
Pour empêcher le basculement automatique, vous pouvez utiliser PowerShell pour configurer `Get-ClusterNode -Name "NodeName").NodeWeight=0`. Cette action supprime le vote sur chaque nœud dans le site de récupération d’urgence. Vous pouvez ensuite utiliser `Start-ClusterNode -PreventQuorum` sur les nœuds dans le site principal et `Start-ClusterNode -ForceQuorum` sur les nœuds dans le site de récupération d’urgence pour forcer le basculement. Il n’existe aucune option graphique pour empêcher le basculement automatique et cette action n’est en outre pas recommandée.  

## <a name="FAQ11"></a>Comment désactiver la résilience de la machine virtuelle?  
Pour empêcher l’exécution de la nouvelle fonctionnalité de résilience de la machine virtuelle Hyper-V et pour mettre par conséquent en pause les machines virtuelles au lieu de les basculer vers le site de récupération d’urgence, exécutez `(Get-Cluster).ResiliencyDefaultPeriod=0`  

## <a name="FAQ12"></a> Comment réduire la durée de la synchronisation initiale?  

Vous pouvez utiliser un stockage alloué dynamiquement comme moyen d’accélérer les durées de synchronisation initiale. Le réplica de stockage recherche et utilise automatiquement le stockage alloué dynamiquement, notamment les espaces de stockage non cluster, les disques dynamiques Hyper-V et les LUN SAN.  

Vous pouvez également utiliser des volumes de données amorcés pour réduire l’utilisation de la bande passante et parfois le temps, en veillant à ce que le volume de destination ait un sous-ensemble des données du volume principal (via une sauvegarde restaurée, un ancien instantané, une réplication précédente, des fichiers copiés, etc.), puis en utilisant l’option Amorcé du Gestionnaire du cluster de basculement ou `New-SRPartnership`. Si le volume est pratiquement vide, l’utilisation de la synchronisation amorcée peut réduire le temps et l’utilisation de la bande passante.

## <a name="FAQ13"></a> Puis-je déléguer des utilisateurs pour gérer la réplication?  

Vous pouvez utiliser l’applet de commande `Grant-SRDelegation` dans Windows Server2016. Cela vous permet de définir des utilisateurs spécifiques dans des scénarios de réplication de serveur à serveur, de cluster à cluster et de cluster étendu comme ayant les autorisations de créer, modifier ou supprimer la réplication, sans être membres du groupe Administrateurs local. Par exemple:  

    Grant-SRDelegation -UserName contso\tonywang  

L’applet de commande vous rappelle que l’utilisateur doit se déconnecter du serveur qu’il envisage de gérer, puis se reconnecter pour que la modification prenne effet. Vous pouvez utiliser `Get-SRDelegation` et `Revoke-SRDelegation` pour mieux contrôler cette opération.  

## <a name="FAQ13"></a> Quelles sont mes options de sauvegarde et de restauration pour les volumes répliqués?
Le réplica de stockage prend en charge la sauvegarde et la restauration du volume source. Il prend également en charge la création et la restauration d’instantanés du volume source. Vous ne pouvez pas sauvegarder ni restaurer le volume de destination tant qu’il est protégé par le réplica de stockage, car il n’est pas monté ni accessible. Si un incident survient et que le volume source est perdu, l’utilisation de `Set-SRPartnership` pour promouvoir le volume de destination précédent afin qu’il devienne une source accessible en lecture/écriture vous permet de sauvegarder ou restaurer ce volume. Vous pouvez également supprimer la réplication avec `Remove-SRPartnership` et `Remove-SRGroup` pour remonter ce volume comme accessible en lecture/écriture.
Pour créer des instantanés cohérents au niveau application réguliers, vous pouvez utiliser VSSADMIN. EXE sur le serveur source pour capturer les volumes de données répliqués. Par exemple, vous répliquez le volume F: avec le réplica de stockage:

    vssadmin create shadow /for=F:
Ensuite, après avoir basculé le sens de la réplication ou supprimé la réplication, ou si vous restez toujours sur le même volume source, vous pouvez restaurer tout instantané à son point dans le temps. Par exemple, en utilisant toujours F::

    vssadmin list shadows
     vssadmin revert shadow /shadow={shadown copy ID GUID listed previously}
Vous pouvez également prévoir une exécution régulière de cet outil à l’aide d’une tâche planifiée. Pour plus d’informations sur l’utilisation de VSS, voir [Vssadmin](https://technet.microsoft.com/library/cc754968.aspx). Il est inutile et sans intérêt de sauvegarder les volumes de journaux. Une telle tentative sera ignorée par VSS.
L’utilisation de la sauvegarde Windows Server, de la sauvegarde Microsoft Azure, de Microsoft DPM, d’un autre instantané, de VSS, de la machine virtuelle ou des technologies basées sur des fichiers est prise en charge par le réplica de stockage tant que ces outils fonctionnent au niveau de la couche du volume. Le réplica de stockage ne prend pas en charge la sauvegarde et la restauration basées sur des blocs.

## <a name="FAQ14"></a> Puis-je configurer la réplication pour restreindre l’utilisation de la bande passante?
Oui, via le limiteur de bande passante SMB. Il s’agit d’un paramètre global pour tout le trafic du réplica de stockage qui, par conséquent, affecte l’ensemble de la réplication de ce serveur. En règle générale, cela est nécessaire uniquement avec la configuration de la synchronisation initiale de réplica de stockage, où toutes les données des volumes doivent être transférées. Si, après la synchronisation initiale, la bande passante réseau est trop faible pour votre charge de travail d’E/S, diminuez les E/S ou augmentez la bande passante.

Vous ne devez l’utiliser qu’avec la réplication asynchrone (notez que la synchronisation initiale est toujours asynchrone même si vous avez spécifié synchrone).
Vous pouvez également utiliser des stratégies de qualité de service réseau pour adapter le trafic du réplica de stockage. L’utilisation de la réplication de réplica de stockage amorcée à forte correspondance permet également de réduire considérablement l’utilisation de la bande passante de synchronisation initiale globale.


Pour définir la limite de bande passante, utilisez:

    Set-SmbBandwidthLimit  -Category StorageReplication -BytesPerSecond x

Pour afficher la limite de bande passante, utilisez:

    Get-SmbBandwidthLimit -Category StorageReplication

Pour supprimer la limite de bande passante, utilisez:

    Remove-SmbBandwidthLimit -Category StorageReplication
    
## <a name="FAQ15"></a>De quels ports réseau a besoin le réplica de stockage?
Le réplica de stockage s’appuie sur SMB et WSMAN pour sa réplication et sa gestion. Cela signifie qu'il nécessite les ports suivants:

   445 (SMB - protocole de transport de réplication) 5445 (SMB iWARP - uniquement utile avec une mise en réseau RDMA iWARP) 5895 (WSManHTTP - protocole de gestion pour WMI/CIM/PowerShell)

Remarque: l’applet de commande Test-SRTopology nécessite ICMPv4/ICMPv6, mais pas pour la réplication ni pour la gestion.

## <a name="FAQ15"></a>Quelles sont les meilleures pratiques en matière de volume du journal?
La taille optimale du journal varie grandement en fonction de l’environnement et de la charge de travail. Elle est déterminée par le nombre d’E/S d’écriture effectuées par votre charge de travail. 

1.  Le volume du journal n'a aucune incidence sur la vitesse.
2.  Un journal plus ou moins volumineux n'a pas d'effet sur le volume des données, que celui-ci soit de 10Go ou de 10To, par exemple.

Un journal plus volumineux collecte et conserve simplement davantage d’E/S d’écriture avant qu’elles ne soient encapsulées. Cela permet de prolonger une interruption de service entre l’ordinateur source et celui de destination, par exemple en cas de panne réseau ou si l’ordinateur de destination est hors ligne. Si le journal peut contenir 10heures d’écriture et que le réseau tombe en panne pendant 2heures, une fois le réseau rétabli, la source peut simplement lire le delta des modifications non synchronisées sur la destination très vite. Vous êtes donc à nouveau protégé très rapidement. Si la durée de conservation du journal est de 10heures et que l’interruption dure 2jours, la source doit alors relire un autre journal appelé bitmap. Il est alors probable qu’elle mette plus longtemps à se resynchroniser. Une fois synchronisée, elle revient à l’utilisation du journal.

Des compteurs de performances SR peuvent vous indiquer le rythme d'activité du journal, ce qui permet de prendre certaines décisions. L’applet de commande Test-SRTopology le permet également. En fait, vous devez simplement examiner les E/S d’écriture d'une charge de travail existante afin de déterminer le flux probable des E/S dans le journal par minute, heure ou jour.

Le réplica de stockage s’appuie sur le journal pour toutes les performances d’écriture. Les performances des journaux sont essentielles aux performances de la réplication. Vous devez vous assurer que le volume du journal soit plus performant que le volume de données, car le journal va sérialiser et séquentialiser toutes les E/S d’écriture. Vous devez toujours utiliser des supports Flash comme SSD sur les volumes de journaux. Vous ne devez jamais autoriser l’exécution d’autres charges de travail sur le volume du journal, tout comme vous ne devez jamais autoriser l’exécution d’autres charges de travail sur des volumes de journaux de base de données SQL. 

Une fois encore, Microsoft recommande vivement que le stockage du journal soit plus rapide que le stockage de données et que les volumes des journaux ne soient jamais utilisés pour d'autres charges de travail.

## <a name="FAQ16"></a>Quel choix privilégier entre une topologie de cluster étendu, de cluster à cluster ou de serveur à serveur?  
Le réplica de stockage est disponible en trois configurations principales: cluster étendu, cluster à cluster et serveur à serveur. Chaque configuration présente différents avantages.

La topologie de cluster étendu est idéale pour les charges de travail nécessitant un basculement automatique avec orchestration, par exemple, des clusters de cloud privé Hyper-V et une instance de cluster de basculement (FCI) SQL Server. Elle présente également une interface graphique intégrée utilisant le Gestionnaire du cluster de basculement. Elle utilise l'architecture de stockage partagé en cluster asymétrique classique des espaces de stockage, SAN, iSCSI et RAID via la réservation persistante. Vous pouvez l'exécuter avec seulement 2nœuds.

La topologie de cluster à cluster utilise deux clusters distincts. Elle est idéale pour les administrateurs qui veulent un basculement manuel, en particulier lorsque le deuxième site est configuré pour la récupération d’urgence et non pour l'utilisation quotidienne. L'orchestration est manuelle. Contrairement à un cluster étendu, cette configuration permet d'utiliser des espaces de stockage direct. Vous pouvez l'exécuter avec seulement quatre nœuds. 

La topologie de serveur à serveur convient parfaitement aux clients qui utilisent du matériel non compatible avec les clusters. Elle requiert une orchestration et un basculement manuels. Elle est parfaite pour les déploiements peu coûteux entre des filiales et des centres de données centralisés, en particulier lorsque vous utilisez la réplication asynchrone. Cette configuration peut souvent remplacer des instances de serveurs de fichiers protégés par DFSR utilisées dans les scénarios de récupération d’urgence à maître unique.

Dans tous les cas, ces topologies fonctionnent aussi bien sur du matériel physique que sur des ordinateurs virtuels. Dans le cas de machines virtuelles, l’hyperviseur sous-jacent ne nécessite pas obligatoirement Hyper-V; il peut s'agir de VMware, KVM, Xen, etc.

Le réplica de stockage dispose également d’un mode serveur unique (server-to-self), dans lequel vous dirigez la réplication vers deux volumes différents sur le même ordinateur.

## <a name="FAQ17"></a> Comment signaler un problème relatif au réplica de stockage ou à ce guide?  
Pour obtenir une assistance technique sur le réplica de stockage, publiez un message sur les [Forums Microsoft TechNet](https://social.technet.microsoft.com/Forums/windowsserver/en-US/home?forum=WinServerPreview). Vous pouvez également envoyer un e-mail à l’adresse srfeed@microsoft.com pour toute question sur le réplica de stockage ou tout problème lié à cette documentation. Le site https://windowsserver.uservoice.com est recommandé pour les demandes de modification de conception, car il permet à vos clients d’assurer un support et de fournir des commentaires sur vos idées.



## <a name="related-topics"></a>Rubriques connexes  
- [Vue d’ensemble du réplica de stockage](storage-replica-overview.md) 
- [Réplication de cluster étendu à l’aide d’un stockage partagé](stretch-cluster-replication-using-shared-storage.md)  
- [Réplication de stockage de serveur à serveur](server-to-server-storage-replication.md)  
- [Réplication du stockage de cluster à cluster](cluster-to-cluster-storage-replication.md)  
- [Réplica de stockage: problèmes connus](storage-replica-known-issues.md)  

## <a name="see-also"></a>Articles associés  
- [Vue d’ensemble du stockage](../storage.md)  
- [Espaces de stockage direct dans Windows Server2016](../storage-spaces/storage-spaces-direct-overview.md)  
