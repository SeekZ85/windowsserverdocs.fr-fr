---
title: À l’aide de la commande Nouveau DiscoverImage
description: 'Rubrique de commandes de Windows pour ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ede9fbbb-0bba-4309-8c21-3cc13e1dc3cd
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1212571fc07b912ab9fa3344b973ce5a25085d86
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59835770"
---
# <a name="using-the-new-discoverimage-command"></a>À l’aide de la commande Nouveau DiscoverImage



Crée une nouvelle image de découverte à partir d’une image de démarrage. Découvrir les images sont des images de démarrage qui forcent le programme Setup.exe pour démarrer en mode Services de déploiement Windows et ensuite découvrir un serveur de Services de déploiement Windows. En général, ces images sont utilisées pour déployer des images sur des ordinateurs qui ne sont pas capables de démarrage PXE. Pour plus d’informations, consultez Création d’Images ([https://go.microsoft.com/fwlink/?LinkId=115311](https://go.microsoft.com/fwlink/?LinkId=115311)).

## <a name="syntax"></a>Syntaxe

```
WDSUTIL [Options] /New-DiscoverImage [/Server:<Server name>]
     /Image:<Image name>
     /Architecture:{x86 | ia64 | x64}
     [/Filename:<File name>]
     /DestinationImage
         /FilePath:<File path and name>
         [/Name:<Name>]
         [/Description:<Description>]
         [/WDSServer:<Server name>]
         [/Overwrite:{Yes | No | Append}]
```

## <a name="parameters"></a>Paramètres

|Paramètre|Description|
|---------|-----------|
|[/ Server :\<nom du serveur >]|Spécifie le nom du serveur. Cela peut être le nom NetBIOS ou le nom FQDN. Si aucun nom de serveur n’est spécifié, le serveur local doit être utilisé.|
|/ Image :\<nom de l’Image >|Spécifie le nom de l’image de démarrage source.|
|/ Architecture : {x86 | ia64 | x64}|Spécifie l’architecture de l’image doit être retournée. Comme il est possible d’avoir le même nom d’image pour les images de démarrage différents dans différentes architectures, en spécifiant la valeur de l’architecture garantit que WDSUTIL retourne l’image correcte.|
|[/ Filename :\<nom de fichier >]|Si l’image ne peut pas être identifié de manière unique par son nom, vous devez utiliser cette option pour spécifier le nom de fichier.|
|/DestinationImage|Spécifie les paramètres de l’image de destination. Vous pouvez spécifier les paramètres à l’aide des options suivantes :</br>-FilePath : < fichier de chemin d’accès et nom - > chemin de fichier complet de jeux pour la nouvelle image.</br>-[/ Nom :\<nom >]-définit le nom complet de l’image. Si aucun nom d’affichage n’est spécifié, le nom complet de l’image source sera utilisé.</br>-[/ Description : \<Description >]-définit la description de l’image.</br>-[/ WDSServer : \<Nom du serveur >]-Spécifie le nom du serveur que tous les clients qui démarre à partir de l’image spécifiée doivent contacter pour télécharger l’image d’installation. Par défaut, tous les clients qui cette image de démarrage détecte un serveur de Services de déploiement Windows valide. À l’aide de cette option permet de contourner la fonctionnalité de découverte et force le client démarré pour contacter le serveur spécifié.</br>-[/Overwrite : {Oui | Non | Append}] : détermine si le fichier spécifié dans **/DestinationImage /** doit être remplacé si un autre fichier portant ce nom existe déjà dans /FilePath. **Oui** écrase le fichier existant. **Ne** (valeur par défaut) provoque une erreur se produit si un autre fichier portant le même nom existe déjà. **Ajouter** joint de l’image générée sous la forme d’une nouvelle image dans le fichier .wim existant.|

## <a name="BKMK_examples"></a>Exemples

Pour créer une image de découverte en dehors de l’image de démarrage et nommez-le WinPEDiscover.wim, tapez :
```
WDSUTIL /New-DiscoverImage /Image:"WinPE boot image" /Architecture:x86 /DestinationImage /FilePath:"C:\Temp\WinPEDiscover.wim"
```
Pour créer une image de découverte en dehors de l’image de démarrage et nommez-le WinPEDiscover.wim avec les paramètres spécifiés, tapez :
```
WDSUTIL /Verbose /Progress /New-DiscoverImage /Server:MyWDSServer
/Image:"WinPE boot image" /Architecture:x64 /Filename:boot.wim /DestinationImage /FilePath:"\\Server\Share\WinPEDiscover.wim" 
/Name:"New WinPE image" /Description:"WinPE image for WDS Client discovery" /Overwrite:No
```

#### <a name="additional-references"></a>Références supplémentaires

[Clé de la syntaxe de ligne de commande](command-line-syntax-key.md)