---
title: bitsadmin setdisplayname
description: Rubrique relative aux commandes Windows pour **Bitsadmin SetDisplayName** -définit le nom complet du travail spécifié.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 13706c53-fb5f-4879-b5ca-82531361d6e1
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 10a5607eb26f8199ec415a4cec17d03015a26bcd
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71380633"
---
# <a name="bitsadmin-setdisplayname"></a>bitsadmin setdisplayname



Définit le nom d’affichage du travail spécifié.

## <a name="syntax"></a>Syntaxe

```
bitsadmin /SetDisplayName <Job> <DisplayName>
```

## <a name="parameters"></a>Paramètres

|Paramètre|Description|
|---------|-----------|
|Tâche|Nom complet ou GUID du travail|
|DisplayName|Texte utilisé pour le nom complet du travail spécifié.|

## <a name="BKMK_examples"></a>Illustre

L’exemple suivant définit le nom complet de la tâche nommée *myDownloadJob* sur *myDownloadJob2*.
```
C:\>bitsadmin /SetDisplayName myDownloadJob "Download Music Job"
```

#### <a name="additional-references"></a>Références supplémentaires

[Clé de syntaxe de ligne de commande](command-line-syntax-key.md)