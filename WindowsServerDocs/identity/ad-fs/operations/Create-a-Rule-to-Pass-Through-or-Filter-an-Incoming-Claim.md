---
ms.assetid: 6127963f-71b2-4d8f-8b53-7c525bf06521
title: Créer une règle pour passer ou filtrer une revendication entrante
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: be20996d1df3898b8ff23422759e810a4b333b3d
ms.sourcegitcommit: 0b5fd4dc4148b92480db04e4dc22e139dcff8582
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/24/2019
ms.locfileid: "66189536"
---
# <a name="create-a-rule-to-pass-through-or-filter-an-incoming-claim"></a>Créer une règle pour passer ou filtrer une revendication entrante

À l’aide de la passer ou filtrer un modèle de règle de revendication entrante dans Active Directory Federation Services \(AD FS\), vous pouvez passer toutes les revendications entrantes avec un type de revendication sélectionné. Vous pouvez également filtrer les valeurs des revendications entrantes avec un type de revendication sélectionné. Par exemple, vous pouvez utiliser ce modèle de règle pour créer une règle qui envoie toutes les revendications de groupe entrantes. Vous pouvez également utiliser cette règle pour envoyer uniquement nom d’utilisateur principal \(UPN\) les revendications qui se terminent par @fabrikam.  
  
Vous pouvez utiliser la procédure suivante pour créer une règle de revendication avec le composant logiciel enfichable Gestion AD FS\-dans.  
  
