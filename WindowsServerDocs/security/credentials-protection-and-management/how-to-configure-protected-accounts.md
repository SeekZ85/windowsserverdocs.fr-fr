---
title: Comment configurer des comptes protégés
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.service: na
ms.suite: na
ms.technology: security-auditing
ms.tgt_pltfrm: na
ms.topic: article
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: f2effdb7a82a25c810bc041475e760145de492d8
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59864610"
---
# <a name="how-to-configure-protected-accounts"></a>Comment configurer des comptes protégés

>S'applique à : Windows Server (canal semi-annuel), Windows Server 2016

Par le biais d'attaques PtH (Pass-the-Hash), une personne malveillante peut s'authentifier sur un service ou un serveur distant à l'aide du hachage NTLM sous-jacent du mot de passe d'un utilisateur (ou d'autres dérivés d'informations d'identification). Microsoft a précédemment [publié des conseils](https://www.microsoft.com/download/details.aspx?id=36036) pour prévenir les attaques PtH.  Windows Server 2012 R2 inclut de nouvelles fonctionnalités pour aider à atténuer ce type d’attaques. Pour plus d’informations sur d’autres fonctionnalités de sécurité permettant de se prémunir contre le vol d’informations d’identification, consultez [Gestion et protection des informations d’identification](https://technet.microsoft.com/library/dn408190.aspx). Cette rubrique décrit comment configurer les nouvelles fonctionnalités suivantes :  
  
-   [Utilisateurs protégés](how-to-configure-protected-accounts.md#BKMK_AddtoProtectedUsers)  
  
-   [Stratégies d’authentification](how-to-configure-protected-accounts.md#BKMK_CreateAuthNPolicies)  
  
-   [Silos de stratégies](how-to-configure-protected-accounts.md#BKMK_CreateAuthNPolicySilos)  
  
Windows 8.1 et Windows Server 2012 R2 présentent d'autres fonctionnalités de prévention contre le vol d'informations d'identification. Elles sont abordées dans les rubriques suivantes :  
  
-   [Mode d’administration restreinte pour Bureau à distance](http://blogs.technet.com/b/kfalde/archive/20../restricted-admin-mode-for-rdp-in-windows-8-1-2012-r2.aspx)  
  
-   [LSA Protection](https://technet.microsoft.com/library/dn408187)  
  
## <a name="BKMK_AddtoProtectedUsers"></a>Utilisateurs protégés  
Il s'agit d'un nouveau groupe de sécurité global auquel vous pouvez ajouter des nouveaux utilisateurs ou des utilisateurs existants. Les appareils Windows 8.1 et Windows Server 2012 R2 hôtes se comportent différemment avec les membres de ce groupe pour fournir une meilleure protection contre le vol d’informations d’identification. Pour un membre du groupe, un appareil Windows 8.1 ou un hôte Windows Server 2012 R2 ne met pas en cache les informations d’identification qui ne sont pas pris en charge pour les utilisateurs protégés. Membres de ce groupe ne sont pas protégés supplémentaires s’ils sont connectés à un appareil qui exécute une version de Windows antérieure à Windows 8.1.  
  
Groupe de membres d’utilisateurs protégés qui sont signés-on sur des appareils Windows 8.1 et les hôtes Windows Server 2012 R2 peuvent *n’est plus* utiliser :  
  
-   la délégation d'informations d'identification par défaut (CredSSP) : les informations d'identification en texte brut ne sont pas mises en cache même si la stratégie **Autoriser la délégation d'informations d'identification par défaut** est activée ;  
  
-   Windows Digest : les informations d'identification en texte brut ne sont pas mises en cache même si elles sont activées ;  
  
-   NTLM : NTOWF n'est pas mis en cache ;  
  
-   les clés à long terme Kerberos : le ticket TGT (Ticket-Granting Ticket) Kerberos s'obtient à l'ouverture de session et ne peut pas être à nouveau obtenu automatiquement ;  
  
-   l'authentification hors ligne : le vérificateur d'ouverture de session en cache n'est pas créé.  
  
Si le niveau fonctionnel du domaine est Windows Server 2012 R2, les membres du groupe ne peuvent plus :  
  
-   effectuer d'authentifications NTLM ;  
  
-   utiliser les suites de chiffrement DES (Data Encryption Standard) ou RC4 dans la pré-authentification Kerberos ;  
  
-   être délégués en utilisant la délégation non contrainte ou contrainte ;  
  
-   renouveler les tickets TGT utilisateur au-delà de la durée de vie initiale de 4 heures.  
  
Pour ajouter des utilisateurs au groupe, vous pouvez utiliser [outils d’interface utilisateur](https://technet.microsoft.com/library/cc753515.aspx) telles que Active Directory Administrative Center (ADAC) ou Active Directory utilisateurs et ordinateurs ou un outil de ligne de commande tel que [groupe Dsmod](https://technet.microsoft.com/library/cc732423.aspx), ou le Windows PowerShell[Add-ADGroupMember](https://technet.microsoft.com/library/ee617210.aspx) applet de commande. Les comptes de services et d'ordinateurs *ne doivent pas* être membres du groupe Utilisateurs protégés. L'appartenance à ces comptes n'offre pas de protection locale car le mot de passe ou le certificat est toujours disponible sur l'hôte.  
  
> [!WARNING]  
> Les restrictions d'authentification n'offrent pas de solutions de contournement, ce qui veut dire que les membres des groupes dotés de privilèges élevés tels que les groupes Administrateurs d'entreprise ou Admins du domaine sont soumis aux mêmes restrictions que les autres membres du groupe Utilisateurs protégés. Si tous les membres de ces groupes sont ajoutés au groupe Utilisateurs protégés, tous ces comptes peuvent être verrouillés. Vous ne devez jamais ajouter des comptes dotés de privilèges élevés au groupe Utilisateurs protégés avant d'avoir testé les éventuelles répercussions en détail.  
  
Les membres du groupe Utilisateurs protégés doivent être capables d'effectuer une authentification à l'aide du chiffrement Kerberos AES (Advanced Encryption Standards). Cette méthode nécessite des clés AES pour le compte dans Active Directory. Le compte administrateur intégré n’a pas une clé AES sauf si le mot de passe a été modifié sur un contrôleur de domaine qui exécute Windows Server 2008 ou version ultérieure. De plus, un compte dont le mot de passe a été modifié sur un contrôleur de domaine exécutant une version antérieure de Windows Server est verrouillé. Nous vous recommandons, par conséquent, de suivre ces meilleures pratiques :  
  
-   Ne testez pas dans les domaines, sauf si **tous les contrôleurs de domaine exécutent Windows Server 2008 ou version ultérieure**.  
  
-   **changer le mot de passe** pour tous les comptes de domaine qui ont été créés *avant* que le domaine ne l'ait été lui-même car cela empêche leur authentification ;  
  
-   **Mot de passe de modification** pour chaque utilisateur avant d’ajouter le compte à utilisateurs protégés groupe ou vérifier que le mot de passe a été modifié récemment sur un contrôleur de domaine qui exécute Windows Server 2008 ou version ultérieure.  
  
### <a name="BKMK_Prereq"></a>Configuration requise pour utiliser des comptes protégés  
Ces derniers doivent respecter les conditions de déploiements requises suivantes :  
  
-   Pour fournir des restrictions côté client pour les utilisateurs protégés, les ordinateurs hôtes doivent exécuter Windows 8.1 ou Windows Server 2012 R2. Un utilisateur doit uniquement s'authentifier avec un compte qui est membre d'un groupe Utilisateurs protégés. Dans ce cas, le groupe utilisateurs protégés peut être créé par [transférer le rôle d’émulateur de contrôleur principal de domaine](https://technet.microsoft.com/library/cc816944(v=ws.10).aspx) à un contrôleur de domaine qui exécute Windows Server 2012 R2. Une fois l'objet de groupe répliqué sur d'autres contrôleurs de domaine, le rôle de l'émulateur PDC peut être hébergé sur un contrôleur de domaine qui exécute une version antérieure de Windows Server.  
  
-   Pour fournir des restrictions côté contrôleur de domaine pour les utilisateurs protégés, c'est-à-dire pour limiter l’utilisation de l’authentification NTLM, et d’autres restrictions, le niveau fonctionnel du domaine doit être Windows Server 2012 R2. Pour plus d’informations sur les niveaux fonctionnels, consultez [Présentation des niveaux fonctionnels des services de domaine Active Directory (AD DS)](../../identity/ad-ds/active-directory-functional-levels.md).  
  
### <a name="BKMK_TrubleshootingEvents"></a>Résoudre les problèmes des événements liés aux utilisateurs protégés  
Cette section aborde de nouveaux journaux qui permettent de résoudre des problèmes liés à des événements concernant les utilisateurs protégés. Elle décrit également comment les utilisateurs protégés peuvent répercuter les modifications pour résoudre les problèmes d'expiration de tickets TGT ou de délégation.  
  
#### <a name="new-logs-for-protected-users"></a>Nouveaux journaux pour les utilisateurs protégés  
Deux nouveaux journaux d'administration opérationnels sont disponibles pour résoudre les problèmes associés aux événements concernant les utilisateurs protégés : Utilisateur protégé - journal du Client et échecs de l’utilisateur protégé - journal de contrôleur de domaine. Ces nouveaux journaux se trouvent dans l'Observateur d'événements et sont désactivés par défaut. Pour activer un journal, cliquez sur **Journaux des applications et des services**, **Microsoft**, **Windows**, **Authentification**, puis cliquez sur le nom du journal et sur **Action** (ou cliquez avec le bouton droit sur le journal), puis sur **Activer le journal**.  
  
Pour plus d’informations sur les événements consignés dans ces journaux, consultez [Stratégies d’authentification et silos de stratégies d’authentification](https://technet.microsoft.com/library/dn486813.aspx).  
  
#### <a name="troubleshoot-tgt-expiration"></a>Résoudre les problèmes d'expiration TGT  
Généralement, le contrôleur de domaine définit la durée de vie et le renouvellement TGT en fonction de la stratégie de domaine, comme illustré dans la fenêtre Éditeur de gestion des stratégies de groupe.  
  
![Comptes protégés](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_TGTExpiration.png)  
  
Dans le cas des **utilisateurs protégés**, les paramètres suivants sont codés en dur :  
  
-   durée de vie maximale pour le ticket utilisateur : 240 minutes.  
  
-   durée de vie maximale pour le renouvellement du ticket utilisateur : 240 minutes.  
  
#### <a name="troubleshoot-delegation-issues"></a>Résoudre les problèmes de délégation  
Auparavant, en cas d'échec d'une technologie utilisant la délégation Kerberos, le compte client était vérifié pour voir si l'option **Le compte est sensible et ne peut pas être délégué** était définie. Cependant, si le compte est membre du groupe **Utilisateurs protégés**, ce paramètre n'est peut-être pas configuré dans le Centre d'administration Active Directory (ADAC). Ainsi, vérifiez le paramètre et l'appartenance au groupe quand vous résolvez les problèmes de délégation.  
  
![Comptes protégés](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_TshootDelegation.gif)  
  
### <a name="BKMK_AuditAuthNattempts"></a>Auditer les tentatives d’authentification  
Pour vérifier les tentatives d'authentification spécifiquement pour les membres du groupe **Utilisateurs protégés**, vous pouvez continuer à collecter les événements de vérification du journal de sécurité ou rassembler les données dans les journaux d'administration opérationnels. Pour plus d’informations sur ces événements, consultez [Stratégies d’authentification et silos de stratégies d’authentification](https://technet.microsoft.com/library/dn486813.aspx).  
  
### <a name="BKMK_ProvidePUdcProtections"></a>Fournir les protections côté contrôleur de domaine pour les services et les ordinateurs  
Les comptes de services et d'ordinateurs ne doivent pas être membres du groupe **Utilisateurs protégés**. Cette section décrit les protections basées sur le contrôleur de domaine qui peuvent être offertes pour ces comptes :  
  
-   rejet de l'authentification NTLM : configurable uniquement via les [stratégies du bloc NTLM](https://technet.microsoft.com/library/jj865674(v=ws.10).aspx) ;  
  
-   rejet de la norme DES (Data Encryption Standard) dans la pré-authentification Kerberos :  Les contrôleurs de domaine Windows Server 2012 R2 n’acceptent pas DES comptes d’ordinateur, sauf si elles sont configurées pour DES uniquement, car chaque version de Windows publiée avec Kerberos prend également en charge RC4.  
  
-   rejet de RC4 dans la pré-authentification Kerberos : non configurable ;  
  
    > [!NOTE]  
    > Même si vous pouvez [modifier la configuration des types de chiffrement pris en charge](http://blogs.msdn.com/b/openspecification/archive/20../windows-configurations-for-kerberos-supported-encryption-type.aspx), il n’est pas recommandé de changer ces paramètres pour les comptes d’ordinateur sans les tester dans l’environnement cible.  
  
-   restreindre les tickets utilisateur (TGT) à une durée de vie initiale de 4 heures : utiliser les stratégies d'authentification ;  
  
-   refuser la délégation avec délégation non contrainte ou contrainte : pour restreindre un compte, ouvrez le Centre d'administration Active Directory (ADAC), puis cochez la case **Le compte est sensible et ne peut pas être délégué**.  
  
    ![Comptes protégés](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_TshootDelegation.gif)  
  
## <a name="BKMK_CreateAuthNPolicies"></a>Stratégies d’authentification  
Il s'agit d'un nouveau conteneur des services de domaine Active Directory (AD DS) comprenant les objets de la stratégie d'authentification. Les stratégies d'authentification peuvent spécifier les paramètres qui permettent de prévenir l'exposition au vol d'informations d'identification, tels que la restriction de la durée de vie TGT des comptes ou l'ajout d'autres conditions associées aux revendications.  
  
Dans Windows Server 2012, le contrôle d’accès dynamique a introduit une classe d’objet de portée de la forêt Active Directory appelée stratégie d’accès centralisée pour fournir un moyen simple de configurer des serveurs de fichiers dans une organisation. Dans Windows Server 2012 R2, une nouvelle classe d’objet appelée stratégie d’authentification (objectClass msDS-AuthNPolicies) peut être utilisée pour appliquer la configuration de l’authentification aux classes de compte dans les domaines Windows Server 2012 R2. Les classes de compte Active Directory sont les suivantes :  
  
-   Utilisateur  
  
-   Computer  
  
-   Compte de service administré et compte de service administré de groupe (GMSA, Group Managed Service Account)  
  
### <a name="quick-kerberos-refresher"></a>Actualisateur Kerberos rapide  
Le protocole d'authentification Kerberos consiste en trois types d'échanges, également connus en tant que sous-protocoles :  
  
![Comptes protégés](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_KerbRefresher.gif)  
  
-   l'échange du service d'authentification (AS, Authentication Service) (KRB_AS_*),  
  
-   l'échange du service d'accord de tickets (TGS, Ticket-Granting Service) (KRB_TGS_*),  
  
-   l'échange client/serveur AP (Application Protocol) (KRB_AP_*).  
  
L’échange AS est où le client utilise les mots de passe ou la clé privée du compte pour créer un pré-authentificateur afin de demander un ticket-granting ticket (TGT ticket). Cela intervient au cours de l'authentification de l'utilisateur ou à la première demande de ticket de service.  
  
L’échange TGS est où le ticket TGT du compte est utilisé pour créer un authentificateur pour demander un ticket de service. Cela se produit quand une connexion authentifiée est nécessaire.  
  
L'échange AP a généralement lieu quand des données se trouvent à l'intérieur du protocole d'application et n'est pas affecté par des stratégies d'authentification.  
  
Pour plus d’informations, consultez [Kerberos Version 5 authentification fonctionnement du protocole] (https://technet.microsoft.com/library/cc772815(v=WS.10.aspx.  
  
### <a name="overview"></a>Vue d'ensemble  
Les stratégies d'authentification complètent le groupe Utilisateurs protégés en fournissant un moyen d'appliquer des restrictions configurables aux comptes et en imposant des restrictions aux comptes de services et d'ordinateurs. Elles entrent en vigueur pendant l'échange AS ou l'échange TGS.  
  
Vous pouvez restreindre l'authentification initiale ou l'échange AS en configurant :  
  
-   une durée de vie TGT ;  
  
-   des conditions de contrôle d'accès pour restreindre l'authentification de l'utilisateur (les appareils d'où provient l'échange AS doivent respecter ces conditions).  
  
![Comptes protégés](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_RestrictAS.gif)  
  
Vous pouvez restreindre les demandes de ticket de service via un échange de service d'accord de tickets (TGS) en configurant :  
  
-   les conditions de contrôle d'accès que le client (utilisateur, service, ordinateur) ou l'appareil d'où émane l'échange TGS doit respecter.  
  
### <a name="BKMK_ReqForAuthnPolicies"></a>Configuration requise pour utiliser des stratégies d’authentification  
  
|Stratégie|Configuration requise|  
|-----|--------|  
|Fournir des durées de vie TGT personnalisées| Domaines de comptes de niveau fonctionnel du domaine Windows Server 2012 R2|  
|Restreindre l'authentification utilisateur|-Domaines de comptes de niveau fonctionnel du domaine Windows Server 2012 R2 avec prise en charge du contrôle d’accès dynamique<br />-Windows 8, Windows 8.1, Windows Server 2012 ou les appareils Windows Server 2012 R2 avec le contrôle d’accès dynamique prend en charge|  
|Restreindre l'émission de tickets de service qui est basée sur le compte d'utilisateur et les groupes de sécurité| Domaines de ressources de niveau fonctionnel du domaine Windows Server 2012 R2|  
|Restreindre l'émission de tickets de service en fonction des revendications d'utilisateur ou du compte d'appareil, des groupes de sécurité ou des revendications| Domaines de ressources de niveau fonctionnel de domaine Windows Server 2012 R2 avec prise en charge du contrôle d’accès dynamique|  
  
### <a name="restrict-a-user-account-to-specific-devices-and-hosts"></a>Restreindre un compte d'utilisateur aux appareils et hôtes spécifiques  
Un compte à valeur élevée assorti d'un privilège d'administration doit être membre du groupe **Utilisateurs protégés** . Par défaut, aucun compte n'est membre du groupe **Utilisateurs protégés**. Avant d'ajouter des comptes au groupe, configurez la prise en charge du contrôleur de domaine et créez une stratégie d'audit pour vérifier qu'il n'y a aucun problème majeur.  
  
#### <a name="configure-domain-controller-support"></a>Configurer la prise en charge du contrôleur de domaine  
Domaine du compte d’utilisateur doit être au niveau fonctionnel du domaine Windows Server 2012 R2 (niveau fonctionnel du domaine). Vérifiez tous les contrôleurs de domaine sont Windows Server 2012 R2 et ensuite utilisent Active Directory Domains and Trusts à [augmenter le niveau fonctionnel du domaine](https://technet.microsoft.com/library/cc753104.aspx) vers Windows Server 2012 R2.  
  
**Pour configurer la prise en charge pour le contrôle d’accès dynamique**  
  
1.  Dans la stratégie des contrôleurs de domaine par défaut, cliquez sur **Activé** pour activer **Prise en charge par le client du centre de distribution de clés des revendications, de l'authentification composée et du blindage Kerberos** dans Configuration ordinateur | Modèles d'administration | Système | KDC.  
  
    ![Comptes protégés](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_EnableKDCClaims.gif)  
  
2.  Sous **Options**, dans la zone de liste déroulante, sélectionnez **Toujours fournir des revendications**.  
  
    > [!NOTE]  
    > **Prise en charge** peut également être configuré, mais étant donné que le domaine est au Windows Server 2012 R2 niveau fonctionnel du domaine, avoir les contrôleurs de domaine AlwaysOn fournissent des revendications permet des vérifications d’accès de basée sur les revendications d’utilisateur pour se produire lors de l’utilisation d’appareils prenant en charge les revendications et les hôtes pour vous connecter à services prenant en charge les revendications.  
  
    ![Comptes protégés](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_AlwaysProvideClaims.png)  
  
    > [!WARNING]  
    > Configuration **les demandes d’authentification non blindées** entraîne des échecs d’authentification à partir de n’importe quel système d’exploitation qui ne prend pas en charge le blindage, tel que Windows 7 et les systèmes d’exploitation précédents, ou l’utilisation de Kerberos systèmes à compter de Windows 8, qui n’ont pas été explicitement configurés pour prendre en charge.  
  
#### <a name="create-a-user-account-audit-for-authentication-policy-with-adac"></a>Créer un audit de compte d'utilisateur pour la stratégie d'authentification avec ADAC  
  
1.  Ouvrez le Centre d'administration Active Directory (ADAC).  
  
    ![Comptes protégés](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_OpenADAC.gif)  
  
    > [!NOTE]  
    > Le texte sélectionné **authentification** nœud est visible pour les domaines qui sont au niveau fonctionnel du domaine de Windows Server 2012 R2. Si le nœud n’apparaît pas, puis essayez à nouveau à l’aide d’un compte d’administrateur de domaine à partir d’un domaine qui se trouve au niveau fonctionnel du domaine de Windows Server 2012 R2.  
  
2.  Cliquez sur **Stratégies d'authentification**, puis sur **Nouveau** pour créer une stratégie.  
  
    ![Comptes protégés](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_NewAuthNPolicy.gif)  
  
    Les stratégies d'authentification doivent avoir un nom d'affichage. Elles sont appliquées par défaut.  
  
3.  Pour créer une stratégie en mode Auditer uniquement, cliquez sur **Auditer uniquement les restrictions de stratégie**.  
  
    ![Comptes protégés](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_NewAuthNPolicyAuditOnly.gif)  
  
    Les stratégies d'authentification sont appliquées en fonction du type de compte Active Directory. Une stratégie unique peut s'appliquer au trois types de compte en configurant les paramètres pour chaque type. Les types de compte sont les suivants :  
  
    -   Utilisateur  
  
    -   Computer  
  
    -   Compte de service administré et compte de service administré de groupe  
  
    Si vous avez étendu le schéma avec de nouveaux principaux qui peuvent être utilisés par le centre de distribution de clés (KDC, Key Distribution Center), le nouveau type de compte est classé à partir du type de compte dérivé le plus proche.  
  
4.  Pour configurer la durée de vie TGT des comptes d'utilisateur, cochez la case **Spécifiez la durée de vie du ticket TGT (Ticket Granting Ticket) pour les comptes d'utilisateur** et entrez la durée en minutes.  
  
    ![Comptes protégés](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_TGTLifetime.gif)  
  
    Par exemple, si vous voulez une durée de vie TGT maximale de 10 heures, entrez **600** comme illustré. Si aucune durée de vie TGT n'est configurée et si le compte est membre du groupe **Protected Users**, la durée de vie et le renouvellement TGT sont de 4 heures. Sinon, la durée de vie et le renouvellement TGT dépendent de la stratégie de domaine comme le montre la fenêtre Éditeur de gestion des stratégies de groupe suivante, pour un domaine comportant des paramètres par défaut.  
  
    ![Comptes protégés](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_TGTExpiration.png)  
  
5.  Pour restreindre la sélection d'appareils du compte d'utilisateur, cliquez sur **Modifier** afin de définir les conditions qui sont nécessaires pour l'appareil.  
  
    ![Comptes protégés](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_EditAuthNPolicy.gif)  
  
6.  Dans la fenêtre **Modifier les conditions de contrôle d'accès** , cliquez sur **Ajouter une condition**.  
  
    ![Comptes protégés](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_AddCondition.png)  
  
##### <a name="add-computer-account-or-group-conditions"></a>Ajouter le compte d'ordinateur ou les conditions du groupe  
  
1.  Pour configurer les comptes d'ordinateur ou les groupes, dans la liste déroulante, sélectionnez la zone de liste déroulante **Membre de chaque** , puis modifiez **Membre de n'importe lequel**.  
  
    ![Comptes protégés](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_AddCompMember.png)  
  
    > [!NOTE]  
    > Ce contrôle d'accès définit les conditions de l'appareil ou de l'hôte à partir duquel l'utilisateur s'authentifie. Dans la terminologie du contrôle d'accès, le compte d'ordinateur de l'appareil ou de l'hôte est l'utilisateur, ce qui explique qu' **Utilisateur** soit la seule option.  
  
2.  Cliquez sur **Ajouter des éléments**.  
  
    ![Comptes protégés](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_AddCompAddItems.png)  
  
3.  Pour modifier les types d'objets, cliquez sur **Types d'objets**.  
  
    ![Comptes protégés](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_ChangeObjects.gif)  
  
4.  Pour sélectionner les objets d'ordinateur dans Active Directory, cliquez sur **Ordinateurs**, puis sur **OK**.  
  
    ![Comptes protégés](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_ChangeObjectsComputers.gif)  
  
5.  Tapez le nom des ordinateurs pour restreindre l'utilisateur, puis cliquez sur **Vérifier les noms**.  
  
    ![Comptes protégés](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_ChangeObjectsCompName.gif)  
  
6.  Cliquez sur OK et créez une autre condition pour le compte d'ordinateur.  
  
    ![Comptes protégés](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_AddCompAddConditions.png)  
  
7.  Une fois terminé, cliquez sur **OK** et les conditions définies apparaîtront pour le compte d'ordinateur.  
  
    ![Comptes protégés](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_AddCompDone.png)  
  
##### <a name="add-computer-claim-conditions"></a>Ajouter des conditions de revendication d'ordinateur  
  
1.  Pour configurer des revendications d'ordinateur, déroulez le groupe pour sélectionner la revendication.  
  
    ![Comptes protégés](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_CompClaim.gif)  
  
    Les revendications sont uniquement disponibles si elles sont déjà déployées dans la forêt.  
  
2.  Tapez le nom de l'unité d'organisation, auprès de laquelle le compte d'utilisateur peut uniquement s'authentifier.  
  
    ![Comptes protégés](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_CompClaimOUName.gif)  
  
3.  Une fois terminé, cliquez sur OK et la zone affichera les conditions définies.  
  
    ![Comptes protégés](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_CompClaimComplete.gif)  
  
##### <a name="troubleshoot-missing-computer-claims"></a>Résoudre les problèmes liés aux revendications d'ordinateur  
Si la revendication a été déployée, mais qu'elle n'est pas disponible, elle est peut être uniquement configurée pour les classes **Ordinateur** .  
  
Supposons que vous vouliez restreindre l’authentification basée sur l’unité d’organisation (UO) de l’ordinateur, ce qui a déjà été configuré, mais uniquement pour les **ordinateur** classes.  
  
![Comptes protégés](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_RestrictComputers.gif)  
  
Pour que la revendication soit disponible et que vous puissiez restreindre l'authentification de l'utilisateur sur l'appareil, cochez la case **Utilisateur**.  
  
![Comptes protégés](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_RestrictUsersComputers.gif)  
  
#### <a name="provision-a-user-account-with-an-authentication-policy-with-adac"></a>Déployer un compte d'utilisateur avec une stratégie d'authentification à l'aide d'ADAC  
  
1.  À partir du compte **Utilisateur**, cliquez sur **Stratégie**.  
  
    ![Comptes protégés](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_UserPolicy.gif)  
  
2.  Cochez la case **Affectez une stratégie d'authentification à ce compte**.  
  
    ![Comptes protégés](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_UserPolicyAssign.gif)  
  
3.  Sélectionnez ensuite la stratégie d'authentification à appliquer à l'utilisateur.  
  
    ![Comptes protégés](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_UserPolicySelect.png)  
  
#### <a name="configure-dynamic-access-control-support-on-devices-and-hosts"></a>Configurer la prise en charge du contrôle d'accès dynamique sur les appareils et les hôtes  
Vous pouvez configurer les durées de vie TGT sans configurer le contrôle d'accès dynamique. Le contrôle d'accès dynamique est uniquement nécessaire pour la vérification AllowedToAuthenticateFrom et AllowedToAuthenticateTo.  
  
À l'aide de la stratégie de groupe ou de l'Éditeur de stratégie de groupe locale, activez **Prise en charge par le client Kerberos des revendications, de l'authentification composée et du blindage Kerberos** Configuration ordinateur | Modèles d'administration | Système | Kerberos :  
  
![Comptes protégés](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_KerbClientDACSupport.gif)  
  
### <a name="BKMK_TroubleshootAuthnPolicies"></a>Résoudre les problèmes de stratégies d’authentification  
  
#### <a name="determine-the-accounts-that-are-directly-assigned-an-authentication-policy"></a>Déterminer les comptes auxquels est directement affectée une stratégie d'authentification  
La section des comptes de la stratégie d'authentification illustre les comptes qui ont directement appliqué la stratégie.  
  
![Comptes protégés](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_AccountsAssigned.gif)  
  
#### <a name="use-the-authentication-policy-failures---domain-controller-administrative-log"></a>Utiliser les échecs de stratégie d’authentification - journal d’administration du contrôleur de domaine  
Un nouveau **échecs de stratégie d’authentification : contrôleur de domaine** journal d’administration sous **journaux des Applications et Services** > **Microsoft**  >  **Windows** > **authentification** a été créé pour faciliter la détection d’échecs liés aux stratégies d’authentification. Le journal est désactivé par défaut. Pour l'activer, cliquez avec le bouton droit sur le nom du journal, puis cliquez sur **Activer le journal**. Le contenu des nouveaux événements est très semblable à celui des événements d'audit du ticket de service et de ticket TGT Kerberos. Pour plus d’informations sur ces événements, consultez [Stratégies d’authentification et silos de stratégies d’authentification](https://technet.microsoft.com/library/dn486813.aspx).  
  
### <a name="BKMK_ManageAuthnPoliciesUsingPSH"></a>Gérer les stratégies d’authentification à l’aide de Windows PowerShell  
Cette commande crée une stratégie d’authentification nommée **TestAuthenticationPolicy**. Le paramètre **UserAllowedToAuthenticateFrom** spécifie les appareils à partir desquels les utilisateurs peuvent s'authentifier par une chaîne SDDL dans le fichier « someFile.txt ».  
  
```  
PS C:\> New-ADAuthenticationPolicy testAuthenticationPolicy -UserAllowedToAuthenticateFrom (Get-Acl .\someFile.txt).sddl  
```  
  
Cette commande obtient toutes les stratégies d'authentification qui correspondent au filtre spécifié par le paramètre **Filter**.  
  
```  
PS C:\> Get-ADAuthenticationPolicy -Filter "Name -like 'testADAuthenticationPolicy*'" -Server Server02.Contoso.com  
  
```  
  
Cette commande modifie la description et les propriétés **UserTGTLifetimeMins** de la stratégie d'authentification spécifiée.  
  
```  
PS C:\> Set-ADAuthenticationPolicy -Identity ADAuthenticationPolicy1 -Description "Description" -UserTGTLifetimeMins 45  
```  
  
Cette commande supprime la stratégie d'authentification spécifiée par le paramètre **Identity**.  
  
```  
PS C:\> Remove-ADAuthenticationPolicy -Identity ADAuthenticationPolicy1  
```  
  
Cette commande utilise l’applet de commande **Get-ADAuthenticationPolicy** avec le paramètre **Filter** pour obtenir toutes les stratégies d’authentification qui ne sont pas appliquées. Le jeu de résultats est dirigé vers l'applet de commande **Remove-ADAuthenticationPolicy**.  
  
```  
PS C:\> Get-ADAuthenticationPolicy -Filter 'Enforce -eq $false' | Remove-ADAuthenticationPolicy  
```  
  
## <a name="BKMK_CreateAuthNPolicySilos"></a>Silos de stratégies  
Il s'agit d'un nouveau conteneur (objectClass msDS-AuthNPolicySilos) des services de domaine Active Directory (AD DS) pour les comptes d'utilisateur, d'ordinateur et de service. Ces silos permettent de protéger des comptes à valeur élevée. Toutes les organisations doivent protéger les membres des groupes Administrateurs d'entreprise, Admins de domaine et Administrateurs de schéma car ces comptes peuvent être utilisés par une personne malveillante pour accéder n'importe où dans la forêt, mais d'autres comptes ont également besoin d'une protection.  
  
Certaines organisations isolent les charges de travail en créant des comptes qui leur sont uniques et en appliquant des paramètres de stratégie de groupe pour limiter l'ouverture de session interactive locale et distante et les privilèges d'administration. Les silos de stratégies d'authentification complètent ce travail en créant un moyen de définir une relation entre les comptes d'utilisateur, d'ordinateur et de service administrés. Ces comptes n'appartiennent qu'à un seul silo. Vous pouvez configurer la stratégie d'authentification pour chaque type de compte pour contrôler :  
  
1.  la durée de vie TGT non renouvelable ;  
  
2.  les conditions de contrôle d'accès pour renvoyer le ticket TGT (Remarque : ne peut s'appliquer aux systèmes car le blindage Kerberos est nécessaire) ;  
  
3.  les conditions de contrôle d'accès pour retourner le ticket de service.  
  
De plus, les comptes figurant dans un silo de stratégies d'authentification comportent une revendication de silo, qui peut être utilisée par les ressources prenant en charge les revendications telles que les serveurs de fichiers pour contrôler l'accès.  
  
Un nouveau descripteur de sécurité peut être configuré pour contrôler l'émission du ticket de service en fonction de :  
  
-   Utilisateur, les groupes de sécurité de l’utilisateur et/ou les revendications de l’utilisateur  
  
-   APPAREIL, les groupe de sécurité de l’appareil et/ou les revendications de l’appareil  
  
Obtention de ces informations aux contrôleurs de domaine de la ressource nécessite le contrôle d’accès dynamique :  
  
-   Revendications d'utilisateur :  
  
    -   Clients Windows 8 et version ultérieure prenant en charge le contrôle d'accès dynamique  
  
    -   Le domaine de compte prend en charge le contrôle d'accès dynamique et les revendications  
  
-   Appareil et/ou groupe de sécurité de l'appareil :  
  
    -   Clients Windows 8 et version ultérieure prenant en charge le contrôle d'accès dynamique  
  
    -   Ressource configurée pour l'authentification composée  
  
-   Revendications de périphérique :  
  
    -   Clients Windows 8 et version ultérieure prenant en charge le contrôle d'accès dynamique  
  
    -   Le domaine d'appareil prend en charge le contrôle d'accès dynamique et les revendications  
  
    -   Ressource configurée pour l'authentification composée  
  
Les stratégies d'authentification peuvent être appliquées à tous les membres d'un silo plutôt qu'à des comptes individuels, ou des stratégies d'authentification distinctes peuvent être appliquées à différents types de comptes à l'intérieur d'un silo. Par exemple, une stratégie d'authentification peut être appliquée à des comptes d'utilisateur dotés de privilèges élevés tandis qu'une autre stratégie peut être appliquée à des comptes de service. Au moins une stratégie d'authentification doit être créée avant qu'un silo de stratégies d'authentification ne puisse l'être.  
  
> [!NOTE]  
> Une stratégie d'authentification peut être appliquée aux membres d'un silo de stratégies d'authentification. Elle peut être aussi appliquée indépendamment des silos pour restreindre l'étendue du compte spécifique. Par exemple, pour protéger un compte unique ou un petit ensemble de comptes, vous pouvez définir une stratégie sur ces comptes sans ajouter les comptes à un silo.  
  
Vous pouvez créer un silo de stratégies d’authentification à l’aide de centre d’administration Active Directory ou Windows PowerShell. Par défaut, un silo de stratégies d’authentification uniquement des audits de stratégies de silos, ce qui équivaut à spécifier le **WhatIf** paramètre dans les applets de commande Windows PowerShell. Dans ce cas, les restrictions du silo de stratégies ne s'appliquent pas, mais les audits sont générés pour indiquer si des échecs se produisent quand les restrictions sont appliquées.  
  
#### <a name="to-create-an-authentication-policy-silo-by-using-active-directory-administrative-center"></a>Pour créer un silo de stratégies d'authentification en utilisant le Centre d'administration Active Directory  
  
1.  Ouvrez **Centre d'administration Active Directory**, cliquez sur **Authentification**, cliquez avec le bouton droit sur **Silos de stratégies d'authentification**, cliquez sur **Nouveau**, puis sur **Silo de stratégies d'authentification**.  
  
    ![Comptes protégés](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_CreateNewAuthNPolicySilo.gif)  
  
2.  Dans **Nom d'affichage**, tapez le nom du silo. Dans **Comptes autorisés**, cliquez sur **Ajouter**, tapez le nom des comptes, puis cliquez sur **OK**. Vous pouvez spécifier les utilisateurs, les ordinateurs ou les comptes de service. Indiquez ensuite si vous allez utiliser une stratégie unique pour tous les principaux ou une stratégie distincte pour chaque type de principal, et le nom de la ou des stratégies.  
  
    ![Comptes protégés](../media/how-to-configure-protected-accounts/ADDS_ProtectAcct_NewAuthNPolicySiloDisplayName.gif)  
  
### <a name="BKMK_ManageAuthnSilosUsingPSH"></a>Gérer les silos de stratégies à l’aide de Windows PowerShell  
Cette commande crée un objet de silo de stratégies d'authentification et l'applique.  
  
```  
PS C:\>New-ADAuthenticationPolicySilo -Name newSilo -Enforce  
```  
  
Cette commande obtient tous les silos de stratégies d’authentification qui correspondent au filtre spécifié par le paramètre **Filter** . La sortie est alors transmise à l’applet de commande **Format-Table** pour afficher le nom de la stratégie et la valeur appliquée ( **Enforce** ) à chaque stratégie.  
  
```  
PS C:\>Get-ADAuthenticationPolicySilo -Filter 'Name -like "*silo*"' | Format-Table Name, Enforce -AutoSize  
  
Name  Enforce  
--  ----  
silo     True  
silos   False  
  
```  
  
Cette commande utilise l’applet de commande **Get-ADAuthenticationPolicySilo** avec le paramètre **Filter** pour obtenir tous les silos de stratégies d’authentification qui ne sont pas appliqués et diriger le résultat du filtre vers l’applet de commande **Remove-ADAuthenticationPolicySilo** .  
  
```  
PS C:\>Get-ADAuthenticationPolicySilo -Filter 'Enforce -eq $False' | Remove-ADAuthenticationPolicySilo  
```  
  
Cette commande octroie l'accès au silo de stratégies d'authentification nommé *Silo* au compte d'utilisateur *User01*.  
  
```  
PS C:\>Grant-ADAuthenticationPolicySiloAccess -Identity Silo -Account User01  
```  
  
Cette commande révoque l'accès au silo de stratégies d'authentification nommé *Silo* pour le compte d'utilisateur *User01*. Le paramètre **Confirm** ayant la valeur **$False**, aucun message de confirmation n’apparaît.  
  
```  
PS C:\>Revoke-ADAuthenticationPolicySiloAccess -Identity Silo -Account User01 -Confirm:$False  
```  
  
Cet exemple utilise d’abord l’applet de commande **Get-ADComputer** pour obtenir tous les comptes d’ordinateur correspondant au filtre spécifié par le paramètre **Filter** . La sortie de cette commande est transmise à **Set-ADAccountAuthenticatinPolicySilo** pour leur affecter le silo de stratégies d’authentification *Silo* et la stratégie d’authentification *AuthenticationPolicy02* .  
  
```  
PS C:\>Get-ADComputer -Filter 'Name -like "newComputer*"' | Set-ADAccountAuthenticationPolicySilo -AuthenticationPolicySilo Silo -AuthenticationPolicy AuthenticationPolicy02  
```  
  

