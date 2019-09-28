---
title: Authentification par clé publique d'appareil joint au domaine
ms.custom: na
ms.prod: windows-server
ms.topic: article
ms.assetid: 7bd17803-6e42-4a3b-803f-e47c74725813
manager: alanth
author: michikos
ms.technology: security-authentication
ms.date: 08/18/2017
ms.openlocfilehash: 616ebf1a8e01f84618d22d535609a0dc8414d718
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71403493"
---
# <a name="domain-joined-device-public-key-authentication"></a>Authentification par clé publique d'appareil joint au domaine

>S’applique à : Windows Server 2016, Windows 10

Kerberos a ajouté la prise en charge des appareils joints à un domaine pour se connecter à l’aide d’un certificat à partir de Windows Server 2012 et Windows 8. Cette modification permet aux fournisseurs tiers de créer des solutions pour approvisionner et initialiser des certificats pour les appareils joints à un domaine à utiliser pour l’authentification de domaine. 

## <a name="automatic-public-key-provisioning"></a>Approvisionnement automatique des clés publiques

À compter de Windows 10 version 1507 et de Windows Server 2016, les appareils joints à un domaine approvisionnent automatiquement une clé publique liée à un contrôleur de domaine Windows Server 2016 (DC). Une fois qu’une clé est approvisionnée, Windows peut utiliser l’authentification par clé publique dans le domaine.

### <a name="public-key-generation"></a>Génération de la clé publique
Si l’appareil exécute Credential Guard, une clé publique est créée protégée par Credential Guard. 

Si Credential Guard n’est pas disponible et qu’un module de plateforme sécurisée est, une clé publique est créée protégée par le module de plateforme sécurisée. 

Si aucun n’est disponible, une clé n’est pas générée et l’appareil peut uniquement s’authentifier à l’aide d’un mot de passe.

### <a name="provisioning-computer-account-public-key"></a>Configuration de la clé publique du compte d’ordinateur
Lorsque Windows démarre, il vérifie si une clé publique est approvisionnée pour son compte d’ordinateur. Si ce n’est pas le cas, il génère une clé publique liée et le configure pour son compte dans Active Directory à l’aide d’un contrôleur de domaine Windows Server 2016 ou version ultérieure. Si tous les contrôleurs de service sont de niveau inférieure, aucune clé n’est approvisionnée.

### <a name="configuring-device-to-only-use-public-key"></a>Configuration de l’appareil pour qu’il utilise uniquement la clé publique
Si le paramètre stratégie de groupe **prise en charge de l’authentification des appareils à l’aide du certificat** est défini sur **force**, alors l’appareil doit trouver un contrôleur de périphérique qui exécute Windows Server 2016 ou une version ultérieure pour s’authentifier. Le paramètre se trouve sous Modèles d’administration système > > Kerberos.

### <a name="configuring-device-to-only-use-password"></a>Configuration de l’appareil pour utiliser uniquement le mot de passe
Si le paramètre stratégie de groupe **prise en charge de l’authentification des appareils à l’aide du certificat** est désactivé, le mot de passe est toujours utilisé. Le paramètre se trouve sous Modèles d’administration système > > Kerberos.

## <a name="domain-joined-device-authentication-using-public-key"></a>Authentification d’appareil joint à un domaine à l’aide d’une clé publique
Lorsque Windows dispose d’un certificat pour l’appareil joint à un domaine, Kerberos s’authentifie d’abord à l’aide du certificat et en cas d’échec de nouvelles tentatives avec un mot de passe. Cela permet à l’appareil de s’authentifier auprès des contrôleurs de gamme de niveau supérieur.

Étant donné que les clés publiques automatiquement approvisionnées ont un certificat auto-signé, la validation du certificat échoue sur les contrôleurs de domaine qui ne prennent pas en charge le mappage de compte de confiance de clé. Par défaut, Windows effectue une nouvelle tentative d’authentification à l’aide du mot de passe de domaine de l’appareil.


