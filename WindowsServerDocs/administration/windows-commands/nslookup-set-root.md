---
title: nslookup set root
description: 'Rubrique de commandes de Windows pour ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 8ad5393c-d4fd-4594-8187-576b1dcde60a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 38cd5a2e9878a8e43393befc5cbd4fc47c65ec53
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66436605"
---
# <a name="nslookup-set-root"></a>nslookup set root

>S'applique à : Windows Server (canal semi-annuel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

modifie le nom du serveur racine utilisé pour les requêtes.
## <a name="syntax"></a>Syntaxe
```
set root=<RootServer>
```
## <a name="parameters"></a>Paramètres

|    Paramètre    |                                   Description                                    |
|-----------------|----------------------------------------------------------------------------------|
|  <RootServer>   | Spécifie le nouveau nom pour le serveur racine. La valeur par défaut est ns.nic.ddn.mil. |
| {aide &#124; ?} |              Affiche un résumé de **nslookup** sous-commandes.               |

## <a name="remarks"></a>Notes
- Le **racine du jeu** sous-commande affecte le **racine** sous-commande.
  ## <a name="additional-references"></a>Références supplémentaires
  [Clé de syntaxe de ligne de commande](command-line-syntax-key.md)
  [racine de nslookup](nslookup-root.md)
