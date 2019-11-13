---
title: 'Étape 3 : approuver et déployer des mises à jour dans WSUS'
description: Rubrique Windows Server Update Service (WSUS)-approuver et déployer des mises à jour dans WSUS est l’étape 3 dans un processus en quatre étapes pour le déploiement de WSUS
ms.prod: windows-server
ms.reviewer: na
ms.technology: manage-wsus
ms.topic: article
ms.assetid: 8d728ff9-170f-47e6-aefe-52be93315a75
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 68ff4c893302167815e3e8368d8b03f97d9be131
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71361692"
---
# <a name="step-3-approve-and-deploy-updates-in-wsus"></a>Étape 3 : Approuver et déployer des mises à jour dans WSUS

>S’applique à : Windows Server (canal semi-annuel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Les ordinateurs d’un groupe d’ordinateurs contactent automatiquement le serveur WSUS dans les 24 heures suivantes pour obtenir des mises à jour. Vous pouvez utiliser la fonctionnalité de création de rapports WSUS pour déterminer si ces mises à jour ont été déployées sur les ordinateurs de test. Lorsque les tests sont correctement effectués, vous pouvez approuver les mises à jour pour les groupes d’ordinateurs applicables dans votre organisation. La liste de contrôle suivante décrit les étapes de l’approbation et du déploiement des mises à jour à l’aide de la console de gestion des services WSUS.

|Tâche|Description|
|----|--------|
|[3,1. approuvez et déployez les mises à jour WSUS](3-approve-and-deploy-updates-in-wsus.md#BKM_3.1.)|Approuvez et déployez des mises à jour WSUS à l’aide de la console de gestion des services WSUS.|
|[3,2. configurer les règles d’approbation automatique](3-approve-and-deploy-updates-in-wsus.md#BKM_3.2.a.)|Configurez WSUS pour approuver automatiquement l'installation des mises à jour pour les groupes sélectionnés et pour déterminer comment approuver les révisions des mises à jour existantes.|
|[3,3. examen des mises à jour installées avec les rapports WSUS](3-approve-and-deploy-updates-in-wsus.md#BKM_3.3.)|Passez en revue les mises à jour qui ont été installées, les ordinateurs qui ont reçu ces mises à jour et d’autres informations à l’aide de la fonctionnalité de création de rapports WSUS.|

## <a name="BKM_3.1."></a>3,1. Approuver et déployer des mises à jour WSUS
Utilisez la procédure suivante pour approuver et déployer des mises à jour.

#### <a name="to-approve-and-deploy-wsus-updates"></a>Pour approuver et déployer des mises à jour WSUS

1.  Dans la console d’administration WSUS, cliquez sur **Mises à jour**. Dans le volet droit, une synthèse de l’état des mises à jour est affichée pour **Toutes les mises à jour**, **Mises à jour critiques**, **Mises à jour de sécurité** et **Mises à jour WSUS**.

2.  Dans la section **Toutes les mises à jour**, cliquez sur **Mises à jour requises par des ordinateurs**.

3.  Dans la liste des mises à jour, sélectionnez celles à approuver pour une installation dans votre groupe d’ordinateurs de test. Les informations relatives à une mise à jour sélectionnée sont disponibles dans le volet inférieur du panneau **Mises à jour**. Pour sélectionner plusieurs mises à jour contiguës, maintenez la touche **MAJ** enfoncée tout en cliquant sur les noms des mises à jour. Pour sélectionner plusieurs mises à jour non contiguës, appuyez sur la touche **CTRL** tout en cliquant sur les noms des mises à jour.

4.  Cliquez avec le bouton droit sur la sélection, puis cliquez sur **Approuver**.

5.  Dans la boîte de dialogue **Approuver les mises à jour**, sélectionnez votre groupe de test, puis cliquez sur la flèche vers le bas.

6.  Cliquez sur **Approuvée pour l’installation**, puis sur **OK**.

7.  La fenêtre **Progression de l’approbation** s’affiche. Elle indique la progression des tâches qui affectent l’approbation des mises à jour. Une fois le processus d’approbation terminé, cliquez sur **Fermer**.

## <a name="BKM_3.2.a."></a>3,2. Configurer les règles d'approbation automatique
Approbations automatiques vous permet de déterminer comment approuver automatiquement l'installation des mises à jour pour les groupes sélectionnés et comment approuver les révisions des mises à jour existantes.

#### <a name="to-configure-automatic-approvals"></a>Pour configurer Approbations automatiques

1.  Dans la console d'administration WSUS, sous **Update Services**, développez le serveur WSUS, puis cliquez sur **Options**. La fenêtre **Options** s'ouvre.

2.  Dans **Options**, cliquez sur **Approbations automatiques**. La boîte de dialogue Approbations automatiques s'ouvre.

3.  Dans **Règles de mise à jour**, cliquez sur **Nouvelle règle**. La boîte de dialogue **Ajouter une règle** s’ouvre.

4.  Dans **Ajouter une règle**, dans **étape 1 : sélectionnez des propriétés**, sélectionnez une option unique ou une combinaison d’options parmi les suivantes :

    -   **Quand une mise à jour se trouve dans une classification spécifique**

    -   **Quand une mise à jour se trouve dans un produit spécifique**

    -   **Définir un délai pour l'approbation**

5.  Dans **étape 2 : modifiez les propriétés**, cliquez sur chacune des options de la liste, puis sélectionnez les options appropriées pour chacune d’elles.

6.  À l’  **Étape 3 : Spécifiez un nom**, tapez le nom de votre règle, puis cliquez sur **OK**.

7.  Cliquez sur **OK** pour fermer la boîte de dialogue Approbations automatiques.

## <a name="BKM_3.3."></a>3,3. Passer en revue les mises à jour installées avec les rapports WSUS
24 heures après avoir approuvé les mises à jour, vous pouvez utiliser la fonctionnalité de création de rapports WSUS pour déterminer si les mises à jour ont été déployées sur les ordinateurs du groupe de test. Pour vérifier l’état d’une mise à jour, vous pouvez utiliser la fonctionnalité de création de rapports WSUS comme suit.

#### <a name="to-review-updates"></a>Pour passer en revue les mises à jour

1.  Dans le volet de navigation de la console d’administration WSUS, cliquez sur **Rapports**.

2.  Dans la page **Rapports** , cliquez sur le rapport **Synthèse de l’état des mises à jour** . La fenêtre du **rapport relatif aux mises à jour** s’affiche.

3.  Si vous voulez filtrer la liste des mises à jour, sélectionnez les critères à utiliser, par exemple **Inclure les mises à jour dans ces classifications**, puis cliquez sur **Exécuter le rapport**.

4.  Le volet du **rapport relatif aux mises à jour** s’affiche. Vous pouvez vérifier l’état de mises à jour individuelles en sélectionnant la mise à jour dans la section gauche du volet. La dernière section du volet de rapport indique la synthèse de l’état de la mise à jour.

5.  Vous pouvez enregistrer ou imprimer ce rapport en cliquant sur l’icône appropriée de la barre d’outils.

6.  Après avoir testé les mises à jour, vous pouvez les approuver pour une installation dans les groupes d’ordinateurs applicables de votre organisation.
