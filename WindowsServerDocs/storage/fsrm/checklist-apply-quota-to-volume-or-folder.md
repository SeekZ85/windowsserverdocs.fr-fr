---
title: Appliquer un quota à un volume ou un dossier
description: Cet article explique comment appliquer un quota de stockage à un volume ou un dossier
ms.date: 7/7/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: e937464ca3af1292de5fd63303ba4a430f831dcd
ms.sourcegitcommit: ed27ddbe316d543b7865bc10590b238290a2a1ad
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/09/2019
ms.locfileid: "65475859"
---
# <a name="checklist-apply-a-quota-to-a-volume-or-folder"></a>Liste de vérification : Appliquer un Quota pour un volume ou un dossier

> S’applique à : Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2, Windows Server (canal semi-annuel)

1. Configurez les paramètres de messagerie si vous prévoyez d’envoyer des notifications de seuil ou des rapports de stockage par courrier électronique. [Configurer des Notifications par courrier électronique](configure-email-notifications.md)

2. Évaluez les besoins de stockage sur le volume ou le dossier. Vous pouvez utiliser des rapports sur le nœud **Gestion des rapports de stockage** pour fournir des données. (Par exemple, exécutez des fichiers par rapport de propriétaire à la demande pour identifier les utilisateurs qui utilisent une grande quantité d’espace disque.) [Générer des rapports à la demande](generate-reports-on-demand.md)

3. Passez en revue les modèles de quotas préconfigurés disponibles. (Dans **gestion de Quota**, cliquez sur le **les modèles de Quota** nœud.) [Modifier les propriétés de modèle de Quota](edit-quota-template-properties.md) 
<br />- Ou - <br /> Créez un nouveau modèle de quota pour appliquer une stratégie de stockage dans votre organisation. [Créer un modèle de Quota](create-quota-template.md)

4. Créez un quota basé sur le modèle sur le volume ou le dossier.  
 [Créer un quota](create-quota.md) <br /> - Ou - <br /> Créez un quota automatique pour générer automatiquement des quotas pour les sous-dossiers sur le volume ou le dossier. [Créer un quota automatique](create-auto-apply-quota.md)

6. Planifiez une tâche de rapport contenant un rapport d’utilisation du quota pour surveiller l’utilisation du quota régulièrement. [Planifier un ensemble de rapports](schedule-set-of-reports.md)

> [!Note]
> Si vous souhaitez filtrer les fichiers sur un volume ou un dossier, consultez [liste de vérification : Appliquer un filtre de fichiers à un Volume ou un dossier](checklist-apply-file-screen-to-volume-or-folder.md).











