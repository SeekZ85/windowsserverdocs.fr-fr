---
title: Nouveautés du client Windows Desktop
description: Découvrir les dernières modifications apportées au client Bureau à distance pour Windows Desktop
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
author: heidilohr
manager: daveba
ms.author: helohr
ms.date: 11/12/2019
ms.localizationpriority: medium
ms.openlocfilehash: db9c2b64e018b41b053974b5459bd320098a6d2d
ms.sourcegitcommit: 315f015102c42c6fa7694e76adecdfb448390391
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/13/2019
ms.locfileid: "74019596"
---
# <a name="whats-new-in-the-windows-desktop-client"></a>Nouveautés du client Windows Desktop

Vous trouverez des informations plus détaillées sur le client Windows Desktop dans la page [Bien démarrer avec le client Windows Desktop](windowsdesktop.md). Vous trouverez les dernières mises à jour du client ci-dessous.

## <a name="latest-client-versions"></a>Versions les plus récentes du client

Le client peut être configuré pour différents [groupes d’utilisateurs](windowsdesktop-admin.md#configure-user-groups). Le tableau suivant liste les versions actuelles disponibles pour chaque groupe d’utilisateurs :

|Groupe d'utilisateurs |Version  |
|-----------|---------|
|Public     |1.2.431  |
|Insider    |1.2.431  |

## <a name="updates-for-version-12431"></a>Mises à jour relatives à la version 1.2.431

*Date de publication : 12/11/2019*

- Les versions 32 bits et ARM64 du client sont disponibles !
- Le client enregistre désormais les changements que vous apportez à la barre de connexion (par exemple, sa position, sa taille et son état épinglé) et les applique aux différentes sessions.
- Mise à jour des informations de passerelle et des boîtes de dialogue d’état de connexion.
- Résolution d’un problème qui entraînait l’invite de deux jeux d’informations d’identification en même temps lors de la tentative de connexion après l’expiration du jeton Azure Active Directory.
- Sur Windows 7, les utilisateurs sont maintenant invités correctement à fournir des informations d’identification s’ils en avaient enregistrées quand le serveur les interdit.
- L’invite Azure Active Directory s’affiche à présent devant la fenêtre de connexion lors de la reconnexion.
- Les éléments épinglés à la barre des tâches sont maintenant mis à jour pendant une actualisation de flux.
- Amélioration du défilement dans le centre de connexion sur écran tactile.
- Suppression de la ligne vide dans le menu déroulant de résolution.
- Suppression des entrées inutiles dans le Gestionnaire d’informations d’identification Windows.
- Les sessions de bureau sont maintenant à la bonne taille quand vous quittez le mode plein écran.
- La boîte de dialogue de déconnexion de RemoteApp apparaît désormais au premier plan quand vous reprenez votre session après être entré en mode veille.
- Résolution de problèmes d’accessibilité comme la navigation au clavier.

## <a name="updates-for-version-12247"></a>Mises à jour relatives à la version 1.2.247

*Date de publication : 17/09/2019*

- Correction d’un plantage qui se produisait lors de l’authentification pendant une connexion.
- Correction d’un plantage qui se produisait lors de la fermeture du client.

## <a name="updates-for-version-12246"></a>Mises à jour pour la version 1.2.246

*Date de publication : 28/8/2019*

- Amélioration des langues de base pour la version localisée. (Par exemple, FR-CA affiche bien le texte en français et non en anglais.)
- Lors de la suppression d’un abonnement, le client supprime désormais correctement les informations d’identification enregistrées du Gestionnaire d’informations d’identification.
- Le processus de mise à jour du client est maintenant sans assistance une fois démarré, et le client est relancé une fois l’opération terminée.
- Le client peut désormais être utilisé sur Windows 10 en mode S.
- Correction d’un problème qui provoquait l’échec du processus de mise à jour pour les utilisateurs dont le nom comprenait un espace.
