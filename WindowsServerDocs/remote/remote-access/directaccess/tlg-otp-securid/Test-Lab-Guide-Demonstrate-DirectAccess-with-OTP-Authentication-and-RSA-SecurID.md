---
title: Guide de laboratoire de test-démonstration de DirectAccess avec l’authentification par mot de passe à usage unique et RSA SecurID
description: 'Cette rubrique fait partie du Guide de laboratoire de test : illustrer DirectAccess avec l’authentification par mot de passe à usage unique et RSA SecurID pour Windows Server 2016'
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 10c7a49c-5671-4bec-b562-13fdd67f4629
ms.author: pashort
author: shortpatti
ms.openlocfilehash: f226c4c4b8a7517458ede95b4e237b567e0c49df
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71404664"
---
# <a name="test-lab-guide-demonstrate-directaccess-with-otp-authentication-and-rsa-securid"></a>Guide du laboratoire de test : Démonstration de DirectAccess avec l’authentification par mot de passe à usage unique et RSA SecurID

>S'applique à : Windows Server (Canal semi-annuel), Windows Server 2016

L’accès à distance est un rôle serveur dans le système d’exploitation Windows Server 2016, Windows Server 2012 R2 et Windows Server 2012 qui permet aux utilisateurs distants d’accéder en toute sécurité aux ressources réseau internes à l’aide de DirectAccess ou des réseaux privés virtuels (VPN) avec le routage et le service d’accès à distance (RRAS). Ce guide contient des instructions pas à pas pour l’extension du Guide de laboratoire [Test : Démonstration de la configuration d’un seul serveur DirectAccess avec Mixed IPv4 et IPv6 @ no__t-0 pour illustrer une configuration de mot de passe à usage unique à accès à distance.  
  
> [!WARNING]  
> La conception de ce guide de laboratoire de test comprend des serveurs d’infrastructure, tels qu’un contrôleur de domaine et une autorité de certification (CA) qui exécutent Windows Server 2012 R2 ou Windows Server 2012. L’utilisation de ce guide de laboratoire de test pour configurer des serveurs d’infrastructure qui exécutent d’autres systèmes d’exploitation n’a pas été testée et les instructions de configuration d’autres systèmes d’exploitation ne sont pas incluses dans ce guide.  
  
## <a name="about-this-guide"></a>À propos de ce guide  
L’accès à distance dans Windows Server 2016, Windows Server 2012 R2 et Windows Server 2012 ajoute la prise en charge de l’authentification du client avec un mot de passe à usage unique. Dans le cadre de ce laboratoire de test, seul RSA SecurID est utilisé pour illustrer la fonctionnalité de mot de passe à usage unique avec accès à distance. D’autres solutions à mot de passe à usage unique RADIUS sont également prises en charge, mais elles ne sont pas abordées dans ce laboratoire de test. Ce guide contient des instructions permettant de configurer le rôle serveur Accès à distance et d’en faire la démonstration à l’aide de six serveurs et deux ordinateurs clients. Le laboratoire de test accès à distance terminé avec mot de passe à usage unique simule un intranet, Internet et un réseau privé, et illustre les fonctionnalités d’accès à distance dans différents scénarios de connexion Internet.  
  
> [!IMPORTANT]  
> Pour appuyer cette démonstration, il utilise un nombre minimum d’ordinateurs. La configuration détaillée dans ce guide est fournie à des fins de tests en laboratoire seulement et ne doit pas être utilisée dans un environnement de production.  
  


