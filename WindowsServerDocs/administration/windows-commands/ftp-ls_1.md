---
title: ftp ls_1
description: 'Rubrique de commandes de Windows pour ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5e03c7db-1e2b-419c-acb2-8a68f3db9615 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: c45e26f6578510837f190ae20e3140e619dc59cb
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59841760"
---
# <a name="ftp-ls1"></a>FTP : ls_1

>S'applique à : Windows Server (canal semi-annuel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012


>S'applique à : Windows Server (canal semi-annuel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Affiche une liste abrégée des fichiers et sous-répertoires de l’ordinateur distant.   
## <a name="syntax"></a>Syntaxe  
```  
ls [<remotedirectory>] [<LocalFile>]  
```  
### <a name="parameters"></a>Paramètres  
|Paramètre|Description|  
|-------|--------|  
|[<remotedirectory>]|Spécifie le répertoire pour lequel vous souhaitez afficher une liste. Si aucun répertoire n’est spécifié, le répertoire de travail actuel sur l’ordinateur distant est utilisé.|  
|[<LocalFile>]|Spécifie un fichier local dans lequel stocker la liste. Si un fichier local n’est pas spécifié, les résultats sont affichés sur l’écran.|  
## <a name="BKMK_Examples"></a>Exemples  
Afficher une liste abrégée des fichiers et sous-répertoires de l’ordinateur distant.  
```  
ls  
```  
Obtenir une liste de répertoires abrégé de **dir1** sur l’ordinateur distant et enregistrez-la dans un fichier local appelé **ListRép.txt**  
```  
ls dir1 dirlist.txt   
```  
## <a name="additional-references"></a>Références supplémentaires  
-   [Clé de la syntaxe de ligne de commande](command-line-syntax-key.md)  
