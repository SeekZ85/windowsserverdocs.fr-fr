---
ms.assetid: f643099e-f9c6-476f-9378-5a9228c39b33
title: "Annexe E - sécurisation des groupes d’administrateurs de l’entreprise dans Active Directory"
description: 
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: 714bc0ab3fe15d09f4ccabb3f35d9b4519e5459c
ms.sourcegitcommit: 70c1b6cedad55b9c7d2068c9aa4891c6c533ee4c
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/03/2017
---
# <a name="appendix-e-securing-enterprise-admins-groups-in-active-directory"></a>Annexe e: sécurisation des groupes d’administrateurs de l’entreprise dans ActiveDirectory

>S’applique à: Windows Server2016, Windows Server2012R2, Windows Server2012


## <a name="appendix-e-securing-enterprise-admins-groups-in-active-directory"></a>Annexe e: sécurisation des groupes d’administrateurs de l’entreprise dans ActiveDirectory  
Le groupe Administrateurs de l’entreprise (EA), qui est hébergé dans le domaine racine de forêt, ne doit contenir aucun utilisateur sur une base quotidienne, à l’exception du compte d’administrateur du domaine racine, à condition qu’il est sécurisé comme décrit dans [annexe d: sécurisation des comptes d’administrateur intégrés dans Active Directory](../../../ad-ds/plan/security-best-practices/Appendix-D--Securing-Built-In-Administrator-Accounts-in-Active-Directory.md).  

Administrateurs de l’entreprise sont, par défaut, les membres du groupe Administrateurs dans chaque domaine dans la forêt. Vous ne devez pas supprimer le groupe EA des groupes d’administrateurs dans chaque domaine, car en cas d’un scénario de récupération d’urgence forêt, droits EA sera probablement requises. Groupe d’administrateurs de l’entreprise de la forêt doit être sécurisé comme décrit dans les instructions pas à pas qui suivent.  

Pour le groupe Administrateurs de l’entreprise dans la forêt:  

1.  Dans la stratégie de groupe liés aux unités d’organisation contenant des serveurs membres et les stations de travail dans chaque domaine, le groupe Administrateurs de l’entreprise doit être ajouté aux droits d’utilisateur suivants dans **ordinateur Configuration ordinateur\Stratégies\Paramètres Windows\Paramètres sécurité\Stratégies Settings\nom droits**:  

    -   Refuser l’accès à cet ordinateur à partir du réseau  

    -   Refuse la connexion en tant que tâche  

    -   Refuse la connexion en tant que service  

    -   Refuse la connexion locale  

    -   Refuse la connexion par le biais des Services Bureau à distance  

2.  Configurez l’audit pour envoyer des alertes si des modifications sont apportées aux propriétés ou l’appartenance au groupe Administrateurs de l’entreprise.  

### <a name="step-by-step-instructions-for-removing-all-members-from-the-enterprise-admins-group"></a>Obtenir des Instructions détaillées sur la suppression de tous les membres du groupe d’administrateurs de l’entreprise  

1.  Dans **le Gestionnaire de serveur**, cliquez sur **outils**, puis cliquez sur **Active Directory Users and Computers**.  

2.  Si vous ne gérez pas le domaine racine de la forêt, dans l’arborescence de la console, faites un clic droit <Domain>, puis cliquez sur **changer de domaine** (où <Domain> est le nom du domaine que vous êtes en train d’administrer).  

    ![sécuriser les groupes d’administrateurs entreprise](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_43.gif)  

3.  Dans le **changer de domaine** boîte de dialogue, cliquez sur **Parcourir**, sélectionnez le domaine racine de la forêt, puis cliquez sur **OK**.  

    ![sécuriser les groupes d’administrateurs entreprise](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_44.gif)  

4.  Pour supprimer tous les membres du groupe EA:  

    1.  Double-cliquez sur le **administrateurs de l’entreprise** de groupe, puis cliquez sur le **membres** onglet.  

        ![sécuriser les groupes d’administrateurs entreprise](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_45.gif)  

    2.  Sélectionnez un membre du groupe, cliquez sur **supprimer**, cliquez sur **Oui**, puis cliquez sur **OK**.  

