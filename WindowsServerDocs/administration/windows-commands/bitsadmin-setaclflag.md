---
title: bitsadmin setaclflag
description: La rubrique commandes Windows pour **Bitsadmin setaclflag** -définit les indicateurs de propagation de la liste de contrôle d’accès.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6e3bcda0-827d-4dfd-8384-d1da018f3e10
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: fbdb12c29af7b4db8b25846d43ee1c93b2454ff2
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380759"
---
# <a name="bitsadmin-setaclflag"></a>bitsadmin setaclflag

Définit les indicateurs de propagation de la liste de contrôle d’accès (ACL) pour le travail. Les indicateurs indiquent que vous souhaitez conserver les informations relatives au propriétaire et à la liste de contrôle d’accès avec le fichier en cours de téléchargement. Par exemple, pour conserver le propriétaire et le groupe avec le fichier, définissez les **indicateurs** Pour `OG`.

## <a name="syntax"></a>Syntaxe

```
bitsadmin /SetAclFlags <Job> <Flags>
```

## <a name="parameters"></a>Paramètres

|Paramètre|Description|
|---------|-----------|
|Tâche|Nom complet ou GUID du travail|
|Flags|Spécifiez une ou plusieurs des valeurs d’indicateur suivantes :</br>SORTIES Copiez les informations de propriétaire avec le fichier.</br>ACTIVÉE Copier les informations de groupe avec le fichier.</br>E Copiez les informations DACL avec le fichier.</br>-S : copie des informations SACL avec le fichier.|

## <a name="remarks"></a>Notes

Le commutateur SetAclFlags est utilisé pour gérer les informations de propriétaire et de liste de contrôle d’accès lorsqu’un travail télécharge des données à partir d’un partage Windows (SMB).

## <a name="BKMK_examples"></a>Illustre

L’exemple suivant définit les indicateurs de propagation de la liste de contrôle d’accès pour le travail nommé *myDownloadJob* afin de conserver les informations de propriétaire et de groupe avec les fichiers téléchargés.
```
C:\>bitsadmin /setaclflags myDownloadJob OG
```

#### <a name="additional-references"></a>Références supplémentaires

[Clé de syntaxe de ligne de commande](command-line-syntax-key.md)