---
title: ntcmdprompt
description: 'Rubrique de commandes de Windows pour ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0063bdbb-dc2b-41c4-99ee-b011603aaa86
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 583f56c294e66542a75efca09e97d57ae54a8cea
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66436424"
---
# <a name="ntcmdprompt"></a>ntcmdprompt

>S'applique à : Windows Server (canal semi-annuel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Exécute l’interpréteur de commandes **Cmd.exe**, plutôt que **Command.com**, après avoir exécuté un Terminate et le rester résident résident ou après le démarrage de l’invite de commandes à partir d’une application pour MS-DOS.
## <a name="syntax"></a>Syntaxe
```
ntcmdprompt
```
### <a name="parameters"></a>Paramètres

| Paramètre |             Description              |
|-----------|--------------------------------------|
|    /?     | Affiche l'aide à l'invite de commandes. |

## <a name="remarks"></a>Notes
- Lorsque **Command.com** est en cours d’exécution, certaines fonctionnalités de **Cmd.exe**, telles que la **doskey** l’affichage de l’historique des commandes, ne sont pas disponibles. Si vous préférez exécuter le **Cmd.exe** interpréteur de commandes une fois que vous avez démarré un Terminate et le rester résident résident ou démarrer l’invite de commandes dans une application basée sur MS-DOS, vous pouvez utiliser le **ntcmdprompt**  commande. Toutefois, n’oubliez pas que le programme résident ne soient pas disponible pour une utilisation lors de l’exécution **Cmd.exe**. Vous pouvez inclure le **ntcmdprompt** commande dans votre **Config.nt** fichier ou le fichier de démarrage personnalisé équivalent dans le fichier (Pif) d’une application.
  ## <a name="examples"></a>Exemples
  Pour inclure **ntcmdprompt** dans votre **Config.nt** fichier ou le fichier de démarrage de configuration spécifié dans le fichier Pif, type : **ntcmdprompt**
  ## <a name="additional-references"></a>Références supplémentaires
- [Clé de syntaxe de ligne de commande](command-line-syntax-key.md)

