---
title: exit
description: 'Rubrique de commandes de Windows pour ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 23d1044b-f5c1-4180-ae6d-f553b48da4d9
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: b3490c6bc95a762bf2cb1da70f389fb8f583344f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59819490"
---
# <a name="exit"></a>exit

>S'applique à : Windows Server (canal semi-annuel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

quitte le programme Cmd.exe (l’interpréteur de commandes) ou le script de commandes actuel.  
Pour obtenir des exemples montrant comment utiliser cette commande, consultez [exemples](#BKMK_examples).  
## <a name="syntax"></a>Syntaxe  
```  
exit [/b] [<exitCode>]  
```  
## <a name="parameters"></a>Paramètres  
|Paramètre|Description|  
|-------|--------|  
|/b|quitte le script de commandes actuel au lieu de quitter Cmd.exe. Si exécutée en dehors d’un script de commandes, quitte à Cmd.exe.|  
|<exitCode>|Spécifie une valeur numérique. Si **/b** est spécifié, la variable d’environnement ERRORLEVEL est définie pour ce numéro. Si vous quitter **Cmd.exe**, le code de sortie est défini sur ce nombre.|  
|/?|Affiche l'aide à l'invite de commandes.|  
## <a name="BKMK_examples"></a>Exemples  
Pour fermer l’interpréteur de commandes Cmd.exe, tapez :  
```  
exit  
```  
## <a name="additional-references"></a>Références supplémentaires  
-   [Clé de la syntaxe de ligne de commande](command-line-syntax-key.md)  
  
