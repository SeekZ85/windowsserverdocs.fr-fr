---
title: Migrer Windows Small Business Server 2011 Standard vers Windows Server Essentials
description: "Décrit comment utiliser WindowsServerEssentials"
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c8325f87-fd79-471b-bf70-3f052692c383
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 5ee0dd816354cb5acc31305de39062e558af1146
ms.sourcegitcommit: db290fa07e9d50686667bfba3969e20377548504
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 12/12/2017
---
# <a name="migrate-windows-small-business-server-2011-standard-to-windows-server-essentials"></a>Migrer Windows Small Business Server 2011 Standard vers Windows Server Essentials

>S’applique à: Windows Server2016Essentials, Windows Server2012R2 Essentials, Windows Server2012Essentials

Ce guide décrit comment migrer un domaine Windows Small Business Server 2011 Standard existant vers Windows Server® 2012 Essentials sur un nouveau matériel, puis comment migrer les paramètres et données. Ce guide décrit également comment supprimer votre serveur existant à partir du réseau de Windows Server Essentials après avoir terminé la migration.  
  
> [!NOTE]
>  Pour éviter tout problème pendant la migration, l’équipe de développement de produit Windows Server Essentials vous recommande vivement de lire ce document avant de commencer la migration.  
  
> [!NOTE]

>  Pour migrer les données de votre serveur vers la dernière version de Windows Server Essentials, consultez [migrer vers Windows Server Essentials](Migrate-from-Previous-Versions-to-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md).  

