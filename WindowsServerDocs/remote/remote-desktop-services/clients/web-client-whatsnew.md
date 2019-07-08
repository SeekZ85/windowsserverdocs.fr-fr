---
title: Nouveautés du client web Bureau à distance
description: En savoir plus sur les dernières modifications apportées au client web Bureau à distance
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
author: lizap
manager: dongill
ms.author: elizapo
ms.date: 05/20/2019
ms.localizationpriority: medium
ms.openlocfilehash: 5be9b05da1e78cc54e12254f43d0f44f7ff65c5d
ms.sourcegitcommit: 3743cf691a984e1d140a04d50924a3a0a19c3e5c
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/17/2019
ms.locfileid: "66804882"
---
# <a name="whats-new-for-the-remote-desktop-web-client"></a>Nouveautés du client web Bureau à distance

Nous mettons régulièrement à jour le [client web Bureau à distance](remote-desktop-web-client.md) en ajoutant de nouvelles fonctionnalités et en corrigeant les problèmes. Découvrez les dernières mises à jour ci-dessous.

> [!NOTE]
> Nous avons modifié le système de contrôle de version du client web. À partir de la version 1.0.18.0, toutes les versions du client web contiendront des numéros (au format « W.X.Y.Z »). Les numéros de version du client web Bureau à distance se termineront toujours par un 0 (par exemple, W.X.Y.0). À chaque version du client web Windows Virtual Desktop, le dernier chiffre changera jusqu'à la publication de la version suivante du client web Bureau à distance (par exemple, 1.0.18.1).

## <a name="updates-for-version-10180"></a>Mises à jour relatives à la version 1.0.18.0
*Date de publication : 14/05/2019*

- Ajout de la configuration Méthode de lancement des ressources dans l'onglet Paramètres pour permettre aux utilisateurs d'ouvrir les ressources à partir du navigateur ou de télécharger un fichier .rdp à gérer avec un autre client. Ce paramètre peut être configuré par votre administrateur. Des informations détaillées sur les configurations administrateur de cette fonctionnalité sont disponibles dans la [documentation consacrée à la configuration du client web](remote-desktop-web-client-admin.md).
- Correction de problèmes de rendu des couleurs pour vous permettre de bénéficier de couleurs plus vives dans votre session à distance.
- Révision des messages liés aux erreurs de flux de ressources distantes. 
- Ajout de la prise en charge de raccourcis supplémentaires, comme le collage spécial (Ctrl + Alt + V).
- Ajout d'un raccourci clavier permettant aux utilisateurs d'appeler la touche Windows dans le cadre de la session à distance (Alt + F3)
- Mise à jour du message d'erreur présenté aux utilisateurs qui tentent de s'authentifier à l'aide d'un mot de passe qui a expiré.
- Actualisation de l'interface utilisateur de flux sur la page Toutes les ressources.
- Résolution du problème de boîtes de dialogue qui se chevauchaient lors de la reconnexion à la session.
- Correction du redimensionnement de l'icône des ressources distantes sur la barre des tâches des ressources.

## <a name="updates-for-version-1011"></a>Mises à jour relatives à la version 1.0.11
*Date de publication : 22/02/2019*

- Activation de la connexion au service Broker Bureau à distance sans passerelle de services Bureau à distance dans Windows Server 2019.
- Les flux sont classés par ordre alphabétique (applications distantes en premier, appareils de bureau en second).
- Correction de différents bogues d'accessibilité améliorant la compatibilité du lecteur d'écran.
- Mise à jour de nos outils de génération.
- Correction de différents bogues.

## <a name="updates-for-version-107"></a>Mises à jour relatives à la version 1.0.7
*Date de publication : 24/01/2019*

- L'utilisation hors connexion est désormais prise en charge sur les réseaux internes.
- Amélioration du rendu sur les navigateurs autres que Microsoft Edge.
- Mise en place d'une limite pour les nouvelles tentatives de récupération du flux afin de prévenir les attaques par déni de service.
- Correction de bogues d'accessibilité permettant aux utilisateurs souffrant de troubles de la vision d'utiliser le client web.
- Amélioration des messages présentés à l'utilisateur pour les erreurs de flux.
- Ajout des raccourcis Ctrl + Alt + Fin (Windows) et Fn + Contrôle + Option + Supprimer (Mac) pour appeler Ctrl + Alt + Suppr sur l'ordinateur distant.
- Amélioration des données de télémétrie en cas d'erreur générale.
- Amélioration de notre pipeline de build et de nos outils de génération.
- Correction de différents bogues.

## <a name="updates-for-version-101"></a>Mises à jour relatives à la version 1.0.1
*Date de publication : 29/10/2018*

- Ajout de l'option **Capturer les informations de support** sur la page À propos de pour diagnostiquer les problèmes.
- Le mode inPrivate est désormais pris en charge.
- Amélioration de la prise en charge des claviers non anglais.
- Correction d'un problème d'affichage des caractères non anglais dans les infobulles.
- Correction d'un problème de rendu des graphismes qui affectait les utilisateurs de Chrome.
- Mise à jour de la redirection du fuseau horaire avec prise en charge complète de l'heure d’été.
- Amélioration du message d'erreur relatif à la mémoire insuffisante.
- Correction de différents bogues.

## <a name="updates-for-version-100"></a>Mises à jour relatives à la version 1.0.0
*Date de publication : 16/07/2018*

- Le client web Bureau à distance est maintenant généralement disponible.
- Les administrateurs peuvent globalement désactiver les données de télémétrie pour le client web.
- Correction de différents bogues.

## <a name="updates-for-version-090"></a>Mises à jour relatives à la version 0.9.0
*Date de publication : 05/07/2018*

- Nouvelle expérience de connexion au sein du client web.
- Les informations d'identification ne sont plus demandées au moment de la connexion d'un appareil de bureau ou d'une application (authentification unique).
- Transfert du client web vers une nouvelle URL : <https://server_FQDN/RDWeb/webclient/index.html>
- Ajout de la redirection du fuseau horaire.
- Correction de différents bogues.

## <a name="updates-for-version-081"></a>Mises à jour relatives à la version 0.8.1
*Date de publication : 17/05/2018*

- Mises à jour en lien avec la correction de l'oracle de chiffrement CredSSP décrite dans CVE-2018-0886.
- Correction d'échecs de connexion liés à certaines langues lorsque l'impression était activée.
- Amélioration du message d'erreur lorsqu'une passerelle ne fait pas partie du déploiement.
- Ajout des options **Aide** et **Commentaires**.

## <a name="updates-for-version-080"></a>Mises à jour relatives à la version 0.8.0
*Date de publication : 28/03/2018*

- Lancement de la préversion publique initiale du client web.
- Copier/coller du texte dans le presse-papiers à l'aide de **CTRL + C** et **CTRL + V**.
- Impression dans un fichier PDF.
- Localisation en 18 langues.
 
