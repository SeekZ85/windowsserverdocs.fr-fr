---
title: récupérer
description: 'Rubrique de commandes de Windows pour ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cf9be2e3-90c8-4773-a201-dc503b91948e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: d6b9b5544394bfc69a2dc9f7be26ed8355a3f690
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66441958"
---
# <a name="recover"></a>récupérer



Récupère les informations lisibles à partir d’un disque défectueux.

Pour obtenir des exemples d’utilisation de cette commande, consultez [Exemples](#BKMK_examples).

## <a name="syntax"></a>Syntaxe

```
recover [<Drive>:][<Path>]<FileName>
```

## <a name="parameters"></a>Paramètres

|           Paramètre           |                                          Description                                          |
|-------------------------------|-----------------------------------------------------------------------------------------------|
| [\<Drive>:][<Path>]<FileName> | Spécifie l’emplacement et le nom du fichier que vous souhaitez récupérer. *Nom de fichier* est requis. |
|              /?               |                             Affiche l'aide à l'invite de commandes.                              |

## <a name="remarks"></a>Notes

-   Le **récupérer** commande lit un fichier, secteur par secteur et récupère les données depuis les secteurs en bon état. Les données dans des secteurs défectueux sont perdues.
-   Secteurs défectueux signalés par **chkdsk** ont été marquées comme « mauvaises » lorsque votre disque a été préparé pour l’opération. Ils ne présentent aucun danger, et **récupérer** n’affecte pas ces derniers.
-   Étant donné que toutes les données dans des secteurs défectueux sont perdues lorsque vous récupérez un fichier, vous devez récupérer un seul fichier à la fois.
-   Vous ne pouvez pas utiliser des caractères génériques ( **&#42;** et **?** ) avec le **récupérer** commande. Vous devez spécifier un fichier (et l’emplacement du fichier s’il n’est pas dans le répertoire actif).

## <a name="BKMK_examples"></a>Exemples

Pour récupérer le fichier MobyDick.txt dans le répertoire \Fiction sur le lecteur D, tapez :
```
recover d:\fiction\story.txt 
```

#### <a name="additional-references"></a>Références supplémentaires

[Clé de syntaxe de ligne de commande](command-line-syntax-key.md)