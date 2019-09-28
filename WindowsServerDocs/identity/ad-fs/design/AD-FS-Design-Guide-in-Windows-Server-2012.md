---
ms.assetid: bb16e39d-566d-436c-b957-394c06d556db
title: Guide de conception AD FS dans Windows Server 2012
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: d9d7ec6f4ff575d3aac30b7127e591b78f5ef49b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71359207"
---
# <a name="ad-fs-design-guide-in-windows-server"></a>Guide de conception de AD FS dans Windows Server 


  
> [!NOTE]  
> Pour plus d’informations sur le déploiement de AD FS dans Windows Server 2012 R2, consultez le [Guide de déploiement de Windows server 2012 r2 AD FS](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md).  
  
Vous pouvez utiliser Active Directory® Federation Services \(AD FS @ no__t-1 avec le système d’exploitation Windows Server® 2012 dans un rôle de fournisseur de services de Fédération pour authentifier en toute transparence vos utilisateurs sur les services ou applications Web @ no__t-2based qui résident dans un organisation partenaire de ressource, sans que les administrateurs aient besoin de créer ou de gérer des approbations externes ou des approbations de forêt entre les réseaux des deux organisations et sans que les utilisateurs aient besoin de se connecter une deuxième fois. Le processus d’authentification sur un réseau lors de l’accès aux ressources d’un autre réseau, sans la charge des actions de connexion répétées par les utilisateurs, est appelé authentification unique @ no__t-0ON \(SSO @ no__t-2.  
  
## <a name="about-this-guide"></a>À propos de ce guide  
Ce guide fournit des recommandations pour vous aider à planifier un nouveau déploiement de AD FS, en fonction des exigences de votre organisation \(also référencées dans ce guide en tant que objectifs de déploiement @ no__t-1 et la conception que vous souhaitez créer. Ce guide est prévu pour une utilisation par un spécialiste d'infrastructure ou un architecte système. Il met en évidence vos principaux points de décision lors de la planification de votre déploiement AD FS. Avant de lire ce guide, vous devez avoir une bonne compréhension de la façon dont AD FS fonctionne sur un niveau fonctionnel. Vous devez également avoir une bonne compréhension des exigences de l’organisation qui seront reflétées dans votre conception de AD FS.  
  
Ce guide décrit un ensemble d’objectifs de déploiement basés sur trois AD FS principales conceptions et vous aide à choisir la conception la plus appropriée pour votre environnement. Vous pouvez utiliser ces objectifs de déploiement pour former l’une des conceptions de AD FS complètes suivantes ou une conception personnalisée qui répond aux besoins de votre environnement :  
  
-   SSO Web fédéré pour la prise en charge des scénarios Business @ no__t-0to @ no__t-1business \(B2B @ no__t-3 et pour la prise en charge de la collaboration entre les divisions avec des forêts indépendantes  
  
-   SSO Web pour la prise en charge de l’accès client aux applications dans Business @ no__t-0to @ no__t-1consumer \(B2C @ no__t-3 scénarios  
  
Pour chaque conception, vous trouverez des indications pour rassembler les données nécessaires à votre environnement, Vous pouvez ensuite utiliser ces instructions pour planifier et concevoir votre déploiement AD FS. Après avoir lu ce guide et terminé la collecte, la documentation et le mappage des exigences de votre organisation, vous disposerez des informations nécessaires pour commencer à déployer AD FS à l’aide des instructions du [Guide de déploiement de Windows Server 2012 AD FS](../../ad-fs/deployment/Windows-Server-2012-AD-FS-Deployment-Guide.md).  
  
## <a name="in-this-guide"></a>Dans ce guide  
  
-   [Identification de vos objectifs de déploiement d’AD FS](Identifying-Your-AD-FS-Deployment-Goals.md)  
  
-   [Mappage de vos objectifs de déploiement sur une conception AD FS](Mapping-Your-Deployment-Goals-to-an-AD-FS-Design.md)  
  
-   [Déterminer votre topologie de déploiement d’AD FS](Determine-Your-AD-FS-Deployment-Topology.md)  
  
-   [Planification de votre déploiement](Planning-Your-Deployment.md)  
  
-   [Planification de la sélection élective du serveur de fédération](Planning-Federation-Server-Placement.md)  
  
-   [Planification de la sélection élective du serveur proxy de fédération](Planning-Federation-Server-Proxy-Placement.md)  
  
-   [Planification de la capacité des serveurs AD FS](Planning-for-AD-FS-Server-Capacity.md)  
  
-   [Annexe A : examen de la configuration requise pour AD FS](Appendix-A--Reviewing-AD-FS-Requirements.md)  
  

