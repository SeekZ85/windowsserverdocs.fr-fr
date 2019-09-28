---
title: Déployer VPN Toujours actif (AlwaysOn)
description: Cette rubrique fournit des instructions détaillées sur le déploiement de Always On VPN dans Windows Server 2016.
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.assetid: ad748de2-d175-47bf-b05f-707dc48692cf
ms.localizationpriority: medium
ms.date: 11/05/2018
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 054a41df281ff9720d381fd4854f34f56ed0307b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71388190"
---
# <a name="deploy-always-on-vpn"></a>Déployer VPN Toujours actif (AlwaysOn)

>S’applique à : Windows Server (canal semi-annuel), Windows Server 2016, Windows Server 2012 R2, Windows 10

- [**Premier** En savoir plus sur les fonctionnalités avancées de VPN Always On @ no__t-0
- [**Situé** Étape 1. Commencer à planifier le déploiement de Always On VPN](always-on-vpn-deploy-planning.md)

Dans cette section, vous allez découvrir le flux de travail pour le déploiement de Always On connexions VPN pour des ordinateurs clients Windows 10 joints à un domaine distant. Si vous souhaitez **configurer l’accès conditionnel** pour ajuster l’accès des utilisateurs VPN à vos ressources, consultez [accès conditionnel pour la connectivité VPN à l’aide de Azure ad](../../ad-ca-vpn-connectivity-windows10.md). Pour en savoir plus sur l’accès conditionnel pour la connectivité VPN à l’aide de Azure AD, consultez [accès conditionnel dans Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal). 

Le diagramme suivant illustre le processus de flux de travail pour les différents scénarios lors du déploiement d’Always On VPN :

![Organigramme du flux de travail de déploiement VPN Always On](../../../../media/Always-On-Vpn/always-on-vpn-deployment-workflow-sm.png)

>[!IMPORTANT]
>Pour ce déploiement, il n’est pas nécessaire que vos serveurs d’infrastructure, tels que les ordinateurs qui exécutent Active Directory Domain Services, Active Directory les services de certificats et le serveur de stratégie réseau, exécutent Windows Server 2016. Vous pouvez utiliser des versions antérieures de Windows Server, telles que Windows Server 2012 R2, pour les serveurs d’infrastructure et pour le serveur qui exécute l’accès à distance.

## <a name="step-1-plan-the-always-on-vpn-deploymentalways-on-vpn-deploy-planningmd"></a>[Étape 1. Planifier le déploiement de VPN Toujours actif (AlwaysOn)](always-on-vpn-deploy-planning.md)

Au cours de cette étape, vous allez commencer à planifier et à préparer votre déploiement Always On VPN. Avant d’installer le rôle serveur d’accès à distance sur l’ordinateur sur lequel vous envisagez d’utiliser en tant que serveur VPN. Après une planification appropriée, vous pouvez déployer VPN Toujours actif (AlwaysOn) et éventuellement configurer l’accès conditionnel pour une connectivité VPN à l’aide d’Azure AD.

## <a name="step-2-configure-the-always-on-vpn-server-infrastructurevpn-deploy-server-infrastructuremd"></a>[Étape 2. Configurer l’infrastructure des serveurs VPN Toujours actif (AlwaysOn)](vpn-deploy-server-infrastructure.md)

Dans cette étape, vous installez et configurez les composants côté serveur nécessaires pour prendre en charge le VPN. Les composants côté serveur incluent la configuration de l’infrastructure à clé publique pour distribuer les certificats utilisés par les utilisateurs, le serveur VPN et le serveur NPS.  Vous configurez également RRAS pour prendre en charge les connexions IKEv2 et le serveur NPS pour effectuer l’autorisation pour les connexions VPN.

Pour configurer l’infrastructure de serveur, vous devez effectuer les tâches suivantes :

- **Sur un serveur configuré avec Active Directory Domain Services :** Activez l’inscription automatique des certificats dans stratégie de groupe pour les ordinateurs et les utilisateurs, créez le groupe utilisateurs VPN, le groupe serveurs VPN et le groupe serveurs NPS, puis ajoutez des membres à chaque groupe.
- **Sur une autorité de certification Active Directory Certificate Server :** Créez les modèles authentification de l’utilisateur, authentification du serveur VPN et certificat d’authentification du serveur NPS.
- **Sur les clients Windows 10 joints à un domaine :** Inscrire et valider des certificats utilisateur.

## <a name="step-3-configure-the-remote-access-server-for-always-on-vpnvpn-deploy-rasmd"></a>[Étape 3. Configurer le serveur d’accès à distance pour VPN Toujours actif (AlwaysOn)](vpn-deploy-ras.md)

Dans cette étape, vous configurez le VPN d’accès à distance pour autoriser les connexions VPN IKEv2, refuser les connexions à partir d’autres protocoles VPN et affecter un pool d’adresses IP statiques pour l’émission d’adresses IP à la connexion de clients VPN autorisés.

Pour configurer RAS, vous devez effectuer les tâches suivantes :

- Inscrire et valider le certificat de serveur VPN
- Installer et configurer le VPN d’accès à distance

## <a name="step-4-install-and-configure-the-nps-servervpn-deploy-npsmd"></a>[Étape 4. Installer et configurer le serveur NPS](vpn-deploy-nps.md)

Dans cette étape, vous installez le serveur NPS (Network Policy Server) à l’aide de Windows PowerShell ou de l’Assistant Gestionnaire de serveur ajouter des rôles et des fonctionnalités. Vous configurez également NPS pour gérer toutes les tâches d’authentification, d’autorisation et de comptabilité pour la demande de connexion qu’il reçoit du serveur VPN.

Pour configurer NPS, vous devez effectuer les tâches suivantes :

- Inscrire le serveur NPS dans Active Directory
- Configurer la gestion des comptes RADIUS pour votre serveur NPS
- Ajouter le serveur VPN en tant que client RADIUS dans NPS
- Configurer la stratégie réseau dans NPS
- Inscrire automatiquement le certificat de serveur NPS

## <a name="step-5-configure-dns-and-firewall-settings-for-always-on-vpnvpn-deploy-dns-firewallmd"></a>[Étape 5. Configurer les paramètres DNS et de pare-feu pour Always On VPN @ no__t-0

Dans cette étape, vous configurez les paramètres DNS et de pare-feu. Lorsque les clients VPN distants se connectent, ils utilisent les mêmes serveurs DNS que ceux utilisés par vos clients internes, ce qui leur permet de résoudre les noms de la même manière que les autres postes de travail internes. 

## <a name="step-6-configure-windows-10-client-always-on-vpn-connectionsvpn-deploy-client-vpn-connectionsmd"></a>[Étape 6. Configurer les connexions VPN Toujours actif (AlwaysOn) du client Windows 10](vpn-deploy-client-vpn-connections.md)

Dans cette étape, vous configurez les ordinateurs clients Windows 10 pour qu’ils communiquent avec cette infrastructure avec une connexion VPN. Vous pouvez utiliser plusieurs technologies pour configurer les clients VPN Windows 10, notamment Windows PowerShell, System Center Configuration Manager et Intune. Les trois nécessitent un profil VPN XML pour configurer les paramètres VPN appropriés.

## <a name="step-7-optional-configure-conditional-access-for-vpn-connectivityad-ca-vpn-connectivity-windows10md"></a>[Étape 7. Facultatif Configurer l’accès conditionnel pour la connectivité VPN @ no__t-0

Dans cette étape facultative, vous pouvez ajuster la façon dont les utilisateurs VPN autorisés accèdent à vos ressources. Avec Azure AD accès conditionnel pour la connectivité VPN, vous pouvez protéger les connexions VPN. L’accès conditionnel est un moteur d’évaluation basé sur des stratégies qui vous permet de créer des règles d’accès pour toutes les Azure AD application connectée. Pour plus d’informations, consultez [Azure Active Directory (Azure AD) accès conditionnel](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-azure-portal).

## <a name="next-step"></a>Étape suivante

[Étape 1. Planifier le déploiement VPN Always On @ no__t-0 : Avant d’installer le rôle serveur d’accès à distance sur l’ordinateur sur lequel vous envisagez d’utiliser en tant que serveur VPN. Après une planification appropriée, vous pouvez déployer VPN Toujours actif (AlwaysOn) et éventuellement configurer l’accès conditionnel pour une connectivité VPN à l’aide d’Azure AD.  
