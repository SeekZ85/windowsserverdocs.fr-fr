---
title: winnt32
description: 'Rubrique de commandes de Windows pour ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5a0a6fb3-ba4e-4ace-8984-7f6d3875560e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 28675ac6d5a1f1a7f56a9b72ef11a3e99e4ed130
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59851260"
---
# <a name="winnt32"></a>winnt32

>S'applique à : Windows Server (canal semi-annuel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Effectue une installation ou la mise à niveau vers un produit dans Windows Server 2003. Vous pouvez exécuter **winnt32** à l’invite de commandes sur un ordinateur exécutant Windows 95, Windows 98, Windows Millennium edition, Windows NT, Windows 2000, Windows XP ou un produit dans Windows Server 2003. Si vous exécutez **winnt32** sur un ordinateur exécutant Windows NT version 4.0, vous devez tout d’abord appliquer des Service Pack 5 ou version ultérieure.
## <a name="syntax"></a>Syntaxe
```
winnt32 [/checkupgradeonly] [/cmd: <CommandLine>] [/cmdcons] [/copydir:{i386|ia64}\<FolderName>] [/copysource: <FolderName>] [/debug[<Level>]:[ <FileName>]] [/dudisable] [/duprepare: <pathName>] [/dushare: <pathName>] [/emsport:{com1|com2|usebiossettings|off}] [/emsbaudrate: <BaudRate>] [/m: <FolderName>]  [/makelocalsource] [/noreboot] [/s: <Sourcepath>] [/syspart: <DriveLetter>] [/tempdrive: <DriveLetter>] [/udf: <ID>[,<UDB_File>]] [/unattend[<Num>]:[ <AnswerFile>]]
```
### <a name="parameters"></a>Paramètres
|Paramètre|Description|
|-------|--------|
|/checkupgradeonly|Vérifie si votre ordinateur pour la compatibilité de mise à niveau avec les produits de Windows Server 2003.<br /><br />Si vous utilisez cette option avec **/ unattend**, aucune entrée utilisateur n’est requise.  Sinon, les résultats sont affichés sur l’écran, et vous pouvez les enregistrer sous le nom de fichier que vous spécifiez. Le nom de fichier par défaut est **upgrade.txt** dans le dossier systemroot.|
|/cmd|Indique le programme d’installation pour exécuter une commande spécifique avant la phase finale du programme d’installation. Cela se produit une fois que votre ordinateur a redémarré et une fois le programme d’installation a collecté les informations de configuration nécessaires, mais avant le programme d’installation est terminée.|
|\<CommandLine>|Spécifie la ligne de commande à exécuter avant la phase finale du programme d’installation.|
|/cmdcons|Sur un ordinateur basé sur le x86, installe la Console de récupération comme option de démarrage.  La Console de récupération est une interface de ligne de commande à partir de laquelle vous pouvez effectuer des tâches comme le démarrage et arrêt des services et l’accès au lecteur local (y compris les lecteurs formatés avec NTFS). Vous pouvez uniquement utiliser le **/cmdcons** option une fois le programme d’installation est terminée.|
|/copydir|Crée un dossier supplémentaire dans le dossier dans lequel sont installés les fichiers de système d’exploitation.  par exemple, pour x86 et ordinateurs x64 64, vous pouvez créer un dossier appelé *Pilotes_privés* dans le dossier source i386 pour votre installation et place les fichiers de pilote dans le dossier. type **/copydir : i386\\*** Pilotes_privés* pour que le programme d’installation copie ce dossier sur votre ordinateur nouvellement installé, ce qui le nouvel emplacement de dossier **systemroot** \\*Pilotes_privés *.<br /><br />-   **i386** spécifie i386<br />-   **ia64** spécifie ia64<br /><br />Vous pouvez utiliser **/copydir** pour créer des dossiers supplémentaires autant que vous le souhaitez.|
|\<FolderName>|Spécifie le dossier que vous avez créé pour conserver des modifications de votre site.|
|/copysource|Crée un dossier temporaire supplémentaire dans le dossier dans lequel sont installés les fichiers de système d’exploitation. Vous pouvez utiliser **/copysource** pour créer des dossiers supplémentaires autant que vous le souhaitez.<br /><br />Contrairement aux dossiers **/copydir** crée, **/copysource** sont supprimés une fois l’installation terminée.|
|/debug|Crée un journal de débogage au niveau spécifié, par exemple, **/debug4:Debug.log**.  Le fichier de journal par défaut est **C:\ systemroot\winnt32.log**, et|
|\<level>|Les valeurs de niveau et les descriptions<br /><br />-   0: Erreurs graves<br />-   1: Erreurs<br />-   2: Niveau par défaut. Avertissements<br />-   3: Informations<br />-4 : des informations détaillées sur le débogage<br /><br />Chaque niveau comprend les niveaux en dessous.|
|/dudisable|Empêche l’exécution de mise à jour dynamique. Sans mise à jour dynamique, le programme d’installation s’exécute uniquement avec les fichiers d’installation d’origine. Cette option désactive la mise à jour dynamique même si vous utilisez un fichier de réponses et spécifiez des options de mise à jour dynamique dans ce fichier.|
|/duprepare|Prépare un partage d’installation afin qu’il peut être utilisé avec les fichiers de mise à jour dynamique que vous avez téléchargé à partir du site Web de mise à jour de Windows. Ce partage peut ensuite être utilisé pour installer Windows XP pour plusieurs clients.|
|\<pathName>|Spécifie le nom de chemin d’accès complet.|
|/dushare|Spécifie un partage sur lequel vous avez précédemment téléchargé des fichiers de mise à jour dynamique (fichiers mis à jour pour une utilisation avec le programme d’installation) à partir du site Web de mise à jour de Windows et sur lequel vous avez précédemment exécuté **/duprepare : *** < chemin d’accès >*. Lorsque vous exécutez sur un client, spécifie que l’installation du client utilisera les fichiers mis à jour sur le partage spécifié dans <pathName>.|
|/emsport|Active ou désactive les Services de gestion d’urgence pendant l’installation et une fois que le système d’exploitation a été installé. Avec les Services de gestion d’urgence, vous pouvez gérer à distance un serveur dans des situations d’urgence qui nécessiteraient normalement un clavier local, une souris et un moniteur, par exemple lorsque le réseau est indisponible ou le serveur ne fonctionne pas correctement. Les Services de gestion d’urgence configuration matérielle spécifique et est disponible uniquement pour les produits dans Windows Server 2003.<br /><br />-   **COM1** s’applique uniquement aux ordinateurs x86 (pas sur l’architecture ordinateurs Itanium).<br />-   **COM2**s’applique uniquement aux ordinateurs x86 (pas sur l’architecture ordinateurs Itanium).<br />-Par défaut. Utilise le paramètre spécifié dans la table de BIOS Port SPCR Serial Console Redirection (), ou sur l’architecture d’un système Itanium, via le chemin d’accès de périphérique de console EFI. Si vous spécifiez **usebiossettings** et qu’aucune table SPCR ou le chemin d’accès du périphérique de console EFI approprié, based de gestion d’urgence n’est pas activé.<br />-   **désactiver** désactive les Services de gestion d’urgence. Vous pouvez l’activer ultérieurement en modifiant les paramètres de démarrage.|
|/emsbaudrate|pour les ordinateurs x86, spécifie la vitesse de transmission pour les Services de gestion d’urgence. (L’option n’est pas applicable pour les ordinateurs basés sur l’architecture Itanium). Doit être utilisé avec **/emsport : COM1** ou **/emsport : COM2** (sinon, **/emsbaudrate** est ignoré).|
|\<BaudRate>|Spécifie la vitesse en bauds de 9 600, 19 200 bauds, 57600 ou 115200. 9600 est la valeur par défaut.|
|/m|Spécifie que le programme d’installation copie les fichiers de remplacement à partir d’un autre emplacement.  Indique le programme d’installation de rechercher dans l’autre emplacement tout d’abord et si les fichiers sont présents, de les utiliser au lieu des fichiers à partir de l’emplacement par défaut.|
|/makelocalsource|Indique le programme d’installation pour copier tous les fichiers sources d’installation sur votre disque dur local.  Utilisez **/makelocalsource** lors de l’installation à partir d’un cd pour fournir les fichiers d’installation lorsque le cd n’est pas disponible plus loin dans l’installation.|
|/noreboot|Indique le programme d’installation ne pas redémarrer l’ordinateur une fois la phase de copie de fichier du programme d’installation est terminée afin que vous puissiez exécuter une autre commande.|
|/s|Spécifie l’emplacement source des fichiers pour votre installation. Pour copier des fichiers à partir de plusieurs serveurs simultanément, tapez le **/s:**\<cheminsource > option plusieurs fois (jusqu'à un maximum de huit). Si vous tapez cette option plusieurs fois, le premier serveur spécifié doit être disponible, ou le programme d’installation échoue.|
|\<SourcePath >|Spécifie le nom de chemin d’accès source complet.|
|/syspart|Sur un ordinateur basé sur le x86, spécifie que vous pouvez copier les fichiers d’installation de démarrage sur un disque dur, marquer ce disque comme étant actif et puis l’installer dans un autre ordinateur. Lorsque vous démarrez cet ordinateur, il démarre automatiquement avec la phase suivante du programme d’installation.<br /><br />Vous devez toujours utiliser le **/tempdrive** paramètre avec le **/syspart** paramètre.<br /><br />Vous pouvez démarrer **winnt32** avec la **/syspart** option sur un ordinateur x86 exécutant Windows NT 4.0, Windows 2000, Windows XP ou un produit dans Windows Server 2003. Si l’ordinateur exécute Windows NT version 4.0, il nécessite le Service Pack 5 ou version ultérieure. L’ordinateur ne peut pas être en cours d’exécution pour Windows 95, Windows 98 ou Windows Millennium edition.|
|\<DriveLetter>|Spécifie la lettre de lecteur.|
|/tempdrive|dirige le programme d’installation de placer les fichiers temporaires sur la partition spécifiée.<br /><br />pour une nouvelle installation, le système d’exploitation sera également être installé sur la partition spécifiée.<br /><br />pour une mise à niveau, le **/tempdrive** option affecte l’emplacement des fichiers temporaires uniquement ; le système d’exploitation sont mis à niveau dans la partition à partir duquel vous exécutez **winnt32**.|
|/udf|Indique un identificateur (\<ID >) que le programme d’installation utilise pour spécifier la façon dont un fichier de base de données de l’unicité (UDB) modifie un fichier de réponses (consultez le **/ unattend** option).  Le UDB remplace les valeurs dans le fichier de réponses et l’identificateur détermine quelles valeurs du fichier UDB sont utilisées. Par exemple, **Notre_societe.udb** substitue les paramètres spécifiés pour l’identificateur Utilisateur_RAS dans le fichier Notre_société.udb. Si aucun \<fichier_UDB > est spécifié, le programme d’installation invite l’utilisateur d’insérer un disque qui contient le **$Unique$ .udb** fichier.|
|\<ID>|Indique un identificateur utilisé pour spécifier la façon dont un fichier de base de données de l’unicité (UDB) modifie un fichier de réponses.|
|\<UDB_file>|Spécifie un fichier de base de données de l’unicité (UDB).|
|/unattend|Sur un ordinateur basé sur le x86, met à niveau votre version précédente de Windows NT 4.0 Server (avec Service Pack 5 ou version ultérieure) ou Windows 2000 en mode d’installation sans assistance. Tous les paramètres utilisateur sont tirés de l’installation précédente, aucune intervention de l’utilisateur n’est donc requis pendant l’installation.|
|\<num>|Spécifie le nombre de secondes entre le moment où le programme d’installation finit de copier les fichiers et quand elle redémarre votre ordinateur. Vous pouvez utiliser \<Num > sur n’importe quel ordinateur exécutant Windows 98, Windows Millennium edition, Windows NT, Windows 2000, Windows XP ou un produit dans Windows Server 2003. Si l’ordinateur exécute Windows NT version 4.0, il nécessite le Service Pack 5 ou version ultérieure.|
|\<AnswerFile>|Fournit le programme d’installation avec vos spécifications personnalisées|
|/?|Affiche l'aide à l'invite de commandes.|

## <a name="remarks"></a>Notes
Si vous déployez Windows XP sur les ordinateurs clients, vous pouvez utiliser la version de winnt32.exe qui est fourni avec Windows XP. Une autre façon de déployer Windows XP consiste à utiliser winnt32.msi, qui fonctionne via le programme d’installation de Windows, partie de la IntelliMirror ensemble de technologies. Pour plus d’informations sur les déploiements de clients, consultez le Kit de déploiement Windows Server 2003 qui est décrit dans [en utilisant le déploiement de Windows et les Kits de ressources](https://technet.microsoft.com/library/cc779317(v=ws.10).aspx).

Sur un ordinateur Itanium, **winnt32** peut être exécuté à partir de l’Interface EFI (Extensible Firmware) ou à partir de Windows Server 2003, Enterprise, Windows Server 2003 R2, Enterprise, Windows Server 2003 R2 Datacenter ou Windows Server 2003 Centre de données. En outre, sur un ordinateur basé sur l’architecture Itanium, **/cmdcons** et **/syspart** ne sont pas disponibles et les options relatives aux mises à niveau ne sont pas disponibles.
Pour plus d’informations sur la compatibilité matérielle, consultez [compatibilité matérielle](https://technet.microsoft.com/library/cc757927(v=ws.10).aspx).
Pour plus d’informations sur l’utilisation de mise à jour dynamique et l’installation de plusieurs clients, consultez le Kit de déploiement Windows Server 2003 qui est décrit dans [en utilisant le déploiement de Windows et les Kits de ressources](https://technet.microsoft.com/library/cc779317(v=ws.10).aspx).
Pour plus d’informations sur la modification des paramètres de démarrage, consultez le déploiement de Windows et les Kits de ressources de Windows Server 2003. Pour plus d’informations, consultez [en utilisant le déploiement de Windows et les Kits de ressources](https://technet.microsoft.com/library/cc779317(v=ws.10).aspx).
À l’aide de la **/ unattend** une option de ligne de commande pour automatiser l’installation, vous confirmez que vous avez lu et accepté le contrat de licence Microsoft pour Windows Server 2003. Avant d’utiliser cette option de ligne de commande pour installer Windows Server 2003 pour le compte d’une organisation autre que le vôtre, vous devez confirmer que l’utilisateur final (si un individu ou une entité unique) a reçu, lu et accepté les termes du contrat de la Microsoft License Accord de ce produit.  Les OEM ne peuvent pas spécifier cette clé sur les machines vendues aux utilisateurs finaux.

## <a name="additional-references"></a>Références supplémentaires
-   [Clé de la syntaxe de ligne de commande](command-line-syntax-key.md)

