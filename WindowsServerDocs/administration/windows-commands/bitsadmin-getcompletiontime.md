---
title: bitsadmin getcompletiontime
description: La rubrique commandes Windows pour **Bitsadmin getcompletiontime** -récupère l’heure à laquelle le travail a terminé le transfert des données.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7a4b3c1c-9832-4724-86b2-cce3c01bfa28
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 190467d5f3a7b7244ed0d7ab3b75d4cbbf56c8d5
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71381743"
---
# <a name="bitsadmin-getcompletiontime"></a>bitsadmin getcompletiontime



Récupère l’heure à laquelle le travail a terminé le transfert des données.

## <a name="syntax"></a>Syntaxe

```
bitsadmin /GetCompletionTime <Job>
```

## <a name="parameters"></a>Paramètres

|Paramètre|Description|
|---------|-----------|
|Tâche|Nom complet ou GUID du travail|

## <a name="BKMK_examples"></a>Illustre

L’exemple suivant récupère l’heure à laquelle le travail nommé *myDownloadJob* a terminé le transfert des données.
```
C:\>bitsadmin /GetCompletionTime myDownloadJob
```

#### <a name="additional-references"></a>Références supplémentaires

[Clé de syntaxe de ligne de commande](command-line-syntax-key.md)