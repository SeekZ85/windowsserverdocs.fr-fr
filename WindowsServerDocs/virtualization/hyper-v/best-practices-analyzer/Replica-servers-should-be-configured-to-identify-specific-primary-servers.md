---
title: Serveurs de réplication doivent être configurés afin d’identifier les serveurs principaux spécifiques autorisés à envoyer le trafic de réplication
description: Fournit des instructions pour résoudre le problème signalé par cette règle de Best Practices Analyzer.
ms.prod: windows-server-threshold
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 0aeb1f4b-2e75-430b-9557-fe64738c4992
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 47b215d4c84e68d93ae1189ddd370358e2781eff
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59822240"
---
# <a name="replica-servers-should-be-configured-to-identify-specific-primary-servers-authorized-to-send-replication-traffic"></a>Serveurs de réplication doivent être configurés afin d’identifier les serveurs principaux spécifiques autorisés à envoyer le trafic de réplication

>S'applique à : Windows Server 2016

Pour plus d’informations sur les bonnes pratiques et les analyses, consultez [Exécuter des analyses Best Practices Analyzer et gérer les résultats des analyses](https://go.microsoft.com/fwlink/p/?LinkID=223177).  
  
|Propriété|Détails|  
|-|-|  
|**Système d'exploitation**|Windows Server 2016|  
|**Produit/fonctionnalité**|Hyper-V|  
|**Niveau de gravité**|Warning|  
|**Catégorie**|Configuration|  
  
Dans les sections suivantes, italique indique le texte de l’interface utilisateur qui apparaît dans l’outil Best Practices Analyzer pour ce problème.  
  
## <a name="issue"></a>Problème  
*Tel que configuré, ce serveur réplica accepte le trafic de réplication à partir de tous les serveurs principaux et les stocke dans un emplacement unique.*  
  
### <a name="impact"></a>Impact  
*Toute la réplication à partir de tous les serveurs principaux est stockées dans un seul emplacement, ce qui peut présenter des problèmes de sécurité ou de confidentialité.*  
  
## <a name="resolution"></a>Résolution  
*Utilisez le Gestionnaire Hyper-V pour créer des entrées d’autorisation pour les serveurs principaux spécifiques et de spécifier des emplacements de stockage distincts pour chacun d’eux. Vous pouvez utiliser des caractères génériques pour regrouper des serveurs principaux en jeux pour chaque entrée d’autorisation.*  
  
#### <a name="create-authorization-entries-using-hyper-v-manager"></a>Créer des entrées d’autorisation à l’aide du Gestionnaire Hyper-V  
  
1.  Ouvrez le Gestionnaire Hyper-V. (Dans le Gestionnaire de serveur, cliquez sur **outils** > **Gestionnaire Hyper-V**.)  
  
2.  Dans la liste des ordinateurs hôtes, cliquez sur celui de votre choix, puis cliquez sur **paramètres Hyper-V**.  
  
3.  Dans le volet de navigation, cliquez sur **Configuration de la réplication**.  
  
4.  Sous **autorisation et stockage**, cliquez sur **autoriser la réplication des serveurs spécifiés**.  
  
5.  Sous la liste des serveurs, cliquez sur **ajouter**.  
  
6.  Sous **ajouter l’entrée d’autorisation**:  
  
    -   Tapez le nom qualifié complet du premier serveur.  
  
    -   Spécifiez un emplacement dédié pour stocker uniquement les fichiers de ce serveur.  
  
7.  Cliquez sur **OK**.  
  
8.  Répétez pour chaque serveur principal.  
  
9. Cliquez sur **OK** à nouveau pour terminer et fermer la fenêtre.  
  
### <a name="create-authorization-entries-using-windows-powershell"></a>Créer des entrées d’autorisation à l’aide de Windows PowerShell  
  
1.  Ouvrez Windows PowerShell. (À partir du bureau, cliquez sur Démarrer et commencez à taper **Windows PowerShell**.)  
  
2.  Avec le bouton droit **Windows PowerShell** et cliquez sur **exécuter en tant qu’administrateur**.  
  
3.  Exécutez une commande semblable à ce qui suit, en remplaçant :  
  
    -   Nom du serveur principal de server01.domain01.contoso.com avec le nom de domaine complet de votre serveur.  
  
    -   L’emplacement du D:\ReplicaVMStorage avec votre emplacement.  
  
    -   Le groupe de confiance nommé par défaut avec le nom de votre groupe, si vous avez créé un. Si ce n’est pas le cas, utilisez la valeur par défaut.  
  
```  
New-VMReplicationAuthorizationEntry server01.domain01.contoso.com D:\ReplicaVMStorage DEFAULT  
```  
  
## <a name="see-also"></a>Voir aussi  
[New-VMReplicationAuthorizationEntry](https://technet.microsoft.com/library/hh848606.aspx)  
  


