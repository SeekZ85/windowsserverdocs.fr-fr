---
ms.assetid: 0039fbbb-b981-4526-a550-f3456ff27635
title: "Créer une règle pour transformer une revendication entrante"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 3745a0ab9d313223c611e58864dd6b4d747f0624
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/03/2017
---
# <a name="create-a-rule-to-send-an-ad-fs-1x-compatible-claim"></a>Créer une règle pour envoyer une revendication Compatible de ADFS 1.x

>S’applique à: Windows Server2016, Windows Server2012R2


Dans les situations dans lesquelles vous utilisez ActiveDirectory Federation Services \(ADFS\) pour émettre des revendications qui seront reçues par les serveurs de fédération ADFS 1.0 \ (Windows Server2003R2\) ou ADFS 1.1 \ (Windows Server2008 ou Windows Server2008R2\), vous devez procédez comme suit:  
  
-   Créer une règle qui envoie un type de revendication d’identificateur de nom avec un format de nom UPN, courrier électronique ou nom commun.  
  
-   Toutes les autres revendications sont envoyées posséder un des types de revendications suivants:  
  
    -   ADFS 1. *x* adresse de messagerie  
  
    -   ADFS 1. *x* UPN  
  
    -   Nom commun  
  
    -   Groupe  
  
    -   Un autre type de revendication qui commence par https://schemas.xmlsoap.org/claims/, tels que https://schemas.xmlsoap.org/claims/EmployeeID  
  
Selon les besoins de votre organisation, utilisez une des procédures suivantes pour créer un ADFS 1. *x* revendication NameID compatible avec:  
  
-   Créez cette règle de revendication d’à l’aide de nom ID problème an ADFS 1.x le **passer ou filtrer un modèle de règle de revendication entrante**  
  
-   Créez cette règle de revendication d’à l’aide de nom ID problème an ADFS 1.x le **transformer un modèle de règle de revendication entrante**. Vous pouvez utiliser ce modèle de règle dans les situations dans lesquelles vous souhaitez modifier le type de revendication existant à un nouveau type de revendication qui fonctionnera avec ADFS 1. *x* revendications.  
  
> [!NOTE]  
> Pour cette règle de fonctionner comme prévu, assurez-vous que la partie de confiance ou une approbation de fournisseur de revendications dans lequel vous créez cette règle a été configurée pour utiliser le **profil ADFS 1.0 et 1.1**. 




## <a name="to-create-a-rule-to-issue-an-ad-fs-1x-name-id-claim-using-the-pass-through-or-filter-an-incoming-claim-rule-template-on-a-relying-party-trust-in-windows-server-2016"></a>Pour créer une règle pour émettre un ADFS 1. *x* identificateur de nom à l’aide de passer par le biais de revendication ou les filtrer un modèle de règle de revendication entrante sur une confiance dans Windows Server2016 

1.  Dans le Gestionnaire de serveur, cliquez sur **outils**, puis sélectionnez **gestion ADFS**.  
  
2.  Dans l’arborescence de la console, sous **ADFS**, cliquez sur **approbations de partie de confiance **. 
![Créer la règle](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule9.PNG)  
  
3.  L’approbation sélectionnée clic droit, puis cliquez sur **modifier la stratégie d’émission de revendication **.
![Créer la règle](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule10.PNG)   
  
4.  Dans le **modifier la stratégie d’émission de revendication** la boîte de dialogue sous **règles de transformation d’émission** cliquez sur **ajouter une règle** pour démarrer l’Assistant règle. 
![Créer la règle](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule11.PNG)    

5.  Sur le **sélectionner le modèle de règle** sous **modèle de règle de revendication**, sélectionnez **passer ou filtrer une revendication entrante** dans la liste, puis cliquez sur **suivant**.  
![Créer la règle](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule4.PNG)    

6.  Sur le **configurer la règle**, tapez un nom de règle de revendication.  
  
7.  Dans **type de revendication entrante**, sélectionnez **identificateur de nom** dans la liste.  
  
8.  Dans **format du nom de code entrant**, sélectionnez une des suivante ADFS 1. *x*\-compatible revendication formats dans la liste:  
  
    -   **UPN**  
  
    -   **Messagerie E\**  
  
    -   **Nom commun**  
  
9. Sélectionnez une des options suivantes, selon les besoins de votre organisation:  
  
    -   **Passer toutes les valeurs de revendication**  
  
    -   **Transmettre uniquement la valeur de revendication spécifique**  
  
    -   **Transmettre uniquement les valeurs de revendication qui correspondent à une valeur de suffixe de messagerie spécifique**  
  
    -   **Transmettre uniquement les valeurs de revendication qui commencent par une valeur spécifique**  
