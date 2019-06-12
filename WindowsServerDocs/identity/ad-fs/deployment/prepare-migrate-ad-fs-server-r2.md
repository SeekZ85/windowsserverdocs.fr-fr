---
title: Préparer la migration du serveur AD FS 2.0 de fédération AD FS sur Windows Server 2012 R2
description: Fournit des informations sur la préparation migrer le serveur AD FS vers Windows Server 2012 R2.
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/10/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: cb301d0d68f00625ccea8c11d315b9defffe40f3
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66444535"
---
# <a name="prepare-to-migrate-the-ad-fs-20-federation-server-to-ad-fs-on-windows-server-2012-r2"></a>Préparer la migration du serveur AD FS 2.0 de fédération AD FS sur Windows Server 2012 R2

Ce document décrit comment migrer un AD FS 2.0 ou une batterie de serveurs de fédération Windows Server 2012 à une batterie de serveurs Windows Server 2012 R2 AD FS.  Les étapes peuvent être utilisés avec les batteries de serveurs AD FS qui utilisent WID ou SQL Server comme base de données sous-jacente.  
  
-   [Plan du processus de migration](prepare-migrate-ad-fs-server-r2.md#migration-process-outline)  
  
-   [Nouvelles fonctionnalités AD FS dans Windows Server 2012 R2](prepare-migrate-ad-fs-server-r2.md#new-ad-fs-functionality-in-windows-server-2012-r2)  
  
-   [Exigences en matière d’AD FS dans Windows Server 2012 R2](prepare-migrate-ad-fs-server-r2.md#ad-fs-requirements-in-windows-server-2012-r2)  
  
-   [Augmenter vos limites de Windows PowerShell](prepare-migrate-ad-fs-server-r2.md#increasing-your-windows-powershell-limits)  
  
-   [Autres considérations et tâches de migration](prepare-migrate-ad-fs-server-r2.md#other-migration-tasks-and-considerations)  
  
##  <a name="migration-process-outline"></a>Plan du processus de migration

 Pour mener à bien la migration de votre batterie de serveurs de fédération AD FS vers Windows Server 2012 R2, vous devez effectuer les tâches suivantes :  
  
1.  Exportez, enregistrez et sauvegardez les données de configuration suivantes dans votre batterie AD FS existante. Pour obtenir des instructions détaillées sur l’exécution de ces tâches, voir [Migration du serveur de fédération AD FS](migrate-ad-fs-fed-server-r2.md).  
  
Les paramètres suivants sont migrés avec les scripts situés dans le dossier \support\adfs sur le CD d’installation de Windows Server 2012 R2 :  
  
-   Approbations de fournisseur de revendications, à l’exception des règles de revendication personnalisées sur l’approbation de fournisseur de revendications Active Directory. Pour plus d’informations, voir [Migration du serveur de fédération AD FS](migrate-ad-fs-fed-server-r2.md).  
  
-   Approbations de partie de confiance.  
  
-   Certificats de déchiffrement de jeton et de signature de jetons auto-signé générés en interne AD FS.  
  
Tous les paramètres personnalisés suivants doivent être migrés manuellement :  
  
- Paramètres de service :  
  
  - certificats de déchiffrement de jeton et de signature de jetons autres que ceux par défaut qui ont été émis par une autorité de certification d’entreprise ou publique ;  
  
  - certificat d’authentification serveur SSL utilisé par AD FS ;  
  
  - certificat de communications de service utilisé par AD FS (par défaut, il s’agit du même certificat que le certificat SSL) ;  
  
    -   valeurs autres que celles par défaut pour les propriétés de tout service de fédération, par exemple AutoCertificateRollover ou la durée de vie SSO ;  
  
    -   Paramètres de point de terminaison AD FS non définis par défaut et descriptions des revendications.  
  
-   Règles de revendication personnalisées sur l’approbation de fournisseur de revendications Active Directory.  
  
    -   Personnalisations de la page de connexion AD FS  
  
Pour plus d’informations, voir [Migration du serveur de fédération AD FS](migrate-ad-fs-fed-server-r2.md).  
  
2. Créez une batterie de serveurs de fédération Windows Server 2012 R2.  
  
3. Importez les données de configuration d’origine dans cette nouvelle batterie AD FS Windows Server 2012 R2.  
  
4. Configurez et personnalisez les pages de connexion AD FS.  
  
##  <a name="new-ad-fs-functionality-in-windows-server-2012-r2"></a>Nouvelles fonctionnalités des services AD FS dans Windows Server 2012 R2  
 La fonctionnalité AD FS suivante change dans Windows Server 2012 R2 impact une migration à partir d’AD FS 2.0 ou AD FS dans Windows Server 2012 :  
  
**Dépendance IIS**  
   - Les services AD FS dans Windows Server 2012 R2 sont auto-hébergés et ne nécessitent pas l’installation des services Internet (IIS). Assurez-vous de noter la remarque suivante comme conséquence de cette modification :  
   -   La gestion des certificats SSL à la fois pour les serveurs de fédération et les ordinateurs proxy de votre batterie AD FS doit maintenant être effectuée via Windows PowerShell.  
  
**Modifications apportées aux paramètres et les personnalisations AD FS sign-in pages**  
-   Dans AD FS dans Windows Server 2012 R2, il existe plusieurs modifications visant à améliorer l’expérience de connexion pour les administrateurs et utilisateurs. Les pages Web hébergées par les services IIS qui existaient dans la version précédente des services AD FS sont maintenant supprimées. L’apparence des pages Web de connexion AD FS est auto-hébergée dans AD FS et peut maintenant être personnalisée en fonction de l’expérience de l’utilisateur. Les modifications sont notamment les suivantes :  
    -   Personnalisation de l’expérience de connexion AD FS, y compris la personnalisation du nom, du logo et de l’image de la société, ainsi que de la description de la connexion.  
    -   Personnalisation des messages d’erreur.  
    -   Personnalisation de l’expérience de découverte de domaine d’accueil AD FS, notamment :  
        -   configuration de votre fournisseur d’identité pour utiliser certains suffixes d’adresses de messagerie ;  
        -   configuration d’une liste de fournisseurs d’identité par partie de confiance ;  
        -   contournement de la découverte de domaine d’accueil pour l’intranet ;  
        -   création de thèmes Web personnalisés.  
  
Pour obtenir des instructions détaillées sur la configuration de l’apparence des pages de connexion AD FS, consultez [Customizing the AD FS Sign-in Pages](../operations/AD-FS-Customization-in-Windows-Server-2016.md).  
  
Si vous avez la personnalisation de pages web dans votre batterie de serveurs AD FS existante que vous souhaitez migrer vers Windows Server 2012 R2, vous pouvez les recréer dans le cadre du processus de migration à l’aide des nouvelles fonctionnalités de personnalisation dans Windows Server 2012 R2.  
  
-   **Autres modifications**  
  
    -   AD FS dans Windows Server 2012 R2 est basé sur Windows Identity Foundation (WIF) 3.5 et non WIF 4.5. Par conséquent, certaines fonctionnalités spécifiques de WIF 4.5 (par exemple, les revendications Kerberos et contrôle d’accès dynamique) ne sont pas pris en charge dans AD FS dans Windows Server 2012 R2.  
  
    -   Service DRS (Device Registration) dans Windows Server 2012 R2 fonctionne sur le port 443 ; ClientTLS pour l’authentification des certificats utilisateur fonctionne sur le port 49443  
  
        -   Pour les clients autres que des navigateurs actifs utilisant l’authentification du mode de transport de certificats qui sont spécifiquement codés en dur pour pointer vers le port 443, une modification du code est requise pour continuer à utiliser l’authentification des certificats utilisateur sur le port 49443.  
  
        -   Pour les applications passives, aucune modification n’est requise, car les services AD FS redirigent vers le port approprié pour l’authentification des certificats utilisateur.  
  
        -   Les ports de pare-feu entre le client et le proxy doivent permettre au trafic du port 49443 de traverser pour l’authentification des certificats utilisateur.  
  
##  <a name="ad-fs-requirements-in-windows-server-2012-r2"></a>Configuration requise pour les services AD FS dans Windows Server 2012 R2  
 Pour migrer votre batterie AD FS vers Windows Server 2012 R2, vous devez respecter les conditions suivantes :  
  
 Pour AD FS fonctionne, chaque ordinateur que vous souhaitez être une fédération doit être joint à un domaine.  
  
 Pour AD FS s’exécutant sur Windows Server 2012 R2 pour la fonction, votre domaine Active Directory doit exécuter une des opérations suivantes :  
  
- Windows Server 2012 R2  
  
- Windows Server 2012  
  
- Windows Server 2008 R2  
  
- Windows Server 2008  
  
  Si vous envisagez d’utiliser un groupe (gMSA) du compte de Service administré comme compte de service pour AD FS, vous devez disposer d’au moins un contrôleur de domaine dans votre environnement est en cours d’exécution sur le système d’exploitation Windows Server 2012 ou Windows Server 2012 R2.  
  
  Si vous envisagez de déployer le Service DRS (Device Registration Service) pour AD Workplace Join dans le cadre de votre déploiement AD FS, le schéma AD DS doit être mis à jour vers le niveau de Windows Server 2012 R2. Il existe trois façons de mettre à jour le schéma :  
  
1.  Dans une forêt Active Directory existante, exécutez adprep /forestprep à partir du dossier \support\adprep du DVD du système d’exploitation Windows Server 2012 R2 sur un serveur 64 bits qui exécute Windows Server 2008 ou version ultérieure. Dans ce cas, aucun contrôleur de domaine supplémentaire ne doit être installé, et aucun contrôleur de domaine existant ne doit être mis à niveau.  
  
Pour exécuter adprep/forestprep, vous devez être membre du groupe Administrateurs du schéma, du groupe Administrateurs de l'entreprise et du groupe Administrateurs du domaine du domaine qui héberge le contrôleur de schéma.  
  
2. Dans une forêt Active Directory existante, installez un contrôleur de domaine qui exécute Windows Server 2012 R2. Dans ce cas, adprep /forestprep est exécuté automatiquement dans le cadre de l’installation du contrôleur de domaine.  
  
Pendant l’installation du contrôleur de domaine, il est possible que vous deviez spécifier d’autres informations d’identification afin d’exécuter adprep /forestprep.  
  
3. Créer une nouvelle forêt Active Directory en installant AD DS sur un serveur qui exécute Windows Server 2012 R2. Dans ce cas, adprep /forestprep doit-elle pas être exécutée, car le schéma sera initialement créé avec tous les conteneurs nécessaires et les objets pour prendre en charge de DRS.  
  
### <a name="sql-server-support-for-ad-fs-in-windows-server-2012-r2"></a>Prise en charge SQL Server des services AD FS dans Windows Server 2012 R2  
 Si vous voulez créer une batterie AD FS et utiliser SQL Server pour stocker vos données de configuration, vous pouvez utiliser SQL Server 2008 et versions plus récentes, notamment SQL Server 2012.  
  
##  <a name="increasing-your-windows-powershell-limits"></a>Augmentation des limites de Windows PowerShell  
 Si vous disposez de plus de 1 000 approbations de fournisseur de revendications et approbations de partie de confiance dans votre batterie AD FS, ou si l’erreur suivante s’affiche lorsque vous essayez d’exécuter l’outil d’exportation/importation de migration AD FS, vous devez augmenter les limites de Windows PowerShell :  
  
```  
'Exception of type 'System.OutOfMemoryException' was thrown. At E:\dev\ds\security\ADFSv2\Product\Migration\Export-FederationConfiguration.ps1:176 char:21 + $configData = Invoke-Command -ScriptBlock $GetConfig -Argume ...  
```  
  
 Cette erreur s’affiche car la limite de la mémoire par défaut de la session Windows PowerShell est insuffisante. Dans Windows PowerShell 2.0, la mémoire par défaut de la session est 150 Mo. Dans Windows PowerShell 3.0, la mémoire par défaut de la session est 1 024 Mo. Vous pouvez vérifier la limite de la mémoire de la session à distance Windows PowerShell en utilisant la commande suivante : `Get-Item wsman:localhost\Shell\MaxMemoryPerShellMB`. Vous pouvez augmenter la limite en exécutant la commande suivante : `Set-Item wsman:localhost\Shell\MaxMemoryPerShellMB 512`.  
  
## <a name="other-migration-tasks-and-considerations"></a>Autres tâches de migration et éléments à prendre en compte  
 Afin de réussir la migration de votre batterie AD FS vers Windows Server 2012 R2, veillez à tenir compte des éléments suivants :  
  
-   Les scripts de migration situés dans le dossier \support\adfs sur le CD d’installation de Windows Server 2012 R2 nécessitent que vous conserviez les mêmes noms de batterie de serveurs de fédération et le nom d’identité de compte de service que vous avez utilisé dans votre batterie AD FS héritée lors de sa migration vers Windows Server 2012 R2.  
  
-   Si vous voulez migrer une batterie AD FS SQL Server, notez que le processus de migration implique la création d’une instance de base de données SQL dans laquelle vous devez importer les données de configuration d’origine.  
  
## <a name="next-steps"></a>Étapes suivantes
 [Migrer des Services de rôle Active Directory Federation Services vers Windows Server 2012 R2](migrate-ad-fs-service-role-to-windows-server-r2.md)   
 [Migration du serveur de fédération AD FS](migrate-ad-fs-fed-server-r2.md)   
 [Migration de serveur Proxy de fédération AD FS](migrate-fed-server-proxy-r2.md)   
 [Vérification de la Migration des services AD FS vers Windows Server 2012 R2](verify-ad-fs-migration.md)