>  Pour migrer les données de votre serveur vers la dernière version de Windows Server Essentials, consultez [migrer vers Windows Server Essentials](../migrate/Migrate-from-Previous-Versions-to-Windows-Server-Essentials-or-Windows-Server-Essentials-Experience.md).  

  
## <a name="additional-resources"></a>Ressources supplémentaires  
 Pour des liens vers des informations supplémentaires, des outils et ressources de la Communauté qui peuvent vous guider tout au long du processus de migration, voir [Migration de Windows Small Business Server](https://go.microsoft.com/fwlink/?LinkId=217520).  
  
## <a name="terms-and-definitions"></a>Termes et définitions  
 **Serveur source:** serveur existant à partir duquel vous migrez vos paramètres et données.  
  
 **Serveur de destination:** le nouveau serveur vers lequel vous migrez vos paramètres et données.  
  
## <a name="migration-process-summary"></a>Résumé du processus de migration  
 Ce Guide de Migration inclut les étapes suivantes:  
  

1.  [Préparer la migration de votre serveur Source pour Windows Server Essentials](Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md).  Vous devez vous assurer que votre serveur Source et le réseau sont prêts pour la migration. Cette section vous guide par le biais de la sauvegarde du serveur Source, l’évaluation de l’intégrité du système de serveur Source, installer les service packs et les correctifs les plus récentes et vérification de la configuration réseau.  
  
2.  [Installer Windows Server Essentials en mode migration](Install-Windows-Server-Essentials-in-migration-mode.md).  Cette section décrit les étapes à suivre pour installer Windows Server Essentials sur le serveur de Destination en mode migration.  
  
3.  [Joindre des ordinateurs au nouveau serveur Windows Server Essentials](Join-computers-to-the-new-Windows-Server-Essentials-server.md).  Cette section explique comment joindre des ordinateurs clients au nouveau réseau Windows Server Essentials et mise à jour les paramètres de stratégie de groupe.  
  
4.  [Déplacer les paramètres de SBS 2011 et données vers le serveur de Destination](Move-Windows-SBS-2011-Standard-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md).  Cette section fournit des informations sur la migration des données et paramètres à partir du serveur Source.  
  
5.  [Activer la redirection de dossiers sur le serveur de Destination Windows Server Essentials](Enable-folder-redirection-on-the-Windows-Server-Essentials-Destination-Server.md).  Si la redirection de dossiers est activée sur le serveur Source, vous pouvez activer la redirection de dossiers sur le serveur de Destination, puis supprimez l’ancien paramètre de stratégie de groupe de Redirection de dossiers.  
  
6.  [Rétrograder et supprimer le serveur Source du nouveau réseau Windows Server Essentials](Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md).  Avant de pouvoir supprimer le serveur Source à partir du réseau, vous devez forcer une mise à jour de stratégie de groupe et rétrograder le serveur Source.  
  
7.  [Effectuer des tâches de post-migration pour la migration de Windows Server Essentials](Perform-post-migration-tasks-for-Windows-Server-Essentials-migration.md).  Après avoir terminé la migration de tous les paramètres et données vers Windows Server Essentials, vous voudrez peut-être mapper les ordinateurs autorisés aux comptes d’utilisateurs.  
  
8.  [Exécuter Windows Server Essentials Best Practices Analyzer](Run-the-Windows-Server-Essentials-Best-Practices-Analyzer.md).  Après avoir terminé la migration des paramètres et données vers Windows Server Essentials, vous devez exécuter l’outil BPA Windows Server Essentials.  

1.  [Préparer la migration de votre serveur Source pour Windows Server Essentials](../migrate/Prepare-your-Source-Server-for-Windows-Server-Essentials-migration.md).  Vous devez vous assurer que votre serveur Source et le réseau sont prêts pour la migration. Cette section vous guide par le biais de la sauvegarde du serveur Source, l’évaluation de l’intégrité du système de serveur Source, installer les service packs et les correctifs les plus récentes et vérification de la configuration réseau.  
  
2.  [Installer Windows Server Essentials en mode migration](../migrate/Install-Windows-Server-Essentials-in-migration-mode.md).  Cette section décrit les étapes à suivre pour installer Windows Server Essentials sur le serveur de Destination en mode migration.  
  
3.  [Joindre des ordinateurs au nouveau serveur Windows Server Essentials](../migrate/Join-computers-to-the-new-Windows-Server-Essentials-server.md).  Cette section explique comment joindre des ordinateurs clients au nouveau réseau Windows Server Essentials et mise à jour les paramètres de stratégie de groupe.  
  
4.  [Déplacer les paramètres de SBS 2011 et données vers le serveur de Destination](../migrate/Move-Windows-SBS-2011-Standard-settings-and-data-to-the-Destination-Server-for-Windows-Server-Essentials-migration.md).  Cette section fournit des informations sur la migration des données et paramètres à partir du serveur Source.  
  
5.  [Activer la redirection de dossiers sur le serveur de Destination Windows Server Essentials](../migrate/Enable-folder-redirection-on-the-Windows-Server-Essentials-Destination-Server.md).  Si la redirection de dossiers est activée sur le serveur Source, vous pouvez activer la redirection de dossiers sur le serveur de Destination, puis supprimez l’ancien paramètre de stratégie de groupe de Redirection de dossiers.  
  
6.  [Rétrograder et supprimer le serveur Source du nouveau réseau Windows Server Essentials](../migrate/Demote-and-remove-the-Source-Server-from-the-new-Windows-Server-Essentials-network.md).  Avant de pouvoir supprimer le serveur Source à partir du réseau, vous devez forcer une mise à jour de stratégie de groupe et rétrograder le serveur Source.  
  
7.  [Effectuer des tâches de post-migration pour la migration de Windows Server Essentials](../migrate/Perform-post-migration-tasks-for-Windows-Server-Essentials-migration.md).  Après avoir terminé la migration de tous les paramètres et données vers Windows Server Essentials, vous voudrez peut-être mapper les ordinateurs autorisés aux comptes d’utilisateurs.  
  
8.  [Exécuter Windows Server Essentials Best Practices Analyzer](../migrate/Run-the-Windows-Server-Essentials-Best-Practices-Analyzer.md).  Après avoir terminé la migration des paramètres et données vers Windows Server Essentials, vous devez exécuter l’outil BPA Windows Server Essentials.  

  
 Plusieurs des procédures de migration, vous devez ouvrir une fenêtre d’invite de commandes en tant qu’administrateur.  
  
###  <a name="BKMK_OpenACommandPromptAsAdmin"></a>Pour ouvrir une fenêtre d’invite de commandes sur le serveur Source en tant qu’administrateur  
  
1.  Cliquez sur **Démarrer**.  
  
2.  Dans la zone de recherche, tapez **cmd**.  
  
3.  Dans la liste des résultats, cliquez sur **cmd**, puis cliquez sur **exécuter en tant qu’administrateur**.  
  
#### <a name="to-open-a-command-prompt-window-on-the-destination-server-as-an-administrator"></a>Pour ouvrir une fenêtre d’invite de commandes sur le serveur de Destination en tant qu’administrateur  
  
1.  Sur le **Démarrer** écran, dans la zone de recherche, tapez **cmd**.  
  
2.  Dans la liste des résultats, cliquez sur **cmd**, puis cliquez sur **exécuter en tant qu’administrateur**.
