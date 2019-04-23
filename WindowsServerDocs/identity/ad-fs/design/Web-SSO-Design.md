---
ms.assetid: eb778f63-f7be-438e-8c5e-1fd9b194b967
title: Conception SSO Web
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 1b8344594c9fc477ed8424c716ec8d7f7fd91ef3
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59852800"
---
# <a name="web-sso-design"></a>Conception SSO Web

>S'applique à : Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Dans l’unique Web\-connexion\-sur \(SSO\) conception dans Active Directory Federation Services \(AD FS\), les utilisateurs doivent s’authentifier qu’une seule fois pour accéder à plusieurs services AD FS\- applications sécurisées ou des services. Dans cette conception, tous les utilisateurs sont externes et en l’absence d’organisation partenaire, il n’existe aucune approbation de fédération. En général, vous déployez cette conception lorsque vous souhaitez fournir un accès consommateur ou un client individuel à un ou plusieurs AD FS sécurisée services ou applications via Internet, comme indiqué dans l’illustration suivante.  
  
![conception sso de Web](media/adfs2_WebSSODesign.gif)  
  
Avec la conception SSO de Web, une organisation qui héberge généralement un AD FS\-sécurisation de l’application ou service dans un réseau de périmètre peut maintenir un magasin distinct de comptes client dans le réseau de périmètre, ce qui le rend plus facile à isoler les clients comptes comptes des employés.  
  
Vous pouvez gérer les comptes locaux pour les clients du réseau de périmètre à l’aide des Services de domaine Active Directory \(AD DS\), SQL Server ou un magasin d’attributs personnalisés.  
  
Cette conception correspond à l’objectif de déploiement de [Provide Your Active Directory Users Access to Your Claims-Aware Applications and Services](Provide-Your-Active-Directory-Users-Access-to-Your-Claims-Aware-Applications-and-Services.md).  
  
Pour obtenir la liste détaillée des tâches que vous pouvez utiliser pour planifier et déployer votre conception SSO de Web, consultez [liste de vérification : Implémentation d’une conception SSO de Web](../../ad-fs/deployment/Checklist--Implementing-a-Web-SSO-Design.md).  
  
## <a name="see-also"></a>Voir aussi
[Guide de conception AD FS dans Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
