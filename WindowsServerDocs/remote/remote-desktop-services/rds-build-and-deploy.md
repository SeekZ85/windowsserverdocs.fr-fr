---
title: Services Bureau à distance - générer et déployer
description: Étapes pour générer un déploiement de bureau à distance
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.author: elizapo
ms.date: 04/18/2017
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 176ae424-96e9-4c78-88f5-da418e76c3d7
author: lizap
manager: dongill
ms.openlocfilehash: 0ab4be6ba326db05e8fc6a9c14e84c8cbb855926
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59814750"
---
# <a name="build-and-deploy-your-remote-desktop-services-deployment"></a>Générer et déployer votre déploiement des Services Bureau à distance

Un déploiement Services Bureau à distance est l’infrastructure utilisée pour partager des applications et des ressources avec vos utilisateurs. En fonction de l’expérience que vous souhaitez fournir, vous pouvez faciliter en tant que petit ou complexe que nécessaire. Déploiements Bureau à distance sont facilement à l’échelle. Vous pouvez augmenter et diminuer l’accès Bureau à distance par le Web, serveurs de passerelle, service Broker pour les connexions et hôte de Session à seront. Vous pouvez utiliser Service Broker pour les connexions Bureau à distance pour distribuer les charges de travail. Authentification Active Directory en fonction fournit un environnement hautement sécurisé. 

[Clients Bureau à distance](clients\remote-desktop-clients.md) activer l’accès à partir de n’importe quelle tablette Windows, Apple ou Android ordinateur, ou par téléphone.

Consultez [architecture des Services Bureau à distance](desktop-hosting-logical-architecture.md) pour une présentation détaillée des différentes parties qui collaborent pour composer votre déploiement des Services Bureau à distance.

Vous avez un déploiement de bureau à distance existant basé sur une version précédente de Windows Server ? Découvrez vos options pour le passage à WIndows Server 2016, où vous pouvez tirer parti des fonctionnalités nouvelles et meilleures performances et mise à l’échelle :

- [Migrer votre déploiement de services Bureau à distance vers Windows Server 2016](migrate-rds-role-services.md)
- [Mettre à niveau votre déploiement des services Bureau à distance vers Windows Server 2016](upgrade-to-rds-2016.md)

Vous souhaitez créer un nouveau déploiement de bureau à distance ? Pour déployer un bureau à distance dans Windows Server 2016, utilisez les informations suivantes :

- [Déployer l’infrastructure de Services Bureau à distance](rds-deploy-infrastructure.md)
- [Créer une collection de sessions pour stocker les applications et les ressources que vous souhaitez partager](rds-create-collection.md)
- [Licence de votre déploiement des services Bureau à distance](rds-client-access-license.md)
- Demandez à vos utilisateurs d’installer un [client Bureau à distance](clients/remote-desktop-clients.md) d’accéder aux applications et ressources. 
- Activer la haute disponibilité en ajoutant des agents de connexion et des hôtes de Session supplémentaires :
   - [Monter en charge une collection de services Bureau à distance existante avec une batterie de serveurs hôte de Session Bureau à distance](rds-scale-rdsh-farm.md)
   - [Ajouter une haute disponibilité à l’infrastructure service Broker pour les connexions Bureau à distance](rds-connection-broker-cluster.md)
   - [Ajouter une haute disponibilité pour le serveur web frontal Web de bureau à distance et passerelle Bureau à distance](rds-rdweb-gateway-ha.md)
   - [Déployer un système de fichiers espaces de stockage Direct de deux nœuds pour le stockage UPD](rds-storage-spaces-direct-deployment.md)


Si vous êtes un partenaire d’hébergement qui souhaitent utiliser le Bureau à distance pour fournir des applications et des ressources à des clients ou un client que vous recherchez quelque chose héberger vos applications, consultez [des Services Bureau à distance, les partenaires d’hébergement](rds-hosting-partners.md) pour plus d’informations sur un Vous pouvez tirer sur l’utilisation des services Bureau à distance dans Azure comme un environnement d’hébergement, ainsi qu’une liste de partenaires qui lui avez passé l’évaluation.
