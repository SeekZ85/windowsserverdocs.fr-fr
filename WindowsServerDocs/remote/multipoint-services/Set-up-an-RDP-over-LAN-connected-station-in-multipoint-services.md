---
title: Configurer une station connectée RDP sur réseau local dans MultiPoint services
description: Découvrez comment configurer un système RDP sur réseau local dans MultiPoint services
ms.custom: na
ms.date: 07/22/2016
ms.prod: windows-server
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 60e1a025-c2fb-4708-a3ff-c44c223a3224
author: evaseydl
manager: scottman
ms.author: evas
ms.openlocfilehash: d0d63a75d3ef6e042d44df0ecf4cc08973e859a6
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71394999"
---
# <a name="set-up-an-rdp-over-lan-connected-station-in-multipoint-services"></a>Configurer une station connectée RDP sur réseau local dans MultiPoint services
Une station connectée au réseau local (RDP) est un client léger, un ordinateur de bureau traditionnel ou un ordinateur portable qui se connecte à MultiPoint services sur un réseau local (LAN) à l’aide du protocole RDP (Remote Desktop Protocol) (RDP). Pour plus d’informations sur ce type de station et les autres, consultez la page sur les [stations multipoint](MultiPoint-services-Stations.md).  
  
## <a name="to-set-up-a-multipoint-station-using-a-computer-or-thin-client-on-a-lan"></a>Pour configurer une station MultiPoint à l’aide d’un ordinateur ou d’un client léger sur un réseau local  
  
1.  Allumez l’ordinateur qui exécute MultiPoint services.  
  
2.  Vérifiez que l’ordinateur MultiPoint Server est connecté au réseau local par le biais d’un commutateur, d’un routeur ou d’un autre périphérique réseau et qu’il a une adresse IP appropriée. (Une adresse IP commençant par 169,254 (une adresse APIPA) peut indiquer un problème avec la connexion au réseau local ou que le serveur DHCP ne peut pas être atteint ou ne fonctionne pas correctement.)  
  
3.  Connectez l’ordinateur client ou le client léger au réseau local.  
  
4.  Activez l’ordinateur client ou le client léger.  
  
5.  Sur l’ordinateur client ou le client léger, démarrez Connexion Bureau à distance ou une application équivalente, puis entrez le nom ou l’adresse IP de l’ordinateur qui exécute MultiPoint services.

## <a name="set-up-a-windows-10-device-for-remote-management-by-using-connector-services"></a>Configurer un appareil Windows 10 pour la gestion à distance à l’aide des services de connecteur
Tout PC ou ordinateur portable exécutant Windows 10 peut être géré à distance, à condition que :
- les services du connecteur ont été activés  
- l’ordinateur a été ajouté aux ordinateurs gérés sur le serveur MultiPoint.  

Sur le PC exécutant Windows 10, procédez comme suit pour activer le connecteur MultiPoint :

1. Dans la zone de recherche, tapez « activer ou désactiver des fonctionnalités Windows », puis sélectionnez le résultat de la recherche approprié. 

2. Dans la liste des fonctionnalités, activez le **connecteur multipoint**. Cela permettra aux services de connecteur MultiPoint nécessaires à la gestion de l’appareil. 

Sur le serveur MultiPoint :
1. Ouvrez le gestionnaire MultiPoint et sélectionnez **Ajouter ou supprimer des ordinateurs personnels** ou **Ajouter ou supprimer des services multipoint**.

2. Sélectionnez les ordinateurs distants que vous souhaitez gérer, puis cliquez sur **OK**.  Vous serez invité à entrer les informations d’identification d’administrateur sur les ordinateurs distants.  Une fois cette opération effectuée, les ordinateurs distants s’affichent sous l’onglet de démarrage de MultiPoint Manager.

Une fois correctement configuré, le gestionnaire de tableaux de bord peut surveiller les utilisateurs qui travaillent sur l’appareil géré.

> [!IMPORTANT]  
> Lors de l’analyse des appareils Windows 10 gérés, administratrive les utilisateurs ne peuvent pas être analysés, sauf si les paramètres du serveur ont été modifiés en conséquence. Consultez [modifier les paramètres du serveur](Edit-Server-Settings.md)