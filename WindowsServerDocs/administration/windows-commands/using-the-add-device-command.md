---
title: Utilisation de la commande Add-Device
description: 'Rubrique relative aux commandes Windows pour * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1e599cc4-464a-421b-b6bb-c101af154131
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 475db63af52df0f26a09e2a8312c4910277e4c0f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71363847"
---
# <a name="using-the-add-device-command"></a>Utilisation de la commande Add-Device

>S'applique à : Windows Server (canal semi-annuel), Windows Server 2016, Windows Server 2012 R2 et Windows Server 2012

Prédéfinit un ordinateur dans les services de domaine Active Directory. Les ordinateurs prédéfinis sont également appelés ordinateurs connus. Cela vous permet de configurer des propriétés pour contrôler l’installation du client. Par exemple, vous pouvez configurer le programme de démarrage réseau et le fichier d’installation sans assistance que le client doit recevoir, ainsi que le serveur à partir duquel le client doit télécharger le programme de démarrage réseau.
pour obtenir des exemples d’utilisation de cette commande, consultez [exemples](#BKMK_examples).
## <a name="syntax"></a>Syntaxe
```
wdsutil /add-Device /Device:<Device name> /ID:<UUID | MAC address> [/ReferralServer:<Server name>] [/BootProgram:<Relative path>] [/WdsClientUnattend:<Relative path>] 
[/User:<Domain\User | User@Domain>] [/JoinRights:{JoinOnly | Full}] [/JoinDomain:{Yes | No}] [/BootImagepath:<Relative path>] [/OU:<DN of OU>] [/Domain:<Domain>]
```
## <a name="parameters"></a>Paramètres
|Paramètre|Description|
|-------|--------|
|/Device : <computer name>|Spécifie le nom de l’ordinateur à ajouter.|
|/ID : < adresse &#124; MAC UUID >|Spécifie le GUID/UUID ou l’adresse MAC de l’ordinateur. Un GUID/UUID doit être dans l’un des deux formats chaîne binaire ou GUID. Exemple :<br /><br />Chaîne binaire : **/ID : ACEFA3E81F20694E953EB2DAA1E8B1B6**<br /><br />Chaîne GUID : **/ID : E8A3EFAC-201F-4e69-953e-B2DAA1E8B1B6**<br /><br />Une adresse MAC doit être au format suivant : **00B056882FDC** (sans tirets) ou **00-B0-56-88-2F-DC** (avec des tirets)|
|[/ReferralServer : <Server name>]|Spécifie le nom du serveur à contacter pour télécharger le programme de démarrage réseau et l’image de démarrage à l’aide d’une protocole FTP simple (TFTP).|
|[/BootProgram : <Relative path>]|Spécifie le chemin d’accès relatif du dossier remoteInstall au programme de démarrage réseau que cet ordinateur doit recevoir. Par exemple : « boot\x86\pxeboot.com »|
|[/WdsClientUnattend : <Relative path>]|Spécifie le chemin d’accès relatif du dossier remoteInstall au fichier d’installation sans assistance qui automatise les écrans d’installation du client des services de déploiement Windows.|
|[/User : < domaine\utilisateur &#124; User@Domain >]|Définit les autorisations sur l’objet de compte d’ordinateur pour accorder à l’utilisateur spécifié les droits nécessaires pour joindre l’ordinateur au domaine.|
|[/JoinRights : {JoinOnly &#124; complet}]|Spécifie le type de droits à assigner à l’utilisateur.<br /><br />-   **JoinOnly** nécessite que l’administrateur réinitialise le compte d’ordinateur pour que l’utilisateur puisse joindre l’ordinateur au domaine.<br />-   **Full** donne un accès complet à l’utilisateur, ce qui inclut le droit de joindre l’ordinateur au domaine.|
|[/JoinDomain : {oui &#124; non}]|Spécifie si l’ordinateur doit être joint au domaine en tant que ce compte d’ordinateur lors de l’installation du système d’exploitation. La valeur par défaut est **Oui**.|
|[/BootImagepath : <Relative path>]|Spécifie le chemin d’accès relatif du dossier remoteInstall à l’image de démarrage que cet ordinateur doit utiliser.|
|[/OU : <DN of OU>]|Nom unique de l’unité d’organisation dans laquelle l’objet compte d’ordinateur doit être créé. Exemple : **Ou = MyOU, CN = test, DC = domain, DC = com**. L’emplacement par défaut est le conteneur de l’ordinateur par défaut.|
|[/Domain : <Domain>]|Domaine dans lequel l’objet compte d’ordinateur doit être créé. L’emplacement par défaut est le domaine local.|
## <a name="BKMK_examples"></a>Illustre
Pour ajouter un ordinateur à l’aide d’une adresse MAC, tapez :
```
wdsutil /add-Device /Device:computer1 /ID:00-B0-56-88-2F-DC
```
Pour ajouter un ordinateur à l’aide d’une chaîne GUID, tapez :
```
wdsutil /add-Device /Device:computer1 /ID:{E8A3EFAC-201F-4E69-953F-B2DAA1E8B1B6} /ReferralServer:WDSServer1 /BootProgram:boot\x86\pxeboot.com 
/WDSClientUnattend:WDSClientUnattend\unattend.xml /User:Domain\MyUser/JoinRights:Full /BootImagepath:boot\x86\images\boot.wim /OU:"OU=MyOU,CN=Test,DC=Domain,DC=com"
```
#### <a name="additional-references"></a>Références supplémentaires
[Clé de syntaxe de ligne de commande](command-line-syntax-key.md)
[à l’aide de la commande AllDevices](using-the-get-alldevices-command.md)
[à l’aide de la commande](using-the-get-device-command.md)Set-Device 
 sous-[commande : Set-Device](subcommand-set-device.md)
[New-WdsClient](https://technet.microsoft.com/library/dn283430.aspx)
