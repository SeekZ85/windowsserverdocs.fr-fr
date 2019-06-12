---
title: ksetup:setrealmflags
description: 'Rubrique de commandes de Windows pour ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bcb2824e-fba7-4ebe-be62-e62b4fae5b17
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 249eb82bb40890e071bd7d1eca3a0201064fa01e
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66437941"
---
# <a name="ksetupsetrealmflags"></a>ksetup:setrealmflags



Définit les indicateurs de domaine pour le domaine Kerberos spécifié. Pour obtenir des exemples d’utilisation de cette commande, consultez [exemples](#BKMK_Examples).

## <a name="syntax"></a>Syntaxe

```
ksetup /setrealmflags <RealmName> [sendaddress] [tcpsupported] [delegate] [ncsupported] [rc4]
```

### <a name="parameters"></a>Paramètres

|Paramètre|Description|
|---------|-----------|
|\<RealmName>|Le nom de domaine est indiqué comme un nom DNS en majuscules, telles que CORP. CONTOSO.COM.|
|Indicateur de domaine|Désigne un des indicateurs suivants :</br>-   SendAddress</br>-   TcpSupported</br>-Délégué</br>-   NcSupported</br>-   RC4|

## <a name="remarks"></a>Notes

Les indicateurs de domaine spécifient des fonctionnalités supplémentaires d’un domaine Kerberos qui ne repose pas sur le système d’exploitation Windows Server. Ordinateurs qui exécutent Windows Server 2003, Windows Server 2008 ou Windows Server 2008 R2 peuvent utiliser un serveur de Kerberos pour administrer l’authentification au lieu d’utiliser un domaine qui exécute un système d’exploitation Windows, et participent à ces systèmes un Domaine Kerberos. Cette entrée établit les fonctionnalités du domaine. Le tableau suivant décrit chacun.

|Value|Indicateur de domaine|Description|
|-----|----------|-----------|
|0xF|Tous|Tous les indicateurs de domaine sont définies.|
|0x00|Aucune|Aucun indicateur de domaine est défini, et aucuns fonctionnalités supplémentaires ne sont activées.|
|0x01|SendAddress|L’adresse IP sera inclus dans les ticket-granting tickets.|
|0x02|TcpSupported|Le protocole TCP (Transmission Control) et le protocole UDP (User Datagram) sont pris en charge dans ce domaine.|
|0x04|Délégué|Tous les membres de ce domaine est approuvé pour délégation.|
|0x08|NcSupported|Ce domaine prend en charge la canonisation nom, ce qui permet des normes d’affectation de noms de domaine DNS.|
|0x80|RC4|Ce domaine prend en charge le chiffrement RC4 pour activer l’approbation entre domaines, ce qui permet l’utilisation de TLS.|

Indicateurs de domaine sont stockés dans le Registre sous **HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa\Kerberos\Domains\\** <em>RealmName</em>. Par défaut, cette entrée n’existe pas dans le Registre. Vous pouvez utiliser la [Ksetup:addrealmflags](ksetup-addrealmflags.md) commande pour remplir le Registre.

Vous pouvez voir quels indicateurs de domaine disponible et défini en affichant la sortie de **ksetup**.

## <a name="BKMK_Examples"></a>Exemples

Répertorier les indicateurs de domaine disponible et défini pour le domaine CONTOSO :
```
ksetup
```
Définissez les deux indicateurs qui ne sont pas actuellement définies :
```
ksetup /setrealmflags CONTOSO ncsupported delegate
```
Exécutez le **ksetup** pour vérifier que l’indicateur de domaine est défini par l’affichage de la sortie et en recherchant **indicateurs de domaine =** .

#### <a name="additional-references"></a>Références supplémentaires

-   [Ksetup:listrealmflags](ksetup-listrealmflags.md)
-   [Ksetup:addrealmflags](ksetup-addrealmflags.md)
-   [Ksetup:delrealmflags](ksetup-delrealmflags.md)
-   [Clé de syntaxe de ligne de commande](command-line-syntax-key.md)