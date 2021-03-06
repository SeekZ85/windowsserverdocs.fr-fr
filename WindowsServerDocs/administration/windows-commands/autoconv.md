---
title: autoconv
description: La rubrique commandes Windows pour **autoconv** -convertit les volumes FAT (File Allocation Table) et FAT32 dans le système de fichiers NTFS.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 17281e54-0b18-4e84-94ac-24586c82df4e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bf36be6bcf3dd8f6c61c6ab0d8780ed77dd8903a
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71383447"
---
# <a name="autoconv"></a>autoconv

>S'applique à : Windows Server (canal semi-annuel), Windows Server 2016, Windows Server 2012 R2 et Windows Server 2012

convertit les volumes FAT (File Allocation Table) et FAT32 dans le système de fichiers NTFS, en laissant les fichiers et répertoires existants intacts au démarrage après l’exécution de **Autochk** . les volumes convertis dans le système de fichiers NTFS ne peuvent pas être reconvertis en FAT ou FAT32.
## <a name="remarks"></a>Notes
Vous ne pouvez pas exécuter **autoconv** sur la ligne de commande. Cette opération est exécutée uniquement au démarrage, si elle est définie via **Convert. exe**.
## <a name="additional-references"></a>Références supplémentaires
[Clé de syntaxe de ligne de commande](command-line-syntax-key.md)
[Autochk](autochk.md)
[convertir](convert.md)
[utilisation des systèmes de fichiers](https://go.microsoft.com/fwlink/?LinkId=4509)
