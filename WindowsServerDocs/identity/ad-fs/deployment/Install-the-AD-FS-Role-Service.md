---
ms.assetid: c28a1b8b-5bec-4eed-8c95-a1a29cfc957c
title: Installer le service de rôle AD FS
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 9851134d1ad73092ee44c34c99bc2d873d20ca07
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59831170"
---
# <a name="install-the-ad-fs-role-service"></a>Installer le service de rôle AD FS

>S'applique à : Windows Server 2016, Windows Server 2012 R2

Vous pouvez utiliser la procédure suivante pour installer le service de rôle AD FS sur un ordinateur qui exécute Windows Server 2012 R2 pour devenir le premier serveur de fédération dans une batterie de serveurs de fédération ou un serveur de fédération dans une batterie de serveurs de fédération existante.  
  
L’appartenance au **administrateurs**, ou équivalente, sur l’ordinateur local est la configuration minimale requise pour effectuer cette procédure.  Examinez les informations relatives à l’utilisation des comptes et des appartenances au groupe appropriés dans la rubrique [Groupes locaux et de domaine par défaut](https://go.microsoft.com/fwlink/?LinkId=83477).   
  
### <a name="to-install-the-ad-fs-server-role-via-the-add-roles-and-features-wizard"></a>Pour installer le rôle de serveur AD FS via l’Assistant Ajout de rôles et fonctionnalités  
  
1.  Ouvrez le Gestionnaire de serveur. Pour ouvrir le Gestionnaire de serveur, cliquez sur **le Gestionnaire de serveur** sur le **Démarrer** écran, ou **le Gestionnaire de serveur** dans la barre des tâches sur le bureau. Sous l’onglet **Démarrage rapide** de la vignette **Bienvenue** dans la page **Tableau de bord**, cliquez sur **Ajouter des rôles et des fonctionnalités**. Vous pouvez également cliquer sur **Ajouter des rôles et fonctionnalités** dans le menu **Gérer** .  
  
2.  Dans la page **Avant de commencer** , cliquez sur **Suivant**.  
  
3.  Sur le **sélectionner type d’installation** , cliquez sur **rôle\-ou une fonctionnalité\-installation basée sur un**, puis cliquez sur **suivant**.  
  
4.  Dans la page **Sélectionner le serveur de destination** , cliquez sur **Sélectionner un serveur du pool de serveurs**, vérifiez que l'ordinateur cible est sélectionné, puis cliquez sur **Suivant**.  
  
5.  Dans la page **Sélectionner des rôles de serveurs** , cliquez sur **Services AD FS (Active Directory Federation Services)**, puis cliquez sur **Suivant**.  
  
6.  Dans la page **Sélectionner les fonctionnalités** , cliquez sur **Suivant**. Les conditions préalables requises sont présélectionnées pour vous. Il est inutile de sélectionner d’autres fonctionnalités.  
  
7.  Sur le **Active Directory Federation Service \(AD FS\)**  , cliquez sur **suivant**.  
  
8.  Après avoir vérifié les informations sur le **confirmer les sélections d’installation** , cliquez sur **installer**.  
  
9. Dans la page **Progression de l'installation** , vérifiez que tout a été correctement installé, puis cliquez sur **Fermer**.  
  
### <a name="to-install-the-ad-fs-server-role-via-windows-powershell"></a>Pour installer le rôle de serveur AD FS via Windows PowerShell  
  
1.  Sur l’ordinateur que vous souhaitez configurer comme serveur de fédération, ouvrez la fenêtre de commande Windows PowerShell, puis exécutez la commande suivante : `Install-windowsfeature adfs-federation –IncludeManagementTools`.  
  
## <a name="see-also"></a>Voir aussi 

[Déploiement d’AD FS](../../ad-fs/AD-FS-Deployment.md)  

[Guide de déploiement de Windows Server 2012 R2 AD FS](../../ad-fs/deployment/Windows-Server-2012-R2-AD-FS-Deployment-Guide.md)  
 
[Déploiement d’une batterie de serveurs de fédération](../../ad-fs/deployment/Deploying-a-Federation-Server-Farm.md)  
  