5.  Répétez l’étape 2 jusqu'à ce que tous les membres du groupe EA ont été supprimés.  

### <a name="step-by-step-instructions-to-secure-enterprise-admins-in-active-directory"></a>Obtenir des Instructions pas à pas pour sécuriser les administrateurs de l’entreprise dans Active Directory  

1.  Dans **le Gestionnaire de serveur**, cliquez sur **outils**, puis cliquez sur **gestion des stratégies de groupe**.  

2.  Dans l’arborescence de la console, développez <Forest>\Domains\\<Domain>, puis **objets de stratégie de groupe** (où <Forest>est le nom de la forêt et <Domain>est le nom du domaine dans lequel vous souhaitez définir la stratégie de groupe).  

    > [!NOTE]  
    > Dans une forêt qui contient plusieurs domaines, un objet de stratégie de groupe similaire doit être créé dans chaque domaine que le groupe Administrateurs de l’entreprise soit sécurisé.  

3.  Dans l’arborescence de la console, cliquez sur **objets de stratégie de groupe**, puis cliquez sur **New**.  

    ![sécuriser les groupes d’administrateurs entreprise](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_46.gif)  

4.  Dans le **nouvel objet GPO** boîte de dialogue, tapez <GPO Name>, puis cliquez sur **OK** (où <GPO Name> est le nom de cet objet de stratégie de groupe).  

    ![sécuriser les groupes d’administrateurs entreprise](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_47.gif)  

5.  Dans le volet d’informations, cliquez sur <GPO Name>, puis cliquez sur **modifier**.  

6.  Accédez à **Configuration ordinateur\Stratégies\Paramètres Windows\Paramètres de Sécurité\stratégies**, puis cliquez sur **attribution des droits utilisateur**.  

    ![sécuriser les groupes d’administrateurs entreprise](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_48.gif)  

7.  Configurez les droits d’utilisateur pour empêcher les membres du groupe Administrateurs de l’entreprise d’accéder à des serveurs membres et les stations de travail sur le réseau en procédant comme suit:  

    1.  Double-cliquez sur **refuser l’accès à cet ordinateur à partir du réseau** et sélectionnez **définir ces paramètres de stratégie**.  

    2.  Cliquez sur **ajouter un utilisateur ou groupe** et cliquez sur **Parcourir**.  

    3.  Type **administrateurs de l’entreprise**, cliquez sur **vérifier les noms**, puis cliquez sur **OK**.  

        ![sécuriser les groupes d’administrateurs entreprise](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_49.gif)  

    4.  Cliquez sur **OK**, et **OK** à nouveau.  

8.  Configurez les droits d’utilisateur pour empêcher les membres du groupe Administrateurs de l’entreprise à partir de l’ouverture de session en tant que traitement par lots en procédant comme suit:  

    1.  Double-cliquez sur **refuse la connexion en tant que traitement par lots** et sélectionnez **définir ces paramètres de stratégie**.  

    2.  Cliquez sur **ajouter un utilisateur ou groupe** et cliquez sur **Parcourir**.  

        > [!NOTE]  
        > Dans une forêt qui contient plusieurs domaines, cliquez sur **emplacements** et sélectionnez le domaine racine de la forêt.  

    3.  Type **administrateurs de l’entreprise**, cliquez sur **vérifier les noms**, puis cliquez sur **OK**.  

        ![sécuriser les groupes d’administrateurs entreprise](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_50.gif)  

    4.  Cliquez sur **OK**, et **OK** à nouveau.  

9. Configurez les droits d’utilisateur pour empêcher les membres du groupe EA d’ouverture de session en tant que service en effectuant les opérations suivantes:  

    1.  Double-cliquez sur **journal refuser en tant que service** et sélectionnez **définir ces paramètres de stratégie**.  

    2.  Cliquez sur **ajouter un utilisateur ou groupe** puis cliquez sur **Parcourir**.  

        > [!NOTE]  
        > Dans une forêt qui contient plusieurs domaines, cliquez sur **emplacements** et sélectionnez le domaine racine de la forêt.  

    3.  Type **administrateurs de l’entreprise**, cliquez sur **vérifier les noms**, puis cliquez sur **OK**.  

        ![sécuriser les groupes d’administrateurs entreprise](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_51.gif)  

    4.  Cliquez sur **OK**, et **OK** à nouveau.  

