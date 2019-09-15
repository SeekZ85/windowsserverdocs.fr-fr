---
title: Problèmes connus du service de migration du stockage
description: Problèmes connus et prise en charge de la résolution des problèmes pour Storage migration service, tels que la collecte des journaux pour Support Microsoft.
author: nedpyle
ms.author: nedpyle
manager: siroy
ms.date: 07/09/2019
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: storage
ms.openlocfilehash: 16e62d9232d0ec1b01333d73bc5b4a1555ffbad0
ms.sourcegitcommit: 61767c405da44507bd3433967543644e760b20aa
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/14/2019
ms.locfileid: "70987404"
---
# <a name="storage-migration-service-known-issues"></a>Problèmes connus du service de migration du stockage

Cette rubrique contient des réponses aux problèmes connus liés à l’utilisation de [Storage migration service](overview.md) pour migrer des serveurs.

Le service de migration de stockage est disponible en deux parties : le service dans Windows Server et l’interface utilisateur dans le centre d’administration Windows. Le service est disponible dans Windows Server, le canal de maintenance à long terme, ainsi que Windows Server, canal semi-annuel ; le centre d’administration Windows est disponible sous forme de téléchargement distinct. Nous incluons également périodiquement des modifications dans les mises à jour cumulatives pour Windows Server, publiées via Windows Update. 