![Créer la règle](media/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim/adfs3.PNG)   

10. Cliquez sur **Terminer**, puis cliquez sur **OK** pour enregistrer la règle.  

  
## <a name="to-create-a-rule-to-issue-an-ad-fs-1x-name-id-claim-using-the-pass-through-or-filter-an-incoming-claim-rule-template-on-a-claims-provider-trust-in-windows-server-2016"></a>Pour créer une règle pour émettre un ADFS 1. *x* identificateur de nom à l’aide de passer par le biais de revendication ou les filtrer un modèle de règle de revendication entrante sur une approbation de fournisseur de revendications dans Windows Server2016 
  
1.  Dans le Gestionnaire de serveur, cliquez sur **outils**, puis sélectionnez **gestion ADFS**.  
  
2.  Dans l’arborescence de la console, sous **ADFS**, cliquez sur **approbations de fournisseur de revendications **. 
![Créer la règle](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule1.PNG)  
  
3.  L’approbation sélectionnée clic droit, puis cliquez sur **modifier les règles de revendication **.
![Créer la règle](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule2.PNG)   
  
4.  Dans le **modifier les règles de revendication** la boîte de dialogue sous **règles de transformation d’acceptation** cliquez sur **ajouter une règle** pour démarrer l’Assistant règle.
![Créer la règle](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule3.PNG)    

5.  Sur le **sélectionner le modèle de règle** sous **modèle de règle de revendication**, sélectionnez **passer ou filtrer une revendication entrante** dans la liste, puis cliquez sur **suivant**.  
![Créer la règle](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule4.PNG)    

6.  Sur le **configurer la règle**, tapez un nom de règle de revendication.  
  
7.  Dans **type de revendication entrante**, sélectionnez **identificateur de nom** dans la liste.  
  
8.  Dans **format du nom de code entrant**, sélectionnez une des suivante ADFS 1. *x*\-compatible revendication formats dans la liste:  
  
    -   **UPN**  
  
    -   **Messagerie E\**  
  
    -   **Nom commun**  
  
9. Sélectionnez une des options suivantes, selon les besoins de votre organisation:  
  
    -   **Passer toutes les valeurs de revendication**  
  
    -   **Transmettre uniquement la valeur de revendication spécifique**  
  
    -   **Transmettre uniquement les valeurs de revendication qui correspondent à une valeur de suffixe de messagerie spécifique**  
  
    -   **Transmettre uniquement les valeurs de revendication qui commencent par une valeur spécifique**  
![Créer la règle](media/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim/adfs3.PNG)   

10. Cliquez sur **Terminer**, puis cliquez sur **OK** pour enregistrer la règle.  

  

## <a name="to-create-a-rule-to-transform-an-incoming-claim-on-a-relying-party-trust-in-windows-server-2016"></a>Pour créer une règle pour transformer une revendication entrante sur une confiance dans Windows Server2016 

1.  Dans le Gestionnaire de serveur, cliquez sur **outils**, puis sélectionnez **gestion ADFS**.  
  
2.  Dans l’arborescence de la console, sous **ADFS**, cliquez sur **approbations de partie de confiance **. 
![Créer la règle](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule9.PNG)  
  
3.  L’approbation sélectionnée clic droit, puis cliquez sur **modifier la stratégie d’émission de revendication **.
![Créer la règle](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule10.PNG)   
  
4.  Dans le **modifier la stratégie d’émission de revendication** la boîte de dialogue sous **règles de transformation d’émission** cliquez sur **ajouter une règle** pour démarrer l’Assistant règle. 
![Créer la règle](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule11.PNG)    

5.  Sur le **sélectionner le modèle de règle** sous **modèle de règle de revendication**, sélectionnez **transformer une revendication entrante** dans la liste, puis cliquez sur **suivant **.  
![Créer la règle](media/Create-a-Rule-to-Transform-an-Incoming-Claim/transform3.PNG)      

6.  Sur le **configurer la règle**, tapez un nom de règle de revendication.  
  
7.  Dans **type de revendication entrante**, sélectionnez le type de revendication entrante que vous souhaitez transformer dans la liste.  
  
8.  Dans **type de revendication sortante**, sélectionnez **identificateur de nom** dans la liste.  
  
9. Dans **format ID de nom sortant**, sélectionnez une des suivante ADFS 1. *x*\-compatible revendication formats dans la liste:  
  
    -   **UPN**  
  
    -   **Messagerie E\**  
  
    -   **Nom commun**  
  
10. Sélectionnez une des options suivantes, selon les besoins de votre organisation:  
  
    -   **Passer toutes les valeurs de revendication**  
  
    -   **Remplacer une valeur de revendication entrante avec une valeur de revendication sortante**  
  
    -   **Remplacer les revendications de suffixe e\ de messagerie entrantes par un nouveau suffixe de messagerie e\**  
