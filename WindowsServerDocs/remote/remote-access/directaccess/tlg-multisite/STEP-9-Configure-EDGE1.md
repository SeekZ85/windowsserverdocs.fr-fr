---
title: ÉTAPE 9 configurer EDGE1
description: 'Cette rubrique fait partie du Guide de laboratoire de test : illustrer un déploiement multisite DirectAccess pour Windows Server 2016'
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-da
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f6e8d85b-de65-43b3-bf3e-ec84471a1fcc
ms.author: pashort
author: shortpatti
ms.openlocfilehash: ce86a75ac5b8d53874d2fc5c6743979506591680
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71388232"
---
# <a name="step-9-configure-edge1"></a>ÉTAPE 9 configurer EDGE1

>S'applique à : Windows Server (Canal semi-annuel), Windows Server 2016

Les procédures suivantes sont effectuées sur le serveur EDGE1 :  
  
1. Configurez les serveurs DNS sur EDGE1. Il est nécessaire de configurer le serveur DNS à partir du domaine corp2.corp.contoso.com sur EDGE1.  
  
2. Configurer le routage entre les sous-réseaux. Configurez le routage sur EDGE1 pour activer la communication entre les sous-réseaux corpnet et 2-Corpnet.  
  
## <a name="IPv6"></a>Configurer les serveurs DNS sur EDGE1  
  
1.  Dans la console Gestionnaire de serveur, cliquez sur **serveur local**, puis dans la zone **Propriétés** , en regard de **corpnet**, cliquez sur le lien.  
  
2.  Dans la fenêtre Connexions réseau, cliquez avec le bouton droit sur **corpnet**, puis cliquez sur **Propriétés**.  
  
3.  Cliquez sur **Protocole Internet version 4 (TCP/IPv4)** , puis sur **Propriétés**.  
  
4.  Dans **serveur DNS auxiliaire**, tapez **10.2.0.1**. puis cliquez sur **OK**.  
  
5.  Cliquez sur **Internet Protocol Version 6 (TCP/IPv6)** , puis cliquez sur **Propriétés**.  
  
6.  Dans **serveur DNS auxiliaire**, tapez **2001 : DB8:2 :: 1** , puis cliquez sur **OK**.  
  
7.  Dans la boîte de dialogue **Propriétés de corpnet** , cliquez sur **Fermer**.  
  
8.  Fermez la fenêtre **Connexions réseau**.  
  
## <a name="ConfigRouting"></a>Configurer le routage entre les sous-réseaux  
  
1.  Dans l’écran d' **Accueil** , tapez**cmd. exe**, cliquez avec le bouton droit sur **cmd**, cliquez sur **avancé**, puis sur **exécuter en tant qu’administrateur**. Si la boîte de dialogue **Contrôle de compte d'utilisateur** s'affiche, vérifiez que l'action affichée est celle que vous voulez, puis cliquez sur **Oui**.  
  
2.  Dans la fenêtre d’invite de commandes, entrez les commandes suivantes. Après avoir entré chaque commande, appuyez sur entrée.  
  
    ```  
    netsh interface IPv4 add route 10.2.0.0/24 Corpnet 10.0.0.254  
    netsh interface IPv6 add route 2001:db8:2::/64 Corpnet 2001:db8:1::fe  
    ```  
  
3.  Fermez la fenêtre d’invite de commandes.  
  


