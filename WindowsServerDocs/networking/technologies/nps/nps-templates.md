---
title: Modèles NPS
description: Cette rubrique fournit une vue d’ensemble des modèles de serveur de stratégie réseau dans Windows Server 2016.
manager: brianlic
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: fdfc0df1-21c7-492c-9fad-38fe9c7d935a
ms.author: pashort
author: shortpatti
ms.openlocfilehash: bafff7a6a15312ab1bdca2e7b98307bc94731d3a
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405319"
---
# <a name="nps-templates"></a>Modèles NPS

>S’applique à : Windows Server (Canal semi-annuel), Windows Server 2016

Le serveur de stratégie réseau \(NPS @ no__t-1 vous permet de créer des éléments de configuration, tels que des protocole RADIUS (Remote Authentication Dial-In User Service) \(RADIUS @ no__t-3 ou des secrets partagés, que vous pouvez réutiliser sur le serveur NPS local et exporter pour une utilisation sur d’autres NPSs.

Les modèles NPS sont conçus pour réduire la durée et le coût nécessaires à la configuration de NPS sur un ou plusieurs serveurs. Les types de modèles NPS suivants sont disponibles pour la configuration dans la gestion des modèles :

- Secrets partagés
- Clients RADIUS
- Serveurs RADIUS distants
- Filtres IP
- Groupes de serveurs de mise à jour

La configuration d’un modèle est différente de la configuration du serveur NPS directement. La création d’un modèle n’affecte pas la fonctionnalité du serveur NPS. C’est uniquement lorsque vous sélectionnez le modèle à l’emplacement approprié dans la console NPS, que le modèle affecte les fonctionnalités du serveur NPS. 

Par exemple, si vous configurez un client RADIUS dans la console NPS sous clients et serveurs RADIUS, vous avez modifié la configuration du serveur NPS et effectué une étape dans la configuration de NPS pour communiquer avec l’un de vos serveurs d’accès réseau \(NAS’s @ no__t-1. \(The étape suivante consiste à configurer le NAS pour communiquer avec NPS. \) Toutefois, si vous configurez un nouveau modèle clients RADIUS dans la console NPS sous **gestion des modèles** au lieu de créer un client RADIUS sous **clients et serveurs RADIUS**, vous avez créé un modèle, mais vous n’avez pas modifié le serveur NPS. fonctionnalité encore. Pour modifier la fonctionnalité de serveur NPS, vous devez sélectionner le modèle à partir de l’emplacement approprié dans la console NPS.

## <a name="creating-templates"></a>Création de modèles

Pour créer un modèle, ouvrez la console NPS, cliquez avec le bouton droit sur un type de modèle, tel que **filtres IP**, puis cliquez sur **nouveau**. Une nouvelle boîte de dialogue Propriétés du modèle s’ouvre et vous permet de configurer votre modèle.

## <a name="using-templates-locally"></a>Utilisation de modèles localement

Vous pouvez utiliser un modèle que vous avez créé dans la **gestion des modèles** en accédant à un emplacement dans la console NPS où le modèle peut être appliqué. Par exemple, si vous créez un nouveau modèle de secrets partagés que vous souhaitez appliquer à une configuration de client RADIUS, dans **clients RADIUS et serveurs** et **clients RADIUS**, ouvrez les propriétés du client RADIUS. Dans **Sélectionner un modèle de secrets partagés existant**, sélectionnez le modèle que vous avez créé précédemment dans la liste des modèles disponibles.

Pour plus d’informations sur NPS, consultez [serveur NPS (Network Policy Server)](nps-top.md).
