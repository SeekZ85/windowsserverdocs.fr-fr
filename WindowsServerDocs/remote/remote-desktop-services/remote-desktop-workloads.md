---
title: Charges de travail Bureau à distance
description: Petite vue d’ensemble des différents types de charges de travail pour les machines virtuelles gérées par Bureau à distance.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: helohr
ms.date: 12/02/2019
ms.tgt_pltfrm: na
ms.topic: article
author: Heidilohr
manager: lizross
ms.openlocfilehash: 693d1abd91fbfa2d44a6af42dd9f5338bd461927
ms.sourcegitcommit: 76469d1b7465800315eaca3e0c7f0438fc3939ed
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/13/2020
ms.locfileid: "75919944"
---
# <a name="remote-desktop-workloads"></a>Charges de travail Bureau à distance

Les utilisateurs peuvent exécuter différents types de charges de travail sur les machines virtuelles gérées par les services Bureau à distance ou Windows Virtual Desktop. Adaptez votre déploiement en fonction du besoin attendu de chaque type d’utilisateur. Le tableau suivant fournit des exemples d’une gamme de types de charges de travail pour vous aider à estimer la taille que vos machines virtuelles doivent avoir. Après avoir configuré vos machines virtuelles, vous devez superviser en permanence leur utilisation véritable et ajuster leur taille en conséquence. Si vous en venez à avoir besoin d’une machine virtuelle plus grande ou plus petite, vous pouvez facilement mettre à l’échelle votre déploiement existant dans Azure.

Le tableau suivant décrit chaque charge de travail. Les « exemples d’utilisateurs » sont les types d’utilisateurs pour lesquels chaque charge de travail peut s’avérer la plus utile. Les « exemples d’applications » sont les genres d’applications qui fonctionnent le mieux pour chaque charge de travail.

| Type de charge de travail | Exemples d’utilisateurs | Exemples d’applications |
| --- | --- | --- |
| Léger | Utilisateurs exécutant des tâches élémentaires de saisie de données | Applications de saisie de base de données, interfaces de ligne de commande |
| Moyen | Consultants et analystes de marché | Applications de saisie de base de données, interfaces de ligne de commande, Microsoft Word, pages web statiques |
| Intensif | Ingénieurs informaticiens, créateurs de contenu | Applications de saisie de base de données, interfaces de ligne de commande, Microsoft Word, pages web statiques, Microsoft Outlook, Microsoft PowerPoint, pages web dynamiques |
| Avancé | Infographistes, créateurs de modèles 3D, chercheurs en Machine Learning | Applications de saisie de base de données, interfaces de ligne de commande, Microsoft Word, pages web statiques, Microsoft Outlook, Microsoft PowerPoint, pages web dynamiques, Adobe Photoshop, Adobe Illustrator, conception assistée par ordinateur (CAO), fabrication assistée par ordinateur (FAO) |

Pour obtenir des informations sur les recommandations de dimensionnement, consultez [Guide de dimensionnement des machines virtuelles](virtual-machine-recs.md).
