---
title: "Déployer Dossiers de travail avec ADFS et le proxy d’application Web: Étape5, configurer les clients"
ms.prod: windows-server-threshold
ms.technology: storage-work-folders
ms.topic: article
manager: klaasl
ms.author: jeffpatt
author: JeffPatt24
ms.date: 4/5/2017
ms.assetid: f168292b-0dbc-44b9-965f-d480e5134a0c
ms.openlocfilehash: fa8b2b15ff411a59b28308a329d7ca2341ef0886
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/17/2017
---
# <a name="deploy-work-folders-with-ad-fs-and-web-application-proxy-step-5-set-up-clients"></a>Déployer Dossiers de travail avec ADFS et le proxy d’application Web: étape5, configurer les clients

>S’applique à: WindowsServer (canal semi-annuel), WindowsServer2016

Cette rubrique décrit la cinquième étape de déploiement de dossiers de travail avec les services de fédération ActiveDirectory (ADFS) et le proxy d’application Web. Vous pouvez trouver les autres étapes de ce processus dans ces rubriques:  
  
-   [Déployer Dossiers de travail avec ADFS et le proxy d’application Web: vue d’ensemble](deploy-work-folders-adfs-overview.md)  
  
-   [Déployer Dossiers de travail avec ADFS et le proxy d’application Web: étape1, configurer ADFS](deploy-work-folders-adfs-step1.md)  
  
-   [Déployer Dossiers de travail avec ADFS et le proxy d’application Web: étape2, tâches post-configuration ADFS](deploy-work-folders-adfs-step2.md)  
  
-   [Déployer Dossiers de travail avec ADFS et le proxy d’application Web: étape3, configurer les dossiers de travail](deploy-work-folders-adfs-step3.md)  
  
-   [Déployer Dossiers de travail avec ADFS et le proxy d’application Web: étape4, configurer le proxy d’application Web](deploy-work-folders-adfs-step4.md)  
  
Utilisez les procédures suivantes pour configurer les clients Windows joints au domaine et ceux qui ne sont pas joints au domaine. Vous pouvez utiliser ces clients pour tester si les fichiers se synchronisent correctement avec les dossiers de travail des clients.  
  
## <a name="set-up-a-domain-joined-client"></a>Configurer un client joint au un domaine  
  
### <a name="install-the-ad-fs-and-work-folder-certificates"></a>Installer les certificats ADFS et des dossiers de travail  
Vous devez installer les certificats ADFS et des dossiers de travail que vous avez créés précédemment dans le magasin de certificats d’un ordinateur local sur l’ordinateur client joint au domaine.  
  
Étant donné que vous installez des certificats auto-signés qui ne permettent pas que l’on remonte à un éditeur dans le magasin de certificats Autorités de Certification racine de confiance, vous devez également copier les certificats vers ce magasin.  
  
Pour installer les certificats, procédez comme suit:  
  
1.  Cliquez sur **Démarrer**, puis sur **Exécuter**.  
  
2.  Tapez **MMC**.  
  
3.  Dans le menu **Fichier**, cliquez sur **Ajouter/Supprimer un composant logiciel enfichable**.  
  
4.  Dans la zone **Composants logiciels enfichables disponibles**, cliquez sur **Certificats**, puis sur **Ajouter**. L’Assistant de composant logiciel enfichable Certificats démarre.  
  
5.  Sélectionnez **Un compte d’ordinateur**, puis cliquez sur **Suivant**.  
  
6.  Sélectionnez **Ordinateur local (l’ordinateur sur lequel cette console s’exécute)**, puis cliquez sur **Terminer**.  
  
7.  Cliquez sur **OK**.  
  
8.  Développez le dossier Racine de la console\Certificats\(Ordinateur local)\Personnel\Certificats.  
  
9. Cliquez avec le bouton droit sur **Certificats**, cliquez sur **Toutes les tâches**, puis cliquez sur **Importer**.  
  
10. Accédez au dossier contenant le certificat ADFS et suivez les instructions de l’Assistant pour importer le fichier et le placer dans le magasin de certificats.  
  
11. Répétez les étapes9 et 10, cette fois en accédant au certificat de dossiers de travail et en l’important.  
  
12. Développez le dossier Racine de la console\Certificats\(Ordinateur local)\Autorités de certification racines de confiance\Certificats.  
  
13. Cliquez avec le bouton droit sur **Certificats**, cliquez sur **Toutes les tâches**, puis cliquez sur **Importer**.  
  
14. Accédez au dossier contenant le certificat ADFS et suivez les instructions de l’Assistant pour importer le fichier et le placer dans le magasin des autorités de certification racines de confiance.  
  
