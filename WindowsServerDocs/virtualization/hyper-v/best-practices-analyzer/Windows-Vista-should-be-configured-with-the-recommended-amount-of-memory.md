---
title: Windows Vista doit être configuré avec la quantité de mémoire recommandée
description: Fournit des instructions pour résoudre le problème signalé par cette règle de Best Practices Analyzer.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 64f4e53b-4adb-4e1d-bc48-c24f5f9d222f
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 6ba96b713bc838ec1ebfc577df7cbbeeb39b1c22
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59826300"
---
# <a name="windows-vista-should-be-configured-with-the-recommended-amount-of-memory"></a>Windows Vista doit être configuré avec la quantité de mémoire recommandée

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
  
*Une machine virtuelle exécutant Windows Vista est configurée avec inférieure à la quantité de RAM, qui est de 1 Go recommandée.*  
  
## <a name="impact"></a>Impact  
  
*Le système d’exploitation invité et les applications peuvent ne pas fonctionner correctement. Il ne peut pas y avoir suffisamment de mémoire pour exécuter plusieurs applications à la fois. Cela affecte les ordinateurs virtuels suivants :*  
  
\<liste des noms de machine virtuelle >  
  
## <a name="resolution"></a>Résolution  
  
*Utilisez le Gestionnaire Hyper-V pour augmenter la mémoire allouée à cette machine virtuelle au moins 1 Go.*  
  
### <a name="to-increase-the-memory-allocated-to-a-virtual-machine"></a>Pour augmenter la mémoire allouée à une machine virtuelle  
  
1.  Ouvrez le Gestionnaire Hyper-V. Cliquez sur **Démarrer**, pointez sur **Outils d'administration**, puis cliquez sur **Gestionnaire Hyper-V**.  
  
2.  Dans le volet de résultats, sous **Machines virtuelles**, sélectionnez la machine virtuelle que vous souhaitez configurer. L’état de la machine virtuelle doit être répertorié en tant que **hors**. Si elle n’est pas le cas, avec le bouton droit de la machine virtuelle, puis cliquez sur **arrêter**.  
  
3.  Dans le volet **Action**, sous le nom de l'ordinateur virtuel, cliquez sur **Paramètres**.  
  
4.  Dans le volet de navigation, cliquez sur **mémoire**.  
  
5.  Sur le **mémoire** , définissez le **RAM de démarrage** au moins 1 Go, puis cliquez sur **OK**.  
  
### <a name="increase-the-memory-using-windows-powershell"></a>Augmentez la mémoire à l’aide de Windows PowerShell  
  
1.  Ouvrez Windows PowerShell. (À partir du bureau, cliquez sur **Démarrer** et commencez à taper **Windows PowerShell**.)  
  
2.  Avec le bouton droit **Windows PowerShell** et cliquez sur **exécuter en tant qu’administrateur**.  
  
3.  Exécutez cette commande après avoir remplacé \<MyVM > par le nom de votre machine virtuelle :  
  
```  
Set-VMMemory <MyVM> -StartupBytes 1GB  
```  
  
## <a name="see-also"></a>Voir aussi  
[Set-VMMemory](https://technet.microsoft.com/library/hh848572.aspx)  
  


