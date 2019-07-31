---
title: Quel est le type d’installation qui vous convient
description: Cette rubrique décrit les différentes options d’installation du centre d’administration Windows, y compris l’installation de sur un PC Windows 10 ou un serveur Windows Server pour une utilisation par plusieurs administrateurs.
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.localizationpriority: medium
ms.prod: windows-server-threshold
ms.date: 06/07/2019
ms.openlocfilehash: 36c9dfcb38ef417df56206cdb18633cc877183c4
ms.sourcegitcommit: af80963a1d16c0b836da31efd9c5caaaf6708133
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/30/2019
ms.locfileid: "68658900"
---
# <a name="what-type-of-installation-is-right-for-you"></a>Quel type d’installation vous convient ?

>S'applique à : Windows Admin Center, Windows Admin Center Preview

Cette rubrique décrit les différentes options d’installation du centre d’administration Windows, y compris l’installation de sur un PC Windows 10 ou un serveur Windows Server pour une utilisation par plusieurs administrateurs. Pour installer le centre d’administration Windows sur une machine virtuelle dans Azure, consultez [déployer le centre d’administration Windows dans Azure](../azure/deploy-wac-in-azure.md).

## <a name="installation-types"></a>Installation : Types

| Client local                                | Serveur de passerelle                                  | Serveur géré                               | Cluster de basculement                           |
|---------------------------------------------|-------------------------------------------------|----------------------------------------------|--------------------------------------------|
| ![IMG](../media/deployment-options/W10.PNG) | ![IMG](../media/deployment-options/gateway.PNG) | ![IMG](../media/deployment-options/node.PNG) | ![IMG](../media/deployment-options/HA.png) |
| Installez sur un client Windows 10 local qui dispose d’une connectivité aux serveurs gérés.  Idéal pour les scénarios de démarrage rapide, de test, ad hoc ou à petite échelle. |Installez sur un serveur de passerelle désigné et accédez à partir de n’importe quel navigateur client avec une connectivité au serveur de passerelle.  Idéal pour les scénarios à grande échelle. | Installez directement sur un serveur géré dans le but de gérer lui-même ou un cluster dans lequel il est un nœud membre.  Idéal pour les scénarios distribués. | Déployez dans un cluster de basculement pour activer la haute disponibilité du service de passerelle. Idéal pour les environnements de production afin de garantir la résilience de votre service de gestion. |

## <a name="installation-supported-operating-systems"></a>Installation : Systèmes d’exploitation pris en charge

Vous pouvez **installer** le centre d’administration Windows sur les systèmes d’exploitation Windows suivants:

| **Multi**                       | **Mode d’installation** |
| -----------------------------------| --------------------- |
| Windows 10, version 1709 ou ultérieure  | Client local |
| Canal semi-annuel Windows Server | Serveur de passerelle, serveur géré, cluster de basculement |
| Windows Server 2016                | Serveur de passerelle, serveur géré, cluster de basculement |
| Windows Server 2019                | Serveur de passerelle, serveur géré, cluster de basculement |

Pour faire fonctionner le centre d’administration Windows:

- **Dans le scénario client local:** Lancez la passerelle du centre d’administration Windows à partir du menu Démarrer et connectez-vous à partir d’un navigateur `https://localhost:6516`Web client en accédant à.
- **Dans d’autres scénarios:** Connectez-vous à la passerelle du centre d’administration Windows sur un autre ordinateur à partir d’un navigateur client via son URL, par exemple,`https://servername.contoso.com`

> [!WARNING]
> L’installation du centre d’administration Windows sur un contrôleur de domaine n’est pas prise en charge. [En savoir plus sur les meilleures pratiques en matière de sécurité du contrôleur de domaine](https://docs.microsoft.com/windows-server/identity/ad-ds/plan/security-best-practices/securing-domain-controllers-against-attack). 

## <a name="installation-supported-web-browsers"></a>Installation : Navigateurs Web pris en charge

Microsoft Edge et Google Chrome sont testés et pris en charge sur Windows 10. D’autres navigateurs Web, y compris Internet Explorer et Firefox, ne font pas partie de notre matrice de test et ne sont donc pas *officiellement* pris en charge. Ces navigateurs peuvent rencontrer des problèmes lors de l’exécution du centre d’administration Windows. Par exemple, Firefox possède son propre magasin de certificats. vous devez donc importer le `Windows Admin Center Client` certificat dans Firefox pour utiliser le centre d’administration Windows sur Windows 10. Pour plus d’informations, consultez [problèmes connus spécifiques au navigateur](../support/known-issues.md#browser-specific-issues).

## <a name="management-target-supported-operating-systems"></a>Cible de gestion: Systèmes d’exploitation pris en charge

Vous pouvez **gérer** les systèmes d’exploitation Windows suivants à l’aide du centre d’administration Windows:

| Version | Gérer les nœuds via *Gestionnaire de serveur* | Gérer le *cluster* via *Gestionnaire du cluster de basculement* | Gérer *HCI* via le *Gestionnaire de cluster HCI* |
| ------------------------- |--------------- | ----- | ------------------------ |
| Windows 10, version 1709 ou ultérieure | Oui (via gestion de l’ordinateur) | N/A | N/A |
| Canal semi-annuel Windows Server | Oui | Oui | N/A |
| Windows Server 2019 | Oui | Oui | Oui |
| Windows Server 2016 | Oui | Oui | Oui, avec la [dernière mise à jour cumulative](../use/manage-hyper-converged.md#prepare-your-windows-server-2016-cluster-for-windows-admin-center) |
| Microsoft Hyper-V Server 2016 | Oui | Oui | N/A |
| Windows Server 2012 R2 | Oui | Oui | N/A |
| Microsoft Hyper-V Server 2012 R2 | Oui | Oui | N/A |
| Windows Server 2012 | Oui | Oui | N/A |
| Windows Server 2008 R2 | Oui, fonctionnalités limitées | N/A | N/A |

> [!NOTE]
> Le centre d’administration Windows requiert des fonctionnalités PowerShell qui ne sont pas incluses dans Windows Server 2008 R2, 2012 et 2012 R2. Si vous souhaitez les gérer à l’aide du centre d’administration Windows, vous devez installer Windows Management Framework (WMF) version 5,1 ou ultérieure sur ces serveurs.
> 
> Saisissez `$PSVersiontable` dans PowerShell pour vérifier que WMF est installé, et que sa version est 5.1 ou ultérieure. 
> 
> Si WMF n’est pas installé, vous pouvez [Télécharger wmf 5,1](https://www.microsoft.com/en-us/download/details.aspx?id=54616).

## <a name="high-availability"></a>Haute disponibilité

Vous pouvez activer la haute disponibilité du service de passerelle en déployant le centre d’administration Windows dans un modèle actif/passif sur un cluster de basculement. Si l’un des nœuds du cluster échoue, le centre d’administration Windows bascule normalement vers un autre nœud, ce qui vous permet de continuer à gérer les serveurs de votre environnement en toute transparence.

[Découvrez comment déployer le centre d’administration Windows avec une haute disponibilité.](../deploy/high-availability.md)

> [!Tip]
> Prêt à installer Windows Admin Center ? [Télécharger maintenant](https://aka.ms/windowsadmincenter)