15. Répétez les étapes13 et 14, cette fois en accédant au certificat de dossiers de travail et en l’important.  
  
### <a name="configure-work-folders-on-the-client"></a>Configurer des dossiers de travail sur le client  
Pour configurer les dossiers de travail sur l’ordinateur client, procédez comme suit:  
  
1.  Sur l’ordinateur client, ouvrez le **Panneau de configuration** et cliquez sur **Dossiers de travail**.  
  
2.  Cliquez sur **Configurer Dossiers de travail**.  
  
3.  Dans la page **Entrez votre adresse e-mail professionnelle**, entrez l’adresse e-mail de l’utilisateur (par exemple, user@contoso.com) ou l’URL des dossiers de travail (dans l’exemple de test, https://workfolders.contoso.com), puis cliquez sur **Suivant**.  
  
4.  Si l’utilisateur est connecté au réseau d’entreprise, l’authentification est effectuée par l’authentification intégrée de Windows. Si l’utilisateur n’est pas connecté au réseau d’entreprise, l’authentification est effectuée par ADFS (OAuth) et on invitera l’utilisateur à fournir des informations d’identification. Entrez vos informations d’utilisation, puis cliquez sur **OK**.  
  
5.  Une fois que vous êtes authentifié, la page **Présentation des dossiers de travail** s’affiche, où vous pouvez éventuellement modifier l’emplacement du répertoire des dossiers de travail. Cliquez sur **Suivant**.  
  
6.  La page **Stratégies de sécurité** répertorie les stratégies de sécurité que vous avez configurées pour les dossiers de travail. Cliquez sur **Suivant**.  
  
7.  Un message s’affiche indiquant que les dossiers de travail ont démarré leur synchronisation avec votre PC. Cliquez sur **Fermer**.  
  
8.  La page **Gérer les dossiers de travail** affiche la quantité d’espace disponible sur le serveur, l’état de la synchronisation et ainsi de suite. Si nécessaire, vous pouvez entrer vos informations d’identification à nouveau ici. Fermez la fenêtre.  
  
9. Votre dossier de dossiers de travail s’ouvre automatiquement. Vous pouvez ajouter du contenu à ce dossier pour le synchroniser entre vos appareils.  
  
    Dans le cadre de l’exemple de test, ajoutez un fichier de test à ce dossier Dossiers de travail. Après avoir configuré les dossiers de travail sur l’ordinateur non joint au domaine, vous serez en mesure de synchroniser des fichiers entre les dossiers de travail de chaque ordinateur.  
  
## <a name="set-up-a-non-domain-joined-client"></a>Configurer un client non joint au domaine  
  
### <a name="install-the-ad-fs-and-work-folder-certificates"></a>Installer les certificats ADFS et des dossiers de travail  
Installer les certificats ADFS et des dossiers de travail sur l’ordinateur non joint au domaine, à l’aide de la même procédure que vous avez utilisée pour l’ordinateur joint au domaine.  
  
### <a name="update-the-hosts-file"></a>Mettre à jour le fichier hôtes  
Le fichier hôtes sur le client non joint au domaine doit être mis à jour pour l’environnement de test, car aucun enregistrement DNS public n’a été créé pour les dossiers de travail. Ajoutez ces entrées dans le fichier hôtes:  
  
-  workfolders.domaine  
  
-  Service ADFS nom.domaine  
  
-  enterpriseregistration.domain  
  
Dans l’exemple de test, utilisez ces valeurs:  
  
-  **10.0.0.10 workfolders.contoso.com**  
  
-  **10.0.0.10 blueadfs.contoso.com**  
  
-  **10.0.0.10 enterpriseregistration.contoso.com**  
  
### <a name="configure-work-folders-on-the-client"></a>Configurer des dossiers de travail sur le client  
Configurez les dossiers de travail sur l’ordinateur non joint au domaine à l’aide de la même procédure que vous avez utilisée pour l’ordinateur joint au domaine.  
  
Lorsque le nouveau dossier dossiers de travail s’ouvre sur ce client, vous pouvez voir que le fichier à de l’ordinateur joint au domaine a déjà été synchronisé à l’ordinateur non joint au domaine. Vous pouvez commencer à ajouter du contenu au dossier pour le synchroniser entre vos appareils.  
  
La procédure de déploiement de dossiers de travail, ADFS et le proxy d’application Web via l’interface utilisateur de Windows Server est terminée.  
  
## <a name="see-also"></a>Voir aussi  
[Vue d’ensemble des Dossiers de travail](Work-Folders-Overview.md)  
  

