---
title: sxstrace
description: Découvrez comment diagnostiquer les problèmes de côte à côte.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: fcd26eeb-fbd9-4a86-b6a9-dfa5e9c6e4fc
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 396d06bf079c0cfa8ba4864f71333eec39f7b255
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59814100"
---
# <a name="sxstrace"></a>sxstrace

>S'applique à : Windows Server (canal semi-annuel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Diagnostique les problèmes de côte à côte.    

## <a name="syntax"></a>Syntaxe  
```  
sxstrace [{[trace /logfile:<FileName> [/nostop]|[parse /logfile:<FileName> /outfile:<ParsedFile>  [/filter:<AppName>]}]  
```  

### <a name="parameters"></a>Paramètres  
|Paramètre|Description|  
|-------|--------|  
|trace|Active le traçage pour sxs (côte à côte)|  
|/LogFile|Spécifie le fichier journal brut.|  
|\<FileName>|Enregistre le journal de suivi *FileName*.|  
|/nostop|Ne spécifie aucune invite pour arrêter le suivi.|  
|Analyser|Convertit le fichier de trace brutes.|  
|/outfile|Spécifie le nom de fichier de sortie.|  
|\<ParsedFile>|Spécifie le nom de fichier du fichier analysé.|  
|/Filter|Permet à la sortie à filtrer.|  
|\<AppName>|Spécifie le nom de l’application.|  
|stoptrace|Arrêtez la trace s’il n’est pas arrêté avant.|  
|/?|Affiche l'aide à l'invite de commandes.|  

## <a name="BKMK_Examples"></a>Exemples  
Activer le suivi et enregistrer le fichier de trace à **sxstrace.etl**:  
```  
sxstrace trace /logfile:sxstrace.etl  
```  
Convertir le fichier de trace brutes dans un format lisible et enregistrer le résultat à **sxstrace.txt**:  
```  
sxstrace parse /logfile:sxstrace.etl /outfile:sxstrace.txt  
```  

## <a name="additional-references"></a>Références supplémentaires  
-   [Clé de la syntaxe de ligne de commande](command-line-syntax-key.md)  
  
