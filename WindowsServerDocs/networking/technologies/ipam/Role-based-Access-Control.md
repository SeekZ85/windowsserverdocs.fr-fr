---
title: Contrôle d’accès basé sur les rôles
description: Cette rubrique fait partie du guide de gestion de la gestion des adresses IP (IPAM) dans Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology:
- networking-ipam
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ecdfc589-fa14-4bb3-ab7e-456ebc719385
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 86a57e5a74073ecf749c4ec8209999e8ace31508
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59838900"
---
# <a name="role-based-access-control"></a>Contrôle d’accès basé sur les rôles

>S’applique à : Windows Server (canal semi-annuel), Windows Server 2016

Cette rubrique fournit des informations sur l’utilisation de contrôle d’accès en fonction du rôle dans IPAM.  
  
> [!NOTE]  
> Outre cette rubrique, la documentation de contrôle d’accès IPAM suivante est disponible dans cette section.  
>   
> -   [Gérer en fonction du rôle avec le Gestionnaire de serveur de contrôle d’accès](../../technologies/ipam/Manage-Role-Based-Access-Control-with-Server-Manager.md)  
> -   [Gérer en fonction du rôle contrôle d’accès avec Windows PowerShell](../../technologies/ipam/Manage-Role-Based-Access-Control-with-Windows-PowerShell.md)  
  
Contrôle d’accès en fonction du rôle vous permet de spécifier des privilèges d’accès à différents niveaux, y compris le serveur DNS, zone DNS et niveaux d’enregistrement des ressources DNS.  
En utilisant le contrôle d’accès en fonction du rôle, vous pouvez spécifier qui a un contrôle granulaire sur les opérations pour créer, modifier et supprimer différents types d’enregistrements de ressource DNS.  
  
Vous pouvez configurer le contrôle d’accès afin que les utilisateurs sont limités pour les autorisations suivantes.  
  
-   Les utilisateurs peuvent modifier uniquement des enregistrements de ressource DNS spécifiques  
  
-   Les utilisateurs peuvent modifier les enregistrements de ressource DNS d’un type spécifique, tel que PTR ou MX  
  
-   Les utilisateurs peuvent modifier les enregistrements de ressource DNS pour des zones spécifiques  
  
## <a name="see-also"></a>Voir aussi  
[Gérer en fonction du rôle avec le Gestionnaire de serveur de contrôle d’accès](../../technologies/ipam/Manage-Role-Based-Access-Control-with-Server-Manager.md)  
[Gérer en fonction du rôle contrôle d’accès avec Windows PowerShell](../../technologies/ipam/Manage-Role-Based-Access-Control-with-Windows-PowerShell.md)  
[Gérer IPAM](Manage-IPAM.md)  
  


