---
title: nslookup set root
description: 'Rubrique relative aux commandes Windows pour * * * *- '
ms.custom: na
ms.prod: windows-server
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
ms.openlocfilehash: 5a1737275bf6321525bbba56cd4d6a77ef973423
ms.sourcegitcommit: 9a6a692a7b2a93f52bb9e2de549753e81d758d28
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/18/2019
ms.locfileid: "72591026"
---
# <a name="nslookup-set-root"></a>nslookup set root

>S’applique à : Windows Server (canal semi-annuel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Modifie le nom du serveur racine utilisé pour les requêtes.
## <a name="syntax"></a>Syntaxe
```
set root=<RootServer>
```
## <a name="parameters"></a>Paramètres

|    Paramètre    |                                   Description                                    |
|-----------------|----------------------------------------------------------------------------------|
|  <RootServer>   | Spécifie le nouveau nom du serveur racine. La valeur par défaut est ns.nic.ddn.mil. |
| {Help &#124; ?} |              Affiche un bref résumé des sous-commandes **nslookup** .               |

## <a name="remarks"></a>Notes
- La sous-commande **Set root** affecte la sous-commande **racine** .
  ## <a name="additional-references"></a>Références supplémentaires
  [Clé de syntaxe de ligne de commande](command-line-syntax-key.md) 
  [racine nslookup](nslookup-root.md)