10. Configurez les droits d’utilisateur pour empêcher les membres du groupe Administrateurs de l’entreprise à partir de la session locale sur les serveurs membres et stations de travail en procédant comme suit:  

    1.  Double-cliquez sur **refuse la connexion locale** et sélectionnez **définir ces paramètres de stratégie**.  

    2.  Cliquez sur **ajouter un utilisateur ou groupe** puis cliquez sur **Parcourir**.  

        > [!NOTE]  
        > Dans une forêt qui contient plusieurs domaines, cliquez sur **emplacements** et sélectionnez le domaine racine de la forêt.  

    3.  Type **administrateurs de l’entreprise**, cliquez sur **vérifier les noms**, puis cliquez sur **OK**.  

        ![sécuriser les groupes d’administrateurs entreprise](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_52.gif)  

    4.  Cliquez sur **OK**, et **OK** à nouveau.  

11. Configurez les droits d’utilisateur pour empêcher les membres du groupe Administrateurs de l’entreprise d’accéder à des serveurs membres et les stations de travail via les Services Bureau à distance en effectuant les opérations suivantes:  

    1.  Double-cliquez sur **refuse la connexion par le biais des Services Bureau à distance** et sélectionnez **définir ces paramètres de stratégie**.  

    2.  Cliquez sur **ajouter un utilisateur ou groupe** puis cliquez sur **Parcourir**.  

        > [!NOTE]  
        > Dans une forêt qui contient plusieurs domaines, cliquez sur **emplacements** et sélectionnez le domaine racine de la forêt.  

    3.  Type **administrateurs de l’entreprise**, cliquez sur **vérifier les noms**, puis cliquez sur **OK**.  

        ![sécuriser les groupes d’administrateurs entreprise](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_53.gif)  

    4.  Cliquez sur **OK**, et **OK** à nouveau.  

12. Pour quitter **éditeur de gestion de stratégie de groupe**, cliquez sur **fichier**, puis cliquez sur **quitter**.  

13. Dans **gestion des stratégies de groupe**, liez l’objet de stratégie de groupe pour les serveurs membres et d’une station de travail unités d’organisation en procédant comme suit:  

    1.  Accédez à la <Forest>\Domains\\<Domain> (où <Forest>est le nom de la forêt et <Domain>est le nom du domaine dans lequel vous souhaitez définir la stratégie de groupe).  

    2.  Avec le bouton droit de l’unité d’organisation que l’objet de stratégie de groupe seront appliqués au et cliquez sur **lier un objet de stratégie de groupe existant**.  

        ![sécuriser les groupes d’administrateurs entreprise](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_54.gif)  

    3.  Sélectionnez l’objet de stratégie de groupe que vous venez de créer, cliquez sur **OK**.  

        ![sécuriser les groupes d’administrateurs entreprise](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_55.gif)  

    4.  Créer des liens vers tous les autres unités d’organisation qui contiennent des stations de travail.  

    5.  Créer des liens vers tous les autres unités d’organisation qui contiennent des serveurs membres.  

    6.  Dans une forêt qui contient plusieurs domaines, un objet de stratégie de groupe similaire doit être créé dans chaque domaine que le groupe Administrateurs de l’entreprise soit sécurisé.  

> [!IMPORTANT]  
> Si les serveurs de renvoi sont utilisés pour administrer des contrôleurs de domaine et Active Directory, assurez-vous que les serveurs de renvoi sont trouvent dans une unité d’organisation sur lesquels cette stratégie de groupe n’est pas lié.  

### <a name="verification-steps"></a>Étapes de vérification  

#### <a name="verify-deny-access-to-this-computer-from-the-network-gpo-settings"></a>Vérifier les paramètres de stratégie de groupe «Refuser l’accès à cet ordinateur à partir du réseau»  
À partir de n’importe quel serveur membre ou une station de travail n’est pas affectée par les modifications de stratégie de groupe (par exemple, un «serveur de renvoi»), essayez d’accéder à un serveur membre ou une station de travail sur le réseau qui est affecté par les modifications de stratégie de groupe. Pour vérifier les paramètres de stratégie de groupe, tenter de mapper le lecteur du système à l’aide de la **NET USE** commande en effectuant les étapes suivantes:  

