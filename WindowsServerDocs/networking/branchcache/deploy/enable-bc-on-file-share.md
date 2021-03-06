---
title: Activer BranchCache sur un partage de fichiers (facultatif)
description: Cette rubrique fait partie du Guide de déploiement BranchCache pour Windows Server 2016, qui montre comment déployer BranchCache en mode de cache distribué et hébergé pour optimiser l’utilisation de la bande passante WAN dans les filiales.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-bc
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 9c465a9e-c504-44ec-9ebc-4e06ba54db30
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 37bab11a0914a3f6854314016bb59297aa6954f2
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71406364"
---
# <a name="enable-branchcache-on-a-file-share-optional"></a>Activer BranchCache sur un partage de fichiers (facultatif)

>S’applique à : Windows Server (Canal semi-annuel), Windows Server 2016

Vous pouvez utiliser cette procédure pour activer BranchCache sur un partage de fichiers.  
  
> [!IMPORTANT]  
> Vous n’avez pas besoin d’effectuer cette procédure si vous configurez le paramètre de publication de hachage avec la valeur **autoriser la publication de hachages pour tous les dossiers partagés**.  
  
Pour exécuter cette procédure, il est nécessaire d'appartenir au minimum au groupe **Administrateurs** ou à un groupe équivalent.  
  
### <a name="to-enable-branchcache-on-a-file-share"></a>Pour activer BranchCache sur un partage de fichiers  
  
1.  Ouvrez Windows PowerShell, saisissez **mmc**, puis appuyez sur ENTRÉE. La console MMC s'affiche.  
  
2.  Dans la console MMC, dans le menu **Fichier**, cliquez sur **Ajouter/Supprimer un composant logiciel enfichable**. La boîte de dialogue **Ajouter ou supprimer des composants logiciels enfichables** s'ouvre.  
  
3.  Dans **Ajouter ou supprimer des composants logiciels enfichables**, dans **composants logiciels enfichables disponibles**, double-cliquez sur **dossiers partagés**. L’Assistant dossiers partagés s’ouvre avec l’objet ordinateur local sélectionné. Configurez l’affichage de votre choix, cliquez sur **Terminer**, puis sur **OK**.  
  
4.  Double-cliquez sur **dossiers partagés (local)** , puis cliquez sur **partages**.  
  
5.  Dans le volet d’informations, cliquez avec le bouton droit sur un partage, puis cliquez sur **Propriétés**. La boîte de dialogue **Propriétés** du partage s’ouvre.  
  
6.  Dans la boîte de dialogue **Propriétés** , sous l’onglet **général** , cliquez sur **paramètres hors connexion**. La boîte de dialogue **paramètres hors connexion** s’ouvre.  
  
7.  Assurez-vous que **seuls les fichiers et les programmes spécifiés par les utilisateurs sont disponibles hors connexion** est sélectionné, puis cliquez sur **activer BranchCache**.  
  
8.  Cliquez deux fois sur **OK**.  
  

