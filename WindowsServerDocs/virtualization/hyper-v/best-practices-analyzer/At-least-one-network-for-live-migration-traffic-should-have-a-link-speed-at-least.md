---
title: Au moins un réseau pour le trafic de migration en direct doit avoir une vitesse de liaison d’au moins 1 Gbit/s
description: Version en ligne du texte pour cette règle de Best Practices Analyzer.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 5714df3f-f810-4618-8c93-e24881651100
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: ef75f73bd934b863b146e93f4cdc7323e5d4c6fb
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59837730"
---
# <a name="at-least-one-network-for-live-migration-traffic-should-have-a-link-speed-of-at-least-1-gbps"></a>Au moins un réseau pour le trafic de migration en direct doit avoir une vitesse de liaison d’au moins 1 Gbit/s

>S'applique à : Windows Server 2016


  
|Propriété|Détails|  
|-|-|  
|**Système d'exploitation**|Windows Server 2016|  
|**Produit/fonctionnalité**|Hyper-V|  
|**Niveau de gravité**|Erreur|  
|**Catégorie**|Configuration|  
  
Dans les sections suivantes, italique indique le texte de l’interface utilisateur qui apparaît dans l’outil Best Practices Analyzer pour ce problème.  
  
## <a name="issue"></a>Problème  
*Aucun des réseaux pour le trafic de migration en direct ont une vitesse de liaison d’au moins 1 Gbit/s.*  
  
## <a name="impact"></a>Impact  
*Migrations dynamiques peuvent se produire lentement, ce qui peut entraîner une interruption la connexion de réseau en raison d’un délai d’expiration de la connexion TCP.*  
  
## <a name="resolution"></a>Résolution  
*Configurez au moins un réseau de migration en direct avec une vitesse de 1 Gbit/s ou plus rapide.*  
  
Consultez la documentation de votre fournisseur de matériel réseau pour déterminer si vos cartes réseau existant peuvent prendre en charge une vitesse de liaison d’au moins 1 Gbit/s.  
  


