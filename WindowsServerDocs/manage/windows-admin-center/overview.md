---
title: Vue d’ensemble de Windows Admin Center
description: Découvrez comment gérer Windows Server à l’aide de Windows Admin Center (projet Honolulu)
ms.technology: manage
ms.topic: article
author: nwashburn-ms
ms.author: niwashbu
ms.localizationpriority: high
ms.prod: windows-server-threshold
ms.openlocfilehash: e23d02fd8da96392f44874ad6ea4d6c40e2be940
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59828200"
---
# <a name="windows-admin-center"></a>Windows Admin Center

>S'applique à : Windows Admin Center, version préliminaire de Windows Admin Center

Bienvenue sur Windows Admin Center !

**Windows Admin Center** (baptisé **projet Honolulu**) est une évolution des outils de gestion de l’emploi de Windows Server ; il est un volet unique qui consolide tous les aspects de la gestion des serveurs locaux et distants. Comme il s'agit d'une expérience de gestion basée sur un navigateur et déployée localement, il n'est pas obligatoire de disposer d'Azure et d'une connexion Internet. Windows Admin Center vous offre un contrôle total sur tous les aspects de votre déploiement, notamment les réseaux privés qui ne sont pas connectés à Internet.

## <a name="introduction"></a>Introduction

>[!VIDEO https://www.youtube.com/embed/PcQj6ZklmK0]

![Infographie Windows Admin Center](media/WAC1809Poster_thumb.PNG)

[Téléchargez le fichier PDF](https://github.com/MicrosoftDocs/windowsserverdocs/raw/master/WindowsServerDocs/manage/windows-admin-center/media/WindowsAdminCenter1809Poster.pdf)

## <a name="quick-start"></a>Démarrage rapide

Vous pouvez installer et exécuter Windows Admin Center dans votre environnement en quelques minutes :

1. [Télécharger](https://aka.ms/windowsadmincenter)
2. [Installer](deploy/install.md)
3. [Prise en main](use/get-started.md)

## <a name="contents-at-a-glance"></a>Contenu en un clin de œil

<table>
    <tr></tr>
    <tr>
        <td style="vertical-align: top;">
            <h3>Comprendre</h3>
            <ul>
            <li><a href="understand/what-is.md">Qu’est Windows Admin Center ?</a>
            <li><a href="understand/faq.md">FAQ</a>
            <li><a href="understand/case-studies.md">Études de cas</a>
            <li><a href="understand/related-management.md">Produits de gestion</a>
            <li><a href="understand/videos.md">Vidéos</a>
            </ul>
        </td>
        <td style="vertical-align: top;">
            <h3>Planifier</h3>
            <ul>
            <li><a href="plan/installation-options.md">Quel type d’installation vous convient ?</a>
            <li><a href="plan/user-access-options.md">Options d’accès utilisateur</a>
            <li><a href="plan/azure-integration-options.md">Quelles options d’intégration d’Azure sont ?</a>
            <br>
            </ul>
        </td>
    </tr>
    <tr>
        <td style="vertical-align: top;">
            <h3>Déployer</h3>
            <ul>
            <li><a href="deploy/prepare-environment.md">Préparer votre environnement</a>
            <li><a href="deploy/install.md">Installer Windows Admin Center</a>
            <li><a href="deploy/high-availability.md">Activer la haute disponibilité</a>
         </ul>
        </td>
        <td style="vertical-align: top;">
            <h3>Configuration</h3>
            <ul>
            <li><a href="configure/settings.md">Paramètres Windows Admin Center</a>
            <li><a href="configure/user-access-control.md">Autorisations et contrôle d’accès utilisateur</a>
            <li><a href="configure/using-extensions.md">Extensions</a>
            <li><a href="configure/azure-integration.md">Intégrer avec Azure</a>
            <li><a href="configure/manage-azure-vms.md">Gérer des machines virtuelles Azure avec Windows Admin Center</a>
            </ul>
        </td>
    </tr>
    <tr>
        <td style="vertical-align: top;">
            <h3>Utilisez</h3>
            <ul>
            <li><a href="use/get-started.md">Lancer & Ajouter des connexions</a>
            <li><a href="use/manage-servers.md">Gérer les serveurs</a>
            <li><a href="use/manage-hyper-converged.md">Gérer l’infrastructure Hyper-convergée</a>
            <li><a href="use/manage-failover-clusters.md">Gérer les clusters de basculement</a>
            <li><a href="use/manage-virtual-machines.md">Gérer des machines virtuelles</a>
            <li><a href="use/azure-services.md">Tirer parti des services Azure</a>
            <li><a href="use/troubleshooting.md">Étapes de dépannage courantes</a>
            <li><a href="use/logging.md">Journalisation</a>
            <li><a href="use/known-issues.md">Problèmes connus</a>
            </ul>
        </td>
        <td style="vertical-align: top;">
            <h3>Étendre</h3>
            <ul>
            <li><a href="extend/extensibility-overview.md">Vue d’ensemble des extensions</a>
            <li><a href="extend/understand-extensions.md">Extensions de présentation</a>
            <li><a href="extend/developing-extensions.md">Développer une extension</a>
            <li><a href="extend/publish-extensions.md">Guides</a>
            <li><a href="extend/publish-extensions.md">Extensions de publication</a>
            </ul>
        </td>
    </tr>

</table>

## <a name="release-history"></a>Historique des versions

Découvrez nos toutes dernières fonctionnalités :

- Version [1902] (https://aka.ms/wac1902) ajouté une liste de connexions partagées et des améliorations à la gestion de réseau (SDN) software-defined, y compris les nouveaux outils SDN pour gérer les ACL, les connexions de passerelle et les réseaux logiques.
- Version [1812](https://aka.ms/wac1812) ajoute un thème foncé (dans la version d’évaluation), les paramètres de configuration de l’alimentation, des informations BMC et la prise en charge de PowerShell pour gérer les [extensions](./configure/using-extensions.md#manage-extensions-with-powershell) et les [connexions](./use/get-started.md#use-powershell-to-import-or-export-your-connections-with-tags).
- Version [1809.5](https://aka.ms/wac1809.5) est une mise à jour cumulative de GA qui inclut différentes améliorations de qualité et fonctionnelles, ainsi que des résolutions de bogues dans toute la plateforme et quelques nouvelles fonctionnalités dans la solution de gestion d’infrastructure hyperconvergée.
- Version [1809](https://cloudblogs.microsoft.com/windowsserver/2018/09/20/windows-admin-center-1809-and-sdk-now-generally-available/) était une version GA qui affiche les fonctionnalités qui étaient auparavant en préversion dans le canal GA.
- La version [1808](https://aka.ms/WACPreview1808-InsiderBlog) introduit l’outil Applications installées, un grand nombre d’améliorations en coulisses et d’importantes mises à jour de la préversion du SDK.
- Version [1807](https://aka.ms/WACPreview1807-InsiderBlog) ajoute une expérience de connexion à Azure simplifiée, des améliorations à la page d’inventaire de l'ordinateur virtuel, la fonctionnalité de partage de fichiers, l'intégration de la gestion des mises à jour Azure et bien plus encore. 
- Version [1806](https://aka.ms/WACPreview1806-InsiderBlog) ajoute l'affichage du script PowerShell, la gestion SDN, les connexions à 2008 R2, SDN, les tâches planifiées et beaucoup d’autres améliorations.
- Version 1804.25 : mise à jour de maintenance pour prendre en charge les utilisateurs qui installent Windows Admin Center dans des environnements entièrement hors ligne.
- Version [1804](https://cloudblogs.microsoft.com/windowsserver/2018/04/12/announcing-windows-admin-center-our-reimagined-management-experience/) : le projet Honolulu devient Windows Admin Center et ajoute des fonctionnalités de sécurité et de contrôle d’accès en fonction du rôle. Notre première version GA.
- La version [1803](https://blogs.windows.com/windowsexperience/2018/03/13/announcing-project-honolulu-technical-preview-1803-and-rsat-insider-preview-for-windows-10) a ajouté la prise en charge du contrôle d’accès Azure AD, la journalisation détaillée, le contenu redimensionnable et une série d’améliorations de l’outil.
- La version [1802](https://blogs.windows.com/windowsexperience/2018/02/13/announcing-windows-server-insider-preview-build-17093-project-honolulu-technical-preview-1802) a ajouté la prise en charge de l’accessibilité, de la localisation, des déploiements à haute disponibilité, du marquage, des paramètres de l’hôte Hyper-V et de l'authentification de passerelle.
- La version [1712](https://blogs.windows.com/windowsexperience/2017/12/19/announcing-project-honolulu-technical-preview-1712-build-05002) a ajouté d'autres fonctionnalités de machine virtuelle et des améliorations des performances dans tous les outils.
- La version [1711](https://cloudblogs.microsoft.com/windowsserver/2017/12/01/1711-update-to-project-honolulu-technical-preview-is-now-available/) a ajouté des outils très attendus (Bureau à distance et PowerShell), ainsi que d’autres améliorations.
- La version [1709](https://cloudblogs.microsoft.com/windowsserver/2017/09/22/project-honolulu-technical-preview-is-now-available-for-download/) a été lancée comme notre première version d’évaluation publique.

## <a name="stay-updated"></a>Restez informé

<a target="_blank" class="mscom-link twitter-follow-link" title="Suivez-nous sur Twitter" aria-label="Follow us on Twitter" data-info="Twitter" href="https://twitter.com/servermgmt"><picture><source srcset="//img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/REOolR" media="(min-width:0)"><img srcset="//img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/REOolR" alt="Follow us on Twitter" src="//img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/REOolR"></picture></a>
 | 
<a target="_blank" class="mscom-link blogs-follow-link" title="Lisez nos Blogs" aria-label="Visit our Blogs" data-info="Blogs" href="https://blogs.technet.microsoft.com/servermanagement/"><picture><source srcset="//img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/REOtyw" media="(min-width:0)"><img srcset="//img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/REOtyw" alt="Follow us on Blogs" src="//img-prod-cms-rt-microsoft-com.akamaized.net/cms/api/am/imageFileData/REOtyw"></picture></a>