---
ms.assetid: 9eab8c43-a0f2-4d19-a5a4-e1399f0d5f25
title: Déterminez votre stratégie d’application fédérée dans le partenaire de ressource
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 0cc7a9202813cd3f8d45a72305d13ad197f5b04d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71359164"
---
# <a name="determine-your-federated-application-strategy-in-the-resource-partner"></a>Déterminez votre stratégie d’application fédérée dans le partenaire de ressource

Une partie importante de la conception d’une nouvelle infrastructure Services ADFS \(AD FS @ no__t-1 dans l’organisation partenaire de ressource consiste à déterminer l’ensemble complet des applications et services qui seront utilisés pour participer à la Fédération et les partenaires de compte qui seront les destinataires de ces ressources. Avant de concevoir une application fédérée et une stratégie de services, posez-vous les questions suivantes :  
  
-   Allez-vous activer et déployer une application ASP.NET ou un service Windows Communication Foundation \(WCF @ no__t-1 pour la Fédération ?  
  
-   Les utilisateurs de votre réseau d’entreprise auront-ils besoin d’accéder à l’application fédérée ou au service via l’authentification intégrée de Windows ?  
  
-   Les utilisateurs de votre réseau de périmètre devront-ils utiliser l’application fédérée ou le service ? Dans ce cas, l’authentification intégrée de Windows sera-t-elle nécessaire ?  
  
-   Tous les serveurs Web hébergeant des applications fédérées qui exécutent un système d’exploitation Windows Server et Internet Information Services \(IIS @ no__t-1 ?  
  
-   Qui sera le destinataire des ressources fournies par l’application fédérée ou le service ?  
  
La réponse à ces questions vous aidera à planifier une conception solide de AD FS. Cela vous permettra également de créer une application fédérée et une stratégie de services rentables et efficaces en matière d’utilisation des ressources. Pour plus d’informations sur la conception de l’application fédérée et de la stratégie de services les plus appropriées pour votre organisation, consultez les rubriques suivantes de ce guide :  
  
-   [Fournir à vos utilisateurs Active Directory un accès à vos applications et services prenant en charge les revendications](Provide-Your-Active-Directory-Users-Access-to-Your-Claims-Aware-Applications-and-Services.md)  
  
-   [Fournir à vos utilisateurs Active Directory un accès aux applications et services d’autres organisations](Provide-Your-Active-Directory-Users-Access-to-the-Applications-and-Services-of-Other-Organizations.md)  
  
-   [Fournir aux utilisateurs d’une autre organisation un accès à vos applications et services prenant en charge les revendications](Provide-Users-in-Another-Organization-Access-to-Your-Claims-Aware-Applications-and-Services.md)  
  
Pour plus d’informations sur la création d’une application de revendications @ no__t-0aware ASP.NET ou d’un service WCF, consultez le [Kit de développement logiciel (SDK) Windows Identity Foundation](https://go.microsoft.com/fwlink/?LinkId=122266).  
  
## <a name="see-also"></a>Voir aussi
[Guide de conception AD FS dans Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)

