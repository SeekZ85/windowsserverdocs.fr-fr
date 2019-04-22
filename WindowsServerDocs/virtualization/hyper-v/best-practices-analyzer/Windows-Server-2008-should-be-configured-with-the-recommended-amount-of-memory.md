---
title: Windows Server 2008 doit être configurée avec la quantité de mémoire recommandée
description: Fournit des instructions pour résoudre le problème signalé par cette règle de Best Practices Analyzer.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: a98a8594-603b-487a-8739-78887c568e57
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 77410eb545c8c8ce6b02d083c7c875b569c63937
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59818790"
---
# <a name="windows-server-2008-should-be-configured-with-the-recommended-amount-of-memory"></a>Windows Server 2008 doit être configurée avec la quantité de mémoire recommandée

>S'applique à : Windows Server 2016

Pour plus d'informations sur les meilleures pratiques et les analyses, consultez [Best Practices Analyzer](https://go.microsoft.com/fwlink/?LinkId=122786).  
  
|Propriété|Détails|  
|-|-|  
|**Système d'exploitation**|Windows Server 2016|  
|**Produit/fonctionnalité**|Hyper-V|  
|**Niveau de gravité**|Warning|  
|**Catégorie**|Configuration|  
  
Dans les sections suivantes, italique indique le texte de l’interface utilisateur qui apparaît dans l’outil Best Practices Analyzer pour ce problème.  
  
## <a name="issue"></a>Problème  
  
*Une machine virtuelle exécutant Windows Server 2008 est configurée avec inférieure à la quantité de RAM, qui est de 2 Go recommandée.*  
  
## <a name="impact"></a>Impact  
  
*Le système d’exploitation invité et les applications peuvent ne pas fonctionner correctement. Il ne peut pas y avoir suffisamment de mémoire pour exécuter plusieurs applications à la fois. Cela affecte les ordinateurs virtuels suivants :*  
   
\<liste des noms de machine virtuelle >  
  
## <a name="resolution"></a>Résolution  
  
*Utilisez le Gestionnaire Hyper-V pour augmenter la mémoire allouée à cette machine virtuelle au moins 2 Go.*  
  
### <a name="increase-the-memory-using-hyper-v-manager"></a>Augmentez la mémoire à l’aide du Gestionnaire Hyper-V  
  
1.  Ouvrez le Gestionnaire Hyper-V. Cliquez sur **Démarrer**, pointez sur **Outils d'administration**, puis cliquez sur **Gestionnaire Hyper-V**.  
  
2.  Dans le volet de résultats, sous **Machines virtuelles**, sélectionnez la machine virtuelle que vous souhaitez configurer. L’état de la machine virtuelle doit être répertorié en tant que **hors**. Si elle n’est pas le cas, avec le bouton droit de la machine virtuelle, puis cliquez sur **arrêter**.  
  
3.  Dans le volet **Action**, sous le nom de l'ordinateur virtuel, cliquez sur **Paramètres**.  
  
4.  Dans le volet de navigation, cliquez sur **mémoire**.  
  
5.  Sur le **mémoire** , définissez le **RAM de démarrage** au moins 2 Go, puis cliquez sur **OK**.  
  
### <a name="increase-memory-using-windows-powershell"></a>Augmentez la mémoire à l’aide de Windows PowerShell  
  
1.  Ouvrez Windows PowerShell. (À partir du bureau, cliquez sur **Démarrer** et commencez à taper **Windows PowerShell**.)  
  
2.  Avec le bouton droit **Windows PowerShell** et cliquez sur **exécuter en tant qu’administrateur**.  
  
3.  Exécutez une commande semblable à ce qui suit, en remplaçant \<MyVM > par le nom de votre machine virtuelle et la mémoire des valeurs avec au moins les valeurs indiquées ci-dessous.  
  
```  
Set-VMMemory <MyVM> -StartupBytes 2GB  
```  
  
## <a name="see-also"></a>Voir aussi  
[Set-VMMemory](https://technet.microsoft.com/library/hh848572.aspx)  
  


