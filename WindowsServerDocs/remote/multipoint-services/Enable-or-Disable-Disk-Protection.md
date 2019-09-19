---
title: Activer ou désactiver la Protection des disques
description: Découvrez comment utiliser la protection des disques avec MultiPoint services
ms.custom: na
ms.prod: windows-server-threshold
ms.technology: multipoint-services
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 00aba4c4-0244-4b39-8c85-c46fd96e1d6a
author: lizap
manager: dongill
ms.author: elizapo
ms.openlocfilehash: d037b0843f5ba50c98e0d6e7cb10836c8d6fa23a
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70871749"
---
# <a name="enable-or-disable-disk-protection"></a>Activer ou désactiver la Protection des disques
La fonctionnalité Protection des disques vous permet de réinitialiser votre système MultiPoint Services à un état spécifique chaque fois que vous redémarrez le système. À l’aide de la Protection des disques, les utilisateurs peuvent modifier temporairement le système MultiPoint Services. Ces modifications sont ensuite annulées lors du redémarrage du serveur. Les exemples de modifications qui seront ignorés lors du redémarrage du serveur incluent la personnalisation du profil d’un utilisateur, l’enregistrement des fichiers, la modification des paramètres ou l’installation d’applications.  
  
## <a name="enable-disk-protection"></a>Activer la protection des disques  
  
1.  Dans le gestionnaire MultiPoint, cliquez sur l’onglet dossier de **démarrage** , puis, sous **tâches** *nom de l’ordinateur , cliquez sur **activer la protection des disques**.  
  
2.  Vérifiez les informations, puis cliquez sur **OK**.  
  
Après le redémarrage du système, toutes les modifications apportées au système, dont les nouvelles applications installées, sont annulées à chaque redémarrage suivant.  
  
## <a name="disable-disk-protection"></a>Désactiver la protection des disques  
  
1.  Dans le gestionnaire MultiPoint, cliquez sur l’onglet dossier de **démarrage** , puis, sous **tâches** *nom de l’ordinateur*, cliquez sur **désactiver la protection des disques**.  
  
2.  Vérifiez les informations, puis cliquez sur **OK**.  
  
Après le redémarrage du système, toutes les modifications apportées au système, dont les applications qui sont installées sur le serveur, sont permanentes et ne sont pas annulées lors du prochain redémarrage du système.  
  
