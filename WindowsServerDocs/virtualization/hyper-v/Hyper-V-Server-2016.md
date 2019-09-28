---
title: Microsoft Hyper-V Server 2016
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: f815ada0-4c63-4e73-9c24-dc5eb21526c7
author: KBDAzure
ms.author: kathydav
ms.date: 07/26/2017
ms.openlocfilehash: c9e1b5e2d30276bf89bc2d56482ec76d1c2241a2
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71365577"
---
# <a name="microsoft-hyper-v-server-2016"></a>Microsoft Hyper-V Server 2016

Microsoft Hyper-V Server 2016 est un produit @ no__t-0alone stand qui contient uniquement l’hyperviseur Windows, un modèle de pilote Windows Server et les composants de virtualisation. Il fournit une solution de virtualisation simple et fiable pour vous aider à améliorer l’utilisation de vos serveurs et à réduire les coûts.

La technologie d’hyperviseur Windows dans Microsoft Hyper-V Server 2016 est identique à celle du rôle Hyper @ no__t-0V sur Windows Server 2016. Ainsi, une grande partie du contenu disponible pour le rôle Hyper @ no__t-0V sur Windows Server 2016 s’applique également à Microsoft Hyper-V Server 2016.

## <a name="hyper-v-server-resources-for-it-pros"></a>Hyper @ no__t-ressources de serveur 0V pour les professionnels de l’informatique

|Tâches|Ressources|
|-|-|
|![Respecte le symbole des exigences](media/All_Symbols_MeetsRequirements.png)|**Évaluer Hyper-V**<br /><br />[vue d’ensemble de la technologie Hyper-V](hyper-v-technology-overview.md) -   <br />- [Nouveautés d’Hyper-V sur Windows Server 2016](what-s-new-in-hyper-v-on-windows.md)<br />-   [Configuration système requise pour Hyper-V sur Windows Server 2016](system-requirements-for-hyper-v-on-windows.md)<br />-   [systèmes d’exploitation invités Windows pris en charge pour Hyper-V](supported-windows-guest-operating-systems-for-hyper-v-on-windows.md)<br />[machines virtuelles Linux et FreeBSD prises en charge](supported-linux-and-freebsd-virtual-machines-for-hyper-v-on-windows.md) par -   <br />-   [compatibilité des fonctionnalités par génération et invité](hyper-v-feature-compatibility-by-generation-and-guest.md)<br /><br />**Planifier Hyper-V**<br /><br />-Choisissez la [génération d’ordinateur virtuel](plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v.md) qui répond à vos besoins. <br/>-Si vous déplacez ou importez des machines virtuelles, décidez quand [mettre à niveau la version](deploy/upgrade-virtual-machine-version-in-hyper-v-on-windows-or-windows-server.md). <br />[extensibilité](plan/plan-hyper-v-scalability-in-windows-server.md) -  <br />[mise en réseau](plan/plan-hyper-v-networking-in-windows-server.md) -  <br />- [sécurité](plan/plan-hyper-v-security-in-windows-server.md)|
|![Symbole de prise en main](media/All_Symbols_GetStarted.png)|**Prise en main d’Hyper-V Server**<br /><br />[Téléchargez et installez Microsoft Hyper @ no__t-1V Server 2016](https://www.microsoft.com/evalcenter/evaluate-hyper-v-server-2016). Cela installe l’hyperviseur Windows, un modèle de pilote Windows Server et les composants de virtualisation. Elle est similaire à l’exécution de l’option d’installation Server Core de Windows Server 2016 et du rôle Hyper @ no__t-0V.|
|![Gérer les symboles](media/All_Symbols_Administrator.png)|**Configurer et gérer le serveur Hyper-V**<br /><br />Hyper @ no__t-0V Server ne dispose pas d’une interface utilisateur graphique \(GUI @ no__t-2. Vous pouvez utiliser les outils suivants pour configurer et gérer hyper @ no__t-0V Server.<br /><br />-   [configurer une installation Server Core de Windows server 2016 avec sconfig. cmd](../../get-started/sconfig-on-ws2016.md) pour mettre à jour les paramètres de domaine ou de groupe de travail, modifier les paramètres de Windows Update, activer la gestion à distance, et bien plus encore.<br />-Utilisez une [invite](../../administration/windows-commands/windows-commands.md) de commandes ordinaire pour les commandes non disponibles dans sconfig.<br />-Utilisez [hyper @ no__t-1V Manager](https://msdn.microsoft.com/virtualization/hyperv_on_windows/user_guide/remote_host_management) ou [Virtual Machine Manager](https://docs.microsoft.com/system-center/vmm) pour gérer à distance le serveur Hyper @ no__t-3V. Pour utiliser hyper @ no__t-0V Manager, [Installez le rôle Hyper @ no__t-2V sur Windows 10](https://docs.microsoft.com/virtualization/hyper-v-on-windows/quick-start/enable-hyper-v) ou [Windows Server 2016](get-started/install-the-hyper-v-role-on-windows-server.md).<br />-Voir [Installer Server Core](../../get-started/getting-started-with-server-core.md) pour obtenir des options de gestion supplémentaires pour les fonctions de serveur de base qui ne sont pas spécifiques à hyper @ No__t-1V. La plupart des méthodes de gestion documentées sont également compatibles avec Hyper @ no__t-0V Server.<br /><br />**Configurer et gérer les machines virtuelles hyper @ no__t-1V**<br /><br />-   [créer un commutateur virtuel pour les machines virtuelles Hyper-V](get-started/create-a-virtual-switch-for-hyper-v-virtual-machines.md)<br />-   [créer une machine virtuelle dans Hyper-V](get-started/create-a-virtual-machine-in-hyper-v.md)<br />-   [choisir entre des points de contrôle standard ou de production](manage/choose-between-standard-or-production-checkpoints-in-hyper-v.md)<br />-   [activer ou désactiver les points de contrôle](manage/enable-or-disable-checkpoints-in-hyper-v.md)<br />-   [gérer des machines virtuelles Windows avec PowerShell direct](manage/manage-windows-virtual-machines-with-powershell-direct.md) <br /><br />**Déployer**<br /><br />-   [configurer des hôtes pour la migration dynamique sans clustering de basculement](deploy/set-up-hosts-for-live-migration-without-failover-clustering.md)<br />- [mettre à niveau les nœuds de cluster Windows Server](../../failover-clustering/cluster-operating-system-rolling-upgrade.md)<br />[version de la machine virtuelle de mise à niveau](deploy/upgrade-virtual-machine-version-in-hyper-v-on-windows-or-windows-server.md) @no__t 0<br />|