1.  Ouvrez une session localement à l’aide d’un compte qui est membre du groupe EA.  

2.  Avec la souris, déplacez le pointeur dans le coin supérieur droit ou inférieur droit de l’écran. Lorsque le **icônes** barre s’affiche, cliquez sur **recherche**.  

3.  Dans le **recherche**, tapez **invite de commandes**, avec le bouton droit **invite de commandes**, puis cliquez sur **exécuter en tant qu’administrateur** pour ouvrir une invite de commandes avec élévation de privilèges.  

4.  Lorsque vous êtes invité à approuver l’élévation, cliquez sur **Oui**.  

    ![sécuriser les groupes d’administrateurs entreprise](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_56.gif)  

5.  Dans le **invite de commandes** fenêtre, tapez **commande net use \\\<Server Name>\c$**, où <Server Name> est le nom du serveur membre ou de station de travail que vous tentez d’accéder via le réseau.  

6.  La capture d’écran suivante affiche le message d’erreur qui doit apparaître.  

    ![sécuriser les groupes d’administrateurs entreprise](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_57.gif)  

#### <a name="verify-deny-log-on-as-a-batch-job-gpo-settings"></a>Vérifier les paramètres de stratégie de groupe «Refuse la connexion en tant que tâche»  

À partir de n’importe quel serveur membre ou une station de travail affectées par les modifications de stratégie de groupe, ouvrez une session localement.  

##### <a name="create-a-batch-file"></a>Créer un fichier de commandes  

1.  Avec la souris, déplacez le pointeur dans le coin supérieur droit ou inférieur droit de l’écran. Lorsque le **icônes** barre s’affiche, cliquez sur **recherche**.  

2.  Dans le **recherche**, tapez **le bloc-notes**, puis cliquez sur **le bloc-notes**.  

3.  Dans **le bloc-notes**, type **dir c:**.  

4.  Cliquez sur **fichier**, puis cliquez sur **Enregistrer sous**.  

5.  Dans le **fichier** nom, tapez ** <Filename>.bat** (où <Filename> est le nom du nouveau fichier de commandes).  

##### <a name="schedule-a-task"></a>Planifier une tâche  

1.  Avec la souris, déplacez le pointeur dans le coin supérieur droit ou inférieur droit de l’écran. Lorsque le **icônes** barre s’affiche, cliquez sur **recherche**.  

2.  Dans le **recherche** , tapez **le Planificateur de tâches**, puis cliquez sur **le Planificateur de tâches**.  

    > [!NOTE]  
    > Sur les ordinateurs exécutant Windows 8, dans le **recherche** , tapez **planifier des tâches**, puis cliquez sur **planifier des tâches**.  

3.  Cliquez sur **Action**, puis cliquez sur **créer une tâche**.  

4.  Dans le **créer une tâche** boîte de dialogue, tapez ** <Task Name> ** (où <Task Name> est le nom de la nouvelle tâche).  

5.  Cliquez sur le **Actions** onglet, puis cliquez sur **New**.  

6.  Dans le **Action** champ, sélectionnez **démarrer un programme**.  

7.  Sous **programme ou le script**, cliquez sur **Parcourir**, recherchez et sélectionnez le fichier de commandes créé dans le **créer un fichier de commandes** section, puis cliquez sur **ouvrir**.  

8.  Cliquez sur **OK**.  

9. Cliquez sur le **général** onglet.  

10. Dans le **options de sécurité** , cliquez sur **modifier un utilisateur ou groupe**.  

11. Tapez le nom d’un compte qui est membre du groupe EAs, cliquez sur **vérifier les noms**, puis cliquez sur **OK**.  

12. Sélectionnez **exécuter même si l’utilisateur est connecté ou non** et sélectionnez **ne stockent pas de mot de passe**. La tâche n’aura accès aux ressources de l’ordinateur local.  

13. Cliquez sur **OK**.  

14. Une boîte de dialogue doit apparaître, compte d’utilisateur demande des informations d’identification pour exécuter la tâche.  

