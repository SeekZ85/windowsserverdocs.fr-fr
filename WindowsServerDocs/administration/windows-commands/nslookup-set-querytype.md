---
title: nslookup set querytype
description: 'Rubrique de commandes de Windows pour ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5af54ac5-fc1a-4af6-977b-f8e97c8eba90
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5d698e6d4603afb332efeaf1cdc79eeeee37d66d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59813120"
---
# <a name="nslookup-set-querytype"></a>nslookup set querytype

>S'applique à : Windows Server (canal semi-annuel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

modifie le type d’enregistrement de ressource pour la requête.
## <a name="syntax"></a>Syntaxe
```
set querytype=<ResourceRecordtype>
```
## <a name="parameters"></a>Paramètres
<ResourceRecordtype> Spécifie un type d’enregistrement de ressource DNS. Le type d’enregistrement de ressource par défaut est A. Le tableau suivant répertorie les valeurs valides pour cette commande.
|Value|Description|
|-----|--------|
|A|Spécifie l’adresse IP d’un ordinateur|
|N’IMPORTE QUEL|Spécifie l’adresse IP d’un ordinateur.|
|CNAME|Spécifie un nom canonique d’un alias.|
|GID|Spécifie un identificateur de groupe d’un nom de groupe.|
|HINFO|Spécifie le processeur et le type de système d’exploitation d’un ordinateur.|
|Mo|Spécifie un nom de domaine de boîte aux lettres.|
|MG|Spécifie un membre du groupe messagerie.|
|MINFO|Spécifie les informations de liste de boîte aux lettres ou de messagerie.|
|MR|Spécifie le nom de domaine de changement de nom de messagerie.|
|MX|Spécifie le serveur de messagerie.|
|NS|Spécifie un serveur de noms DNS pour la zone nommée.|
|PTR|Spécifie un ordinateur nom si la requête est une adresse IP ; Sinon, spécifie le pointeur vers d’autres informations.|
|SOA|Spécifie la début d’autorité pour une zone DNS.|
|TXT|Spécifie les informations de texte.|
|UID|Spécifie l’identificateur d’utilisateur.|
|UINFO|Spécifie les informations utilisateur.|
|WKS|Décrit un service connu.|
{aide | ?}
Affiche un résumé de **nslookup** sous-commandes
## <a name="remarks"></a>Notes
-   Le **définissez type** commande effectue la même fonction que la **définir querytype** commande.
-   Pour plus d’informations sur les types d’enregistrements de ressources, consultez la demande de commentaire (Rfc) 1035.
## <a name="additional-references"></a>Références supplémentaires
[Clé de syntaxe de ligne de commande](command-line-syntax-key.md)
[nslookup définie le type](nslookup-set-type.md)
