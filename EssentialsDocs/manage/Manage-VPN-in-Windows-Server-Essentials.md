---
title: Gérer les VPN dans Windows Server Essentials
description: Décrit comment utiliser Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cc2b264a-b9a8-4114-9f7b-8604f77096e5
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: ec367337318d12161a250572745d8f303d098ffe
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59849200"
---
# <a name="manage-vpn-in-windows-server-essentials"></a>Gérer les VPN dans Windows Server Essentials

>S'applique à : Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials 
  
 Les connexions VPN permettent aux utilisateurs qui travaillent à leur domicile ou en déplacement d'accéder à un serveur sur un réseau privé à l'aide de l'infrastructure fournie par un réseau public, tel qu'Internet. Pour utiliser VPN pour l’accès aux ressources serveur, vous devez procéder comme suit :  
  
-   [Activer VPN pour l’accès à distance sur le serveur](Manage-VPN-in-Windows-Server-Essentials.md#BKMK_1)  
  
-   [Définir des autorisations pour les utilisateurs du réseau VPN](Manage-VPN-in-Windows-Server-Essentials.md#BKMK_2)  
  
-   [Connecter des ordinateurs clients au serveur](Manage-VPN-in-Windows-Server-Essentials.md#BKMK_Connect)  
  
-   [Utiliser VPN pour se connecter à Windows Server Essentials](Manage-VPN-in-Windows-Server-Essentials.md#BKMK_3)  
  
##  <a name="BKMK_1"></a> Activer VPN pour l’accès à distance sur le serveur  
 Effectuez la procédure suivante pour configurer un VPN dans Windows Server Essentials pour activer l’accès à distance.  
  
#### <a name="to-enable-vpn-in-windows-server-essentials"></a>Pour activer un VPN dans Windows Server Essentials  
  
1.  Ouvrez le tableau de bord.  
  
2.  Cliquez sur **Paramètres**, puis sur l’onglet **Accès en tout lieu** .  
  
3.  Cliquez sur **configurer**. L’Assistant Configurer l’accès en tout lieu s’affiche.  
  
4.  Dans la page **Choisir les fonctions d’Accès en tout lieu à activer** , activez la case à cocher **Réseau privé virtuel (VPN)** .  
  
5.  Suivez les instructions pour exécuter l'Assistant.  
  
##  <a name="BKMK_2"></a> Définir des autorisations pour les utilisateurs du réseau VPN  
 Vous pouvez utiliser un réseau VPN pour vous connecter à Windows Server Essentials et accéder à toutes les ressources stockées sur le serveur. Cela est particulièrement utile si vous disposez d'un ordinateur client configuré avec des comptes réseau pouvant être utilisés pour se connecter à un serveur Windows Server Essentials hébergé via une connexion VPN. Tous les comptes d'utilisateur récemment créés sur le serveur Windows Server Essentials hébergé doivent utiliser le réseau VPN pour se connecter à l'ordinateur client pour la première fois.  
  
#### <a name="to-set-vpn-permissions-for-network-users"></a>Pour changer les autorisations VPN des utilisateurs réseau  
  
1.  Ouvrez le tableau de bord.  
  
2.  Dans la barre de navigation, cliquez sur **UTILISATEURS**.  
  
3.  Dans la liste des comptes d'utilisateur, sélectionnez le compte d'utilisateur auquel vous voulez accorder des autorisations pour accéder au Bureau à distance.  
  
4.  Dans le **< compte d’utilisateur\> tâches** volet, cliquez sur **propriétés**.  
  
5.  Dans le **< compte d’utilisateur\> propriétés**, cliquez sur le **accès en tout lieu** onglet.  
  
6.  Sous l’onglet **Accès en tout lieu** , pour autoriser un utilisateur à se connecter au serveur à l’aide d’un VPN, activez la case **Autoriser le Réseau privé virtuel (VPN)**  .  
  
7.  Cliquez sur **Appliquer**, puis sur **OK**.  
  
##  <a name="BKMK_Connect"></a> Connecter des ordinateurs clients au serveur  
 Une fois que le VPN est activé sur un serveur exécutant Windows Server Essentials pour l’accès à distance, vous pouvez utiliser une connexion VPN pour vous connecter et accéder à toutes vos ressources qui sont stockées sur le serveur. Toutefois, vous devez d’abord connecter l’ordinateur au serveur. Lorsque vous connectez un ordinateur au serveur à l’aide de l’Assistant Connecter mon ordinateur au serveur, une connexion réseau VPN est automatiquement générée sur l’ordinateur client et permet d’accéder aux ressources serveur lorsque vous travaillez à votre domicile ou êtes en déplacement. Pour obtenir des instructions pas à pas sur la connexion d’ordinateurs au serveur, consultez [Connect computers to the server](../use/Get-Connected-in-Windows-Server-Essentials.md#BKMK_9).  
  
##  <a name="BKMK_3"></a> Utiliser VPN pour se connecter à Windows Server Essentials  
 Si vous disposez d'un ordinateur client configuré avec des comptes de réseau pouvant être utilisés pour se connecter à un serveur hébergé exécutant Windows Server Essentials via une connexion VPN, tous les comptes d'utilisateur qui viennent d'être créés sur le serveur hébergé doivent utiliser VPN pour se connecter à l'ordinateur client pour la première fois. Procédez comme suit à partir de l’ordinateur client qui est connecté au serveur.  
  
#### <a name="to-use-vpn-to-remotely-access-server-resources"></a>Pour utiliser VPN pour accéder aux ressources du serveur à distance  
  
1.  Appuyez sur Ctrl+Alt+Suppr sur l’ordinateur client.  
  
2.  Cliquez sur **Changer d’utilisateur** sur l’écran d’ouverture de session.  
  
3.  Cliquez sur l'icône d'ouverture de session réseau dans le coin inférieur droit de l'écran.  
  
4.  Ouvrez une session sur le réseau Windows Server Essentials à l'aide de vos nom d'utilisateur et mot de passe réseau.  
  
## <a name="see-also"></a>Voir aussi  
  
-   [Travailler à distance](../use/Work-Remotely-in-Windows-Server-Essentials.md)  
  
-   [Gérer l’accès en tout lieu](Manage-Anywhere-Access-in-Windows-Server-Essentials.md)  
  
-   [Gérer Windows Server Essentials](Manage-Windows-Server-Essentials.md)
