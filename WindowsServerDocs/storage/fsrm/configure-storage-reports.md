---
title: Configurer des rapports de stockage
description: "Cet article explique comment configurer les paramètres par défaut des rapports de stockage"
ms.date: 7/7/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: f62109a8d3ea3e4e6386956789d276f9aa911e80
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/17/2017
---
# <a name="configure-storage-reports"></a>Configurer des rapports de stockage

> S’applique à: WindowsServer (canal semi-annuel), WindowsServer2016, WindowsServer2012R2, WindowsServer2012, WindowsServer2008R2

Vous pouvez configurer les paramètres par défaut des rapports de stockage. Ces paramètres par défaut sont utilisés pour les rapports d’incidents générés par un événement de quota ou de filtrage de fichiers. Ils servent également aux rapports planifiés et à la demande. Vous pouvez remplacer les paramètres par défaut lorsque vous définissez les propriétés spécifiques de ces rapports.

> [!Important]
> Lorsque vous modifiez les paramètres par défaut pour un type de rapport, les modifications affectent tous les rapports d'incidents et toutes les tâches de rapport planifiées existantes qui utilisent les paramètres par défaut.

## <a name="to-configure-the-default-parameters-for-storage-reports"></a>Pour configurer les paramètres par défaut des rapports de stockage

1. Dans l'arborescence de la console, cliquez avec le bouton droit sur **Gestionnaire de ressources du serveur de fichiers**, puis cliquez sur **Configurer les options**. La boîte de dialogue **Options du Gestionnaire de ressources du serveur de fichiers** s'affiche.

2. Sous l'onglet **Rapports de stockage**, sous **Configurer les paramètres par défaut**, sélectionnez le type de rapport que vous souhaitez modifier.

3. Cliquez sur **Modifier les paramètres**.

4. Selon le type de rapport sélectionné, différents paramètres de rapport à modifier sont proposés. Effectuez toutes les modifications nécessaires, puis cliquez sur **OK** pour les enregistrer en tant que paramètres par défaut pour ce type de rapport.

5.  Répétez les étapes2 à4 pour chaque type de rapport à modifier.

6. Pour afficher la liste des paramètres par défaut pour tous les rapports, cliquez sur **Consulter les rapports**. Cliquez ensuite sur **Fermer**.

7.  Cliquez sur **OK**.

## <a name="see-also"></a>Articles associés

-   [Définition des options du Gestionnaire de ressources du serveur de fichiers](setting-file-server-resource-manager-options.md)
-   [Gestion des rapports de stockage](storage-reports-management.md)