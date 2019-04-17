---
title: "Créer une propriété de classification"
description: "Cet article décrit les propriétés de classification utilisées pour affecter des valeurs à des fichiers dans un dossier ou un volume spécifié."
ms.date: 7/7/2017
ms.prod: windows-server-threshold
ms.technology: storage
ms.topic: article
author: JasonGerend
manager: brianlic
ms.author: jgerend
ms.openlocfilehash: aa1f1a2ab4422f4bb36a737e47894b22b60160e1
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/17/2017
---
# <a name="create-a-classification-property"></a>Créer une propriété de classification

> S’applique à: WindowsServer (canal semi-annuel), WindowsServer2016, WindowsServer2012R2, WindowsServer2012, WindowsServer2008R2

Les propriétés de classification sont utilisées pour affecter des valeurs à des fichiers dans un dossier ou un volume spécifié. Vous avez le choix entre de nombreux types de propriétés, en fonction de vos besoins. Le tableau suivant définit les types de propriétés disponibles:

|Propriété | Description |
| --- | --- |
| Oui/Non | Propriété booléenne qui peut être **Oui** ou **Non**. Lorsque plusieurs valeurs sont combinées lors de la classification ou à partir du contenu du fichier, une valeur **Non** sera remplacée par une valeur **Oui**. |
| Date-heure | Simple propriété de date/heure. Lorsque plusieurs valeurs sont combinées lors de la classification ou à partir du contenu du fichier, les valeurs conflictuelles empêchent la reclassification. |
| Numéro | Simple propriété de numéro. Lorsque plusieurs valeurs sont combinées lors de la classification ou à partir du contenu du fichier, les valeurs conflictuelles empêchent la reclassification. |
| Liste triée | Liste de valeurs fixes. Une seule valeur peut être affectée à une propriété à la fois. Lorsque plusieurs valeurs sont combinées lors de la classification ou à partir du contenu du fichier, la première valeur de la liste est utilisée. |
| Chaîne | Simple propriété de type chaîne. Lorsque plusieurs valeurs sont combinées lors de la classification ou à partir du contenu du fichier, les valeurs conflictuelles empêchent la reclassification. |
| Sélection multiple | Liste des valeurs qui peuvent être affectées à une propriété. Plusieurs valeurs peuvent être affectées à une propriété à la fois. Lorsque plusieurs valeurs sont combinées lors de la classification ou à partir du contenu du fichier, chaque valeur de la liste est utilisée. |
| Chaîne multiple | Liste de chaînes qui peuvent être affectées à une propriété. Plusieurs valeurs peuvent être affectées à une propriété à la fois. Lorsque plusieurs valeurs sont combinées lors de la classification ou à partir du contenu du fichier, chaque valeur de la liste est utilisée. |

<br />

La procédure suivante vous guide tout au long du processus de création d’une propriété de classification.

## <a name="to-create-a-classification-property"></a>Pour créer une propriété de classification

1.  Dans **Gestion de la classification**, cliquez sur le nœud **Propriétés de classification**.

2.  Cliquez avec le bouton droit sur **Propriétés de classification**, puis cliquez sur **Créer une propriété** (ou cliquez sur **Créer une propriété** dans le volet **Actions**). La boîte de dialogue **Définitions de propriété de la classification** s’affiche.

3.  Dans la zone de texte **Nom de la propriété**, tapez un nom pour la propriété.

4.  Dans la zone de texte **Description**, ajoutez une description facultative pour la propriété.

5.  Dans la liste déroulante **Type de propriété**, sélectionnez un type de propriété.

6.  Cliquez sur **OK**.

## <a name="see-also"></a>Articles associés

-   [Créer une règle de classification automatique](create-automatic-classification-rule.md)
-   [Gestion de la classification](classification-management.md)