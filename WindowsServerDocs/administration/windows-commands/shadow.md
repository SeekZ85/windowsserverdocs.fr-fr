---
title: shadow
description: 'Rubrique relative aux commandes Windows pour * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f81d9717-6883-4e14-9508-4b2a87e48ea7 Lizap
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: cb2fad4b0a553e736755f2dc56e5d88297a1fef5
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71383959"
---
# <a name="shadow"></a>shadow

>S’applique à : Windows Server (canal semi-annuel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Vous permet de contrôler à distance une session active d’un autre utilisateur sur un serveur hôte de session Bureau à distance (hôte de session Bureau à distance).
pour obtenir des exemples d’utilisation de cette commande, consultez [exemples](#BKMK_examples).

## <a name="syntax"></a>Syntaxe
```
shadow {<SessionName> | <SessionID>} [/server:<ServerName>] [/v]
```

### <a name="parameters"></a>Paramètres
|Paramètre|Description|
|-------|--------|
|\<NomSession >|Spécifie le nom de la session que vous souhaitez contrôler à distance.|
|\<SessionID >|Spécifie l’ID de la session que vous souhaitez contrôler à distance. Utilisez **query User** pour afficher la liste des sessions et leurs ID de session.|
|/Server :\<ServerName >|Spécifie le serveur hôte de session Bureau à distance contenant la session que vous souhaitez contrôler à distance. Par défaut, le serveur host4 de session Bureau à distance actuel est utilisé.|
|/v|Affiche des informations sur les actions en cours d’exécution.|
|/?|Affiche l'aide à l'invite de commandes.|

## <a name="remarks"></a>Notes
-   Vous pouvez afficher ou contrôler activement la session. Si vous choisissez de contrôler activement la session d’un utilisateur, vous serez en mesure d’entrer des actions au clavier et à la souris dans la session.
-   Vous pouvez toujours contrôler à distance vos propres sessions (à l’exception de la session active), mais vous devez disposer de l’autorisation contrôle total ou accès spécial contrôle à distance pour contrôler une autre session à distance.
-   Vous pouvez également lancer le contrôle à distance à l’aide de Services Bureau à distance Manager.
-   Avant le début de l’analyse, le serveur avertit l’utilisateur que la session va être contrôlée à distance, sauf si cet avertissement est désactivé. Votre session peut paraître gelée pendant quelques secondes, alors qu’elle attend une réponse de l’utilisateur. Pour configurer le contrôle à distance pour les utilisateurs et les sessions, utilisez l’outil de configuration Services Bureau à distance ou les extensions Services Bureau à distance pour les utilisateurs et les groupes locaux et les utilisateurs et ordinateurs Active Directory.
-   Votre session doit pouvoir prendre en charge la résolution vidéo utilisée au cours de la session que vous contrôlez à distance, sinon l’opération échoue.
-   La session de console ne peut pas contrôler à distance une autre session et ne peut pas être contrôlée à distance par une autre session.
-   Lorsque vous souhaitez terminer le contrôle à distance (occultation), appuyez sur CTRL +\* (à l’aide de \* à partir du pavé numérique uniquement).

## <a name="BKMK_examples"></a>Illustre
-   Pour occulter la session 93, tapez :
    ```
    shadow 93
    ```
-   Pour occulter la session ACCTG01, tapez :
    ```
    shadow ACCTG01
    ```

#### <a name="additional-references"></a>Références supplémentaires
[Clé de syntaxe de ligne de commande](command-line-syntax-key.md)
[ &#40;services Bureau à distance&#41; référence de commande des services Terminal Server](remote-desktop-services-terminal-services-command-reference.md)
