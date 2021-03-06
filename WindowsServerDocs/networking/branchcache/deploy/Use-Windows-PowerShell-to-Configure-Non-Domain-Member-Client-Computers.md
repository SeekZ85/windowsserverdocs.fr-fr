---
title: Utiliser Windows PowerShell pour configurer des ordinateurs clients non membres du domaine
description: Cette rubrique fait partie du Guide de déploiement BranchCache pour Windows Server 2016, qui montre comment déployer BranchCache en mode de cache distribué et hébergé pour optimiser l’utilisation de la bande passante WAN dans les filiales.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-bc
ms.topic: get-started-article
ms.assetid: 1b511e1a-686d-441f-a1c7-d4d029e1a061
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 9743d93fe7bc21a971ff886a7e255eed3b775c97
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71406427"
---
# <a name="use-windows-powershell-to-configure-non-domain-member-client-computers"></a>Utiliser Windows PowerShell pour configurer des ordinateurs clients non membres du domaine

>S’applique à : Windows Server (Canal semi-annuel), Windows Server 2016

Vous pouvez utiliser cette procédure pour configurer manuellement un ordinateur client BranchCache pour le mode de cache distribué ou le mode de cache hébergé.  
  
> [!NOTE]  
> Si vous avez configuré des ordinateurs clients BranchCache à l’aide de stratégie de groupe, les paramètres stratégie de groupe remplacent toute configuration manuelle des ordinateurs clients auxquels les stratégies sont appliquées.  
  
Pour exécuter cette procédure, il est nécessaire d'appartenir au minimum au groupe **Administrateurs** ou à un groupe équivalent.  
  
### <a name="to-enable-branchcache-distributed-or-hosted-cache-mode"></a>Pour activer le mode de cache distribué ou hébergé de BranchCache  
  
1.  Sur l’ordinateur client BranchCache que vous souhaitez configurer, exécutez Windows PowerShell en tant qu’administrateur, puis effectuez l’une des opérations suivantes.  
  
    -   Pour configurer l’ordinateur client pour le mode de cache distribué BranchCache, tapez la commande suivante, puis appuyez sur entrée.  
  
        `Enable-BCDistributed`  
  
    -   Pour configurer l’ordinateur client pour le mode de cache hébergé de BranchCache, tapez la commande suivante, puis appuyez sur entrée.  
  
        `Enable-BCHostedClient`  
  
        > [!TIP]  
        > Si vous souhaitez spécifier les serveurs de cache hébergé disponibles, utilisez le paramètre `-ServerNames` avec une liste séparée par des virgules de vos serveurs de cache hébergé comme valeur de paramètre. Par exemple, si vous avez deux serveurs de cache hébergé nommés HCS1 et HCS2, configurez l’ordinateur client pour le mode de cache hébergé à l’aide de la commande suivante.  
        >   
        > `Enable-BCHostedClient -ServerNames HCS1,HCS2`  
  


