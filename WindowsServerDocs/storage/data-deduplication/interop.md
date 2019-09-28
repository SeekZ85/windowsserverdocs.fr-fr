---
ms.assetid: 60fca6b2-f1c0-451f-858f-2f6ab350d220
title: Interopérabilité de la déduplication des données
ms.technology: storage-deduplication
ms.prod: windows-server
ms.topic: article
author: wmgries
manager: klaasl
ms.author: wgries
ms.date: 09/16/2016
ms.openlocfilehash: fb3c9842f1d698151bffebbe5f77618c8b19b366
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71403200"
---
# <a name="data-deduplication-interoperability"></a>Interopérabilité de la déduplication des données

> S’applique à : Windows Server (canal semi-annuel), Windows Server 2016, Windows Server 2019

## <a name="supported"></a>Prise en charge

### <a name="refs"></a>ReFS
La déduplication des données est prise en charge à partir de Windows Server 2019. 

### <a name="failover-clustering"></a>Clustering de basculement

Le [clustering de basculement](../..//failover-clustering/failover-clustering-overview.md) est entièrement pris en charge si la [fonctionnalité de déduplication des données](install-enable.md#install-dedup) est installée sur chaque nœud du cluster. Autres remarques importantes :

* Des [travaux de déduplication des données démarrés manuellement](run.md#running-dedup-jobs-manually) doivent être exécutés sur le nœud Propriétaire du volume partagé de cluster.
* Les travaux planifiés de la déduplication des données sont stockés dans la tâche de cluster planifiée, si bien que si le volume dédupliqué est repris par un autre nœud, la tâche planifiée est appliquée au prochain intervalle planifié.
* La déduplication des données interagit entièrement avec la fonctionnalité de [mise à niveau propagée du système d’exploitation du cluster](../..//failover-clustering/cluster-operating-system-rolling-upgrade.md).
* La déduplication des données est entièrement prise en charge sur les volumes NTFS des [espaces de stockage direct](../storage-spaces/storage-spaces-direct-overview.md) (miroir ou parité). La déduplication n’est pas prise en charge sur les volumes à plusieurs niveaux. Pour plus d’informations, consultez [Déduplication des données sur ReFS](#unsupported).

### <a name="storage-replica"></a>Réplica de stockage
[Le réplica de stockage](../storage-replica/storage-replica-overview.md) est entièrement pris en charge. La déduplication des données doit être configurée de manière à ne pas s’exécuter sur la copie secondaire.

### <a name="branchcache"></a>BranchCache
Vous pouvez optimiser l’accès aux données sur le réseau en activant [BranchCache](../../networking/branchcache/branchcache.md) sur les serveurs et les clients. Quand un système prenant en charge BranchCache communique sur un réseau étendu (WAN) avec un serveur de fichiers distant qui exécute la déduplication des données, tous les fichiers dédupliqués sont déjà indexés et hachés. Par conséquent, les demandes de données provenant d’une filiale sont rapidement traitées. Cela revient à préindexer ou préhacher un serveur qui prend en charge BranchCache.

### <a name="dfs-replication"></a>Réplication DFS
La déduplication des données fonctionne avec la réplication du système de fichiers DFS. L’optimisation ou la non optimisation d’un fichier ne déclenche de réplication car le fichier ne change pas. La réplication DFS utilise la compression différentielle à distance (RPC), pas les blocs du magasin de blocs, pour réaliser des économies de réseau. Les fichiers du réplica peuvent également être optimisés à l’aide de la déduplication si le réplica utilise la déduplication des données.

### <a name="quotas"></a>quotas.
La déduplication des données ne prend pas en charge la création d’un quota inconditionnel sur un dossier racine de volume sur lequel la déduplication est également activée. Lorsqu’un quota inconditionnel est présent sur une racine du volume, l’espace libre réel sur le volume et l’espace limité par le quota sur le volume sont différents. Cela peut entraîner l’échec des travaux d’optimisation de la déduplication. Il est possible cependant de créer un quota conditionnel sur une racine de volume sur laquelle la déduplication est activée. 

Quand le quota est activé sur un volume dédupliqué, il tient compte de la taille logique du fichier et non de sa taille physique. L’utilisation de quotas (y compris tous les seuils de quotas) n’est pas modifiée lorsqu’un fichier est traité par déduplication. Toutes les autres fonctionnalités de quota, notamment les quotas conditionnels de racine de volume et les quotas sur les sous-dossiers, fonctionnent normalement quand la déduplication est utilisée.

### <a name="windows-server-backup"></a>Sauvegarde Windows Server
La Sauvegarde Windows Server peut sauvegarder un volume optimisé en l’état (autrement dit, sans supprimer les données dédupliquées). Les étapes suivantes montrent comment sauvegarder un volume et comment restaurer un volume ou certains fichiers d’un volume.
1. Installez la Sauvegarde Windows Server.  
    ```PowerShell
    Install-WindowsFeature -Name Windows-Server-Backup
    ```

2. Sauvegardez le volume E: sur un autre volume en exécutant la commande suivante, en adaptant les noms de volume appropriés à votre cas.  
    ```PowerShell
    wbadmin start backup –include:E: -backuptarget:F: -quiet
    ```
3. Obtenez l’ID de version de la sauvegarde que vous venez de créer.

    ```PowerShell
    wbadmin get versions
    ```

    Cet ID de version de sortie est une chaîne de date et d’heure, par exemple : 08/18/2016-06:22.

4. Restaurez l’intégralité du volume.
    ```PowerShell
    wbadmin start recovery –version:02/16/2012-06:22 -itemtype:Volume  -items:E: -recoveryTarget:E:
    ```

    **--OU--**  

    Restaurer un dossier particulier (dans ce cas, le dossier E:\Docs) :
    ```PowerShell
    wbadmin start recovery –version:02/16/2012-06:22 -itemtype:File  -items:E:\Docs  -recursive
    ```

## <a name="unsupported"></a>Non pris en charge

### <a name="windows-10-client-os"></a>Windows 10 (système d’exploitation client)
La déduplication des données n’est pas prise en charge sur Windows 10. Il existe plusieurs billets de blog connus dans la communauté Windows décrivant comment supprimer les fichiers binaires de Windows Server 2016 et les installer sur Windows 10, mais ce scénario n’a pas été validé dans le cadre du développement de la déduplication des données. [Votez pour cet élément pour Windows 10 sur Windows Server Storage UserVoice](https://windowsserver.uservoice.com/forums/295056-storage/suggestions/9011008-add-deduplication-support-to-client-os).

### <a name="windows-search"></a>Windows Search
Windows Search ne prend pas en charge la déduplication des données. La déduplication des données utilise des points d’analyse que Windows Search ne peut pas indexer. De ce fait, Windows Search ignore tous les fichiers dédupliqués, les excluant ainsi de l’index. Par conséquent, les résultats de recherche peuvent être incomplets pour les volumes dédupliqués. [Votez pour cet élément pour Windows Server vNext sur Windows Server Storage UserVoice](https://windowsserver.uservoice.com/forums/295056-storage/suggestions/17888647-make-windows-search-service-work-with-data-dedupli).

### <a name="robocopy"></a>Robocopy
L’exécution de Robocopy avec une déduplication des données n’est pas recommandée car certaines commandes Robocopy peuvent endommager le magasin de blocs. Le magasin de blocs est stocké dans le dossier System Volume Information d’un volume. Si ce dossier est supprimé, les fichiers optimisés (points d’analyse) qui sont copiés à partir du volume source sont endommagés, car les blocs de données ne sont pas copiés sur le volume de destination.
