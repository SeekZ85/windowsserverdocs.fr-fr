---
title: Architecture Hyper-V
description: Architecture Hyper-v condsiderations pour le réglage des performances
ms.prod: windows-server
ms.technology: performance-tuning-guide
ms.topic: article
ms.author: Asmahi; SandySp; JoPoulso
author: phstee
ms.date: 10/16/2017
ms.openlocfilehash: 0feb2977791dd181907c381e4898924ff51c2bc5
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71383492"
---
# <a name="hyper-v-architecture"></a>Architecture Hyper-V

Hyper-V propose une architecture basée sur un hyperviseur de type 1. L’hyperviseur virtualise les processeurs et la mémoire et fournit des mécanismes pour la pile de virtualisation dans la partition racine afin de gérer des partitions enfants (ordinateurs virtuels) et d’exposer des services tels que des périphériques d’e/s aux ordinateurs virtuels.

La partition racine possède un accès direct aux périphériques d’e/s physiques. La pile de virtualisation dans la partition racine fournit un gestionnaire de mémoire pour les machines virtuelles, les API de gestion et les périphériques d’e/s virtualisés. Il implémente également des appareils émulés tels que le contrôleur de disque IDE (Integrated Device Electronics) et le port d’entrée PS/2, et prend en charge les appareils synthétiques spécifiques à Hyper-V pour accroître les performances et réduire la surcharge.

![architecture basée sur l’hyperviseur Hyper-v](../../media/perftune-guide-hyperv-arch.png)

L’architecture d’e/s spécifique à Hyper-V se compose des fournisseurs de services de virtualisation (VSPs) dans les clients de la partition racine et du service de virtualisation (VSC) de la partition enfant. Chaque service est exposé comme un appareil sur VMBus, qui agit comme un bus d’e/s et permet une communication hautes performances entre les ordinateurs virtuels qui utilisent des mécanismes tels que la mémoire partagée. Le gestionnaire de Plug-and-Play du système d’exploitation invité énumère ces appareils, y compris VMBus, et charge les pilotes de périphériques appropriés (clients de service virtuel). Les services autres que les e/s sont également exposés via cette architecture.

À compter de Windows Server 2008, le système d’exploitation propose des options d’inversion pour optimiser son comportement lorsqu’il s’exécute sur des machines virtuelles. Les avantages incluent la réduction du coût de la virtualisation de mémoire, l’amélioration de l’évolutivité multicœur et la diminution de l’utilisation de l’UC en arrière-plan du système d’exploitation invité.

Les sections suivantes suggèrent des méthodes recommandées qui améliorent les performances sur les serveurs qui exécutent le rôle Hyper-V.

## <a name="see-also"></a>Voir aussi

-   [Terminologie Hyper-V](terminology.md)

-   [Configuration du serveur Hyper-V](configuration.md)

-   [Performances du processeur Hyper-V](processor-performance.md)

-   [Performances de la mémoire Hyper-V](memory-performance.md)

-   [Performances E/S du stockage Hyper-V](storage-io-performance.md)

-   [Performances E/S du réseau Hyper-V](network-io-performance.md)

-   [Détecter les goulots d’étranglement dans un environnement virtualisé](detecting-virtualized-environment-bottlenecks.md)

-   [Ordinateurs virtuels Linux](linux-virtual-machine-considerations.md)