Pour effectuer cette procédure, vous devez au minimum être membre du groupe **Administrateurs**ou d'un groupe équivalent sur l'ordinateur local.  Examinez les informations relatives à l’utilisation des comptes et des appartenances au groupe appropriés dans la rubrique [Groupes locaux et de domaine par défaut](https://go.microsoft.com/fwlink/?LinkId=83477).   

## <a name="to-create-a-rule-to-pass-through-or-filter-an-incoming-claim-on-a-relying-party-trust-in-windows-server-2016"></a>Pour créer une règle pour passer ou filtrer une revendication entrante sur une confiance dans Windows Server 2016 

1.  Dans le Gestionnaire de serveur, cliquez sur **outils**, puis sélectionnez **gestion AD FS**.  
  
2.  Dans l’arborescence de la console, sous **AD FS**, cliquez sur **confiance**. 
![Créer la règle](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule9.PNG)  
  
3.  Droite\-cliquez sur l’approbation sélectionnée, puis cliquez sur **modifier la stratégie d’émission de revendication**.
![Créer la règle](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule10.PNG)   
  
4.  Dans le **modifier la stratégie d’émission de revendication** boîte de dialogue **règles de transformation d’émission** cliquez sur **ajouter une règle** pour démarrer l’Assistant règle. 
![Créer la règle](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule11.PNG)    

5.  Sur le **sélectionner le modèle de règle** page sous **modèle de règle de revendication**, sélectionnez **passer ou filtrer une revendication entrante** dans la liste, puis cliquez sur **suivant** .  
![Créer la règle](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule4.PNG)    

6.  Sur le **configurer la règle** page sous **nom de règle de revendication** tapez le nom complet de cette règle, **type de revendication entrante** sélectionnez un type de revendication dans la liste, puis sélectionnez une du options suivantes, selon les besoins de votre organisation :  
  
    -   **Passer toutes les valeurs de revendication**  
  
    -   **Transmettre uniquement la valeur de revendication spécifique**  
  
    -   **Transmettre uniquement les valeurs de revendication qui correspondent à une valeur de suffixe d’adresse de messagerie spécifique**  
  
    -   **Transmettre uniquement les valeurs de revendication qui commencent par une valeur spécifique**  
![Créer la règle](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule5.PNG)    

7.  Cliquez sur le **Terminer** bouton.  
  
8.  Dans le **modifier les règles de revendication** boîte de dialogue, cliquez sur **OK** pour enregistrer la règle.
  
## <a name="to-create-a-rule-to-pass-through-or-filter-an-incoming-claim-on-a-claims-provider-trust-in-windows-server-2016"></a>Pour créer une règle pour passer ou filtrer une revendication entrante sur une approbation de fournisseur de revendications dans Windows Server 2016 
  
1.  Dans le Gestionnaire de serveur, cliquez sur **outils**, puis sélectionnez **gestion AD FS**.  
  
2.  Dans l’arborescence de la console, sous **AD FS**, cliquez sur **approbations de fournisseur de revendications**. 
![Créer la règle](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule1.PNG)  
  
3.  Droite\-cliquez sur l’approbation sélectionnée, puis cliquez sur **modifier les règles de revendication**.
![Créer la règle](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule2.PNG)   
  
4.  Dans le **modifier les règles de revendication** boîte de dialogue **règles de transformation d’acceptation** cliquez sur **ajouter une règle** pour démarrer l’Assistant règle.
![Créer la règle](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule3.PNG)    

5.  Sur le **sélectionner le modèle de règle** page sous **modèle de règle de revendication**, sélectionnez **passer ou filtrer une revendication entrante** dans la liste, puis cliquez sur **suivant** .  
![Créer la règle](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule4.PNG)    

6.  Sur le **configurer la règle** page sous **nom de règle de revendication** tapez le nom complet de cette règle, **type de revendication entrante** sélectionnez un type de revendication dans la liste, puis sélectionnez une du options suivantes, selon les besoins de votre organisation :  
  
    -   **Passer toutes les valeurs de revendication**  
  
    -   **Transmettre uniquement la valeur de revendication spécifique**  
  
    -   **Transmettre uniquement les valeurs de revendication qui correspondent à une valeur de suffixe d’adresse de messagerie spécifique**  
  
    -   **Transmettre uniquement les valeurs de revendication qui commencent par une valeur spécifique**  
![Créer la règle](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule5.PNG)    

7.  Cliquez sur le **Terminer** bouton.  
  
8.  Dans le **modifier les règles de revendication** boîte de dialogue, cliquez sur **OK** pour enregistrer la règle.  

## <a name="to-create-a-rule-to-pass-through-or-filter-an-incoming-claim-in-windows-server-2012-r2"></a>Pour créer une règle pour passer ou filtrer une revendication entrante dans Windows Server 2012 R2

1.  Dans le Gestionnaire de serveur, cliquez sur **outils**, puis sélectionnez **gestion AD FS**.  
  
2.  Dans l’arborescence de la console, sous **FSAD AD FS\\relations d’approbation**, cliquez sur **approbations de fournisseur de revendications** ou **confiance**, puis cliquez sur un niveau de confiance spécifique dans la liste où vous souhaitez créer cette règle.  
  
3.  Droite\-cliquez sur l’approbation sélectionnée, puis cliquez sur **modifier les règles de revendication**.
![Créer la règle](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule6.PNG)   
  
4.  Dans le **modifier les règles de revendication** boîte de dialogue, sélectionnez une les onglets suivants, en fonction de l’approbation que vous modifiez et quelle règle vous voulez créer cette règle dans, puis cliquez sur **ajouter une règle** pour démarrer l’Assistant règle qui est associé à cet ensemble de règles :  
  
    -   **Règles de transformation d’acceptation**  
  
    -   **Règles de transformation d’émission**  
  
    -   **Règles d’autorisation d’émission**  
  
    -   **Règles d’autorisation de délégation**  
![Créer la règle](media/Create-a-Rule-to-Permit-All-Users/permitall5.PNG)    

5.  Sur le **sélectionner le modèle de règle** page sous **modèle de règle de revendication**, sélectionnez **passer ou filtrer une revendication entrante** dans la liste, puis cliquez sur **suivant** .  
![Créer la règle](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule7.PNG)    

6.  Sur le **configurer la règle** page sous **nom de règle de revendication** tapez le nom complet de cette règle, **type de revendication entrante** sélectionnez un type de revendication dans la liste, puis sélectionnez une du options suivantes, selon les besoins de votre organisation :  
  
    -   **Passer toutes les valeurs de revendication**  
  
    -   **Transmettre uniquement la valeur de revendication spécifique**  
  
    -   **Transmettre uniquement les valeurs de revendication qui correspondent à une valeur de suffixe d’adresse de messagerie spécifique**  
  
    -   **Transmettre uniquement les valeurs de revendication qui commencent par une valeur spécifique**  
![Créer la règle](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule8.PNG)    

7.  Cliquez sur le **Terminer** bouton.  
  
8.  Dans le **modifier les règles de revendication** boîte de dialogue, cliquez sur **OK** pour enregistrer la règle.  



  
## <a name="additional-references"></a>Références supplémentaires  
[Configurer les règles de revendication](Configure-Claim-Rules.md)  
  
[Quand utiliser un passthrough ou filtrer la règle de revendication](../../ad-fs/technical-reference/When-to-Use-a-Pass-Through-or-Filter-Claim-Rule.md)  
  
[Rôle des revendications](../../ad-fs/technical-reference/The-Role-of-Claims.md)  
  
[Rôle des règles de revendication](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md)  
  
