---
title: Vue d’ensemble du scénario de laboratoire de test de cluster DirectAccess avec équilibrage de charge réseau
description: Cette rubrique fait partie du Guide de laboratoire de test-démonstration de DirectAccess dans un cluster avec Windows NLB pour Windows Server 2016
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cd1e9efd-19e9-49e7-8432-881f661c9792
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 487b85713d415cdda9ee40548091abdb5fe7fc2e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71404836"
---
# <a name="overview-of-the-directaccess-cluster-nlb-test-lab-scenario"></a>Vue d’ensemble du scénario de laboratoire de test de cluster DirectAccess avec équilibrage de charge réseau

>S'applique à : Windows Server (Canal semi-annuel), Windows Server 2016

Dans ce scénario de laboratoire de test, DirectAccess est déployé avec :  
  
-   **DC1**: serveur configuré en tant que contrôleur de domaine, serveur DNS (Domain Name System) et serveur DHCP (Dynamic Host Configuration Protocol).  
  
-   **Edge1**: serveur sur le réseau interne qui est configuré en tant que premier serveur d’accès à distance dans un cluster de serveurs d’accès à distance. Ce serveur a deux cartes réseau ; l’une connectée au réseau interne et l’autre connectée au réseau externe.  
  
-   **EDGE2**: serveur sur le réseau interne qui est configuré en tant que deuxième serveur d’accès à distance dans un cluster de serveurs d’accès à distance. Ce serveur a deux cartes réseau ; l’une connectée au réseau interne et l’autre connectée au réseau externe.  
  
-   **App1**: un serveur sur le réseau interne qui est configuré en tant que serveur Web et de fichiers, et en tant qu’autorité de certification racine d’entreprise.  
  
-   **App2**: un ordinateur sur le réseau interne configuré en tant que serveur Web et serveur de fichiers IPv4 uniquement. Cet ordinateur est utilisé pour mettre en surbrillance les fonctionnalités NAT64/DNS64.  
  
-   **INET1**: serveur configuré en tant que serveur DNS Internet et serveur DHCP.  
  
-   **NAT1**: ordinateur client configuré en tant qu’appareil NAT (Network Address Translator) à l’aide du partage de connexion Internet.  
  
-   **CLIENT1**: un ordinateur client configuré en tant que client DirectAccess qui sera utilisé pour tester la connectivité DirectAccess lors du déplacement entre le réseau interne, l’Internet simulé et un réseau privé.  
  
Le laboratoire de test se compose de trois sous-réseaux qui simulent les éléments suivants :  
  
-   Un réseau local nommé HomeNet (192.168.137.0/24) connecté à Internet par un NAT.  
  
-   Le réseau externe représenté par le sous-réseau Internet (131.107.0.0/24).  
  
-   Un réseau interne nommé corpnet (10.0.0.0/24 ; 2001 : DB8:1 ::/64), séparé d’Internet par le serveur d’accès à distance.  
  
Les ordinateurs de chaque sous-réseau se connectent à l’aide d’un concentrateur ou d’un concentrateur physique ou virtuel, comme illustré dans la figure suivante.  
  
![Vue d’ensemble du laboratoire de test](../../../media/Overview-of-the-Test-Lab-Scenario_5/TLG_DA_Cluster.png)  
  


