---
title: Évitez d’activer des machines virtuelles configurées avec des adaptateurs de Fibre Channel virtuel pour autoriser les migrations dynamiques lorsqu’il y a moins de chemins vers Fibre Channel d’unités logiques (LUN) sur la destination que sur la source.
description: Version en ligne du texte de cette règle de Best Practices Analyzer.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: c55a8c76391ae1b01f43492dc5c72e3760371b80
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71365278"
---
# <a name="avoid-enabling-virtual-machines-configured-with-virtual-fibre-channel-adapters-to-allow-live-migrations-when-there-are-fewer-paths-to-fibre-channel-logical-units-luns-on-the-destination-than-on-the-source"></a>Évitez d’activer des machines virtuelles configurées avec des adaptateurs de Fibre Channel virtuel pour autoriser les migrations dynamiques lorsqu’il y a moins de chemins vers Fibre Channel d’unités logiques (LUN) sur la destination que sur la source.

>S’applique à Windows Server 2016

Pour plus d’informations sur les bonnes pratiques et les analyses, consultez [Exécuter des analyses Best Practices Analyzer et gérer les résultats des analyses](https://go.microsoft.com/fwlink/p/?LinkID=223177).  
  
|Propriété|Détails|  
|-|-|  
|**Système d'exploitation**|Windows Server 2016|  
|**Produit/fonctionnalité**|Hyper-V|  
|**Va**|Avertissement|  
|**Catégorie**|Configuration|

Dans les sections suivantes, l’italique indique le texte de l’interface utilisateur qui s’affiche dans l’outil Best Practices Analyzer pour ce problème.
  
## <a name="issue"></a>**Problème**  
*Une ou plusieurs machines virtuelles ont la propriété AllowReducedFcRedunancy définie dans le fournisseur WMI de virtualisation.*  
  
## <a name="impact"></a>**Impact**  
*La migration dynamique des machines virtuelles suivantes peut entraîner une perte de données ou une interruption des e/s dans le stockage :*  
  
\<liste des machines virtuelles >  
  
## <a name="resolution"></a>**Résolution**  
*Envisagez d’effacer la propriété WMI AllowReducedFcRedundancy sur les machines virtuelles affectées. Lorsque cette propriété est désactivée, vous pouvez effectuer une migration dynamique sur des ordinateurs virtuels configurés avec des adaptateurs de Fibre Channel virtuel uniquement lorsque le nombre de chemins d’accès à Fibre Channel sur la destination est identique ou supérieur au nombre de chemins d’accès sur la source. Ces contrôles permettent d’éviter la perte de données ou l’interruption des e/s vers le stockage.* 