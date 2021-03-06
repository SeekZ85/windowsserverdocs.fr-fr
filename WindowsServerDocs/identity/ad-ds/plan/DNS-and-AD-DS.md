---
ms.assetid: c32606b4-2ee2-4df3-a704-8ac6723e188f
title: DNS et services AD DS
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/08/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: 82c96ac3f146510c5590aabea75a60ca0f5f90cc
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402686"
---
# <a name="dns-and-ad-ds"></a>DNS et services AD DS

>S'applique à : Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Active Directory Domain Services (AD DS) utilise des services de résolution de noms DNS (Domain Name System) pour permettre aux clients de localiser les contrôleurs de domaine et les contrôleurs de domaine qui hébergent le service d’annuaire pour communiquer entre eux.  
  
AD DS permet d’intégrer facilement l’espace de noms Active Directory dans un espace de noms DNS existant. Les fonctionnalités telles que les zones DNS intégrées à Active Directory facilitent le déploiement de DNS en éliminant la nécessité de configurer des zones secondaires, puis de configurer des transferts de zone.  
  
Pour plus d’informations sur la façon dont DNS prend en charge AD DS, consultez la section [prise en charge de DNS pour Active Directory informations techniques de référence](https://go.microsoft.com/fwlink/?LinkID=48147).  
  
> [!NOTE]  
> Si vous implémentez un espace de noms disjoint dans lequel le nom de domaine AD DS diffère du suffixe DNS principal utilisé par les clients, l’intégration AD DS avec DNS est plus complexe. Pour plus d’informations, consultez [espace de noms disjoint](../../ad-ds/plan/../../ad-ds/plan/Disjoint-Namespace.md).  
  
## <a name="in-this-section"></a>Dans cette section  
  
- [Emplacement des contrôleurs de domaine](../../ad-ds/plan/Domain-Controller-Location.md)  
- [Zones DNS intégrées à Active Directory](../../ad-ds/plan/Active-Directory-Integrated-DNS-Zones.md)  
- [Noms d’ordinateurs](../../ad-ds/plan/Computer-Naming.md)  
- [Espace de noms dissocié](../../ad-ds/plan/../../ad-ds/plan/Disjoint-Namespace.md)  
