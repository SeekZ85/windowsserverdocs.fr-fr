---
title: bitsadmin getowner
description: Rubrique de commandes de Windows pour **bitsadmin getowner** -récupère le propriétaire de la tâche spécifiée.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5203f84c-a879-4f31-ae3e-7ea74bd63ca5
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1381bc1268b2b81e2bde18d0d8e17bd760345e0f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59886710"
---
# <a name="bitsadmin-getowner"></a>bitsadmin getowner

Affiche le nom d’affichage ou le GUID du propriétaire de la tâche spécifiée.

## <a name="syntax"></a>Syntaxe

```
bitsadmin /GetOwner <Job>
```

## <a name="parameters"></a>Paramètres

|Paramètre|Description|
|---------|-----------|
|Tâche|Nom d’affichage ou le GUID du travail|

## <a name="BKMK_examples"></a>Exemples

L’exemple suivant affiche le propriétaire du travail *myDownloadJob*.
```
C:\>bitsadmin /GetOwner myDownloadJob
```

#### <a name="additional-references"></a>Références supplémentaires

[Clé de la syntaxe de ligne de commande](command-line-syntax-key.md)