15. Après avoir entré les informations d’identification, cliquez sur **OK**.  

16. Une boîte de dialogue semblable à la suivante doit apparaître.  

    ![sécuriser les groupes d’administrateurs entreprise](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_58.gif)  

#### <a name="verify-deny-log-on-as-a-service-gpo-settings"></a>Vérifier les paramètres de stratégie de groupe «Refuse la connexion en tant que service»  

1.  À partir de n’importe quel serveur membre ou une station de travail affectées par les modifications de stratégie de groupe, ouvrez une session localement.  

2.  Avec la souris, déplacez le pointeur dans le coin supérieur droit ou inférieur droit de l’écran. Lorsque le **icônes** barre s’affiche, cliquez sur **recherche**.  

3.  Dans le **recherche** , tapez **services**, puis cliquez sur **Services**.  

4.  Recherchez et double-cliquez sur **spouleur d’impression**.  

5.  Cliquez sur le **ouverture de session** onglet.  

6.  Sous **ouvrir une session en tant que**, sélectionnez **ce compte**.  

7.  Cliquez sur **Parcourir**, tapez le nom d’un compte qui est membre du groupe EAs, cliquez sur **vérifier les noms**, puis cliquez sur **OK**.  

8.  Sous **mot de passe:** et **confirmer le mot de passe**, tapez le mot de passe du compte sélectionné, puis cliquez sur **OK**.  

9. Cliquez sur **OK** trois fois de plus.  

10. Avec le bouton droit le **spouleur d’impression** de service et sélectionnez **redémarrer**.  

11. Lorsque le service est redémarré, une boîte de dialogue semblable au suivant doit s’afficher.  

    ![sécuriser les groupes d’administrateurs entreprise](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_59.gif)  

#### <a name="revert-changes-to-the-printer-spooler-service"></a>Annuler les modifications pour le Service Spouleur d’imprimante  

1.  À partir de n’importe quel serveur membre ou une station de travail affectées par les modifications de stratégie de groupe, ouvrez une session localement.  

2.  Avec la souris, déplacez le pointeur dans le coin supérieur droit ou inférieur droit de l’écran. Lorsque le **icônes** barre s’affiche, cliquez sur **recherche**.  

3.  Dans le **recherche** , tapez **services**, puis cliquez sur **Services**.  

4.  Recherchez et double-cliquez sur **spouleur d’impression**.  

5.  Cliquez sur le **ouverture de session** onglet.  

6.  Sous **ouvrir une session en tant que**, sélectionnez le **système Local** de compte, puis cliquez sur **OK**.  

#### <a name="verify-deny-log-on-locally-gpo-settings"></a>Vérifier les paramètres de stratégie de groupe «Interdire l’ouverture d’une session locale»  

1.  À partir de n’importe quel serveur membre ou une station de travail affectées par les modifications de stratégie de groupe, tentent de se connecter localement à l’aide d’un compte qui est membre du groupe EA. Une boîte de dialogue semblable à la suivante doit apparaître.  

    ![sécuriser les groupes d’administrateurs entreprise](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_60.gif)  

#### <a name="verify-deny-log-on-through-remote-desktop-services-gpo-settings"></a>Vérifier les paramètres de stratégie de groupe «Refuse la connexion par le biais des Services Bureau à distance»  

1.  Avec la souris, déplacez le pointeur dans le coin supérieur droit ou inférieur droit de l’écran. Lorsque le **icônes** barre s’affiche, cliquez sur **recherche**.  

2.  Dans le **recherche** , tapez **connexion Bureau à distance**, puis cliquez sur **connexion Bureau à distance**.  

3.  Dans le **ordinateur** , tapez le nom de l’ordinateur que vous souhaitez vous connecter à, puis cliquez sur **Connect**. (Vous pouvez également taper l’adresse IP au lieu du nom d’ordinateur).  

4.  Lorsque vous y êtes invité, fournissez les informations d’identification d’un compte qui est membre du groupe EA.  

5.  Une boîte de dialogue semblable à la suivante doit apparaître.  

    ![sécuriser les groupes d’administrateurs entreprise](media/Appendix-E--Securing-Enterprise-Admins-Groups-in-Active-Directory/SAD_61.gif)  
