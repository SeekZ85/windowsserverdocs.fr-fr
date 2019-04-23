---
title: dfsrmig
description: 'Rubrique de commandes de Windows pour ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e1b6a464-6a93-4e66-9969-04f175226d8d
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: da05aec5ca5a5634585c5f5406181c5c90ee3a30
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59856940"
---
# <a name="dfsrmig"></a>dfsrmig

>S'applique à : Windows Server (canal semi-annuel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Le `dfsrmig` commande migre la réplication SYSvol dans le Service de réplication de fichiers (FRS) à la réplication de système de fichiers distribués (DFS, Distributed File System), fournit des informations sur la progression de la migration et modifie des objets active directory Domain Services (AD DS) prend en charge la migration.
Pour obtenir des exemples montrant comment utiliser cette commande, consultez le [exemples](#BKMK_examples) section plus loin dans ce document.
## <a name="syntax"></a>Syntaxe
```
dfsrmig [/SetGlobalState <state> | /GetGlobalState | /GetMigrationState | /createGlobalObjects | 
/deleteRoNtfrsMember [<read_only_domain_controller_name>] | /deleteRoDfsrMember [<read_only_domain_controller_name>] | /?]
```
## <a name="parameters"></a>Paramètres
|Paramètre|Description|
|-------|--------|
|/SetGlobalState <state>|Définit l’état de migration de globales souhaitée pour le domaine à l’état qui correspond à la valeur spécifiée par *état*.<br /><br />Pour poursuivre la migration ou les processus de restauration, utilisez cette commande pour faire défiler les états valides. Cette option vous permet de lancer et de contrôler le processus de migration en définissant l’état de la migration globale dans AD DS sur l’émulateur de contrôleur de domaine principal. Si l’émulateur de contrôleur de domaine principal n’est pas disponible, cette commande échoue.<br /><br /> Vous pouvez uniquement définir l’état de migration global à un état stable. Les valeurs valides pour *état*, par conséquent, sont **0** pour l’état de démarrage, **1** pour l’état préparé, **2** pour l’état redirigé, et **3** pour l’état éliminé.<br /><br />Migration vers l’état éliminé est irréversible et de restauration à partir de cet état n’est pas possible, par conséquent, utilisez la valeur **3** pour *état* uniquement lorsque vous êtes entièrement committd à l’utilisation de la réplication DFS pour SYSvol réplication.|
|/GetGlobalState|Récupère l’état actuel de la migration globale pour le domaine à partir de la copie locale de la base de données AD DS, en cas d’exécution sur l’émulateur PDC.<br /><br />Utilisez cette option pour confirmer que vous définissez l’état de migration global correct. Seuls les États de la migration stable peuvent être des États de migration global, par conséquent, les résultats qui le **dfsrmig** commande rapports avec la **/GetGlobalState** option correspondent aux États que vous pouvez définir avec le **/SetGlobalState** option.<br /><br />Vous devez exécuter le **dfsrmig** commande avec le **/GetGlobalState** option uniquement sur l’émulateur PDC. la réplication Active directory réplique l’état global pour les autres contrôleurs de domaine dans le domaine, mais les latences de réplication peuvent provoquer des incohérences si vous exécutez le **dfsrmig** avec la **/GetGlobalState**  option sur un contrôleur de domaine autre que l’émulateur PDC. Pour vérifier l’état de migration local d’un contrôleur de domaine autre que l’émulateur de contrôleur de domaine principal, utilisez la **/GetMigrationState** plutôt l’option.|
|/GetMigrationState|Récupère l’état actuel de la migration local pour tous les contrôleurs de domaine dans le domaine et détermine si ces États locales correspond à l’état actuel de la migration globale.<br /><br />Utilisez cette option pour déterminer si tous les contrôleurs de domaine ont atteint l’état de la migration globale. La sortie de la **dsfrmig** commande lorsque vous utilisez le **/GetMigrationState** option indique si ou n’est pas la migration de l’état global en cours est terminée, et il répertorie l’état de migration local pour toutes contrôleurs de domaine qui n’ont pas atteint l’état actuel de la migration globale. État de migration local pour les contrôleurs de domaine peut inclure des États de transition pour les contrôleurs de domaine qui n’ont pas atteint l’état actuel de la migration globale.|
|/createGlobalObjects|crée les objets globaux et les paramètres dans les services AD DS qui utilise la réplication DFS.<br /><br />Vous ne devez pas utiliser cette option lors d’un processus de migration normal, car le service de réplication DFS crée automatiquement ces paramètres et les objets AD DS lors de la migration à partir de l’état de démarrage à l’état préparé. Utilisez cette option pour créer manuellement ces objets et des paramètres dans les situations suivantes :<br /><br />-   **Un nouveau contrôleur de domaine en lecture seule est promu au cours de migration**. Le service de réplication DFS crée automatiquement les objets AD DS et les paramètres pour la réplication DFS lors de la migration à partir de l’état de démarrage à l’état préparé. Si un contrôleur de domaine en lecture seule est promu dans le domaine après cette transition, mais avant la migration vers l’état éliminé, puis les objets qui correspondent au contrôleur de domaine de lecture seule qui vient d’être activée ne sont pas créés dans AD DS à l’origine de la réplication et Échec de la migration.<br />-Dans ce cas, vous pouvez exécuter la **dfsrmig** commande empêchait le **/createGlobalObjects** option permettant de créer manuellement les objets sur des contrôleurs de domaine en lecture seule qui n’est pas déjà les. Exécution de cette commande n’affecte pas les contrôleurs de domaine qui ont déjà des objets et des paramètres pour le service de réplication DFS.<br />-   **Les paramètres globaux pour le service de réplication DFS sont manquants ou ont été supprimées**. Si ces paramètres sont manquants pour un contrôleur de domaine particulier, la migration à partir de l’état de démarrage à l’état prêt s’arrête au niveau de l’état de transition de préparation du contrôleur de domaine. Dans ce cas, vous pouvez utiliser la **dfsrmig** commande avec le **/createGlobalObjects** option permettant de créer manuellement les paramètres. **Remarque :** Étant donné que les paramètres globaux de services AD DS pour le service de réplication DFS pour un contrôleur de domaine en lecture seule sont créés sur l’émulateur de contrôleur de domaine principal, ces paramètres nécessaires pour répliquer vers le contrôleur de domaine en lecture seule à partir de l’émulateur PDC avant que le service de réplication DFS sur le Ces paramètres permettent au contrôleur de domaine en lecture seule. En raison de latences de réplication active IRE, cette réplication peut prendre un certain temps à se produire.|
|/deleteRoNtfrsMember [< read_only_domain_controller_name >]|Supprime les paramètres AD DS globaux pour la réplication FRS qui correspondent à ce contrôleur de domaine en lecture seule, ou supprime les paramètres globaux de services AD DS pour la réplication FRS pour tous les contrôleurs de domaine en lecture seule si aucune valeur n’est spécifiée pour *read_only_ nom_contrôleur_domaine*.<br /><br />Vous ne devez pas utiliser cette option lors d’un processus de migration normal, car le service de réplication DFS supprime automatiquement ces paramètres AD DS lors de la migration de l’état redirigée vers l’état éliminé. Étant donné que les contrôleurs de domaine en lecture seule ne peut pas supprimer ces paramètres à partir d’AD DS, l’émulateur PDC effectue cette opération, et les modifications seront répliquées par la suite aux contrôleurs de domaine en lecture seule après les latences applicables pour la réplication active directory.<br /><br />Vous utilisez cette option pour supprimer manuellement les paramètres AD DS uniquement lorsque la suppression automatique échoue sur un contrôleur de domaine en lecture seule et entrave le contrôleur de domaine en lecture seule pour un ime long pendant la migration à partir de l’état redirigée vers l’état éliminé.|
|/deleteRoDfsrMember [<read_only_domain_controller_name>]|Supprime les paramètres AD DS globaux pour la réplication DFS qui correspondent à ce contrôleur de domaine en lecture seule, ou supprime les paramètres globaux de services AD DS pour la réplication DFS pour tous les contrôleurs de domaine en lecture seule si aucune valeur n’est spécifiée pour *read_only_ nom_contrôleur_domaine*.<br /><br />Utilisez cette option pour supprimer manuellement les paramètres AD DS uniquement lorsque la suppression automatique échoue sur un contrôleur de domaine en lecture seule et entrave le contrôleur de domaine en lecture seule pendant un long temps lors de la restauration de la migration à partir de l’état préparé dans l’état de démarrage.|
|/?|Affiche l'aide à l'invite de commandes. Équivaut à exécuter **dfsrmig** sans aucune option.|
## <a name="remarks"></a>Notes
-   DFSRMIG.exe, l’outil de migration pour le service de réplication DFS, est installé avec le service de réplication DFS.
    pour un nouveau serveur Windows Server 2008, Dcpromo.exe installe et démarre le service de réplication DFS lorsque vous promouvez l’ordinateur à un contrôleur de domaine. Lorsque vous mettez à niveau un serveur à partir de Windows Server 2003 vers Windows Server 2008, les installations de mise à niveau et démarre le service de réplication DFS. Vous n’avez pas besoin d’installer le service de rôle réplication DFS pour que le service de réplication DFS installé et démarré.
-   Le **dfsrmig** outil est pris en charge uniquement sur des contrôleurs de domaine qui s’exécutent au niveau fonctionnel de domaine Windows Server 2008, étant donné que SYSvol migration de FRS vers la réplication DFS est uniquement possible sur les contrôleurs de domaine qui fonctionnent à la  Niveau fonctionnel du domaine Windows Server 2008.
-   Vous pouvez exécuter la **dfsrmig** objets de commande sur n’importe quel contrôleur de domaine, mais les opérations qui créent ou manipulent les services AD DS sont autorisés uniquement sur les contrôleurs de domaine compatible en lecture-écriture (pas sur les contrôleurs de domaine en lecture seule).
-   En cours d’exécution **dfsrmig** sans aucune option affiche l’aide à l’invite de commandes.
## <a name="BKMK_examples"></a>Exemples
Pour définir l’état de migration global préparée (**1**) et de lancer la migration vers ou restauration à partir de l’état préparé, type :
```
dfsrmig /SetGlobalState 1
```
Pour définir l’état de migration global pour démarrer (**0**) et lancer la restauration de l’état de démarrage, type :
```
dfsrmig /SetGlobalState 0
```
Pour afficher l’état de migration global, tapez :
```
dfsrmig /GetGlobalState
```
Cet exemple montre l’exemple de résultat à partir de la **dfsrmig /GetGlobalState** commande.
```
Current DFSR global state:  Prepared 
Succeeded.
```
Pour afficher les informations sur indique si les États de migration local sur tous les contrôleurs de domaine correspond à l’état global de migration et les États de migration local pour des contrôleurs de domaine dans lequel l’état local ne correspond pas à l’état global, tapez :
```
dfsrmig /GetMigrationState
```
Cet exemple montre l’exemple de résultat à partir de la **dfsrmig /GetMigrationState** commande quand les États de migration local sur tous les contrôleurs de domaine correspond à l’état de la migration globale.
```
All Domain Controllers have migrated successfully to Global state ( Prepared ).
Migration has reached a consistent state on all Domain Controllers.
Succeeded.
```
Cet exemple montre l’exemple de résultat à partir de la **dfsrmig /GetMigrationState** commande lorsque les États de migration locale sur certains contrôleurs de domaine ne correspondent pas à l’état de la migration globale.
```
The following Domain Controllers are not in sync with Global state ( Prepared ):
Domain Controller (Local Migration State)   DC type
=========
CONTOSO-DC2 ( start )   ReadOnly DC
CONTOSO-DC3 ( Preparing )   Writable DC
Migration has not yet reached a consistent state on all domain controllers
State information might be stale due to AD latency.
```
Pour créer les objets globaux et les paramètres qui utilise la réplication DFS dans AD DS sur des contrôleurs de domaine dans lequel ces paramètres n'ont pas été créés automatiquement pendant la migration ou où ces paramètres sont manquants, tapez :
```
dfsrmig /createGlobalObjects
```
Pour supprimer les paramètres globaux de services AD DS pour la réplication FRS pour un contrôleur de domaine en lecture seule nommée contoso-CD2 si ces paramètres n’ont pas supprimés automatiquement supprimé par le processus de migration, tapez :
```
dfsrmig /deleteRoNtfrsMember contoso-dc2
```
Pour supprimer les paramètres globaux de services AD DS pour la réplication FRS pour tous les contrôleurs de domaine en lecture seule si ces paramètres ne sont pas supprimés automatiquement par le processus de migration, tapez :
```
dfsrmig /deleteRoNtfrsMember
```
Pour supprimer les paramètres globaux de services AD DS pour la réplication DFS pour un contrôleur de domaine en lecture seule nommée contoso-CD2 si ces paramètres ne sont pas supprimés automatiquement par le processus de migration, tapez :
```
dfsrmig /deleteRoDfsrMember contoso-dc2
```
Pour supprimer les paramètres globaux de services AD DS pour la réplication DFS pour tous les contrôleurs de domaine en lecture seule si ces paramètres ne sont pas supprimés automatiquement par le processus de migration, tapez :
```
dfsrmig /deleteRoDfsrMember
```
## <a name="additional-references"></a>Références supplémentaires
[Clé de la syntaxe de ligne de commande](https://go.microsoft.com/fwlink/?LinkId=122056)

[Série de Migration de SYSvol : Part 2 dfsrmig.exe: L’outil de Migration SYSvol](https://go.microsoft.com/fwlink/?LinkID=121757)