![Créer la règle](media/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim/adfs4.PNG)    

11. Cliquez sur **Terminer**, puis cliquez sur **OK** pour enregistrer la règle.  

  


## <a name="to-create-a-rule-to-transform-an-incoming-claim-on-a-claims-provider-trust-in-windows-server-2016"></a>Pour créer une règle pour transformer une revendication entrante sur une approbation de fournisseur de revendications dans Windows Server2016 
  
1.  Dans le Gestionnaire de serveur, cliquez sur **outils**, puis sélectionnez **gestion ADFS**.  
  
2.  Dans l’arborescence de la console, sous **ADFS**, cliquez sur **approbations de fournisseur de revendications **. 
![Créer la règle](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule1.PNG)  
  
3.  L’approbation sélectionnée clic droit, puis cliquez sur **modifier les règles de revendication **.
![Créer la règle](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule2.PNG)   
  
4.  Dans le **modifier les règles de revendication** la boîte de dialogue sous **règles de transformation d’acceptation** cliquez sur **ajouter une règle** pour démarrer l’Assistant règle.
![Créer la règle](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule3.PNG)    

5.  Sur le **sélectionner le modèle de règle** sous **modèle de règle de revendication**, sélectionnez **transformer une revendication entrante** dans la liste, puis cliquez sur **suivant **.  
![Créer la règle](media/Create-a-Rule-to-Transform-an-Incoming-Claim/transform3.PNG)      

6.  Sur le **configurer la règle**, tapez un nom de règle de revendication.  
  
7.  Dans **type de revendication entrante**, sélectionnez le type de revendication entrante que vous souhaitez transformer dans la liste.  
  
8.  Dans **type de revendication sortante**, sélectionnez **identificateur de nom** dans la liste.  
  
9. Dans **format ID de nom sortant**, sélectionnez une des suivante ADFS 1. *x*\-compatible revendication formats dans la liste:  
  
    -   **UPN**  
  
    -   **Messagerie E\**  
  
    -   **Nom commun**  
  
10. Sélectionnez une des options suivantes, selon les besoins de votre organisation:  
  
    -   **Passer toutes les valeurs de revendication**  
  
    -   **Remplacer une valeur de revendication entrante avec une valeur de revendication sortante**  
  
    -   **Remplacer les revendications de suffixe e\ de messagerie entrantes par un nouveau suffixe de messagerie e\**  
![Créer la règle](media/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim/adfs4.PNG)    

11. Cliquez sur **Terminer**, puis cliquez sur **OK** pour enregistrer la règle.  













  
## <a name="to-create-a-rule-to-issue-an-ad-fs-1x-name-id-claim-using-the-pass-through-or-filter-an-incoming-claim-rule-template-on-windows-server-2012-r2"></a>Pour créer une règle pour émettre un ADFS 1. *x* identificateur de nom à l’aide de passer par le biais de revendication ou les filtrer un modèle de règle de revendication entrante sur Windows Server2012R2
  
1.  Dans le Gestionnaire de serveur, cliquez sur **outils**, puis cliquez sur **gestion ADFS **.  
  
2.  Dans l’arborescence de la console, sous **ADFS\\Trust relations**, cliquez sur **approbations de fournisseur de revendications** ou **approbations de partie de confiance**, puis cliquez sur une approbation spécifique dans la liste dans laquelle vous souhaitez créer cette règle.  
  
3.  L’approbation sélectionnée clic droit, puis cliquez sur **modifier les règles de revendication **.  
![Créer la règle](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule6.PNG) 
  
4.  Dans le **modifier les règles de revendication** boîte de dialogue, sélectionnez une les onglets suivants, en fonction de l’approbation que vous modifiez et définie de règle qui vous souhaitez créer cette règle, puis cliquez sur **ajouter une règle** pour démarrer l’Assistant règle qui est associé à cet ensemble de règles:  
  
    -   **Règles de transformation d’acceptation**  
  
    -   **Règles de transformation d’émission**  
  
    -   **Règles d’autorisation d’émission**  
  
    -   **Règles d’autorisation de délégation**  
![Créer la règle](media/Create-a-Rule-to-Permit-All-Users/permitall5.PNG)    

5.  Sur le **sélectionner le modèle de règle** sous **modèle de règle de revendication**, sélectionnez **passer ou filtrer une revendication entrante** dans la liste, puis cliquez sur **suivant**.  
![Créer la règle](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule7.PNG)  
  
6.  Sur le **configurer la règle**, tapez un nom de règle de revendication.  
  
