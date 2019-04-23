---
title: driverquery
description: 'Rubrique de commandes de Windows pour ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 92ca4b84-e4e2-405b-9f31-bf6db9f66839
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 6436ea47e3ec5c7c9ceee9fd50d052dba4a49724
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59861170"
---
# <a name="driverquery"></a>driverquery



Permet à un administrateur afficher une liste des pilotes de périphériques installés et leurs propriétés. Si utilisée sans paramètres, **driverquery** s’exécute sur l’ordinateur local.

Pour obtenir des exemples d’utilisation de cette commande, consultez [Exemples](#BKMK_examples).

## <a name="syntax"></a>Syntaxe

```
driverquery [/s <System> [/u [<Domain>\]<Username> [/p <Password>]]] [/fo {table | list | csv}] [/nh] [/v | /si]
```

## <a name="parameters"></a>Paramètres

|Paramètre|Description|
|---------|-----------|
|/s \<système >|Spécifie le nom ou l’adresse IP d’un ordinateur distant. N’utilisez pas de barres obliques inverses. La valeur par défaut est l'ordinateur local.|
|/u [\<domaine >\]<Username>|Exécute la commande avec les informations d’identification du compte d’utilisateur comme spécifié par *utilisateur* ou *domaine*\*utilisateur *. Par défaut, **/s** utilise les informations d’identification de l’utilisateur actuellement connecté à l’ordinateur qui émet la commande. **/u** ne peut pas être utilisé, sauf si **/s** est spécifié.|
|/p \<mot de passe >|Spécifie le mot de passe du compte d’utilisateur qui est spécifié dans le **/u** paramètre. **/p** ne peut pas être utilisé, sauf si **/u** est spécifié.|
|/FO {table | list | csv}|Spécifie le format pour afficher les informations du pilote. Les valeurs valides sont **table**, **liste**, et **csv**. Le format par défaut pour la sortie est **table**.|
|/nh|Omet la ligne d’en-tête à partir des informations affichées sur les pilotes. Non valide si le **/fo** paramètre est défini sur **liste**.|
|/v|Affiche la sortie détaillée. **/v** n’est pas valide pour les pilotes signés.|
|/si|Fournit des informations sur les pilotes signés.|
|/?|Affiche l'aide à l'invite de commandes.|

## <a name="BKMK_examples"></a>Exemples

Pour afficher une liste de pilotes de périphériques installés sur l’ordinateur local, tapez :
```
driverquery 
```
Pour afficher la sortie dans un format de valeurs séparées par des virgules (CSV), tapez :
```
driverquery /fo csv 
```
Pour masquer la ligne d’en-tête dans la sortie, tapez :
```
driverquery /nh 
```
Pour utiliser le **driverquery** commande sur un serveur distant nommé **server1** en utilisant vos informations d’identification actuelles sur l’ordinateur local, tapez :
```
driverquery /s server1
```
Pour utiliser le **driverquery** commande sur un serveur distant nommé **server1** utilisant les informations d’identification **user1** sur le domaine **maindom**, type :
```
driverquery /s server1 /u maindom\user1 /p p@ssw3d
```

#### <a name="additional-references"></a>Références supplémentaires

[Clé de la syntaxe de ligne de commande](command-line-syntax-key.md)