Par exemple, Windows Server, version 1903 comprend de nouvelles fonctionnalités et des correctifs pour le service de migration de stockage, qui sont également disponibles pour Windows Server 2019 et Windows Server version 1809 en installant [KB4512534](https://support.microsoft.com/help/4512534/windows-10-update-kb4512534).

## <a name="collecting-logs"></a>Comment collecter des fichiers journaux lors de l’utilisation de Support Microsoft

Le service de migration de stockage contient des journaux des événements pour le service Orchestrator et le service proxy. Le serveur urchestrator contient toujours les journaux des événements, et les serveurs de destination sur lesquels le service proxy est installé contiennent les journaux du proxy. Ces journaux se trouvent sous :

- Journaux des applications et des services \ Microsoft \ Windows \ StorageMigrationService
- Journaux des applications et des services \ Microsoft \ Windows \ StorageMigrationService-proxy

Si vous devez rassembler ces journaux pour une consultation hors connexion ou pour les envoyer à Support Microsoft, un script PowerShell Open source est disponible sur GitHub :

 [Programme d’assistance de Storage migration service](https://aka.ms/smslogs) 

Consultez le fichier Lisez-moi pour plus d’utilisation.

## <a name="storage-migration-service-doesnt-show-up-in-windows-admin-center-unless-managing-windows-server-2019"></a>Le service de migration de stockage n’apparaît pas dans le centre d’administration Windows, sauf si vous gérez Windows Server 2019

Lorsque vous utilisez la version 1809 du centre d’administration Windows pour gérer un Windows Server 2019 Orchestrator, vous ne voyez pas l’option outil pour le service de migration de stockage. 

L’extension du service de migration de stockage du centre d’administration Windows est liée à une version pour gérer uniquement les systèmes d’exploitation Windows Server 2019 version 1809 ou ultérieures. Si vous l’utilisez pour gérer des systèmes d’exploitation Windows Server plus anciens ou des versions préliminaires Insider, l’outil ne s’affiche pas. Ce comportement est normal. 

Pour résoudre, utiliser ou effectuer une mise à niveau vers Windows Server 2019 Build 1809 ou version ultérieure.

## <a name="storage-migration-service-doesnt-let-you-choose-static-ip-on-cutover"></a>Storage migration service ne vous permet pas de choisir une adresse IP statique sur le basculement

Lorsque vous utilisez la version 0,57 de l’extension Storage migration service dans le centre d’administration Windows et que vous atteignez la phase de basculement, vous ne pouvez pas sélectionner une adresse IP statique pour une adresse. Vous êtes contraint d’utiliser DHCP.

Pour résoudre ce problème, dans le centre d’administration Windows, sous **paramètres** > **Extensions** , recherchez une alerte indiquant que la version mise à jour de Storage migration service 0.57.2 est disponible pour l’installation. Vous devrez peut-être redémarrer l’onglet de votre navigateur pour le centre d’administration Windows.

## <a name="storage-migration-service-cutover-validation-fails-with-error-access-is-denied-for-the-token-filter-policy-on-destination-computer"></a>La validation du basculement du service de migration du stockage échoue avec l’erreur « Accès refusé pour la stratégie de filtre de jeton sur l’ordinateur de destination »

Lors de l’exécution de la validation du basculement, vous recevez l’erreur «échec : L’accès est refusé pour la stratégie de filtre de jeton sur l’ordinateur de destination.» Cela se produit même si vous avez fourni des informations d’identification d’administrateur local correctes pour les ordinateurs source et de destination.

Ce problème est causé par une erreur de code dans Windows Server 2019. Le problème se produit lorsque vous utilisez l’ordinateur de destination en tant qu’orchestrateur du service de migration du stockage.

Pour contourner ce problème, installez le service de migration de stockage sur un ordinateur Windows Server 2019 qui n’est pas la destination de migration prévue, puis connectez-vous à ce serveur à l’aide du centre d’administration Windows et effectuez la migration.

Nous l’avons résolu dans une version ultérieure de Windows Server. Veuillez ouvrir un dossier de support via [support Microsoft](https://support.microsoft.com) pour demander la création d’un rétroporter de ce correctif.

## <a name="storage-migration-service-isnt-included-in-windows-server-2019-evaluation-or-windows-server-2019-essentials-edition"></a>Storage migration service n’est pas inclus dans Windows Server 2019 Evaluation ou Windows Server 2019 Essentials Edition

Lorsque vous utilisez le centre d’administration Windows pour vous connecter à une [version d’évaluation de Windows server 2019](https://www.microsoft.com/evalcenter/evaluate-windows-server-2019) ou à l’édition windows server 2019 Essentials, il n’est pas possible de gérer le service de migration de stockage. Le service de migration de stockage n’est pas non plus inclus dans les rôles et les fonctionnalités.

Ce problème est dû à un problème de maintenance dans le support d’évaluation de Windows Server 2019 et Windows Server 2019 Essentials. 

Pour contourner ce problème à des fins d’évaluation, installez une version commerciale, MSDN, OEM ou de licence en volume de Windows Server 2019 et ne l’activez pas. Sans activation, toutes les éditions de Windows Server fonctionnent en mode d’évaluation pendant 180 jours. 

Nous avons résolu ce problème dans une version ultérieure de Windows Server.  

## <a name="storage-migration-service-times-out-downloading-the-transfer-error-csv"></a>Le service de migration du stockage expire le téléchargement de l’erreur de transfert CSV

Lorsque vous utilisez le centre d’administration Windows ou PowerShell pour télécharger le journal CSV d’opérations de transfert (messages détaillés uniquement), vous recevez l’erreur suivante :

 >   Journal de transfert-Vérifiez que le partage de fichiers est autorisé dans votre pare-feu. : Cette opération de demande envoyée à net. TCP : biais : 28940/SMS/service/1/Transfer n’a pas reçu de réponse dans le délai d’expiration configuré (00:01:00). Le temps alloué à cette opération est peut-être une partie d’un délai d’expiration plus long. Cela peut être dû au fait que le service traite toujours l’opération ou parce que le service n’a pas pu envoyer un message de réponse. Envisagez d’incrémenter le délai d’expiration de l’opération (en convertissant le canal/proxy vers IContextChannel et en définissant la propriété OperationTimeout) et vérifiez que le service est en mesure de se connecter au client.

Ce problème est dû à un très grand nombre de fichiers transférés qui ne peuvent pas être filtrés dans le délai d’attente d’une minute par défaut autorisé par le service de migration de stockage. 

Pour contourner ce problème :

1. Sur l’ordinateur Orchestrator, modifiez le fichier *%systemroot%\SMS\Microsoft.StorageMigration.service.exe.config* à l’aide de Notepad. exe pour remplacer la valeur par défaut « sendTimeout » par 10 minutes.

   ```
     <bindings>
      <netTcpBinding>
        <binding name="NetTcpBindingSms"
                 sendTimeout="00:01:00"
   ```

2. Redémarrez le service de migration de stockage sur l’ordinateur Orchestrator. 
3. Sur l’ordinateur Orchestrator, démarrez regedit. exe.
4. Localisez la sous-clé de Registre suivante, puis cliquez dessus : 

   `HKEY_LOCAL_MACHINE\Software\Microsoft\SMSPowershell`

5. Dans le menu Edition, pointez sur Nouveau, puis cliquez sur DWORD Value. 
6. Tapez « WcfOperationTimeoutInMinutes » pour le nom de la valeur DWORD, puis appuyez sur entrée.
7. Cliquez avec le bouton droit sur « WcfOperationTimeoutInMinutes », puis cliquez sur modifier. 
8. Dans la zone données de base, cliquez sur « décimal ».
9. Dans la zone données de la valeur, tapez « 10 », puis cliquez sur OK.
10. Quittez l’éditeur du Registre.
11. Essayez à nouveau de télécharger le fichier CSV d’erreurs uniquement. 

Nous avons l’intention de modifier ce comportement dans une version ultérieure de Windows Server 2019.  

## <a name="cutover-fails-when-migrating-between-networks"></a>Échec du basculement lors de la migration entre des réseaux

Lors de la migration vers un ordinateur de destination s’exécutant sur un réseau différent de celui de la source, par exemple une instance Azure IaaS, le basculement échoue lorsque la source utilise une adresse IP statique. 

Ce comportement est lié à la conception, afin d’éviter les problèmes de connectivité après la migration à partir d’utilisateurs, d’applications et de scripts se connectant via une adresse IP. Lorsque l’adresse IP est déplacée de l’ancien ordinateur source vers la nouvelle cible de destination, elle ne correspond pas aux nouvelles informations de sous-réseau du réseau, et peut-être à DNS et WINS.

Pour contourner ce problème, effectuez une migration vers un ordinateur sur le même réseau. Ensuite, déplacez cet ordinateur vers un nouveau réseau et réaffectez ses informations IP. Par exemple, si vous migrez vers Azure IaaS, migrez d’abord vers une machine virtuelle locale, puis utilisez Azure Migrate pour déplacer la machine virtuelle vers Azure.  

Nous avons résolu ce problème dans une version ultérieure du centre d’administration Windows. Nous vous autorisons maintenant à spécifier des migrations qui ne modifient pas les paramètres réseau du serveur de destination. L’extension mise à jour sera répertoriée ici lors de la publication. 

## <a name="validation-warnings-for-destination-proxy-and-credential-administrative-privileges"></a>Avertissements de validation pour le proxy de destination et les privilèges d’administration des informations d’identification

Lors de la validation d’une tâche de transfert, les avertissements suivants s’affichent :

 > **Les informations d’identification ont des privilèges d’administrateur.**
 > Avertissement : L’action n’est pas disponible à distance.
 > **Le proxy de destination est inscrit.**
 > Avertissement : Le proxy de destination est introuvable.

Si vous n’avez pas installé le service proxy de service de migration de stockage sur l’ordinateur de destination Windows Server 2019, ou si l’ordinateur de destination est Windows Server 2016 ou Windows Server 2012 R2, ce comportement est normal. Nous vous recommandons de migrer vers un ordinateur Windows Server 2019 avec le proxy installé pour améliorer considérablement les performances de transfert.  

## <a name="certain-files-do-not-inventory-or-transfer-error-5-access-is-denied"></a>Certains fichiers ne sont pas inventaires ou transférés, erreur 5 « accès refusé »

Lors de l’inventaire ou du transfert de fichiers d’un ordinateur source vers un ordinateur de destination, la migration des fichiers à partir desquels un utilisateur a supprimé les autorisations du groupe administrateurs échoue. Examen du service de migration de stockage-débogage du proxy :

  Nom du journal :      Source Microsoft-Windows-StorageMigrationService-proxy/débogage :        Microsoft-Windows-StorageMigrationService-date du proxy :          ID d’événement 2/26/2019 9:00:04 AM :      10000 catégorie de tâche : Aucun niveau :         Mots clés d’erreur :      
  Utilisateur :          Ordinateur de SERVICE réseau : description de srv1.contoso.com :

  02/26/2019-09:00:04.860 [erreur] erreur de transfert \\pour SRV1. contoso. com\public\indy.png : (5) l’accès est refusé.
Trace de la pile : au niveau de Microsoft. StorageMigration. proxy. service. Transfer. FileDirUtils. OpenFile (String fileName, DesiredAccess desiredAccess, ShareMode shareMode, CreationDisposition creationDisposition, FlagsAndAttributes flagsAndAttributes) à l’adresse Microsoft. StorageMigration. proxy. service. Transfer. FileDirUtils. GetTargetFile (chemin d’accès de chaîne) au niveau de Microsoft. StorageMigration. proxy. service. Transfer. FileDirUtils. GetTargetFile (fichier FileInfo) à l’adresse Microsoft. StorageMigration. proxy. service. Transfer. FileTransfer. InitializeSourceFileInfo () à Microsoft. StorageMigration. proxy. service. Transfer. FileTransfer. Transfer () à l’adresse Microsoft. StorageMigration. proxy. service. Transfer. FileTransfer. TryTransfer () [d:\os\src\base\dms\proxy\transfer\transferproxy\FileTransfer.cs :: TryTransfer :: 55]


Ce problème est dû à une erreur de code dans le service de migration de stockage où le privilège de sauvegarde n’a pas été appelé. 

Pour résoudre ce problème, installez [Windows Update le 2 avril 2019 — KB4490481 (version 17763,404 du système d’exploitation)](https://support.microsoft.com/help/4490481/windows-10-update-kb4490481) sur l’ordinateur Orchestrator et l’ordinateur de destination si le service proxy y est installé. Assurez-vous que le compte d’utilisateur de migration source est un administrateur local sur l’ordinateur source et le service de migration de stockage Orchestrator. Assurez-vous que le compte d’utilisateur de migration de destination est un administrateur local sur l’ordinateur de destination et le service de migration de stockage Orchestrator. 

## <a name="dfsr-hashes-mismatch-when-using-storage-migration-service-to-preseed-data"></a>Incompatibilité de hachages DFSR lors de l’utilisation du service de migration de stockage pour préamorcer des données

Lorsque vous utilisez le service de migration de stockage pour transférer des fichiers vers une nouvelle destination, en configurant le réplication DFS (DFSR) pour répliquer ces données avec un serveur DFSR existant via la réplication prédéfinie ou le clonage de base de données DFSR, tous les fichiers experiemce un hachage discordance et sont à nouveau répliquées. Les flux de données, les flux de sécurité, les tailles et les attributs semblent être parfaitement mis en correspondance après l’utilisation de SMS pour les transférer. L’examen des fichiers avec ICACLS ou le journal de débogage de clonage de base de données DFSR révèle :

Fichier source :

  icacls d:\test\Source :

  icacls d:\test\thatcher.png/Save out. txt/t Thatcher. png D :AI (A ;; FA ;;; BA) (A ;; 0 x1200a9 ;;;D D) (A ;; 0 x1301bf ;;;D U) (A ; ID ; FA ;;; BA) (A ; ID ; FA ;;; SY) (A ; ID ; ACE 0x1200a9 ;;; BU

Fichier de destination :

  icacls d:\test\thatcher.png/Save out. txt/t Thatcher. png D :AI (A ;; FA ;;; BA) (A ;; 0 x1301bf ;;;D U) (A ;; 0 x1200a9 ;;;D D) (A ; ID ; FA ;;; BA) (A ; ID ; FA ;;; SY) (A ; ID ; ACE 0x1200a9 ;;; BU)**S :PAINO_ACCESS_CONTROL**

Journal de débogage DFSR :

  20190308 10:18:53.116 3948 DBCL 4045 [WARN] DBClone :: IDTableImportUpdate enregistrement incompatibilité a été trouvé. 

  Hachage de la liste de contrôle d’accès local : 1BCDFE03-A18BCE01-D1AE9859-23A0A5F6 LastWriteTime : 20190308 18:09:44.876 FileSizeLow : 1131654 FileSizeHigh : 0 Attributs : 32 

  Clone ACL Hash :**DDC4FCE4-DDF329C4-977CED6D-F4D72A5B** LastWriteTime : 20190308 18:09:44.876 FileSizeLow : 1131654 FileSizeHigh : 0 Attributs : 32 

Ce problème est dû à un défaut de code dans une bibliothèque utilisée par le service de migration de stockage pour définir des ACL d’audit de sécurité (SACL). Une liste SACL non null est définie de manière involontaire lorsque la liste SACL était vide, ce qui a pour but d’identifier correctement une incompatibilité de hachage. 

Pour contourner ce problème, continuez à utiliser Robocopy pour les [opérations de clonage de base de données DFSR et DFSR](../dfs-replication/preseed-dfsr-with-robocopy.md) au lieu du service de migration de stockage. Nous étudions ce problème et nous envisageons de le résoudre dans une version ultérieure de Windows Server et éventuellement un Windows Update en sortie. 

## <a name="error-404-when-downloading-csv-logs"></a>Erreur 404 lors du téléchargement des journaux CSV

Lorsque vous tentez de télécharger les journaux de transfert ou d’erreurs à la fin d’une opération de transfert, vous recevez l’erreur suivante :

  $jobname : Journal de transfert : erreur Ajax 404

Cette erreur est attendue si vous n’avez pas activé la règle de pare-feu « partage de fichiers et d’imprimantes (SMB-in) » sur le serveur Orchestrator. Les téléchargements de fichiers du centre d’administration Windows nécessitent le port TCP/445 (SMB) sur les ordinateurs connectés.  

## <a name="error-couldnt-transfer-storage-on-any-of-the-endpoints-when-transferring-from-windows-server-2008-r2"></a>Erreur « Impossible de transférer le stockage sur l’un des points de terminaison » lors du transfert à partir de Windows Server 2008 R2

Lorsque vous tentez de transférer des données à partir d’un ordinateur source Windows Server 2008 R2, aucun transfert de données ne s’affiche et vous recevez l’erreur suivante :  

  Impossible de transférer le stockage sur l’un des points de terminaison.
0x9044

Cette erreur est attendue si votre ordinateur Windows Server 2008 R2 n’est pas entièrement corrigé avec toutes les mises à jour critiques et importantes de Windows Update. Quel que soit le service de migration de stockage, nous vous recommandons de toujours mettre à jour un ordinateur Windows Server 2008 R2 à des fins de sécurité, car ce système d’exploitation ne contient pas les améliorations de sécurité des versions plus récentes de Windows Server.

## <a name="error-couldnt-transfer-storage-on-any-of-the-endpoints-and-check-if-the-source-device-is-online---we-couldnt-access-it"></a>Erreur « Impossible de transférer le stockage sur l’un des points de terminaison » et « vérifiez si l’appareil source est en ligne, nous n’avons pas pu y accéder ».

Lorsque vous tentez de transférer des données à partir d’un ordinateur source, certains ou tous les partages ne sont pas transférés, avec une erreur de Résumé :

   Impossible de transférer le stockage sur l’un des points de terminaison.
0x9044

L’examen des détails du transfert SMB affiche l’erreur suivante :

   Vérifiez si l’appareil source est en ligne, nous n’avons pas pu y accéder.

L’examen du journal des événements StorageMigrationService/admin affiche :

   Impossible de transférer le stockage.

   Attente ID Job1 :  
   État : Échec de l’erreur : Message d’erreur 36931 : 

   Instructions : Vérifiez l’erreur détaillée et assurez-vous que les conditions de transfert sont remplies. La tâche de transfert n’a pas pu transférer les ordinateurs source et de destination. Cela peut être dû au fait que l’ordinateur Orchestrator n’a pu atteindre aucun ordinateur source ou de destination, peut-être en raison d’une règle de pare-feu ou d’autorisations manquantes.

L’examen du journal StorageMigrationService-proxy/Debug affiche :

   07/02/2019-13:35:57.231 [erreur] échec de la validation du transfert. ErrorCode 40961, le point de terminaison source n’est pas accessible ou n’existe pas, les informations d’identification source ne sont pas valides, ou l’utilisateur authentifié ne dispose pas des autorisations suffisantes pour y accéder.
à Microsoft. StorageMigration. proxy. service. Transfer. TransferOperation. Validate () à Microsoft. StorageMigration. proxy. service. Transfer. TransferRequestHandler. ProcessRequest (FileTransferRequest fileTransferRequest, Guid operationId)    [d:\os\src\base\dms\proxy\transfer\transferproxy\TransferRequestHandler.cs::

Cette erreur est attendue si votre compte de migration ne dispose pas au minimum d’autorisations d’accès en lecture aux partages SMB. Pour contourner cette erreur, ajoutez un groupe de sécurité contenant le compte de migration source aux partages SMB sur l’ordinateur source et accordez-lui l’autorisation lecture, modification ou contrôle total. Une fois la migration terminée, vous pouvez supprimer ce groupe.

## <a name="error-0x80005000-when-running-inventory"></a>Erreur 0x80005000 lors de l’exécution de l’inventaire

Après l’installation de [KB4512534](https://support.microsoft.com/en-us/help/4512534/windows-10-update-kb4512534) et la tentative d’exécution de l’inventaire, l’inventaire échoue avec des erreurs :

  EXCEPTION DE HRESULT : 0x80005000
  
  Nom du journal :      Source Microsoft-Windows-StorageMigrationService/admin :        Microsoft-Windows-StorageMigrationService Date :          ID d’événement 9/9/2019 5:21:42 PM :      2503 catégorie de tâche : Aucun niveau :         Mots clés d’erreur :      
  Utilisateur :          Ordinateur de SERVICE réseau :      FS02. Description de TailwindTraders.net : Impossible d’inventorier les ordinateurs.
Tâche : ID foo2 : État de 20ac3f75-4945-41d1-9a79-d11dbb57798b : Échec de l’erreur : Message d’erreur 36934 : Échec de l’inventaire pour tous les appareils : Vérifiez l’erreur détaillée et assurez-vous que les conditions d’inventaire sont remplies. Le travail n’a pas pu inventorier les ordinateurs source spécifiés. Cela peut être dû au fait que l’ordinateur Orchestrator n’a pas pu l’atteindre sur le réseau, peut-être en raison d’une règle de pare-feu ou d’autorisations manquantes.
  
  Nom du journal :      Source Microsoft-Windows-StorageMigrationService/admin :        Microsoft-Windows-StorageMigrationService Date :          ID d’événement 9/9/2019 5:21:42 PM :      2509 catégorie de tâche : Aucun niveau :         Mots clés d’erreur :      
  Utilisateur :          Ordinateur de SERVICE réseau :      FS02. Description de TailwindTraders.net : Impossible d’inventorier un ordinateur.
Travail : ordinateur foo2 : FS01. État de TailwindTraders.net : Échec de l’erreur :-2147463168 message d’erreur : Instructions : Vérifiez l’erreur détaillée et assurez-vous que les conditions d’inventaire sont remplies. L’inventaire n’a pas pu déterminer les aspects de l’ordinateur source spécifié. Cela peut être dû à des autorisations ou des privilèges manquants sur la source ou sur un port de pare-feu bloqué.
  
Cette erreur est due à un défaut de code dans le service de migration de stockage lorsque vous fournissez des informations d’identification de migration sous la forme d’un nom d'meghan@contoso.comutilisateur principal (UPN), tel que «». Le service d’analyse du service de migration du stockage ne parvient pas à analyser ce format correctement, ce qui provoque un échec dans une recherche de domaine qui a été ajoutée pour la prise en charge de la migration de cluster dans KB4512534 et 19H1.

Pour contourner ce problème, fournissez les informations d’identification au format domaine\utilisateur, par exemple « Contoso\Meghan ».

## <a name="error-serviceerror0x9006-or-the-proxy-isnt-currently-available-when-migrating-to-a-windows-server-failover-cluster"></a>Erreur « ServiceError0x9006 » ou « le proxy n’est pas disponible actuellement ». lors de la migration vers un cluster de basculement Windows Server

Lorsque vous tentez de transférer des données sur un serveur de fichiers en cluster, vous recevez des erreurs telles que : 

   Assurez-vous que le service proxy est installé et en cours d’exécution, puis réessayez. Le proxy n’est pas disponible actuellement.
0x9006 ServiceError0x9006, Microsoft. StorageMigration. Commands. UnregisterSmsProxyCommand

Cette erreur est attendue si la ressource de serveur de fichiers a été déplacée de son nœud propriétaire de cluster Windows Server 2019 d’origine vers un nouveau nœud et que la fonctionnalité de proxy de service de migration de stockage n’a pas été installée sur ce nœud.

Pour résoudre ce problème, replacez la ressource du serveur de fichiers de destination sur le nœud de cluster propriétaire d’origine qui était utilisé lorsque vous avez configuré pour la première fois les jumelages de transfert.

Une autre solution de contournement consiste à :

1. Installez la fonctionnalité de proxy du service de migration de stockage sur tous les nœuds d’un cluster.
2. Exécutez la commande PowerShell de service de migration de stockage suivante sur l’ordinateur Orchestrator : 

   ```PowerShell
   Register-SMSProxy -ComputerName *destination server* -Force
   ```

## <a name="see-also"></a>Voir aussi

- [Vue d’ensemble de Storage migration service](overview.md)