7.  Dans **type de revendication entrante**, sélectionnez **identificateur de nom** dans la liste.  
  
8.  Dans **format du nom de code entrant**, sélectionnez une des suivante ADFS 1. *x*\-compatible revendication formats dans la liste:  
  
    -   **UPN**  
  
    -   **Messagerie E\**  
  
    -   **Nom commun**  
  
9. Sélectionnez une des options suivantes, selon les besoins de votre organisation:  
  
    -   **Passer toutes les valeurs de revendication**  
  
    -   **Transmettre uniquement la valeur de revendication spécifique**  
  
    -   **Transmettre uniquement les valeurs de revendication qui correspondent à une valeur de suffixe de messagerie spécifique**  
  
    -   **Transmettre uniquement les valeurs de revendication qui commencent par une valeur spécifique**  
![Créer la règle](media/\Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim/adfs1.PNG)   

10. Cliquez sur **Terminer**, puis cliquez sur **OK** pour enregistrer la règle.  

  
## <a name="to-create-a-rule-to-issue-an-ad-fs-1x-name-id-claim-using-the-transform-an-incoming-claim-rule-template-in-windows-server-2012-r2"></a>Pour créer une règle pour émettre un ADFS 1. *x* revendication d’identificateur de nom à l’aide de la transformation un modèle de règle de revendication entrante dans Windows Server2012R2  
  
1.  Dans le Gestionnaire de serveur, cliquez sur **outils**, puis cliquez sur **gestion ADFS **.  
  
2.  Dans l’arborescence de la console, sous **ADFS\\Trust relations**, cliquez sur **approbations de fournisseur de revendications** ou **approbations de partie de confiance**, puis cliquez sur une approbation spécifique dans la liste dans laquelle vous souhaitez créer cette règle.  
  
3.  L’approbation sélectionnée clic droit, puis cliquez sur **modifier les règles de revendication **.  
![Créer la règle](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule6.PNG) 
  
4.  Dans le **modifier les règles de revendication** boîte de dialogue, sélectionnez une les onglets suivants, qui dépend de l’approbation que vous modifiez et dans la règle définissez vous souhaitent créer cette règle, puis cliquez sur **ajouter une règle** pour démarrer l’Assistant règle qui est associé à cet ensemble de règles:  
  
    -   **Règles de transformation d’acceptation**  
  
    -   **Règles de transformation d’émission**  
  
    -   **Règles d’autorisation d’émission**  
  
    -   **Règles d’autorisation de délégation**  
![Créer la règle](media/Create-a-Rule-to-Permit-All-Users/permitall5.PNG)
  
5.  Sur le **sélectionner le modèle de règle** sous **modèle de règle de revendication**, sélectionnez **transformer une revendication entrante** dans la liste, puis cliquez sur **suivant **.  
![Créer la règle](media/Create-a-Rule-to-Transform-an-Incoming-Claim/transform1.PNG)   
  
6.  Sur le **configurer la règle**, tapez un nom de règle de revendication.  
  
7.  Dans **type de revendication entrante**, sélectionnez le type de revendication entrante que vous souhaitez transformer dans la liste.  
  
8.  Dans **type de revendication sortante**, sélectionnez **identificateur de nom** dans la liste.  
  
9. Dans **format ID de nom sortant**, sélectionnez une des suivante ADFS 1. *x*\-compatible revendication formats dans la liste:  
  
    -   **UPN**  
  
    -   **Messagerie E\**  
  
    -   **Nom commun**  
  
10. Sélectionnez une des options suivantes, selon les besoins de votre organisation:  
  
    -   **Passer toutes les valeurs de revendication**  
  
    -   **Remplacer une valeur de revendication entrante avec une valeur de revendication sortante**  
  
    -   **Remplacer les revendications de suffixe e\ de messagerie entrantes par un nouveau suffixe de messagerie e\**  
![Créer la règle](media/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim/adfs2.PNG)    

11. Cliquez sur **Terminer**, puis cliquez sur **OK** pour enregistrer la règle.  

## <a name="additional-references"></a>Références supplémentaires 
[Configurer des règles de revendication](Configure-Claim-Rules.md)  
 
[Liste de vérification: Création de règles de revendication pour une partie de confiance](https://technet.microsoft.com/library/ee913578.aspx)  

[Liste de vérification: Approuvent créer des règles de revendication pour un fournisseur de revendications](https://technet.microsoft.com/library/ee913564.aspx)  
  
[Quand utiliser une règle de revendication d’autorisation](../../ad-fs/technical-reference/When-to-Use-an-Authorization-Claim-Rule.md)  

[Le rôle de revendications](../../ad-fs/technical-reference/The-Role-of-Claims.md)  
  
[Le rôle de règles de revendication](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md) 
