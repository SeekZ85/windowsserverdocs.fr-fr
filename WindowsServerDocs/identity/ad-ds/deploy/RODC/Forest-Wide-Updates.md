---
ms.assetid: 3647b7e3-54a4-46c6-ab68-82fcf3bfacda
title: Mises à jour à l’échelle de la forêt Active Directory
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 10/29/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 90b7bb4c8012e7e1a29ea2c1b542d78e75e7708f
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59816830"
---
# <a name="forest-wide-updates"></a>Mises à jour de la forêt

>S'applique à : Windows Server

Vous pouvez consulter l’ensemble de modifications pour aider à comprendre et à préparer les mises à jour de schéma sont effectuées par adprep /forestprep dans Windows Server 2019 suivant.

À compter de Windows Server 2012, les commandes Adprep s’exécutent automatiquement en fonction des besoins lors de l’installation d’AD DS. Ils peuvent également être exécutés séparément avant l’installation d’AD DS. Pour plus d’informations, voir [Exécution d’Adprep.exe](https://technet.microsoft.com/library/dd464018(v=ws.10).aspx).

Pour plus d’informations sur la façon d’interpréter les chaînes d’entrée du contrôle accès, consultez [chaînes d’ACE](https://msdn.microsoft.com/library/aa374928(VS.85).aspx). Pour plus d’informations sur la façon d’interpréter les chaînes d’ID (SID) de sécurité, consultez [les chaînes de SID](https://msdn.microsoft.com/library/aa379602(VS.85).aspx).

## <a name="windows-server-2016-forest-wide-updates"></a>Windows Server 2016 : Mises à jour de la forêt

Après les opérations sont effectuées par le **forestprep** commande dans Windows Server 2016 (opérations 136-142) sont terminées, le **révision** attribut pour CN = ActiveDirectoryUpdate, CN = ForestUpdates, CN = Configuration, DC = domaine_racine_forêt objet est défini sur **16**.

|Nombre d’opérations et GUID|Description|Attributs|Autorisations|
|-----------------------------|---------------|--------------|---------------|
|**Opération 136**: {328092FB-16E7-4453-9AB8-7592DB56E9C4}|Octroi le « CN = envoi-comme suit : CN = doté de droits étendus » aux comptes de service administré de groupe.|N/A|N/A|
|**Opération 137**: {3A1C887F-DF0A-489F-B3F2-2D0409095F6E}|Octroi le « CN = réception-comme suit : CN = doté de droits étendus » aux comptes de service administré de groupe.|N/A|N/A|
|**Opération 138**: {232E831F-F988-4444-8E3E-8A352E2FD411}|Octroi le « CN = informations personnelles, CN = doté de droits étendus » aux comptes de service administré de groupe.|N/A|N/A|
|**Opération 139**: {DDDDCF0C-BEC9-4A5A-AE86-3CFE6CC6E110}|Octroi le « CN = informations publiques, CN = doté de droits étendus » aux comptes de service administré de groupe.|N/A|N/A|
|**Opération 140**: {A0A45AAC-5550-42DF-BB6A-3CC5C46B52F2}|Octroi le « CN = validé-SPN, CN = doté de droits étendus » aux comptes de service administré de groupe.|N/A|N/A|
|**Opération 141**: {3E7645F3-3EA5-4567-B35A-87630449C70C}|Octroi le « CN = Allowed-à-Authenticate, CN = doté de droits étendus » aux comptes de service administré de groupe.|N/A|N/A|
|**Opération 142**: {E634067B-E2C4-4D79-B6E8-73C619324D5E}|Octroi le « CN = MS-TS-GatewayAccess, CN = doté de droits étendus » aux comptes de service administré de groupe.|N/A|N/A|

## <a name="windows-server-2012-r2-forest-wide-updates"></a>Windows Server 2012 R2 : Mises à jour de la forêt

Après les opérations sont effectuées par le **forestprep** commande dans Windows Server 2012 R2 (opérations 131-135) sont terminées, le **révision** attribut pour CN = ActiveDirectoryUpdate, CN = ForestUpdates, CN = Configuration, DC = domaine_racine_forêt objet est défini sur **15**.

|Nombre d’opérations et GUID|Description|Attributs|Autorisations|
|-----------------------------|---------------|--------------|---------------|
|**Opération 131**: {b83818c1-01a6-4f39-91b7-a3bb581c3ae3}|Créé un nouvel objet d’authentification stratégie configuration conteneur CN = Configuration de la stratégie AuthN, CN = Services dans la partition de Configuration.|-   objectClass: container<br />-   displayName: Configuration de la stratégie d’authentification<br />-   description: Contient la configuration de stratégie d’authentification.<br />-   showInAdvancedViewOnly: True|(A;;RPLCLORC;;;AU)<br />(A;;RPWPCRLCLOCCRCWDWOSW;;;EA)<br />(A;;RPWPCRLCLOCCDCRCWDWOSDDTSW;;;SY)|
|**Opération 132**: {bbbb9db0-4009-4368-8c40-6674e980d3c3}|Créé un nouvel objet de stratégies d’authentification CN = AuthN Policies, CN = Configuration de la stratégie AuthN, CN = Services dans la partition de Configuration.|-   objectClass: msDS-AuthNPolicies<br />-   displayName: Stratégies d'authentification<br />-   description: Contient des objets de stratégie d’authentification.<br />-   showInAdvancedViewOnly: True|(A;;RPWPCRCCDCLCLOLORCWOWDSDDTDTSW;;;EA)<br />(A ; RPWPCRCCDCLCLORCWOWDSDDTSW ; ; SY)<br />(A;;RPLCLORC;;;AU)|
|**Opération 133**: {f754861c-3692-4a7b-b2c2-d0fa28ed0b0b}|Créé un nouveau silos de stratégies de l’objet CN = AuthN Silos, CN = Configuration de la stratégie AuthN, CN = Services dans la partition de Configuration.|-   objectClass: msDS-AuthNPolicySilos<br />-   displayName: Silos de stratégies d'authentification<br />-   description: Contient des objets silos de stratégies d’authentification.<br />-   showInAdvancedViewOnly: True|(A;;RPWPCRCCDCLCLOLORCWOWDSDDTDTSW;;;EA)<br />(A ; RPWPCRCCDCLCLORCWOWDSDDTSW ; ; SY)<br />(A;;RPLCLORC;;;AU)|
|**Opération 134**: {d32f499f-3026-4af0-a5bd-13fe5a331bd2}|Créé un nouvel objet d’authentification silo revendication type CN = ad : / / ext/AuthenticationSilo, CN = des Types de revendication, CN = Configuration des revendications, CN = Services dans la partition de Configuration.|-   objectClass: msDS-ClaimType<br />-displayname : AuthenticationSilo<br />-nom : ad : / ext/AuthenticationSilo<br />-Activé : True<br />-   msDS-ClaimIsValueSpaceRestricted: True<br />-msDS-ClaimIsSingleValued : True<br />-msDS-ClaimSourceType : Construit<br />-   msDS-ClaimValueType: 3<br />-   msDS-ClaimTypeAppliesToClass: CN = utilisateurs, CN = Schema, %WS<br />-   msDS-ClaimTypeAppliesToClass: CN = ordinateur, CN = Schema, %WS<br />-   msDS-ClaimTypeAppliesToClass: CN = ms-DS-géré-compte de Service, CN = Schema, %WS<br />-   msDS-ClaimTypeAppliesToClass: CN=ms-DS-Group-Managed-Service-Account,CN=Schema,%WS|(A;;RPWPCRCCDCLCLORCWOWDSDDTSW;;;EA)<br />(A ; RPWPCRCCDCLCLORCWOWDSDDTSW ; ; SY)<br />(A;;RPLCLORC;;;AU)|
|**Opération 135**: {38618886-98ee-4e42-8cf1-d9a2cd9edf8b}|Définissez l’attribut msDS-ClaimIsValueSpaceRestricted sur le nouveau type de revendication de silo de l’authentification sur false|-   msDS-ClaimIsValueSpaceRestricted: False|N/A|

## <a name="windows-server-2012-forest-wide-updates"></a>Windows Server 2012 : Mises à jour de la forêt

Après les opérations sont effectuées par le **forestprep** commande dans Windows Server 2012 (opérations 84-130) sont terminées, le **révision** attribut pour CN = ActiveDirectoryUpdate, CN = ForestUpdates, CN = Configuration, DC = domaine_racine_forêt objet est défini sur **11**.
  
|Nombre d’opérations et GUID|Description|Attributs|Autorisations|
|-----------------------------|---------------|--------------|---------------|
|**Opération 84**: {4664e973-cb20-4def-b3d5-559d6fe123e0}|Créé un nouveau conteneur CN = Configuration des revendications, CN = Services dans la partition de Configuration.|-   objectClass: container|(A;;RPLCLORC;;;AU)<br />(A;;RPWPCRLCLOCCRCWDWOSW;;;EA)<br />(A;;RPWPCRLCLOCCDCRCWDWOSDDTSW;;;SY)|
|**Opération 85**: {2972d92d-a07a-44ac-9cb0-bf243356f345}|Créé un nouvel objet CN = des Types de revendications, CN = Configuration des revendications, CN = Services dans la partition de Configuration.|-   objectClass: msDS-ClaimTypes<br />-   showInAdvancedViewOnly: True|(A;;RPLCLORC;;;AU)<br />(A;;RPWPCRLCLOCCDCRCWDWOSW;;;EA)<br />(A;;RPWPCRLCLOCCDCRCWDWOSDDTSW;;;SY)|
|**Opération 86**: {09a49cb3-6c54-4b83-ab20-8370838ba149}|Créé un nouvel objet CN = Propriétés de ressource, CN = Configuration des revendications, CN = Services dans la partition de Configuration.|-   objectClass: msDS-ResourceProperties<br />-   showInAdvancedViewOnly: True|(A;;RPLCLORC;;;AU)<br />(A;;RPWPCRLCLOCCDCRCWDWOSW;;;EA)<br />(A;;RPWPCRLCLOCCDCRCWDWOSDDTSW;;;SY)|
|**Opération 87**: {77283e65-ce02-4dc3-8c1e-bf99b22527c2}|Créé un nouveau conteneur CN = listes de propriétés de ressource, CN = Configuration des revendications, CN = Services dans la partition de Configuration.|-   objectClass: container<br />-   showInAdvancedViewOnly: True|(A;;RPLCLORC;;;AU)<br />(A;;RPWPCRLCLOCCDCRCWDWOSW;;;EA)<br />(A;;RPWPCRLCLOCCDCRCWDWOSDDTSW;;;SY)|
|**Opération 88**: {0afb7f53-96bd-404b-a659-89e65c269420}|Créé un nouvel objet CN = Sam-domaine dans la partition de schéma.|N/A|Créé l’entrée de contrôle d’accès (ACE) pour accorder d’écrire la propriété à Principal Self sur l’objet suivant :<br /><br />(OA;CIIO;WP;ea1b7b93-5e48-46d5-bc6c-4df4fda78a35;bf967a86-0de6-11d0-a285-00aa003049e2;PS)|
|**Opération 89**: {c7f717ef-fdbe-4b4b-8dfc-fa8b839fbcfa}|Créé un nouvel objet CN = domaine-DNS dans la partition de schéma.|N/A|Créé l’entrée de contrôle d’accès (ACE) pour accorder d’écrire la propriété à Principal Self sur l’objet suivant :<br /><br />(OA;CIIO;WP;ea1b7b93-5e48-46d5-bc6c-4df4fda78a35;bf967a86-0de6-11d0-a285-00aa003049e2;PS)|
|**Opération 90**: {00232167-f3a4-43c6-b503-9acb7a81b01c}|Rappeler une fonction pour mettre à niveau les spécificateurs d’affichage.|N/A|N/A|
|**Opération 91**: {73a9515b-511c-44d2-822b-444a33d3bd33}|Créé un nouveau conteneur CN = Microsoft SPP, CN = Services dans la partition de Configuration.|-   objectClass: container<br />-   showInAdvancedViewOnly: True|(A;;RPLCLORC;;;AU)<br />(A;;RPWPCRLCLOCCRCWDWOSW;;;EA)<br />(A;;RPWPCRLCLOCCDCRCWDWOSDDTSW;;;SY)|
|**Opération 92**: {e0c60003-2ed7-4fd3-8659-7655a7e79397}|Créé un nouveau conteneur d’objets d’Activation CN = les objets d’Activation, CN = Microsoft SPP, CN = Services dans la partition de Configuration.|-   objectClass: msSPP-ActivationObjectsContainer<br />-   showInAdvancedViewOnly: True|(A;;RPLCLORC;;;AU)<br />(A;;RPWPCRLCLOCCRCWDWOSW;;;EA)<br />(A;;RPWPCRLCLOCCDCRCWDWOSDDTSW;;;SY)|
|**Opération 93**: {ed0c8cca-80ab-4b6b-ac5a-59b1d317e11f}|Créé un nouveau conteneur de stratégies d’accès centralisées CN = stratégies d’accès centralisées, CN = Configuration des revendications, CN = Services dans la partition de Configuration.|-   objectClass: msAuthz-CentralAccessPolicies<br />-   showInAdvancedViewOnly: True|(A;;RPLCLORC;;;AU)<br />(A;;RPWPCRLCLOCCDCRCWDWOSW;;;EA)<br />(A;;RPWPCRLCLOCCDCRCWDWOSDDTSW;;;SY)|
|**Opération 94**: {b6a6c19a-afc9-476b-8994-61f5b14b3f05}|Créé un nouveau conteneur d’entrées de stratégie d’accès Central CN = les règles d’accès Central, CN = Configuration des revendications, CN = Services dans la partition de Configuration.|-   objectClass: msAuthz-CentralAccessRules<br />-   showInAdvancedViewOnly: True|(A;;RPLCLORC;;;AU)<br />(A;;RPWPCRLCLOCCDCRCWDWOSW;;;EA)<br />(A;;RPWPCRLCLOCCDCRCWDWOSDDTSW;;;SY)|
|**Opération 95**: {defc28cd-6cb6-4479-8bcb-aabfb41e9713}|Créé un nouveau conteneur de service de Distribution de clés de groupe CN = Service de Distribution de clés de groupe, CN = Services dans la partition de Configuration.|-   objectClass: container<br />-   description: Le conteneur contient les données de configuration et pour le Service de Distribution de clés de groupe.<br />-   showInAdvancedViewOnly: True|(A;;RPLCLORC;;;AU)<br />(A;;RPWPCRLCLOCCRCWDWOSW;;;EA)<br />(A;;RPWPCRLCLOCCDCRCWDWOSDDTSW;;;SY)|
|**Opération 96**: {d6bd96d4-e66b-4a38-9c6b-e976ff58c56d}|Créé un nouveau conteneur de clés de racine principales CN = clés principales de racine, CN = Service de Distribution de clés de groupe, CN = Services dans la partition de Configuration.|-   objectClass: container<br />-   description: Le conteneur contient les clés de la racine principale pour le Service de Distribution de clés de groupe.<br />-   showInAdvancedViewOnly: True|(A;;RPLCLORC;;;AU)<br />(A;;RPWPCRLCLOCCRCWDWOSW;;;EA)<br />(A;;RPWPCRLCLOCCDCRCWDWOSDDTSW;;;SY)|
|**Opération 97**: {bb8efc40-3090-4fa2-8a3f-7cd1d380e695}|Créé un nouveau conteneur de Configuration de serveur CN = serveur de Configuration, CN = Service de Distribution de clés de groupe, CN = Services dans la partition de Configuration.|-   objectClass: container<br />-   description: Le conteneur contient des configurations de Service de Distribution de clés de groupe.<br />-   showInAdvancedViewOnly: True|(A;;RPLCLORC;;;AU)<br />(A;;RPWPCRLCLOCCRCWDWOSW;;;EA)<br />(A;;RPWPCRLCLOCCDCRCWDWOSDDTSW;;;SY)|
|**Opération 98**: {2d6abe1b-4326-489e-920c-76d5337d2dc5}|Créé un serveur vide configuration objets conteneur CN = groupe Key Distribution Service Server Configuration, CN = Configuration du serveur, CN = Service de Distribution de clés de groupe, CN = Services dans la partition de Configuration.|-   objectClass: msKds-ProvServerConfiguration<br />-   description: La configuration des algorithmes de chiffrement utilisé par le Service de Distribution de clés de groupe.<br />-msKds-Version : 1<br />-   showInAdvancedViewOnly: True|(A;;RPLCLORC;;;AU)<br />(A;;RPWPCRLCLOCCRCWDWOSW;;;EA)<br />(A;;RPWPCRLCLOCCDCRCWDWOSDDTSW;;;SY)|
|**Opération 99**: {6b13dfb5-cecc-4fb8-b28d-0505cea24175}|Créé un nouveau conteneur de configuration de stratégies de Transformation des revendications CN = stratégies de Transformation de revendications, CN = Configuration des revendications, CN = Services dans la partition de Configuration.|-   objectClass: msDS-ClaimsTransformationPolicies<br />-   showInAdvancedViewOnly: True|(A;;RPLCLORC;;;AU)<br />(A;;RPWPCRLCLOCCDCRCWDWOSW;;;EA)<br />(A;;RPWPCRLCLOCCDCRCWDWOSDDTSW;;;SY)|
|**Opération 100**: {92e73422-c68b-46c9-b0d5-b55f9c741410}|Créé un nouveau conteneur de configuration de Types valeur CN = des Types valeur, CN = Configuration des revendications, CN = Services dans la partition de Configuration.|-   objectClass: container<br />-   showInAdvancedViewOnly: True|(A;;RPLCLORC;;;AU)<br />(A;;RPWPCRLCLOCCRCWDWOSW;;;EA)<br />(A;;RPWPCRLCLOCCDCRCWDWOSDDTSW;;;SY)|
|**Opération 101**: {c0ad80b4-8e84-4cc4-9163-2f84649bcc42}|Créé un nouvel objet SinglevaluedChoice valeur type configuration CN = MS-DS-SinglevaluedChoice, CN = des Types valeur, CN = Configuration des revendications, CN = Services dans la partition de Configuration.|-   objectClass: msDS-ValueType<br />-   description: Vous pouvez utiliser ce type pour créer une propriété de ressource. Lorsque vous affectez la valeur à une propriété de ressource de ce type de valeur, un utilisateur peut choisir qu’une seule entrée dans une liste de valeurs suggérées.<br />-displayname : Choix d’une valeur unique<br />-   msDS-ClaimValueType: 3<br />-   msDS-ClaimIsValueSpaceRestricted: True<br />-msDS-ClaimIsSingleValued : True<br />-   msDS-IsPossibleValuesPresent: True<br />-   showInAdvancedViewOnly: True|(D;;SDDT;;;WD)<br />(A;;RPLCLORC;;;AU)<br />(A;;RPWPCRLCLOCCRCWDWOSW;;;EA)<br />(A;;RPWPCRLCLOCCDCRCWDWOSDDTSW;;;SY)|
|**Opération 102**: {992fe1d0-6591-4f24-a163-c820fcb7f308}|Créé un nouvel objet YesNo valeur type configuration CN = MS-DS-YesNo, CN = des Types valeur, CN = Configuration des revendications, CN = Services dans la partition de Configuration.|-   objectClass: msDS-ValueType<br />-   description: Les valeurs valides pour ce type sont Oui ou non.<br />-displayname : Oui/Non<br />-   msDS-ClaimValueType: 6<br />-   msDS-ClaimIsValueSpaceRestricted: False<br />-msDS-ClaimIsSingleValued : True<br />-   msDS-IsPossibleValuesPresent: False<br />-   showInAdvancedViewOnly: True|(D;;SDDT;;;WD)<br />(A;;RPLCLORC;;;AU)<br />(A;;RPWPCRLCLOCCRCWDWOSW;;;EA)<br />(A;;RPWPCRLCLOCCDCRCWDWOSDDTSW;;;SY)|
|**Opération 103**: {ede85f96-7061-47bf-b11b-0c0d999595b5}|Créé un nouveau numéro configuration objet de type valeur CN = MS-DS-Number, CN = des Types valeur, CN = Configuration des revendications, CN = Services dans la partition de Configuration.|-   objectClass: msDS-ValueType<br />-   description: Vous pouvez utiliser ce type pour les propriétés de ressource auteur qui contiennent un nombre unique.<br />-displayname : Numéro<br />-   msDS-ClaimValueType: 1<br />-   msDS-ClaimIsValueSpaceRestricted: False<br />-msDS-ClaimIsSingleValued : True<br />-   msDS-IsPossibleValuesPresent: False<br />-   showInAdvancedViewOnly: True|(D;;SDDT;;;WD)<br />(A;;RPLCLORC;;;AU)<br />(A;;RPWPCRLCLOCCRCWDWOSW;;;EA)<br />(A;;RPWPCRLCLOCCDCRCWDWOSDDTSW;;;SY)|
|**Opération 104**: {ee0f3271-eb51-414a-bdac-8f9ba6397a39}|Créé un nouvel objet DateTime valeur type configuration CN = MS-DS-date/heure, CN = des Types valeur, CN = Configuration des revendications, CN = Services dans la partition de Configuration.|-   objectClass: msDS-ValueType<br />-   description: Vous pouvez utiliser ce type pour les propriétés de ressource auteur qui sont au format de date et d’heure.<br />-displayname : Date et heure<br />-   msDS-ClaimValueType: 1<br />-   msDS-ClaimIsValueSpaceRestricted: False<br />-msDS-ClaimIsSingleValued : True<br />-   msDS-IsPossibleValuesPresent: False<br />-   showInAdvancedViewOnly: True|(D;;SDDT;;;WD)<br />(A;;RPLCLORC;;;AU)<br />(A;;RPWPCRLCLOCCRCWDWOSW;;;EA)<br />(A;;RPWPCRLCLOCCDCRCWDWOSDDTSW;;;SY)|
|**Opération 105**: {587d52e0-507e-440e-9d67-e6129f33bb68}|Créé un nouvel objet OrderedList valeur type configuration CN = MS-DS-OrderedList, CN = des Types valeur, CN = Configuration des revendications, CN = Services dans la partition de Configuration.|-   objectClass: msDS-ValueType<br />-   description: Vous pouvez utiliser ce type pour les propriétés de ressource auteur qui contiennent une entrée de choix unique pouvant être comparé à d’autres propriétés de ressource du même type. En règle générale, un utilisateur choisit l’entrée dans une liste de valeurs suggérées ordonnées qui sont fournis par ms-DS--Possible-les valeurs de revendication sur les propriétés de ressource.<br />-displayname : Liste triée<br />-   msDS-ClaimValueType: 1<br />-   msDS-ClaimIsValueSpaceRestricted: True<br />-msDS-ClaimIsSingleValued : True<br />-   msDS-IsPossibleValuesPresent: True<br />-   showInAdvancedViewOnly: True|(D;;SDDT;;;WD)<br />(A;;RPLCLORC;;;AU)<br />(A;;RPWPCRLCLOCCRCWDWOSW;;;EA)<br />(A;;RPWPCRLCLOCCDCRCWDWOSDDTSW;;;SY)|
|**Opération 106**: {ce24f0f6-237e-43d6-ac04-1e918ab04aac}|Créé un objet de texte valeur type configuration CN = MS-DS-Text, CN = des Types valeur, CN = Configuration des revendications, CN = Services dans la partition de Configuration.|-   objectClass: msDS-ValueType<br />-   description: Vous pouvez utiliser ce type pour les propriétés de ressource auteur qui contiennent une entrée de texte unique.<br />-displayname : Text<br />-   msDS-ClaimValueType: 3<br />-   msDS-ClaimIsValueSpaceRestricted: False<br />-msDS-ClaimIsSingleValued : True<br />-   msDS-IsPossibleValuesPresent: False<br />-   showInAdvancedViewOnly: True|(D;;SDDT;;;WD)<br />(A;;RPLCLORC;;;AU)<br />(A;;RPWPCRLCLOCCRCWDWOSW;;;EA)<br />(A;;RPWPCRLCLOCCDCRCWDWOSDDTSW;;;SY)|
|**Opération 107**: {7f77d431-dd6a-434f-ae4d-ce82928e498f}|Créé un nouvel objet MultivaluedText valeur type configuration CN = MS-DS-MultivaluedText, CN = des Types valeur, CN = Configuration des revendications, CN = Services dans la partition de Configuration.|-   objectClass: msDS-ValueType<br />-   description: Vous pouvez utiliser ce type pour les propriétés de ressource auteur qui peuvent avoir plusieurs entrées de texte.<br />-displayname : Texte à valeurs multiples<br />-   msDS-ClaimValueType: 3<br />-   msDS-ClaimIsValueSpaceRestricted: False<br />-msDS-ClaimIsSingleValued : False<br />-   msDS-IsPossibleValuesPresent: False<br />-   showInAdvancedViewOnly: True|(D;;SDDT;;;WD)<br />(A;;RPLCLORC;;;AU)<br />(A;;RPWPCRLCLOCCRCWDWOSW;;;EA)<br />(A;;RPWPCRLCLOCCDCRCWDWOSDDTSW;;;SY)|
|**Opération 108**: {ba14e1f6-7cd1-4739-804f-57d0ea74edf4}|Créé un nouvel objet MultivaluedChoice valeur type configuration CN = MS-DS-MultivaluedChoice, CN = des Types valeur, CN = Configuration des revendications, CN = Services dans la partition de Configuration.|-   objectClass: msDS-ValueType<br />-   description: Vous pouvez utiliser ce type pour les propriétés de ressource auteur qui peuvent avoir plusieurs entrées ne peuvent pas être comparées. En règle générale, un utilisateur choisit chaque entrée dans une liste de valeurs suggérées qui sont fournis par ms-DS--Possible-les valeurs de revendication sur les propriétés de ressource.<br />-displayname : Choix multiple<br />-   msDS-ClaimValueType: 3<br />-   msDS-ClaimIsValueSpaceRestricted: True<br />-msDS-ClaimIsSingleValued : False<br />-   msDS-IsPossibleValuesPresent: True<br />-   showInAdvancedViewOnly: True|(D;;SDDT;;;WD)<br />(A;;RPLCLORC;;;AU)<br />(A;;RPWPCRLCLOCCRCWDWOSW;;;EA)<br />(A;;RPWPCRLCLOCCDCRCWDWOSDDTSW;;;SY)|  
|**Opération 109**: {156ffa2a-e07c-46fb-a5c4-fbd84a4e5cce}|Créé un objet de propriété de nouvelles informations d’identification personnelle ressource CN = PII_MS, CN = Propriétés de ressource, CN = Configuration des revendications, CN = Services dans la partition de Configuration.|-   objectClass: msDS-ResourceProperty<br />-   description: La propriété informations personnellement identifiables (PII) Spécifie si la ressource contient des informations d’identification personnelle et s’il existe, ce qui est le niveau de sensibilité de ces informations.<br />-displayname : Informations d’identification personnelle<br />-Activé : False<br />-   msDS-IsUsedAsResourceSecurityAttribute: True<br />-   msDS-ValueTypeReference: CN = MS-DS-OrderedList, CN = des Types valeur, CN = Configuration des revendications, CN = Services, CN = Configuration, CN =<forest root domain>|(D;;SDDT;;;WD)<br />(A;;RPLCLORC;;;AU)<br />(A;;RPWPCRLCLOCCRCWDWOSW;;;EA)<br />(A;;RPWPCRLCLOCCDCRCWDWOSDDTSW;;;SY)|
|**Opération 110**: {7771d7dd-2231-4470-aa74-84a6f56fc3b6}|Créé un objet propriété de ressource nouveau Protected Health Information CN = ProtectedHealthInformation_MS, CN = Propriétés de ressource, CN = Configuration des revendications, CN = Services dans la partition de Configuration.|-   objectClass: msDS-ResourceProperty<br />-   description: La propriété protégée santé confidentielles (PHI) Spécifie si la ressource contient toutes les données relatives au dossier médical ou l’historique de paiement médical.<br />-displayname : Informations médicales protégées<br />-Activé : False<br />-   msDS-IsUsedAsResourceSecurityAttribute: True<br />-   msDS-ValueTypeReference: CN = MS-DS-YesNo, CN = des Types valeur, CN = Configuration des revendications, CN = Services, CN = Configuration, CN =<forest root domain>|(D;;SDDT;;;WD)<br />(A;;RPLCLORC;;;AU)<br />(A;;RPWPCRLCLOCCRCWDWOSW;;;EA)<br />(A;;RPWPCRLCLOCCDCRCWDWOSDDTSW;;;SY)|
|**Opération 111**: {49b2ae86-839a-4ea0-81fe-9171c1b98e83}|Créé un objet propriété de ressource nouveau Clearance requis CN = RequiredClearance_MS, CN = Propriétés de ressource, CN = Configuration des revendications, CN = Services dans la partition de Configuration.|-   objectClass: msDS-ResourceProperty<br />-   description: La propriété d’habilitation requis spécifie le niveau habilitation qu'un utilisateur doit disposer avant de tenter d’accéder à la ressource.<br />-displayname : Autorisation obligatoire<br />-Activé : False<br />-   msDS-IsUsedAsResourceSecurityAttribute: True<br />-   msDS-ValueTypeReference: CN = MS-DS-OrderedList, CN = des Types valeur, CN = Configuration des revendications, CN = Services, CN = Configuration, CN =<forest root domain>|(D;;SDDT;;;WD)<br />(A;;RPLCLORC;;;AU)<br />(A;;RPWPCRLCLOCCRCWDWOSW;;;EA)<br />(A;;RPWPCRLCLOCCDCRCWDWOSDDTSW;;;SY)|
|**Opération 112**: {1b1de989-57ec-4e96-b933-8279a8119da4}|Créé un objet de propriété de nouveau la confidentialité ressource CN = Confidentiality_MS, CN = Propriétés de ressource, CN = Configuration des revendications, CN = Services dans la partition de Configuration.|-   objectClass: msDS-ResourceProperty<br />-   description: La propriété de la confidentialité Spécifie le niveau de confidentialité de la ressource et l’impact potentiel de l’accès involontaire ou divulgation non autorisés.<br />-displayname : Confidentialité<br />-Activé : False<br />-   msDS-IsUsedAsResourceSecurityAttribute: True<br />-   msDS-ValueTypeReference: CN = MS-DS-OrderedList, CN = des Types valeur, CN = Configuration des revendications, CN = Services, CN = Configuration, CN =<forest root domain>|(D;;SDDT;;;WD)<br />(A;;RPLCLORC;;;AU)<br />(A;;RPWPCRLCLOCCRCWDWOSW;;;EA)<br />(A;;RPWPCRLCLOCCDCRCWDWOSDDTSW;;;SY)|
|**Opération 113**: {281c63f0-2c9a-4cce-9256-a238c23c0db9}|Créé un objet propriété de ressource nouveau conformité CN = Compliancy_MS, CN = Propriétés de ressource, CN = Configuration des revendications, CN = Services dans la partition de Configuration.|-   objectClass: msDS-ResourceProperty<br />-   description: La propriété de la conformité spécifie les frameworks de conformité qui s’appliquent à la ressource.<br />-displayname : Conformité<br />-Activé : False<br />-   msDS-IsUsedAsResourceSecurityAttribute: True<br />-   msDS-ValueTypeReference: CN = MS-DS-MultivaluedChoice, CN = des Types valeur, CN = Configuration des revendications, CN = Services, CN = Configuration, CN =<forest root domain>|(D;;SDDT;;;WD)<br />(A;;RPLCLORC;;;AU)<br />(A;;RPWPCRLCLOCCRCWDWOSW;;;EA)<br />(A;;RPWPCRLCLOCCDCRCWDWOSDDTSW;;;SY)|
|**Opération 114**: {4c47881a-f15a-4f6c-9f49-2742f7a11f4b}|Créé un objet propriété de ressource nouveau détectabilité CN = Discoverability_MS, CN = Propriétés de ressource, CN = Configuration des revendications, CN = Services dans la partition de Configuration.|-   objectClass: msDS-ResourceProperty<br />-   description: La propriété de détectabilité Spécifie si la ressource contient la preuve potentielle qui peut-être nécessiter la divulgation à opposées juridique au cours de litiges actuelles ou futures.<br />-displayname : Détectabilité<br />-Activé : False<br />-   msDS-IsUsedAsResourceSecurityAttribute: True<br />-   msDS-ValueTypeReference: CN = MS-DS-SinglevaluedChoice, CN = des Types valeur, CN = Configuration des revendications, CN = Services, CN = Configuration, CN =<forest root domain>|(D;;SDDT;;;WD)<br />(A;;RPLCLORC;;;AU)<br />(A;;RPWPCRLCLOCCRCWDWOSW;;;EA)<br />(A;;RPWPCRLCLOCCDCRCWDWOSDDTSW;;;SY)|
|**Opération 115**: {2aea2dc6-d1d3-4f0c-9994-66c1da21de0f}|Créé un nouvel objet de propriété de ressource immuable CN = Immutable_MS, CN = Propriétés de ressource, CN = Configuration des revendications, CN = Services dans la partition de Configuration.|-   objectClass: msDS-ResourceProperty<br />-   description: La propriété immuable Spécifie si un utilisateur doit être autorisé à supprimer une ressource ou de modifier son contenu.<br />-displayname : Immuable<br />-Activé : False<br />-   msDS-IsUsedAsResourceSecurityAttribute: True<br />-   msDS-ValueTypeReference: CN = MS-DS-YesNo, CN = des Types valeur, CN = Configuration des revendications, CN = Services, CN = Configuration, CN =<forest root domain>|(D;;SDDT;;;WD)<br />(A;;RPLCLORC;;;AU)<br />(A;;RPWPCRLCLOCCRCWDWOSW;;;EA)<br />(A;;RPWPCRLCLOCCDCRCWDWOSDDTSW;;;SY)|
|**Opération 116**: {ae78240c-43b9-499e-ae65-2b6e0f0e202a}|Créé un objet propriété de ressource nouvelle propriété intellectuelle CN = IntellectualProperty_MS, CN = Propriétés de ressource, CN = Configuration des revendications, CN = Services dans la partition de Configuration.|-   objectClass: msDS-ResourceProperty<br />-   description: La propriété de la propriété intellectuelle (IP) Spécifie si la ressource contient une adresse IP et, le cas échéant, quel type.<br />-displayname : Propriété intellectuelle<br />-Activé : False<br />-   msDS-IsUsedAsResourceSecurityAttribute: True<br />-   msDS-ValueTypeReference: CN = MS-DS-SinglevaluedChoice, CN = des Types valeur, CN = Configuration des revendications, CN = Services, CN = Configuration, CN =<forest root domain>|(D;;SDDT;;;WD)<br />(A;;RPLCLORC;;;AU)<br />(A;;RPWPCRLCLOCCRCWDWOSW;;;EA)<br />(A;;RPWPCRLCLOCCDCRCWDWOSDDTSW;;;SY)|
|**Opération 117**: {261b5bba-3438-4d5c-a3e9-7b871e5f57f0}|Créé un département ressources propriété objet CN = Department_MS, CN = Propriétés de ressource, CN = Configuration des revendications, CN = Services dans la partition de Configuration.|-   objectClass: msDS-ResourceProperty<br />-   description: La propriété du service spécifie le nom du service auquel appartient la ressource.<br />-displayname : Service<br />-Activé : False<br />-   msDS-IsUsedAsResourceSecurityAttribute: True<br />-   msDS-ValueTypeReference: CN = MS-DS-SinglevaluedChoice, CN = des Types valeur, CN = Configuration des revendications, CN = Services, CN = Configuration, CN =<forest root domain>|(D;;SDDT;;;WD)<br />(A;;RPLCLORC;;;AU)<br />(A;;RPWPCRLCLOCCRCWDWOSW;;;EA)<br />(A;;RPWPCRLCLOCCDCRCWDWOSDDTSW;;;SY)|
|**Opération 118**: {3fb79c05-8ea1-438c-8c7a-81f213aa61c2}|Créé un impact sur les ressources propriété objet CN = Impact_MS, CN = Propriétés de ressource, CN = Configuration des revendications, CN = Services dans la partition de Configuration.|-   objectClass: msDS-ResourceProperty<br />-   description: La propriété Impact Spécifie le niveau d’impact d’organisation contre tout accès inapproprié ou une perte de la ressource.<br />-displayname : Impact<br />-Activé : False<br />-   msDS-IsUsedAsResourceSecurityAttribute: True<br />-   msDS-ValueTypeReference: CN = MS-DS-OrderedList, CN = des Types valeur, CN = Configuration des revendications, CN = Services, CN = Configuration, CN = < domaine racine de forêt<br />-msDS-ClaimPossibleValues : Haute - haute impact commercial (MBI) - impact sur les entreprises moyennes (IEA) - 3000, modéré - 2000, basse - faible impact sur l’activité (LBI) - 1000 >|(D;;SDDT;;;WD)<br />(A;;RPLCLORC;;;AU)<br />(A;;RPWPCRLCLOCCRCWDWOSW;;;EA)<br />(A;;RPWPCRLCLOCCDCRCWDWOSDDTSW;;;SY)|
|**Opération 119**: {0b2be39a-d463-4c23-8290-32186759d3b1}|Créé un usage personnel ressource propriété objet CN = PersonalUse_MS, CN = Propriétés de ressource, CN = Configuration des revendications, CN = Services dans la partition de Configuration.|-   objectClass: msDS-ResourceProperty<br />-   description: La propriété utiliser personnelles Spécifie si le fichier est pour une utilisation personnelle (pas l’activité).<br />-displayname : Utilisation personnelle<br />-Activé : False<br />-   msDS-IsUsedAsResourceSecurityAttribute: True<br />-   msDS-ValueTypeReference: CN = MS-DS-YesNo, CN = des Types valeur, CN = Configuration des revendications, CN = Services, CN = Configuration, CN =<forest root domain>|(D;;SDDT;;;WD)<br />(A;;RPLCLORC;;;AU)<br />(A;;RPWPCRLCLOCCRCWDWOSW;;;EA)<br />(A;;RPWPCRLCLOCCDCRCWDWOSDDTSW;;;SY)|
|**Opération 120**: {f0842b44-bc03-46a1-a860-006e8527fccd}|Créé un projet ressource propriété objet CN = Project_MS, CN = Propriétés de ressource, CN = Configuration des revendications, CN = Services dans la partition de Configuration.|-   objectClass: msDS-ResourceProperty<br />-   description: La propriété de projet spécifie les noms d’un ou plusieurs projets qui correspondent à la ressource.<br />-displayname : Projet<br />-Activé : False<br />-   msDS-IsUsedAsResourceSecurityAttribute: True<br />-   msDS-ValueTypeReference: CN = MS-DS-MultivaluedChoice, CN = des Types valeur, CN = Configuration des revendications, CN = Services, CN = Configuration, CN =<forest root domain>|(D;;SDDT;;;WD)<br />(A;;RPLCLORC;;;AU)<br />(A;;RPWPCRLCLOCCRCWDWOSW;;;EA)<br />(A;;RPWPCRLCLOCCDCRCWDWOSDDTSW;;;SY)|
|**Opération 121**: {93efec15-4dd9-4850-bc86-a1f2c8e2ebb9}|Créé un objet propriété de ressource nouvelle période de rétention CN = RetentionPeriod_MS, CN = Propriétés de ressource, CN = Configuration des revendications, CN = Services dans la partition de Configuration.|-   objectClass: msDS-ResourceProperty<br />-   description: La propriété de la période de rétention spécifie la durée maximale pour laquelle le fichier doit être conservé.<br />-displayname : Période de rétention<br />-Activé : False<br />-   msDS-IsUsedAsResourceSecurityAttribute: True<br />-   msDS-ValueTypeReference: CN = MS-DS-SinglevaluedChoice, CN = des Types valeur, CN = Configuration des revendications, CN = Services, CN = Configuration, CN =<forest root domain>|(D;;SDDT;;;WD)<br />(A;;RPLCLORC;;;AU)<br />(A;;RPWPCRLCLOCCRCWDWOSW;;;EA)<br />(A;;RPWPCRLCLOCCDCRCWDWOSDDTSW;;;SY)|
|**Opération 122**: {9e108d96-672f-40f0-b6bd-69ee1f0b7ac4}|Créé un objet propriété de ressource nouvelle Date de début de rétention CN = RetentionStartDate_MS, CN = Propriétés de ressource, CN = Configuration des revendications, CN = Services dans la partition de Configuration.|-   objectClass: msDS-ResourceProperty<br />-   description: La propriété de Date de début de rétention définit la date de début pour une période de rétention. Commencez la période de rétention sur la Date de début de rétention.<br />-displayname : Date de début de rétention<br />-Activé : False<br />-   msDS-IsUsedAsResourceSecurityAttribute: False<br />-   msDS-ValueTypeReference: CN = MS-DS-date/heure, CN = des Types valeur, CN = Configuration des revendications, CN = Services, CN = Configuration, CN =<forest root domain>|(D;;SDDT;;;WD)<br />(A;;RPLCLORC;;;AU)<br />(A;;RPWPCRLCLOCCRCWDWOSW;;;EA)<br />(A;;RPWPCRLCLOCCDCRCWDWOSDDTSW;;;SY)|
|**Opération 123**: {1e269508-f862-4c4a-b01f-420d26c4ff8c}|Créé un objet propriété de ressource nouvelle société CN = Company_MS, CN = Propriétés de ressource, CN = Configuration des revendications, CN = Services dans la partition de Configuration.|-   objectClass: msDS-ResourceProperty<br />-   description: La société propriété spécifie la ressource d’entreprise appartient.<br />-displayname : Société<br />-Activé : False<br />-   msDS-IsUsedAsResourceSecurityAttribute: True<br />-   msDS-ValueTypeReference: CN = MS-DS-SinglevaluedChoice, CN = des Types valeur, CN = Configuration des revendications, CN = Services, CN = Configuration, CN =<forest root domain>|(D;;SDDT;;;WD)<br />(A;;RPLCLORC;;;AU)<br />(A;;RPWPCRLCLOCCRCWDWOSW;;;EA)<br />(A;;RPWPCRLCLOCCDCRCWDWOSDDTSW;;;SY)|
|**Opération 125**: {e1ab17ed-5efb-4691-ad2d-0424592c5755} **Remarque :** Opération 124 a été supprimée.|Créé un objet propriété de ressource nouvelle utilisation du dossier CN = FolderUsage_MS, CN = Propriétés de ressource, CN = Configuration des revendications, CN = Services dans la partition de Configuration.|-   objectClass: msDS-ResourceProperty<br />-   description: La propriété utilisation du dossier spécifie l’objet du dossier et le type des fichiers stockés dans celui-ci.<br />-displayname : Utilisation du dossier<br />-Activé : False<br />-   msDS-IsUsedAsResourceSecurityAttribute: False<br />-   msDS-AppliestoResourceTypes: MS-DS-Container<br />-   msDS-ValueTypeReference: CN = MS-DS-MultivaluedChoice, CN = des Types valeur, CN = Configuration des revendications, CN = Services, CN = Configuration, CN =<forest root domain>|(D;;SDDT;;;WD)<br />(A;;RPLCLORC;;;AU)<br />(A;;RPWPCRLCLOCCRCWDWOSW;;;EA)<br />(A;;RPWPCRLCLOCCDCRCWDWOSDDTSW;;;SY)| 
|**Opération 126**: {0e848bd4-7c70-48f2-b8fc-00fbaa82e360}|Créé un nouvel objet de configuration de liste de propriétés de ressource globales CN = liste de propriétés de ressources globales, CN = listes de propriétés de ressource, CN = Configuration des revendications, CN = Services dans la partition de Configuration.|-   objectClass: msDS-ResourcePropertyList<br />-   description: Il s’agit global en dehors de la liste de propriétés de ressource de zone qui contient toutes les propriétés de ressources qui peuvent être utilisées par les applications.<br />-   showInAdvancedViewOnly: True<br />-   msDS-MembersOfResourcePropertyList: CN = PII_MS, CN = Propriétés de ressource, CN = Configuration des revendications, CN = Services, CN = Configuration, CN =<forest root domain><br />-   msDS-MembersOfResourcePropertyList: CN = ProtectedHealthInformation_MS, CN = Propriétés de ressource, CN = Configuration des revendications, CN = Services, CN = Configuration, CN =<forest root domain><br />-   msDS-MembersOfResourcePropertyList: CN = RequiredClearance_MS, CN = Propriétés de ressource, CN = Configuration des revendications, CN = Services, CN = Configuration, CN =<forest root domain><br />-   msDS-MembersOfResourcePropertyList: CN = Confidentiality_MS, CN = Propriétés de ressource, CN = Configuration des revendications, CN = Services, CN = Configuration, CN =<forest root domain><br />-   msDS-MembersOfResourcePropertyList: CN = Compliancy_MS, CN = Propriétés de ressource, CN = Configuration des revendications, CN = Services, CN = Configuration, CN =<forest root domain><br />-   msDS-MembersOfResourcePropertyList: CN = Discoverability_MS, CN = Propriétés de ressource, CN = Configuration des revendications, CN = Services, CN = Configuration, CN =<forest root domain><br />-   msDS-MembersOfResourcePropertyList: CN = Immutable_MS, CN = Propriétés de ressource, CN = Configuration des revendications, CN = Services, CN = Configuration, CN =<forest root domain><br />-   msDS-MembersOfResourcePropertyList: CN = IntellectualProperty_MS, CN = Propriétés de ressource, CN = Configuration des revendications, CN = Services, CN = Configuration, CN =<forest root domain><br />-   msDS-MembersOfResourcePropertyList: CN = Department_MS, CN = Propriétés de ressource, CN = Configuration des revendications, CN = Services, CN = Configuration, CN =<forest root domain><br />-   msDS-MembersOfResourcePropertyList: CN = Impact_MS, CN = Propriétés de ressource, CN = Configuration des revendications, CN = Services, CN = Configuration, CN =<forest root domain><br />-   msDS-MembersOfResourcePropertyList: CN = PersonalUse_MS, CN = Propriétés de ressource, CN = Configuration des revendications, CN = Services, CN = Configuration, CN =<forest root domain><br />-   msDS-MembersOfResourcePropertyList: CN = Project_MS, CN = Propriétés de ressource, CN = Configuration des revendications, CN = Services, CN = Configuration, CN =<forest root domain><br />-   msDS-MembersOfResourcePropertyList: CN = RetentionPeriod_MS, CN = Propriétés de ressource, CN = Configuration des revendications, CN = Services, CN = Configuration, CN =<forest root domain><br />-   msDS-MembersOfResourcePropertyList: CN = RetentionStartDate_MS, CN = Propriétés de ressource, CN = Configuration des revendications, CN = Services, CN = Configuration, CN =<forest root domain><br />-   msDS-MembersOfResourcePropertyList: CN = Company_MS, CN = Propriétés de ressource, CN = Configuration des revendications, CN = Services, CN = Configuration, CN =<forest root domain><br />-   msDS-MembersOfResourcePropertyList: CN = FolderUsage_MS, CN = Propriétés de ressource, CN = Configuration des revendications, CN = Services, CN = Configuration, CN =<forest root domain>|(D;;SDDT;;;WD)<br />(A;;RPLCLORC;;;AU)<br />(A;;RPWPCRLCLOCCRCWDWOSW;;;EA)<br />(A;;RPWPCRLCLOCCDCRCWDWOSDDTSW;;;SY)|
|**Opération 127**: {016f23f7-077d-41fa-a356-de7cfdb01797}|Rappeler une fonction pour mettre à niveau les spécificateurs d’affichage.|N/A|N/A|
|**Opération 128**: {49c140db-2de3-44c2-a99a-bab2e6d2ba81}|Mise à jour des chaînes pour l’objet de propriété de ressource de l’utilisation du dossier CN = FolderUsage_MS, CN = Propriétés de ressource, CN = Configuration des revendications, CN = Services dans la partition de Configuration.|-   description: La propriété utilisation du dossier spécifie l’objet du dossier et le type des fichiers stockés dans celui-ci.|N/A|
|**Opération 129**: {e0b11c80-62c5-47f7-ad0d-3734a71b8312}|Ajouté des ACE pour accorder la propriété d’écriture Principal Self et propriété de lecture sur CN = objet de domaine de Sam.|N/A|(OA;CIOI;RPWP;3f78c3e5-f79a-46bd-a0b8-9d18116ddc79;;PS)|
|**Opération 130**: {2ada1a2d-b02f-4731-b4fe-59f955e24f71}|Ajouté des ACE pour accorder la propriété d’écriture Principal Self et propriété de lecture sur CN = objet de domaine DNS.|N/A|(OA;CIOI;RPWP;3f78c3e5-f79a-46bd-a0b8-9d18116ddc79;;PS)|