---
title: Configurez au moins la quantité de mémoire requise pour un ordinateur virtuel exécutant Windows Server 2012 et activé pour Mémoire dynamique
description: Version en ligne du texte de cette règle de Best Practices Analyzer.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 46f9a5dc-355b-415b-863d-fb740609d6b6
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 1398252f2f5e842f170ad1f932bb047720d82ab2
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71365004"
---
# <a name="configure-at-least-the-required-amount-of-memory-for-a-virtual-machine-running-windows-server-2012-and-enabled-for-dynamic-memory"></a>Configurez au moins la quantité de mémoire requise pour un ordinateur virtuel exécutant Windows Server 2012 et activé pour Mémoire dynamique

>S’applique à Windows Server 2016

Pour plus d’informations sur les bonnes pratiques et les analyses, consultez [Exécuter des analyses Best Practices Analyzer et gérer les résultats des analyses](https://go.microsoft.com/fwlink/p/?LinkID=223177).  
  
|Propriété|Détails|  
|-|-|  
|**Système d'exploitation**|Windows Server 2016|  
|**Produit/fonctionnalité**|Hyper-V|  
|**Va**|Erreur|  
|**Catégorie**|Configuration|  
  
Dans les sections suivantes, l’italique indique le texte de l’interface utilisateur qui s’affiche dans l’outil Best Practices Analyzer pour ce problème.  
  
## <a name="issue"></a>**Problème**  
*Une ou plusieurs machines virtuelles sont configurées pour utiliser Mémoire dynamique avec une quantité de mémoire inférieure à celle requise pour Windows Server 2012.*  
  
## <a name="impact"></a>**Impact**  
*Le système d’exploitation invité sur les ordinateurs virtuels suivants peut ne pas s’exécuter ou ne pas fonctionner de manière fiable :*  
  
\<liste des machines virtuelles >  
  
## <a name="resolution"></a>**Résolution**  
*Utilisez le Gestionnaire Hyper-V pour augmenter la mémoire minimale à au moins 256 Mo, et la mémoire de démarrage et la mémoire maximale à au moins 512 Mo pour cette machine virtuelle.*  
  
### <a name="increase-memory-using-hyper-v-manager"></a>Augmenter la mémoire à l’aide du Gestionnaire Hyper-V  
  
1.  Ouvrez le Gestionnaire Hyper-V. (À partir de Gestionnaire de serveur, cliquez sur **outils** > **Gestionnaire Hyper-V**.)  
  
2.  Dans la liste des ordinateurs virtuels, cliquez avec le bouton droit sur celui que vous souhaitez, puis cliquez sur **paramètres**.  
  
3.  Dans le volet de navigation, cliquez sur **mémoire**.  
  
4.  Remplacez la **RAM** par au moins 512 Mo.  
  
5.  Sous **mémoire dynamique**, définissez la **RAM minimale** sur au moins 256 Mo et la **RAM maximale** sur 512 Mo.  
  
6.  Cliquez sur **OK**.  
  
### <a name="increase-memory-using-windows-powershell"></a>Augmenter la mémoire à l’aide de Windows PowerShell  
  
1.  Ouvrez Windows PowerShell. (À partir du bureau, cliquez sur **Démarrer** et commencez à taper **Windows PowerShell**.)  
  
2.  Cliquez avec le bouton droit sur **Windows PowerShell** , puis cliquez sur **exécuter en tant qu’administrateur**.  
  
3.  Exécutez une commande semblable à la suivante, en remplaçant MyVM par le nom de votre machine virtuelle et les valeurs de mémoire par au moins les valeurs indiquées ci-dessous.  
  
```  
Get-VM MyVM | Set-VMMemory -DynamicMemoryEnabled $True -MaximumBytes 512MB -MinimumBytes 256MB -StartupBytes 512MB  
```  
  


