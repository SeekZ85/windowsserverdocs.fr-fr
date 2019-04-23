---
title: Pourquoi des stations de travail accès privilégié peut vous aider à sécuriser votre organisation
description: Comment PAW peut augmenter la posture de sécurité de votre organisation
ms.prod: windows-server-threshold
ms.topic: article
ms.assetid: 93589778-3907-4410-8ed5-e7b6db406513
ms.date: 02/14/2019
ms.author: joflore
author: MicrosoftGuyJFlo
manager: daveba
ms.reviewer: mas
ms.openlocfilehash: fd87ef674fcfefa8e2dc1d7122de64ed8f5510a0
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59891260"
---
# <a name="privileged-access-workstations"></a>Stations de travail à accès privilégié

>S'applique à : Windows Server

Les stations de travail à accès privilégié (PAW) fournissent un système d’exploitation dédié pour que les tâches sensibles soient protégées contre les attaques sur Internet et les vecteurs de menace. Séparer ces tâches et comptes sensibles des stations de travail et appareils utilisés quotidiennement offre une très forte protection contre les attaques par hameçonnage, les vulnérabilités d’applications et du système d’exploitation, diverses attaques d’emprunt d’identité, et les vols d’informations d’identification, par exemple par enregistrement de frappe, [Pass-the-Hash](https://www.microsoft.com/en-us/download/details.aspx?id=36036) ou [Pass-the-Ticket](https://download.microsoft.com/download/7/7/A/77ABC5BD-8320-41AF-863C-6ECFB10CB4B9/Mitigating%20Pass-the-Hash%20(PtH)%20Attacks%20and%20Other%20Credential%20Theft%20Techniques_English.pdf).

## <a name="what-is-a-privileged-access-workstation"></a>Qu’est une station de travail d’accès privilégié ?

En termes plus simples, un PAW est une station de travail renforcée et verrouillée conçue pour offrir des garanties de haute sécurité pour les tâches et comptes sensibles.  Les PAW sont recommandés pour l’administration des systèmes d’identité, les services cloud et la structure de cloud privé ainsi que les fonctions sensibles de l’entreprise.

> [!NOTE]
> L’architecture PAW ne nécessite pas un mappage 1:1 des comptes sur les postes de travail, même s’il s’agit d’une configuration courante. Un PAW crée un environnement de station de travail de confiance qui peut être utilisé par un ou plusieurs comptes.

Afin d’offrir la plus grande sécurité, les Paw doivent toujours exécuter le système d’exploitation plus récente et plus sécurisé disponible : Microsoft recommande fortement Windows 10 entreprise, qui inclut un certain nombre de fonctionnalités de sécurité supplémentaires non disponibles dans d’autres éditions (en particulier, [Credential Guard](https://technet.microsoft.com/library/mt483740%28v=vs.85%29.aspx) et [Device Guard](https://technet.microsoft.com/library/dn986865(v=vs.85).aspx)).

> [!NOTE]
> Les organisations sans accès à Windows 10 Entreprise peuvent utiliser Windows 10 Pro, qui comprend de nombreuses technologies fondamentales critiques pour les PAW, y compris Trusted Boot, BitLocker et Bureau à distance.  Les utilisateurs du secteur de l’éducation peuvent utiliser Windows 10 Éducation.  Windows 10 Édition familiale ne doit pas être utilisé pour un PAW.
>
> Pour un tableau de comparaison des différentes éditions de Windows 10, lisez [cet article](https://www.microsoft.com/en-us/WindowsForBusiness/Compare).

Les contrôles de sécurité dans le PAW visent à atténuer l’impact le plus élevé et les risques les plus probables de compromission. Ils comprennent notamment l’atténuation des attaques sur l’environnement et l’atténuation des risques que les contrôles du PAW se dégradent au fil du temps :

* **Attaques Internet** - La plupart des attaques proviennent de sources Internet, directement ou indirectement, et utilisent Internet pour l’exfiltration, les commandes et le contrôle (C2). Isoler le PAW de l’Internet public est un élément clé pour garantir que le PAW n’est pas compromis.
* **Risques liés à la facilité d’utilisation** - Si un PAW est trop difficile à utiliser pour les tâches quotidiennes, les administrateurs seront encouragés créer des solutions de contournement pour faciliter leurs tâches. Fréquemment, ces solutions de contournement exposent la station de travail d’administration et les comptes à des risques de sécurité substantiels, il est donc essentiel d’impliquer et permettre aux utilisateurs du PAW et d’atténuer ces problèmes de facilité d’utilisation de façon sûre. Cela se fait souvent en écoutant leurs commentaires, en installant des outils et scripts requis pour leur travail et en veillant à ce que le personnel administratif comprenne pourquoi il doit utiliser un PAW, ce qu’est un PAW et comment l’utiliser correctement et avec succès.
* **Risques de l’environnement** - Étant donné que de nombreux autres ordinateurs et comptes de l’environnement sont exposés aux risques d’Internet directement ou indirectement, un PAW doit être protégé contre les attaques de ressources compromises dans l’environnement de production. Cela nécessite de limiter au strict minimum nécessaire les outils de gestion et les comptes qui ont accès au PAW pour sécuriser et surveiller ces stations de travail spécialisées.
* **Falsification de la chaîne logistique** - S’il est impossible d’éliminer tous les risques possibles de falsification de la chaîne logistique pour le matériel et les logiciels, vous pouvez atténuer les vecteurs d’attaque critiques qui sont accessibles aux pirates en prenant quelques mesures essentielles. Cela comprend la validation de l’intégrité de tous les supports d’installation ([principe de source propre](http://aka.ms/cleansource)) et l’utilisation d’un fournisseur approuvé et digne de confiance pour le matériel et les logiciels.
* **Attaques physiques** - Les PAW pouvant être physiquement mobiles et utilisés en dehors des emplacements physiquement sécurisés, ils doivent être protégés contre les attaques qui exploitent l’accès physique à l’ordinateur.

> [!NOTE]
> Un PAW ne protègera pas un environnement d’un pirate qui a déjà acquis un accès administratif sur une forêt Active Directory.
> De nombreuses implémentations existantes des services de domaine Active Directory ayant été utilisées pendant des années, au risque du vol d’informations d’identification, les organisations doivent considérer que des violations ont eu lieu et envisager la possibilité d’une compromission de domaine ou d’une perte d’informations d’identification d’administrateur non détectée. Une organisation qui soupçonne la compromission d’un domaine doit envisager l'utilisation des services de réponse aux incidents professionnels.
>
> Pour plus d’informations sur les instructions de réponse et de récupération, consultez « Répondre à une activité suspecte » et « Récupérer d’une violation » de [Limitation de Pass-the-Hash et autres vols d’informations d’identification](https://www.microsoft.com/pth), version 2.
>
> Visitez la page [Services de réponse aux incidents et de récupération de Microsoft](https://www.microsoft.com/en-us/microsoftservices/campaigns/cybersecurity-protection.aspx) pour plus d’informations.

### <a name="paw-hardware-profiles"></a>Profils matériels PAW

Le personnel d’administration est également composé d’utilisateurs standard : ils doivent avoir non seulement une PAW, mais aussi une station de travail utilisateur standard pour consulter leur messagerie électronique, naviguer sur le web et accéder aux applications métier de l’entreprise.  Il est essentiel de s’assurer que les administrateurs peuvent rester productifs et sécurisés pour le succès du déploiement d’un PAW.  Une solution de sécurité qui limite considérablement la productivité est abandonnée par les utilisateurs en faveur de ce qui améliore la productivité (même si la solution n’est pas sécurisée).

Afin d’équilibrer les besoins de sécurité et ceux de productivité, Microsoft recommande d’utiliser un de ces profils de matériel de PAW :

* **Matériel dédié** - Séparer les appareils dédiés aux tâches de l’utilisateur et aux tâches d’administration
* **Utilisation simultanée** - Un appareil unique qui peut exécuter les tâches d’administration et les tâches utilisateur simultanément en tirant parti de la virtualisation du système d’exploitation ou de la présentation.

Les organisations peuvent utiliser un seul profil ou les deux. Il n’y aucun problème d’interopérabilité entre les profils matériels, et les organisations ont la flexibilité nécessaire pour faire correspondre le profil matériel aux à la situation et aux besoins spécifiques d’un administrateur donné.

> [!NOTE]
> Il est essentiel que, dans tous ces scénarios, le personnel administratif reçoive un compte utilisateur standard qui est distinct du ou des comptes administratifs. Les comptes administratifs doivent uniquement être utilisés sur le système d’exploitation du PAW.

Ce tableau récapitule les avantages et inconvénients relatifs de chaque profil matériel du point de vue de la facilité d’utilisation opérationnelle, de la productivité et de la sécurité.  Les deux approches matérielles fournissent une sécurité renforcée pour les comptes administrateur contre le vol et la réutilisation d’informations d’identification.

|**Scénario**|**Avantages**|**Inconvénients**|
|--------|---------|-----------|
|Matériel dédié|-   Signal fort pour la sensibilité des tâches<br />-   Meilleure séparation de sécurité|-   Espace supplémentaire sur le bureau<br />-   Poids supplémentaires (pour le travail à distance)<br />-   Coût du matériel|
|Utilisation simultanée|-   Coût matériel réduit<br />-   Expérience sur appareil unique|-   Le partage de clavier/souris entraîne des risques d’erreurs|

Ce guide contient des instructions détaillées pour la configuration de PAW pour l’approche de matériel dédié. Si vous avez des exigences pour les profils matériels à utilisation simultanée, vous pouvez adapter les instructions vous-même sur la base de ce guide, ou passer par une entreprise de services professionnels comme Microsoft pour vous aider.

#### <a name="dedicated-hardware"></a>Matériel dédié

Dans ce scénario, nous utilisons pour l’administration un PAW complètement distinct de l’ordinateur qui est utilisé pour les activités quotidiennes telles que la consultation du courrier électronique, la modification de documents et le travail de développement. Toutes les applications et tous les outils d’administration sont installés sur le PAW, et toutes les applications de productivité sont installées sur la station de travail utilisateur standard. Les instructions étape par étape de ce guide sont basées sur ce profil matériel.

#### <a name="simultaneous-use---adding-a-local-user-vm"></a>Utilisation simultanée - Ajout d’un utilisateur local de machine virtuelle

Dans ce scénario d’utilisation simultanée, un PC unique est utilisé pour les tâches d’administration et les activités quotidiennes telles que la consultation du courrier électronique, la modification de documents et le travail de développement. Dans cette configuration, le système d’exploitation utilisateur est disponible hors connexion (pour modifier des documents et travailler sur la messagerie électronique mise en cache localement), mais elle requiert du matériel et des processus de support prenant en charge cet état déconnecté.

![Diagramme montrant, dans un scénario d’utilisation simultanée, un PC unique utilisé pour les tâches d’administration et les activités quotidiennes telles que la consultation du courrier électronique, la modification de documents et le travail de développement](../media/privileged-access-workstations/PAWFig10.JPG)

Le matériel physique exécute deux systèmes d’exploitation localement :

* **Système d’exploitation admin** - L’hôte physique exécute Windows 10 sur l’hôte PAW pour les tâches administratives
* **Système d’exploitation de l’utilisateur** - Une machine virtuelle invitée Hyper-V sur client Windows 10 exécute une image d’entreprise

Avec Windows 10 Hyper-V, une machine de virtuelle invitée (également en cours d’exécution Windows 10) peut avoir une expérience utilisateur riche, y compris son, vidéo et les applications de communication Internet comme Skype for Business.

Dans cette configuration, les tâches quotidiennes qui ne nécessitent pas de privilèges d’administrateur s’effectuent dans la machine virtuelle du système d’exploitation utilisateur qui possède une image Windows 10 d’entreprise ordinaire, et ne sont pas soumises aux restrictions appliquées à l’hôte PAW. Toutes les tâches d’administration sont effectuées sur le système d’exploitation de l’administrateur.

Pour configurer cela, suivez les instructions de ce guide pour l’hôte PAW, ajoutez les fonctionnalités de client Hyper-V, créez une machine virtuelle utilisateur, puis installez une image d’entreprise Windows 10 sur la machine virtuelle utilisateur.

Lisez l’article sur le [Client Hyper-V](https://technet.microsoft.com/library/hh857623.aspx) article pour plus d’informations sur cette fonctionnalité. Veuillez noter que le système d’exploitation dans les machines virtuelles invitées doivent disposer d’une licence par [Licence produit Microsoft ](https://www.microsoft.com/en-us/Licensing/product-licensing/products.aspx), ce qui est également décrit [ici](https://www.microsoft.com/en-us/Licensing/learn-more/brief-windows-virtual-machine.aspx).

#### <a name="simultaneous-use---adding-remoteapp-rdp-or-a-vdi"></a>Utilisation simultanée - Ajout de RemoteApp, RDP ou une infrastructure VDI

Dans ce scénario d’utilisation simultanée, un PC unique est utilisé pour les tâches d’administration et les activités quotidiennes telles que la consultation du courrier électronique, la modification de documents et le travail de développement. Dans cette configuration, les systèmes d’exploitation utilisateur sont déployés et gérés de façon centralisée (sur le cloud ou dans votre centre de données), mais ne sont pas disponibles hors connexion.

![Figure montrant, dans un scénario d’utilisation simultanée, un PC unique utilisé pour les tâches d’administration et les activités quotidiennes telles que la consultation du courrier électronique, la modification de documents et le travail de développement](../media/privileged-access-workstations/PAWFig11.JPG)

Le matériel physique exécute un seul système d’exploitation PAW localement pour les tâches administratives et contacte un service de bureau à distance Microsoft ou tiers pour les applications utilisateur telles que la messagerie, la modification de documents et les applications d’entreprise.

Dans cette configuration, les tâches quotidiennes qui ne nécessitent pas de privilèges d’administrateur s’effectuent dans le ou les systèmes d’exploitation à distance et les applications qui ne sont pas soumises aux restrictions appliquées à l’hôte PAW. Toutes les tâches d’administration sont effectuées sur le système d’exploitation de l’administrateur.

Pour ce faire, suivez les instructions de ce guide pour l’hôte PAW, autorisez la connectivité réseau pour les services de bureau à distance, puis ajoutez des raccourcis au bureau de l’utilisateur PAW pour accéder aux applications. Les services de bureau à distance peuvent être hébergés de nombreuses façons, dont les suivantes :

* Un service de bureau à distance ou VDI existant (local ou dans le cloud)
* Un nouveau service que vous installez en local ou dans le cloud
* Azure RemoteApp avec des modèles Office 365 préconfigurés ou vos propres images d’installation

Pour plus d'informations sur Azure RemoteApp, visitez [cette page](https://www.remoteapp.windowsazure.com).

## <a name="how-microsoft-is-using-administrative-workstations"></a>Comment Microsoft utilise les stations de travail administratives

Chez Microsoft, nous utilisons l’approche d’architecturale PAW en interne sur nos systèmes ainsi qu’avec nos clients. Microsoft utilise des stations de travail administratives en interne pour un certain nombre de fonctions, notamment l’administration de l’infrastructure informatique de Microsoft, le développement et l’exploitation de l’infrastructure cloud Microsoft, et d’autres ressources à valeur élevée.

Ce guide est directement basé sur l’architecture de référence de station de travail d’accès privilégié (PAW) déployé par nos équipes de services professionnels en cybersécurité pour protéger les clients contre les attaques de sécurité. Les stations de travail administratives sont également un élément clé de la protection la plus robuste pour les tâches d’administration, l’architecture de référence de forêt d’administration améliorée sécurité Enhanced Security Administrative Environment (ESAE).

Pour plus d’informations sur la forêt d’administration ESAE, consultez la section [Approche de conception de la forêt d’administration ESAE](http://aka.ms/ESAE) dans[Référence sur la sécurisation de l’accès privilégié](../securing-privileged-access/securing-privileged-access-reference-material.md).

## <a name="architecture-overview"></a>Présentation de l'architecture

Le schéma ci-dessous représente un « canal » distinct pour l’administration (une tâche très sensible) qui est créé en conservant des comptes et stations de travail d’administration dédiés.

![Diagramme montrant un « canal » distinct d’administration (une tâche très sensible) créé en conservant des comptes et stations de travail d’administration dédiés](../media/privileged-access-workstations/PAWFig1.JPG)

Cette approche architecturale s’appuie sur les protections trouvées dans la [Protection des informations d’identification](https://technet.microsoft.com/library/mt483740%28v=vs.85%29.aspx) et la [Protection des appareils](https://technet.microsoft.com/library/dn986865(v=vs.85).aspx) de Windows 10, et va au-delà de ces protections pour les comptes et tâches sensibles.

Cette méthodologie est appropriée pour les comptes ayant accès aux ressources à valeur élevée :

* **Des privilèges d’administrateur** -Paw fournissent offrent une sécurité accrue pour impact élevé rôles administratifs informatiques et les tâches. Cette architecture peut être appliquée à l’administration de nombreux types de systèmes, y compris les domaines et forêts Active Directory, les clients Microsoft Azure Active Directory, les clients Office 365, les réseaux de contrôle de processus (PCN), les systèmes de contrôle et de collecte de données (SCADA) et de contrôle des systèmes, les guichets automatiques de banque et les appareils de point de vente (PoS).
* **Professionnels de l’Information de sensibilité élevées** -l’approche utilisée dans un PAW peut également fournir une protection pour les tâches de travail des informations hautement confidentielles et personnel comme ceux impliquant avant fusion et acquisition d’activité d’annonce, en version préliminaire rapports financiers, présence de l’organisation de médias sociaux, communications d’executive, les secrets commerciaux non brevetées, sensibles des recherches et autres données propriétaires ou sensibles. Ce guide n’aborde pas la configuration de ces scénarios de traitement des informations en profondeur, et n’inclut pas ce scénario dans les instructions techniques.

    > [!NOTE]
    > Microsoft IT utilise les PAW (appelés en interne « stations de travail admin sécurisées », ou SAW) pour gérer l’accès sécurisé à des systèmes à haute valeur au sein de Microsoft. Ce guide propose ci-dessous des détails supplémentaires sur l’utilisation de PAW chez Microsoft dans la section « Comment Microsoft utilise les stations de travail admin ». Pour plus d’informations sur cette approche d’environnement de ressources à haute valeur, reportez-vous à l’article [Protection des de ressources à haute valeur avec les stations de travail admin sécurisées](https://msdn.microsoft.com/en-us/library/mt186538.aspx).

Ce document décrit pourquoi cette pratique est recommandée pour la protection des comptes privilégiés à impact élevé, à quoi ces solutions PAW ressemblent pour la protection des privilèges administratifs et comment déployer rapidement une solution PAW pour l’administration de services cloud et de domaine.

Ce document fournit des instructions détaillées sur l’implémentation de plusieurs configurations PAW et inclut des instructions d’implémentation détaillées pour vous aider à commencer à protéger des comptes à impact élevé :

* [**Phase 1 : déploiement immédiat pour les administrateurs Active Directory** ](#phase-1-immediate-deployment-for-active-directory-administrators) ainsi rapidement un PAW qui peut protéger en local, les rôles d’administration de domaine et de forêt
* [**Phase 2 - étendre les PAW à tous les administrateurs** ](#phase-2-extend-paw-to-all-administrators) Active la protection pour les administrateurs de services cloud comme Office 365 et Azure, des serveurs d’entreprise, des applications d’entreprise et des stations de travail
* [**Phase 3 - sécurité avancée avec PAW** ](#phase-3-extend-and-enhance-protection) traite les protections supplémentaires et les considérations relatives à la sécurité PAW

### <a name="why-dedicated-workstations"></a>Pourquoi dédié de stations de travail ?

L’environnement de menace actuel pour les organisations est truffé d’hameçonnages sophistiqués et d’autres attaques Internet qui constituent une menace de sécurité continue pour les comptes et stations de travail exposés à Internet.

Cet environnement de menace doit pousser les organisations à adopter une posture de sécurité qui suppose qu’une brèche a déjà été ouverte lors de la conception des protections pour les ressources à valeur élevée, comme les comptes d’administration et les ressources sensibles de l’entreprise. Ces ressources à valeur élevée doivent être protégées contre les menaces directes sur Internet ainsi que contre les attaques montées à partir d’autres stations de travail, serveurs et appareils de l’environnement.

![Figure montrant le risque pour les ressources gérées si un pirate prend le contrôle d’une station de travail utilisateur contenant des informations d’identification sensibles](../media/privileged-access-workstations/PAWFig2.JPG)

Cette illustration décrit les risques pour les ressources gérées si un pirate gagne le contrôle d’une station de travail utilisateur où des informations d’identification sensibles sont utilisées.

Un pirate aux commandes d’un système d’exploitation a plusieurs façons d’accéder à toutes les activités sur la station de travail et d’emprunter l’identité du compte légitime. Diverses techniques d’attaque connues et inconnues permettent d’obtenir ce niveau d’accès. Les volumes croissants et la sophistication des cyberattaques ont rendu nécessaire d’étendre ce concept de séparation pour séparer complètement les systèmes d’exploitation client pour les comptes sensibles. Pour plus d’informations sur ces types d’attaques, visitez le [site web Pass The Hash](https://www.microsoft.com/pth) pour des livres blancs, des vidéos et plus encore.

L’approche PAW est une extension de la pratique recommandée établie d’utiliser des comptes d’utilisateur et d’administration séparés pour le personnel administratif. Cette pratique utilise un compte d’administration affecté de manière individuelle, qui est complètement distinct du compte standard de l’utilisateur. PAW s’appuie sur cette pratique de séparation des comptes en fournissant une station de travail de confiance pour les comptes sensibles.

Ce guide PAW est conçu pour vous aider à implémenter cette fonctionnalité pour la protection des comptes importants, comme les comptes d’administrateurs informatiques à privilèges élevés et les comptes d’entreprise à haute sensibilité. Le guide vous aide à :

* Limiter l’exposition des informations d’identification aux seuls hôtes approuvés
* Fournir une station de travail haute sécurité aux administrateurs afin de pouvoir facilement effectuer les tâches d’administration.

La restriction des comptes sensibles à l’utilisation exclusive de PAW renforcés est une protection simple pour ces comptes, facilement utilisable pour les administrateurs et très difficile à défaire pour les pirates.

### <a name="alternate-approaches"></a>Autres approches

Cette section contient des informations de comparaison de la sécurité des approches alternatives par rapport à PAW, et sur la façon d’intégrer correctement ces approches dans une architecture PAW. Toutes ces approches comportent des risques importants lors de l’implémentation de manière isolée, mais peuvent ajouter de valeur à une implémentation PAW dans certains scénarios.

#### <a name="credential-guard-and-windows-hello-for-business"></a>Credential Guard et Windows Hello entreprise

Nouvelle fonctionnalité de Windows 10, la [Protection des informations d’identification](https://technet.microsoft.com/library/mt483740%28v=vs.85%29.aspx) utilise une sécurité basée sur le matériel et la virtualisation pour atténuer les vols d’informations d’identification courantes, par exemple de type Pass-the-Hash, en protégeant les informations d’identification dérivées. La clé privée pour les informations d’identification utilisées par [Windows Hello entreprise](http://aka.ms/passport) peut être également être protégé par le matériel du Module de plateforme sécurisée (TPM).

Il s’agit d’atténuations puissantes, mais les stations de travail peuvent encore être vulnérables à certaines attaques même si les informations d’identification sont protégées par Credential Guard ou Windows Hello entreprise. Les attaques peuvent inclure l’utilisation abusive des privilèges et l’utilisation des informations d’identification directement à partir d’un appareil, la réutilisation des informations d’identification précédemment volées avant l’activation de Credential Guard et les abus d’outils de gestion et de configurations d’applications faibles sur la station de travail.

Le guide PAW de cette section comprend l’utilisation d’un grand nombre de ces technologies pour les comptes et tâches à sensibilité élevée.

#### <a name="administrative-vm"></a>Machines virtuelles administratives

Une machine virtuelle d’administration (administrateur VM) est un système d’exploitation dédié aux tâches administratives hébergé sur un ordinateur de bureau utilisateur standard. Cette approche est similaire à PAW, en cela qu’elle fournit un système d’exploitation dédié pour les tâches administratives. Son erreur potentiellement fatale est que machine virtuelle administrative repose sur l’ordinateur de bureau d’utilisateur standard pour sa sécurité.

Le diagramme ci-dessous illustre la capacité des pirates à suivre la chaîne de contrôle vers l’objet d’intérêt cible avec une machine virtuelle administrative sur une station de travail utilisateur, et le fait qu’il est difficile de créer un chemin sur la configuration inverse.

L’architecture PAW ne permet pas d’héberger une VM administrateur sur une station de travail utilisateur, mais une machine virtuelle d’utilisateur avec une image d’entreprise standard peut être hébergée sur un PAW à l’administrateur pour fournir au personnel un PC unique pour toutes les responsabilités.

![Diagramme de l’architecture PAW](../media/privileged-access-workstations/PAWFig9.JPG)

#### <a name="jump-server"></a>Serveur de renvoi

Les architectures de serveur de renvoi administratif configurent un petit nombre de serveurs de console d’administration et restreignent l’utilisation par le personnel pour les tâches administratives. Cela se base généralement sur les services de bureau à distance, une solution de virtualisation de présentation tierce ou une technologie Virtual Desktop Infrastructure (VDI).

Cette approche est souvent proposée pour atténuer les risques pour l’administration et offre des garanties de sécurité, mais l’approche de serveur de renvoi elle-même est vulnérable à certaines attaques, car elle ne respecte pas le [principe de source propre](http://aka.ms/cleansource). Le principe de source propre nécessite que toutes les dépendances de sécurité aient au moins le niveau de confiance de l’objet sécurisé.

![Figure montrant une relation de contrôle simple](../media/privileged-access-workstations/PAWFig3.JPG)

Cette illustration présente une relation de contrôle simple. N’importe quel sujet ayant le contrôle d’un objet est une dépendance de sécurité de cet objet. Si un pirate peut contrôler une dépendance de sécurité d’un objet cible (sujet), il peut contrôler cet objet.

La session administrative sur le serveur de renvoi s’appuie sur l’intégrité de l’ordinateur local qui y accède. Si cet ordinateur est une station de travail utilisateur soumise à des attaques par hameçonnage et d’autres vecteurs d’attaque sur Internet, la session d’administration est également exposée à ces risques.

![Figure montrant comment les pirates peuvent suivre une chaîne de contrôle établie pour atteindre l’objet ciblé](../media/privileged-access-workstations/PAWFig4.JPG)

L’illustration ci-dessus montre comment les pirates peuvent suivre une chaîne de contrôle établie vers l’objet d’intérêt cible.

Bien que certains contrôles de sécurité avancés, comme l’authentification multifacteur peuvent augmenter la difficulté pour un utilisateur malveillant de prendre le contrôle de cette session d’administration à partir de la station de travail utilisateur, aucune fonctionnalité de sécurité ne peut entièrement protéger des attaques techniques lorsqu’une personne malveillante a l’accès administratif à l’ordinateur source (par exemple, injection de commandes illicites dans une session légitime, piratage de processus légitimes, et ainsi de suite.)

La configuration par défaut dans ce guide de PAW installe les outils d’administration sur le PAW, mais une architecture de serveur de renvoi peut également être ajoutée si nécessaire.

![Figure montrant comment l’inversion de la relation de contrôle et l’accès aux applications utilisateur à partir d’une station de travail d’administration ne laissent au pirate aucun chemin d’accès à l’objet ciblé](../media/privileged-access-workstations/PAWFig5.JPG)

Cette illustration montre comment inverser la relation de contrôle et l’accès aux applications de l’utilisateur à partir d’une station de travail administrateur ne laisse à l’attaquant aucun chemin d’accès à l’objet ciblé. Le serveur de renvoi de l’utilisateur est toujours exposé à des risques, aussi des contrôles de protection, des contrôles de détection et des processus de réponse appropriés doivent toujours être appliqués pour cet ordinateur sur Internet.

Cette configuration nécessite que les administrateurs suivent scrupuleusement les pratiques opérationnelles afin d’éviter la saisie accidentelle des informations d’identification de l’administrateur dans la session utilisateur sur l’ordinateur de bureau.

![Figure montrant comment l’accès à un serveur de renvoi administratif à partir d’un PAW ne permet pas à un pirate d’accéder aux ressources d’administration](../media/privileged-access-workstations/PAWFig6.JPG)

Cette illustration montre comment accéder à un serveur de renvoi administratif à partir d’un PAW n’ajoute aucun chemin d’accès pour le pirate dans les ressources d’administration. Un serveur de renvoi avec un PAW permet dans ce cas de consolider le nombre d’emplacements pour l’activité de surveillance administrative et de distribuer des outils et applications d’administration. Cela ajoute une certaine complexité à la conception, mais peut simplifier les mises à jour de logiciels et la surveillance de la sécurité si un grand nombre de comptes et de stations de travail sont utilisés dans votre implémentation PAW. Le serveur de renvoi doit être développé et configuré à des normes de sécurité équivalentes à celles du PAW.

#### <a name="privilege-management-solutions"></a>Solutions de gestion des privilèges

Les solutions de gestion des privilèges sont des applications qui fournissent un accès temporaire à privilèges discrets ou des comptes privilégiés à la demande. Les solutions de gestion des privilèges sont un composant primordial d’une stratégie complète pour sécuriser l’accès privilégié et fournir une visibilité extrêmement importante et plus de transparence pour les activités administratives.

Ces solutions utilisent généralement un flux de travail flexible pour accorder l’accès et beaucoup ont des fonctionnalités de sécurité supplémentaires comme la gestion des mots de passe de compte de service et l’intégration avec les serveurs de renvoi administratifs. Il existe de nombreuses solutions sur le marché qui fournissent des fonctionnalités de gestion des privilèges, une d’elles étant la gestion de l’accès privilégié (PAM) de Microsoft Identity Manager.

Microsoft recommande d’utiliser un PAW pour accéder aux solutions de gestion des privilèges d’accès. L’accès à ces solutions doit être accordé uniquement aux PAW. Microsoft ne recommande pas l’utilisation de ces solutions en remplacement d’un PAW, car l’accès à des privilèges à l’aide de ces solutions à partir d’un ordinateur de bureau utilisateur potentiellement compromis ne respecte pas le principe de [source propre](http://aka.ms/cleansource), comme illustré dans le diagramme ci-dessous :

![Diagramme montrant pourquoi Microsoft ne recommande pas l’utilisation de ces solutions à la place d’un PAW, car l’accès à des privilèges à l’aide de ces solutions à partir d’un ordinateur de bureau potentiellement compromis ne respecte pas le principe de source propre](../media/privileged-access-workstations/PAWFig7.JPG)

Fournir un PAW pour accéder à ces solutions vous permet d’offrir les avantages de sécurité de PAW et la solution de gestion de privilèges, comme illustré dans ce diagramme :

![Diagramme montrant comment la mise à disposition d’un PAW pour accéder à ces solutions vous offre les avantages de sécurité de PAW et de la solution de gestion de privilèges](../media/privileged-access-workstations/PAWFig8.JPG)

> [!NOTE]
> Ces systèmes doivent être classés au niveau le plus élevé du privilège qu’ils gèrent être protégés au même niveau ou au-dessus de ce niveau de sécurité. Ils sont généralement configurés pour gérer des solutions de niveau 0 et des ressources de niveau 0, et doivent être classés au niveau 0.
> Pour plus d’informations sur le modèle de couche, consultez [ http://aka.ms/tiermodel ](http://aka.ms/tiermodel) pour plus d’informations sur les groupes de niveau 0, consultez l’équivalence de niveau 0 dans [sécurisation de la documentation de référence de l’accès privilégié](../securing-privileged-access/securing-privileged-access-reference-material.md).

Pour plus d’informations sur le déploiement de gestion des accès Microsoft Identity Manager (MIM) privilégié (PAM), consultez [http://aka.ms/mimpamdeploy](http://aka.ms/mimpamdeploy)

## <a name="paw-scenarios"></a>Scénarios PAW

Cette section contient des conseils sur les scénarios auxquels ce guide de PAW doit être appliqué. Dans tous ces scénarios, les administrateurs doivent être formés à utiliser uniquement les PAW pour effectuer le support des systèmes distants. Pour encourager une utilisation réussie et sécurisée, tous les utilisateurs de PAW doivent également être encouragés à partager leurs commentaires pour améliorer l’expérience PAW, et ces commentaires doivent être examinés attentivement pour l’intégration avec votre programme PAW.

Dans tous les scénarios, les renforcement supplémentaires lors des phases ultérieures et les différents profils matériels de ce guide peuvent être utilisés pour satisfaire les besoins de facilité d’utilisation et de sécurité des rôles.

> [!NOTE]
> Ce guide différencie explicitement l’accès à des services spécifiques sur internet (par exemple, les portails d’administration Azure et Office 365) et « L’Internet ouvert » de tous les hôtes et les services.

Pour plus d’informations sur les désignations, consultez la [page relative au modèle de niveau](http://aka.ms/tiermodel).

|**Scénarios**|**Utiliser PAW ?**|**Considérations de sécurité et d’étendue**|
|---------|--------|---------------------|
|Administrateurs Active Directory - Niveau 0|Oui|Un PAW créé avec le guide de Phase 1 est suffisant pour ce rôle.<br /><br />-   Une forêt d’administration peut être ajoutée pour fournir le meilleur niveau de protection pour ce scénario. Pour plus d’informations sur la forêt d’administration ESAE, consultez [Approche de conception de la forêt d’administration ESAE](http://aka.ms/esae)<br />-   Un PAW permet de gérer plusieurs domaines ou forêts.<br />-Si les contrôleurs de domaine sont hébergés sur une Infrastructure as a Service (IaaS) ou d’une solution de virtualisation sur site, vous devez définir des priorités l’implémentation des Paw pour les administrateurs de ces solutions.|
|Administration des services Azure IaaS et PaaS - Niveau 0 ou 1 (voir Considérations de conception et d’étendue)|Oui|Un PAW créé à l’aide de l’aide fournie dans la Phase 2 est suffisant pour ce rôle.<br /><br />-   Les PAW doivent être utilisés au moins pour l’administrateur global et l’administrateur de facturation des abonnements. Vous pouvez également utiliser les PAW pour les administrateurs délégués des serveurs critiques ou sensibles.<br />-Les Paw doivent être utilisés pour gérer le système d’exploitation et applications qui fournissent la synchronisation d’annuaires et fédération d’identité pour les services cloud comme [Azure AD Connect](https://azure.microsoft.com/documentation/articles/active-directory-aadconnect/) et Active Directory Federation Services (ADFS).<br />-   Les restrictions du réseau sortant doivent autoriser la connectivité uniquement aux services de cloud autorisés à l’aide du guide de la Phase 2. Aucun accès Internet ouvert ne doit être autorisé à partir des PAW.<br />-Windows Defender Exploit Guard doit être configuré sur la station de travail **Remarque :**     Un abonnement est considéré comme niveau 0 pour une forêt si des contrôleurs de domaine ou d’autres hôtes de niveau 0 se trouvent dans l’abonnement. Un abonnement est de niveau 1 si aucun serveur de niveau 0 n’est hébergé dans Azure.|
|Locataire administrateur d’Office 365 <br />- Niveau 1|Oui|Un PAW créé à l’aide de l’aide fournie dans la Phase 2 est suffisant pour ce rôle.<br /><br />-   Des PAW doivent être utilisés au moins pour l’administrateur de facturation des abonnements, l’administrateur global, l’administrateur d’Exchange, l’administrateur de SharePoint et les rôles d’administration de gestion des utilisateurs. Vous devez également fortement envisager l’utilisation de PAW pour les administrateurs délégués de données très sensibles ou critiques.<br />-Windows Defender Exploit Guard doit être configuré sur la station de travail.<br />-   Les restrictions du réseau sortant doivent autoriser la connectivité uniquement aux services de Microsoft à l’aide du guide de la Phase 2. Aucun accès Internet ouvert ne doit être autorisé à partir des PAW.|
|Admin d’un autre service IaaS ou PaaS<br />- Niveau 0 ou 1 (voir Considérations de conception et d’étendue)||Un PAW créé à l’aide de l’aide fournie dans la Phase 2 est suffisant pour ce rôle.<br /><br />-   Des PAW doivent être utilisés pour n’importe quel rôle qui possède des droits administratifs sur les machines virtuelles hébergées sur cloud, y compris la capacité à installer des agents, l’exportation des fichiers de disque dur ou l’accès au stockage sur lequel sont stockés des disques durs dotés de systèmes d’exploitation, des données sensibles ou des données d’entreprise critiques.<br />-   Les restrictions du réseau sortant doivent autoriser la connectivité uniquement aux services de Microsoft à l’aide du guide de la Phase 2. Aucun accès Internet ouvert ne doit être autorisé à partir des PAW.<br />-Windows Defender Exploit Guard doit être configuré sur la station de travail. **Remarque :** Un abonnement est de niveau 0 pour une forêt si des contrôleurs de domaine ou d’autres hôtes de niveau 0 se trouvent dans l’abonnement. Un abonnement est de niveau 1 si aucun serveur de niveau 0 n’est hébergé dans Azure.|
|Administrateurs de virtualisation<br />- Niveau 0 ou 1 (voir Considérations de conception et d’étendue)|Oui|Un PAW créé à l’aide de l’aide fournie dans la Phase 2 est suffisant pour ce rôle.<br /><br />-   Des PAW doivent être utilisés pour n’importe quel rôle qui possède des droits administratifs sur les machines virtuelles, y compris la capacité à installer des agents, l’exportation des fichiers de disque dur virtuel ou l’accès au stockage sur lequel sont stockés des disques durs dotés d’informations de systèmes d’exploitation invités, des données sensibles ou des données d’entreprise critiques. **Remarque :** Un système de virtualisation (et ses administrateurs) sont considérés de niveau 0 pour une forêt si des contrôleurs de domaine ou d’autres hôtes de niveau 0 se trouvent dans l’abonnement. Un abonnement est de niveau 1 si aucun serveur de niveau 0 n’est hébergé dans le système de virtualisation.|
|Administrateurs de maintenance des serveurs<br />- Niveau 1|Oui|Un PAW créé à l’aide de l’aide fournie dans la Phase 2 est suffisant pour ce rôle.<br /><br />-   Un PAW doit être utilisé pour les administrateurs qui mettent à jour, appliquent des correctifs ou dépannent des serveurs d’entreprise et applications qui exécutent Windows Server, Linux et autres systèmes d’exploitation.<br />-   Des outils de gestion dédiés peuvent avoir à être ajoutés pour que les PAW puissent gérer le déploiement à plus grande échelle de ces administrateurs.|
|Administrateurs de station de travail utilisateur <br />- Niveau 2|Oui|Un PAW créé à l’aide des instructions fournies dans la Phase 2 est suffisant pour les rôles qui ont des droits administratifs sur les appareils de l’utilisateur final (comme les rôles de support technique).<br /><br />-   D’autres applications peuvent avoir à être installées sur les PAW pour permettre la gestion des tickets et autres fonctions de support.<br />-Windows Defender Exploit Guard doit être configuré sur la station de travail.<br />    Des outils de gestion dédiés peuvent avoir à être ajoutés pour que les PAW puissent gérer le déploiement à plus grande échelle de ces administrateurs.|
|Administrateur de SQL, SharePoint, or métier (LOB)<br />- Niveau 1||Un PAW créé avec le guide de Phase 2 est suffisant pour ce rôle.<br /><br />-   Des outils de gestion supplémentaires peuvent avoir à être installés sur les PAW pour permettre aux administrateurs de gérer les applications sans avoir à se connecter aux serveurs avec le bureau à distance.|
|Utilisateurs gérant la présence sur les réseaux sociaux|Partiellement|Un PAW créé en suivant l’aide fournie dans la Phase 2 peut servir comme point de départ pour assurer la sécurité de ces rôles.<br /><br />-   Protégez et gérez les comptes de réseaux sociaux à l’aide d’Azure Active Directory (AAD) pour le partage, la protection et le suivi de l’accès aux comptes des réseaux sociaux.<br />    Pour plus d’informations sur cette fonctionnalité, consultez [ce billet de blog](http://blogs.technet.com/b/ad/archive/2015/02/20/azure-ad-automated-password-roll-over-for-facebook-twitter-and-linkedin-now-in-preview.aspx).<br />-   Les restrictions du réseau sortant doivent autoriser la connexion à ces services. Cela est possible en autorisant les connexions sur l’Internet public (risque beaucoup plus élevé qui annule de nombreuses assurances des PAW) ou en autorisant uniquement les adresses DNS requises pour le service (ce qui peut être difficile à obtenir).|
|Utilisateurs standard|Non|Si la procédure de renforcement peut être utilisée pour les utilisateurs standard, les PAW sont conçus pour isoler les comptes d’un accès à l’Internet public, dont la plupart des utilisateurs ont besoin pour accomplir leur travail.|
|Borne/VDI invitée|Non|Si la procédure de renforcement peut être utilisée pour un système de borne pour les invités, l’architecture PAW est conçue pour fournir une sécurité accrue pour les comptes à sensibilité élevée, et non davantage de sécurité pour les comptes à sensibilité moindre.|
|Utilisateur VIP (exécutif, chercheur, etc.)|Partiellement|Un PAW créé à l’aide des instructions fournies dans la Phase 2 peut être utilisé comme point de départ pour assurer la sécurité pour ces rôles.<br /><br />-   Ce scénario est similaire à celui d’un ordinateur de bureau utilisateur standard, mais a généralement un profil d’application plus petit, plus simple et mieux connu. Ce scénario nécessite généralement la découverte et la protection des données, services et applications sensibles (qui peuvent être présents ou non sur les ordinateurs de bureau).<br />-   Ces rôles requièrent généralement un haut degré de sécurité et un très haut degré de facilité d’utilisation, ce qui nécessite des modifications de conception pour répondre aux préférences de l’utilisateur.|
|Systèmes de contrôle industriel (systèmes de contrôle et de collecte de données - SCADA, réseaux de contrôle de processus - PCN, et DCS)|Partiellement|Un PAW créé à l’aide des instructions fournies dans la Phase 2 peut être utilisé comme point de départ pour assurer la sécurité pour ces rôles, car la plupart des consoles ICS (y compris des normes communes comme SCADA et PCN) ne nécessitent pas de naviguer sur l’Internet public et de consulter des e-mails.<br /><br />-Les applications utilisées pour contrôler les machines physiques devrait être intégré et testées pour leur compatibilité et protégées de manière appropriée.|
|Système d’exploitation embarqué|Non|Si de nombreuses mesures de renforcement de PAW peuvent être utilisées pour les systèmes d’exploitation intégrés, une solution personnalisée doit être développé pour le renforcement de la sécurité dans ce scénario.|

> [!NOTE]
> **Scénarios combinés** - Certains membres du personnel peuvent avoir des responsabilités administratives qui couvrent plusieurs scénarios.
> Dans de tels cas, le point essentiel à retenir est que les règles de modèle de couche doivent être respectées à tout moment. Pour plus d’informations, consultez la page relative au modèle de niveau.

> [!NOTE]
> **Évolution du programme PAW** - Lorsque votre programme évolue pour englober plusieurs administrateurs et rôles, vous devez continuer à garantir la conformité aux normes de sécurité et à la facilité d’utilisation. Cela peut nécessiter la mise à jour de votre structure de support informatique ou la création de nouvelles structures pour répondre à des défis spécifiques à PAW, comme les processus d’intégration de PAW, la gestion des incidents, la gestion de la configuration et la collecte de commentaires pour répondre aux problèmes de facilité d’utilisation.  Un exemple peut être que votre organisation décide d’autoriser des scénarios de travail à domicile pour les administrateurs, ce qui nécessite une transition de PAW de bureau à des PAW sur ordinateur portable, un changement qui peut impliquer des considérations de sécurité supplémentaires.  Un autre exemple courant est la création ou mise à jour des formations pour les nouveaux administrateurs, formations qui doivent désormais inclure le contenu sur l’utilisation appropriée des PAW (y compris leur importance est ce qu’ils sont et ne sont pas).  Pour plus de considérations à garder à l’esprit lors de l’évolution de votre programme PAW, consultez la Phase 2 des instructions.

Ce guide contient des instructions détaillées pour la configuration de PAW pour les scénarios ci-dessus. Si vous avez des exigences pour d’autres scénarios, vous pouvez adapter les instructions vous-même sur la base de ce guide, ou passer par une entreprise de services professionnels comme Microsoft pour vous aider.

Pour plus d’informations sur l’utilisation des services Microsoft pour concevoir un PAW adapté à votre environnement, contactez votre représentant Microsoft ou visitez [cette page](https://www.microsoft.com/en-us/microsoftservices/campaigns/cybersecurity-protection.aspx).

## <a name="paw-phased-implementation"></a>Implémentation de PAW échelonnées

Étant donné que le PAW doit fournir une source sécurisée et fiable pour l’administration, il est essentiel que le processus de création soit sécurisé et fiable.  Cette section fournit des instructions détaillées qui vous permettent de créer votre propre PAW à l’aide de principes et concepts très similaires à ceux utilisés par Microsoft IT et les organisations de gestion des services et d’ingénierie de Microsoft.

Les instructions sont divisées en trois phases axées sur la mise en place rapide des atténuations les plus critiques, puis l’augmentation progressive et l’extension de l’utilisation des PAW dans l’entreprise.

* [Phase 1 : déploiement immédiat pour les administrateurs d’Active Directory](#phase-1-immediate-deployment-for-active-directory-administrators)
* [Phase 2 - étendre les PAW à tous les administrateurs](#phase-2-extend-paw-to-all-administrators)
* [Phase 3 - sécurité avancée avec PAW](#phase-3-extend-and-enhance-protection)

Il est important de noter que ces phases doivent toujours être effectuées dans l’ordre, même si elles sont planifiées et implémentées dans le cadre du même projet global.

### <a name="phase-1-immediate-deployment-for-active-directory-administrators"></a>Phase 1 : Déploiement immédiat pour les administrateurs d’Active Directory

Fonction : Fournit un PAW rapidement pour protéger les rôles d’administration de domaine et la forêt locale.

Objectif : Administrateurs de niveau 0, y compris les administrateurs de l’entreprise, Admins du domaine (pour tous les domaines) et les administrateurs d’autres systèmes d’identité faisant autorité.

La phase 1 se concentre sur les administrateurs qui gèrent votre domaine Active Directory local, des rôles critiques fréquemment ciblés par des pirates. Ces systèmes d’identité fonctionneront efficacement pour protéger ces administrateurs, que vos contrôleurs de domaine Active Directory (DC) soient hébergés dans des centres de données locaux, sur l’Infrastructure en tant que Service (IaaS) d’Azure ou sur un autre fournisseur IaaS.

Lors de cette phase, vous allez créer la structure d’unité d’organisation administrative sécurisée (UO) Active Directory pour héberger votre station de travail d’accès privilégié (PAW), ainsi que déployer les PAW eux-mêmes.  Cette structure comprend également les stratégies de groupe et les groupes requis pour prendre en charge le PAW.  Vous allez créer la majeure partie de la structure à l’aide de scripts PowerShell qui sont disponibles dans [la Galerie TechNet](http://aka.ms/pawmedia).

Les scripts créeront les unités d’organisation et les groupes de sécurité suivants :

* Unités d’organisation (UO)
   * Six nouvelles UO niveau supérieur :  Administrateur ; Groupes ; Serveurs de niveau 1 ; Stations de travail. Comptes d’utilisateur ; et mise en quarantaine de l’ordinateur.  Chaque UO de niveau supérieur contient un certain nombre d’unités d’organisation enfant.
* Groups
   * Six nouveaux globales groupes à sécurité activée :  Maintenance de réplication de niveau 0 ; Maintenance du serveur de niveau 1 ; Opérateurs de Service Desk ; Maintenance de la station de travail ; Utilisateurs PAW ; Maintenance PAW.

Vous allez également créer un nombre d’objets de stratégie de groupe : Configuration PAW - ordinateur ; Configuration PAW - utilisateur ; RestrictedAdmin requis - ordinateur ; Restrictions sortantes de PAW ; Restreindre la station de travail d’ouverture de session ; Restreindre l’ouverture de session de serveur.

La phase 1 inclut les étapes suivantes :

#### <a name="complete-the-prerequisites"></a>Remplir les conditions requises

1. **Assurez-vous que tous les administrateurs utilisent des comptes distincts et individuels pour les activités d’administration et celles d’utilisateur final** (y compris la consultation du courrier électronique, la navigation sur Internet, les applications d’entreprise et autres activités non administratives).  L’affectation d’un compte administratif distinct du compte d’utilisateur standard à chaque membre du personnel est essentielle pour le modèle PAW, car seuls certains comptes seront autorisés à se connecter au PAW lui-même.

   > [!NOTE]
   > Chaque administrateur doit utiliser son propre compte pour l’administration.  Ne partagez pas un compte d’administrateur.

2. **Réduisez le nombre d’administrateurs privilégiés de niveau 0**.  Étant donné que chaque administrateur doit utiliser un PAW, réduire le nombre d’administrateurs réduit également le nombre de PAW requis ainsi que les coûts associés. Le nombre moindre d’administrateurs entraîne également une exposition réduite à ces privilèges et aux risques associés. S’il est possible pour les administrateurs d’un emplacement de partager un PAW, les administrateurs à des emplacements physiques séparés auront besoin de PAW distincts.
3. **Acquérez du matériel auprès d’un fournisseur de confiance qui répond à toutes les exigences techniques**. Microsoft vous recommande l’acquisition du matériel répondant aux exigences techniques de l’article [Protéger les informations d’identification de domaine avec la protection des informations d’identification](https://technet.microsoft.com/library/mt483740%28v=vs.85%29.aspx).

   > [!NOTE]
   > Les PAW installés sur le matériel sans ces fonctionnalités peuvent fournir une protection significative, mais les fonctionnalités de sécurité avancées telles que la protection des informations d’identification et la protection d’appareil ne seront pas disponibles.  La protection des informations d’identification et la protection d’appareil ne sont pas requises pour le déploiement de la Phase 1, mais sont vivement recommandées dans le cadre de la Phase 3 (renforcement de sécurité avancé).
   >
   > Assurez-vous que le matériel utilisé pour le PAW provient d’un fabricant et d’un fournisseur dont les politiques de sécurité sont approuvées par l’organisation. Il s’agit d’une application du principe de source propre pour la sécurité de la chaîne logistique.
   >
   > Pour plus d’informations sur l’importance de la sécurité de la chaîne logistique, visitez [ce site](https://www.microsoft.com/security/cybersecurity/).

4. **Acquérez et validez les logiciels d’application requis Windows 10 Édition entreprise**. Obtenez les logiciels requis pour le PAW et validez-les à l’aide du guide dans [Source propre pour le support d’installation](http://aka.ms/cleansource).

   * Windows 10 Édition Entreprise
   * [Outils d’administration de serveur distant](https://www.microsoft.com/en-us/download/details.aspx?id=45520.) pour Windows 10
   * [Lignes de base de sécurité de Windows 10](http://aka.ms/win10baselines)

      > [!NOTE]
      > Microsoft publie les hachages MD5 pour tous les systèmes d’exploitation et applications sur MSDN, mais tous les éditeurs de logiciels ne proposent pas une documentation similaire.  Dans ce cas, d’autres stratégies seront nécessaires.  Pour plus d’informations sur la validation des logiciels, reportez-vous à [Source propre](http://aka.ms/cleansource) pour le support d’installation.

5. **Assurez-vous que le serveur WSUS est disponible sur l’intranet**. Vous aurez besoin d’un serveur WSUS sur l’intranet pour télécharger et installer les mises à jour pour PAW. Ce serveur WSUS doit être configuré pour approuver automatiquement toutes les mises à jour de sécurité pour Windows 10, ou un membre du personnel administratif doit avoir des la responsabilité d’approuver rapidement les mises à jour logicielles.

   > [!NOTE]
   > Pour plus d’informations, consultez la section « Approuver automatiquement les mises à jour pour l’installation » dans le guide [Approbation des mises à jour](https://technet.microsoft.com/library/cc708458(v=ws.10).aspx).

#### <a name="deploy-the-admin-ou-framework-to-host-the-paws"></a>Déployer l’infrastructure d’unité d’organisation Admin pour héberger les PAW

1. Télécharger la bibliothèque de scripts PAW depuis [la Galerie TechNet](http://aka.ms/PAWmedia)

   > [!NOTE]
   > Téléchargez tous les fichiers et enregistrez-les dans le même répertoire, puis exécutez-les dans l’ordre indiqué ci-dessous.  Create-PAWGroups repose sur la structure d’unité d’organisation créée par Create-PAWOUs, et Set-PAWOUDelegation repose sur les groupes créés par Create-PAWGroups.
   > Ne modifiez pas les scripts ou le fichier à valeurs séparées par des virgules (CSV).

2. **Exécutez le script de Create-PAWOUs.ps1**.  Ce script crée la nouvelle structure d’unité d’organisation (UO) dans Active Directory et bloque l’héritage de stratégie de groupe sur les nouvelles unités d’organisation comme il convient.
3. **Exécutez le script Create-PAWGroups.ps1**.  Ce script créera de nouveaux groupes de sécurité globaux dans les unités d’organisation appropriées.

   > [!NOTE]
   > Bien que ce script crée les groupes de sécurité, il ne les remplit pas.

4. **Exécutez le script Set-PAWOUDelegation.ps1**.  Ce script affecte les autorisations aux nouvelles unités d’organisation pour les groupes appropriés.

#### <a name="move-tier-0-accounts-to-the-admintier-0accounts-ou"></a>Déplacez les comptes de niveau 0 vers l’UO Admin\Tier 0\Accounts

Déplacez chaque compte qui est membre de l’administrateur de domaine, de l’administrateur d’entreprise, ou des groupes équivalents de niveau 0 (y compris l’appartenance imbriquée) à cette unité d’organisation. Si votre organisation possède vos propres groupes ajoutés à ces groupes, vous devez les déplacer vers l’UO Admin\Tier 0\Groups.

   > [!NOTE]
   > Pour plus informations sur les groupes qui sont de niveau 0, consultez « Équivalence de niveau 0 » dans le [Matériel de référence sur la sécurisation de l’accès privilégié](../securing-privileged-access/securing-privileged-access-reference-material.md).

#### <a name="add-the-appropriate-members-to-the-relevant-groups"></a>Ajoutez les membres appropriés aux groupes pertinents

1. **Utilisateurs PAW** - Ajoutez les administrateurs de niveau 0 avec les groupes d’administration de domaine ou d’entreprise que vous avez identifiés à l’étape 1 de la Phase 1.
2. **Maintenance de PAW** - Ajoutez au moins un compte qui sera utilisé pour la maintenance de PAW et le dépannage des tâches. Les comptes de maintenance de PAW seront rarement utilisés.

   > [!NOTE]
   > N’ajoutez pas le même compte d’utilisateur ou groupe à la fois à Utilisateurs de PAW et Maintenance de PAW.  Le modèle de sécurité PAW repose en partie sur l’hypothèse que le compte d’utilisateur PAW a des droits privilégiés sur les systèmes gérés ou sur le PAW lui-même, mais pas les deux.
   >
   > * Cela est important pour la mise en place de bonnes pratiques administratives et habitudes en Phase 1.
   > * Cela est extrêmement important pour la Phase 2 et au-delà, afin d’éviter le parcours ascendant des privilèges via le PAW, car les PAW servent à couvrir les niveaux.
   >
   > Dans l’idéal, aucun membre du personnel n’est affecté à plusieurs niveaux pour appliquer le principe de répartition des responsabilités, mais Microsoft est conscient que de nombreuses organisations peuvent avoir un personnel limité (ou avoir d’autres besoins dans l’organisation), ce qui ne permet pas d’atteindre cette séparation complète. Dans ce cas, le même personnel peut être affecté à ces deux rôles, mais il ne doit pas utiliser le même compte pour ces fonctions.

#### <a name="create-paw-configuration---computer-group-policy-object-gpo"></a>Créer l’objet stratégie de groupe (GPO) « Configuration de PAW – ordinateur »

Dans cette section, vous allez créer un nouveau « PAW Configuration – ordinateur » GPO qui fournit des protections spécifiques pour ces Paw et liez-le à l’unité d’organisation de périphériques de niveau 0 (« appareils » sous Tier 0\Admin).

   > [!NOTE]
   > **N’ajoutez pas ces paramètres à la stratégie de domaine par défaut**.  Cela affecterait potentiellement les opérations sur l’ensemble de votre environnement Active Directory.  Configurez uniquement ces paramètres dans l’objet de stratégie de groupe nouvellement créé décrit ici, et appliquez-les uniquement à l’unité d’organisation du PAW.

1. **Accès de maintenance du PAW** - Ce paramètre va définir l’appartenance de groupes privilégiés spécifiques des PAW sur un ensemble spécifique d’utilisateurs. Accédez à *Configuration de l’ordinateur\Préférences\Paramètres du panneau de configuration\Utilisateurs* et Groupes, et suivez les étapes ci-dessous :
   1. Cliquez sur **Nouveau** et cliquez sur **Groupe local**
   2. Sélectionnez l’action **Mise à jour**, puis « Administrateurs (intégré) » (n’utilisez pas le bouton Parcourir pour sélectionner le groupe de domaine Administrateurs).
   3. Cochez les cases **Supprimer tous les utilisateurs membres** et **Supprimer tous les groupes de membres**
   4. Ajoutez Maintenance de PAW (pawmaint) et Administrateur (là encore, n’utilisez pas le bouton Parcourir pour sélectionner Administrateur).

      > [!NOTE]
      > N’ajoutez pas le groupe d’utilisateurs PAW à la liste des membres du groupe Administrateurs local.  Pour vous assurer que les utilisateurs PAW ne peuvent pas accidentellement ou intentionnellement modifier les paramètres de sécurité du PAW eux-mêmes, ils ne doivent pas être membres du groupe Administrateurs local.
      >
      > Pour plus d’informations sur l’utilisation des préférences de stratégie de groupe pour modifier l’appartenance à un groupe, reportez-vous à l’article TechNet [Configurer un élément groupe Local](https://technet.microsoft.com/library/cc732525.aspx).

2. **Limiter l’appartenance au groupe local** - ce paramètre garantit que l’appartenance aux groupes d’administrateurs locaux sur la station de travail est toujours vide
   1. Accédez à Configuration de l’ordinateur\Préférences\Paramètres du panneau de configuration\Utilisateurs et Groupes, et suivez les étapes ci-dessous :
      1. Cliquez sur **Nouveau** et cliquez sur **Groupe local**
      2. Sélectionnez l’action **Mise à jour**, puis « Opérateurs de sauvegarde (intégré) » (n’utilisez pas le bouton Parcourir pour sélectionner le groupe de domaine Opérateurs de sauvegarde).
      3. Cochez les cases **Supprimer tous les utilisateurs membres** et **Supprimer tous les groupes de membres**.
      4. N'ajoutez pas de membres au groupe.  Cliquez simplement sur **OK**.  En affectant une liste vide, la stratégie de groupe supprimera automatiquement tous les membres et garantira une liste de membres vide chaque fois qu’une stratégie de groupe est actualisée.
   2. Suivez les étapes ci-dessus pour les groupes supplémentaires suivants :
      * Opérateurs de chiffrement
      * Administrateurs Hyper-V
      * Opérateurs de configuration réseau
      * Utilisateurs avec pouvoir
      * Utilisateurs du Bureau à distance
      * Réplicateurs
   3. **Restrictions de connexion PAW** -ce paramètre limite les comptes qui peuvent se connecter au PAW. Suivez les étapes ci-dessous pour configurer ce paramètre :
      1. Allez dans Configuration\Stratégies\Paramètres Windows\Paramètres de sécurité\Stratégies locales\Affectation des droits utilisateur\Autoriser la connexion locale.
      2. Sélectionnez définir ces paramètres de stratégie et d’ajouter des « Utilisateurs PAW » et les administrateurs (là encore, ne pas utiliser le bouton Parcourir pour sélectionner les administrateurs).
   4. **Bloquer le trafic réseau entrant** - Ce paramètre garantit qu’aucun trafic réseau entrant non sollicité n’est autorisé sur le PAW. Suivez les étapes ci-dessous pour configurer ce paramètre :
      1. Allez dans Configuration ordinateur\Stratégies\Paramètres Windows\Paramètres de Sécurité\pare-feu Windows avec Advanced sécurité\Pare-feu Windows avec fonctions avancées de sécurité et suivez les étapes ci-dessous :
         1. Cliquez avec le bouton droit sur Pare-feu Windows avec paramètres de sécurité avancés, puis sélectionnez **Importer la stratégie**.
         2. Cliquez sur **Oui** pour accepter que cette opération remplace les stratégies de pare-feu existantes.
         3. Accédez à PAWFirewall.wfw et sélectionnez **Ouvrir**.
         4. Cliquez sur **OK**.

            > [!NOTE]
            > Vous pouvez ajouter des adresses ou sous-réseaux qui doivent atteindre le PAW avec le trafic non sollicité à ce stade (par ex. logiciels de gestion ou d’analyse de sécurité.
            > Les paramètres dans le fichier WFW activent le pare-feu en mode « Bloc – Par défaut » pour tous les profils de pare-feu, désactivent la fusion de règles et activent la journalisation des paquets ignorés et transmis correctement. Ces paramètres bloquent le trafic non sollicité tout en autorisant la communication bidirectionnelle sur les connexions établies à partir du PAW, empêchent les utilisateurs disposant d’un accès local de créer des règles de pare-feu locales qui remplaceraient les paramètres de stratégie de groupe, et assurent que le trafic vers et depuis le PAW est enregistré.
            > **Ouvrir ce pare-feu pour agrandira la surface d’attaque pour le PAW et augmentera les risques de sécurité. Avant d’ajouter des adresses, consultez la section Gestion et exploitation de PAW dans ce guide**.

   5. **Configurer Windows Update pour WSUS** - Suivez les étapes ci-dessous pour modifier les paramètres de configuration de Windows Update pour les PAW :
      1. Accédez à Configuration ordinateur\Stratégies\Modèles d’administration\Composants Windows\Windows mises à jour et suivez les étapes ci-dessous :
         1. Activez la stratégie **Configuration du service Mises à jour automatiques**.
         2. Sélectionnez l’option **4 - Téléchargement automatique et planification des installations**.
         3. Modifiez l’option **Jour de l’installation planifiée** sur **0 - Tous les jours** et l’option **Heure de l’installation planifiée** selon les préférences de votre organisation.
         4. Activer l’option **spécifier l’emplacement intranet du service de mise à jour Microsoft** stratégie, puis indiquez dans les deux options l’URL du serveur WSUS d’ESAE.
   6. Lier le « PAW Configuration – ordinateur » GPO comme suit :

         |Stratégie|Emplacement du lieu|
         |-----|---------|
         |Configuration PAW - Ordinateur |Admin\Tier 0\Devices|

#### <a name="create-paw-configuration---user-group-policy-object-gpo"></a>Créer l’objet stratégie de groupe (GPO) « Configuration de PAW – utilisateur »

Dans cette section, vous allez créer un nouveau « PAW Configuration – utilisateur » GPO qui fournit des protections spécifiques pour ces Paw et un lien vers l’unité d’organisation de comptes de niveau 0 (« comptes » sous Tier 0\Admin).

   > [!NOTE]
   > N’ajoutez pas ces paramètres à la stratégie de domaine par défaut

1. **Bloquer la navigation Internet** - Pour empêcher la navigation sur Internet par inadvertance, cette option définit une adresse de proxy d’une adresse de bouclage (127.0.0.1).
   1. Allez dans configuration\preferences\paramètres windows\registre. Cliquez sur le Registre, sélectionnez **New** > **élément de Registre** et configurez les paramètres suivants :
      1. Action :  Remplacer
      2. Ruche : HKEY_CURRENT_USER
      3. Chemin de clé :  Software\Microsoft\Windows\CurrentVersion\Internet Settings
      4. Nom de la valeur : ProxyEnable

         > [!NOTE]
         > Ne cochez pas la case Par défaut à gauche du nom de la valeur.

      5. Type de valeur : REG_DWORD
      6. Données de valeur : 1
         1. Cliquez sur l’onglet Commun et sélectionnez **Supprimer cet élément lorsqu’il n’est plus appliqué**.
         2. Dans l’onglet Commun, sélectionnez **Ciblage du niveau d’élément** et cliquez sur **Ciblage**.
         3. Cliquez sur **Nouvel élément** et sélectionnez **Groupe de sécurité**.
         4. Sélectionnez le bouton «... » et recherchez le groupe Utilisateurs de PAW.
         5. Cliquez sur **Nouvel élément** et sélectionnez **Groupe de sécurité**.
         6. Sélectionnez le bouton «... » et recherchez le groupe **Administrateurs des services cloud**.
         7. Cliquez sur l’élément **Administrateurs de services cloud**, puis cliquez sur **Options de l’élément**.
         8. Sélectionnez **N’est pas**.
         9. Cliquez sur **OK** dans la fenêtre de ciblage.
      7. Cliquez sur **OK** pour terminer la configuration de la stratégie du groupe ProxyServer
   2. Allez dans configuration\preferences\paramètres windows\registre. Cliquez sur le Registre, sélectionnez **New** > **élément de Registre** et configurez les paramètres suivants :

      * Action : Remplacer
      * Ruche : HKEY_CURRENT_USER
      * Chemin de clé : Software\Microsoft\Windows\CurrentVersion\Internet Settings
         * Nom de la valeur : ProxyServer

            > [!NOTE]
            > Ne cochez pas la case Par défaut à gauche du nom de la valeur.

         * Type de valeur : REG_SZ
         * Données de valeur : 127.0.0.1:80
            1. Cliquez sur l’onglet **Commun** et sélectionnez **Supprimer cet élément lorsqu’il n’est plus appliqué**.
            2. Dans l’onglet **Commun**, sélectionnez **Ciblage du niveau d’élément** et cliquez sur **Ciblage**.
            3. Cliquez sur **Nouvel élément** et sélectionnez Groupe de sécurité.
            4. Sélectionnez le bouton «... » et ajoutez le groupe Utilisateurs de PAW.
            5. Cliquez sur **Nouvel élément** et sélectionnez Groupe de sécurité.
            6. Sélectionnez le bouton «... » et recherchez le groupe **Administrateurs des services cloud**.
            7. Cliquez sur l’élément **Administrateurs de services cloud**, puis cliquez sur **Options de l’élément**.
            8. Sélectionnez **N’est pas**.
            9. Cliquez sur **OK** dans la fenêtre de ciblage.

   3. Cliquez sur **OK** pour terminer la configuration de la stratégie du groupe ProxyServer.
2. Accédez à l’utilisateur Configuration ordinateur\Stratégies\Modèles d’administration\Composants Windows\Internet Explorer et activez les options ci-dessous. Ces paramètres empêchent les administrateurs de remplacer manuellement les paramètres de proxy.
   1. Activez les paramètres **Désactiver la modification des paramètres de la configuration automatique**.
   2. Activez **Empêcher la modification des paramètres de proxy**.

#### <a name="restrict-administrators-from-logging-onto-lower-tier-hosts"></a>Empêcher les administrateurs de se connecter à des hôtes de niveau inférieur

Dans cette section, nous allons configurer des stratégies de groupe pour empêcher les comptes administratifs privilégiés d’accéder à des hôtes de niveau inférieur.

1. Créez le nouvel objet de stratégie de groupe **Restriction de connexion à la station de travail** - Ce paramètre empêchera les comptes administratifs de niveau 0 et 1 de se connecter à des stations de travail standard.  Cet objet de stratégie de groupe doit être lié à l’UO de niveau supérieur « Stations de travail » et ont les paramètres suivants :
   * Dans ordinateur Configuration ordinateur\Stratégies\Paramètres Windows\Paramètres sécurité\Stratégies locales\Attribution des droits utilisateurs\refuser une session en tant que traitement par lots, sélectionnez **définir ces paramètres de stratégie** et ajoutez les groupes de niveau 1 et le niveau 0 :     Enterprise Admins du domaine Administrateurs du schéma administrateurs DOMAINE\Administrateurs compte sauvegarde opérateurs d’impression opérateurs serveur opérateurs domaine contrôleurs groupe des contrôleurs de domaine en lecture seule stratégie Créateurs propriétaires chiffrement opér ators

         > [!NOTE]
         > Built-in Tier 0 Groups, see Tier 0 equivalency for more details.

         Other Delegated Groups

         > [!NOTE]
         > Any custom created groups with effective Tier 0 access, see Tier 0 equivalency for more details.

         Tier 1 Admins

         > [!NOTE]
         > This Group was created earlier in Phase 1.

   * Dans ordinateur Configuration ordinateur\Stratégies\Paramètres Windows\Paramètres sécurité\Stratégies locales\Attribution des droits utilisateurs\refuser une session en tant que service, sélectionnez **définir ces paramètres de stratégie** et ajoutez les groupes de niveau 1 et le niveau 0 :     Enterprise Admins du domaine Administrateurs du schéma administrateurs DOMAINE\Administrateurs compte sauvegarde opérateurs d’impression opérateurs serveur opérateurs domaine contrôleurs groupe des contrôleurs de domaine en lecture seule stratégie Créateurs propriétaires chiffrement opér ators

         > [!NOTE]
         > Note: Built-in Tier 0 Groups, see Tier 0 equivalency for more details.

         Other Delegated Groups

         > [!NOTE]
         > Note: Any custom created groups with effective Tier 0 access, see Tier 0 equivalency for more details.

         Tier 1 Admins

         > [!NOTE]
         > Note: This Group was created earlier in Phase 1

2. Créer le nouvel **restriction de connexion serveur** GPO - ce paramètre empêchera les comptes d’administrateur de niveau 0 se connecter à des serveurs de niveau 1.  Cet objet de stratégie de groupe doit être lié à l’unité d’organisation de niveau supérieur de « Couche 1 serveurs » et ont les paramètres suivants :
   * Dans ordinateur Configuration ordinateur\Stratégies\Paramètres Windows\Paramètres sécurité\Stratégies locales\Attribution des droits utilisateurs\refuser une session en tant que traitement par lots, sélectionnez **définir ces paramètres de stratégie** et ajoutez les groupes de niveau 0 :     Enterprise Admins du domaine Administrateurs du schéma administrateurs DOMAINE\Administrateurs compte sauvegarde opérateurs d’impression opérateurs serveur opérateurs domaine contrôleurs groupe des contrôleurs de domaine en lecture seule stratégie Créateurs propriétaires chiffrement opér ators

         > [!NOTE]
         > Built-in Tier 0 Groups, see Tier 0 equivalency for more details.

         Other Delegated Groups

         > [!NOTE]
         > Any custom created groups with effective Tier 0 access, see Tier 0 equivalency for more details.

   * Dans ordinateur Configuration ordinateur\Stratégies\Paramètres Windows\Paramètres sécurité\Stratégies locales\Attribution des droits utilisateurs\refuser une session en tant que service, sélectionnez **définir ces paramètres de stratégie** et ajoutez les groupes de niveau 0 :     Enterprise Admins du domaine Administrateurs du schéma administrateurs DOMAINE\Administrateurs compte sauvegarde opérateurs d’impression opérateurs serveur opérateurs domaine contrôleurs groupe des contrôleurs de domaine en lecture seule stratégie Créateurs propriétaires chiffrement opér ators

         > [!NOTE]
         > Built-in Tier 0 Groups, see Tier 0 equivalency for more details.

         Other Delegated Groups

         > [!NOTE]
         > Any custom created groups with effective Tier 0 access, see Tier 0 equivalency for more details.

   * Dans ordinateur Configuration ordinateur\Stratégies\Paramètres Windows\Paramètres sécurité\Stratégies locales\Attribution des droits utilisateurs\refuser une session localement, sélectionnez **définir ces paramètres de stratégie** et ajoutez les groupes de niveau 0 :     Opérateurs domaine contrôleurs groupe des contrôleurs de domaine en lecture seule stratégie Créateurs propriétaires chiffrement opérateurs de serveur d’impression Enterprise Admins du domaine Administrateurs du schéma compte Admins du opérateurs opérateurs de sauvegarde

         > [!NOTE]
         > Note: Built-in Tier 0 Groups, see Tier 0 equivalency for more details.

         Other Delegated Groups

         > [!NOTE]
         > Note: Any custom created groups with effective Tier 0 access, see Tier 0 equivalency for more details.

#### <a name="deploy-your-paws"></a>Déploiement de vos PAW

   > [!NOTE]
   > Assurez-vous que le PAW est déconnecté du réseau pendant le processus de création du système d’exploitation.

1. Installez Windows 10 avec le support d’installation à source propre que vous avez obtenu précédemment.

   > [!NOTE]
   > Vous pouvez utiliser Microsoft Deployment Toolkit (MDT) ou un autre système de déploiement automatisé d’images pour automatiser le déploiement du PAW, mais vous devez vérifier que le processus de génération est au moins aussi fiable que le PAW. Les pirates cherchent spécifiquement des images d’entreprise et systèmes de déploiement (y compris les fichiers ISO, les packages de déploiement, etc.) comme mécanisme de persistance, les images ou systèmes de déploiement existants ne doivent donc pas être utilisés.
   >
   > Si vous automatisez le déploiement du PAW, vous devez :
   >
   > * Créer le système à l’aide du support d’installation validé en utilisant les instructions de [Source propre pour support d’installation](http://aka.ms/cleansource).
   > * Assurez-vous que le système de déploiement automatisé est déconnecté du réseau pendant le processus de création du système d’exploitation.

2. Définissez un mot de passe complexe pour le compte administrateur local.  N’utilisez pas un mot de passe qui a été utilisé pour un autre compte dans l’environnement.

   > [!NOTE]
   > Microsoft recommande d’utiliser [Local Administrator Password Solution (LAPS)](https://www.microsoft.com/en-us/download/details.aspx?id=46899) pour gérer le mot de passe administrateur local pour toutes les stations de travail, y compris les PAW.  Si vous utilisez LAPS, veillez à n’accorder qu’au groupe Maintenance de PAW le droit de lire les mots de passe gérés par LAPS pour les PAW.

3. Installez les outils d'administration de serveur distant pour Windows 10 à l’aide du support d’installation à source propre.
4. Configurer Windows Defender Exploit Guard

   > [!NOTE]
   > Conseils de configuration à suivre

5. Connectez le PAW au réseau.  Assurez-vous que le PAW peut se connecter à au moins un contrôleur de domaine (DC).
6. En utilisant un compte membre du groupe Maintenance de PAW, exécutez la commande PowerShell suivante à partir du PAW nouvellement créé pour le joindre au domaine dans l’unité d’organisation appropriée :

   `Add-Computer -DomainName Fabrikam -OUPath "OU=Devices,OU=Tier 0,OU=Admin,DC=fabrikam,DC=com"`

   Remplacez les références à *Fabrikam* avec votre nom de domaine, comme nécessaire.  Si votre nom de domaine s’étend à plusieurs niveaux (par exemple, child.fabrikam.com), ajoutez les noms supplémentaires avec l’identificateur « DC = » dans l’ordre dans lequel ils apparaissent dans le nom de domaine complet.

   > [!NOTE]
   > Si vous avez déployé une [Forêt d’administration ESAE](http://aka.ms/esae) (pour les administrateurs de niveau 0 de la Phase 1) ou un [PAM Microsoft Identity Manager (MIM)](http://aka.ms/mimpamdeploy) (pour les administrateurs de niveau 1 et 2 dans la Phase 2), vous joignez le PAW au domaine dans cet environnement au lieu du domaine de production.

7. Appliquez toutes les mises à jour Windows critiques et importantes avant d’installer tout autre logiciel (y compris les outils d’administration, les agents, etc.).
8. Forcez l’application de la stratégie de groupe.
   1. Ouvrez une invite de commandes avec élévation de privilèges et entrez la commande suivante : `Gpupdate /force /sync`
   2. Redémarrer l'ordinateur

9. (Facultatif) Installer les autres outils requis pour les administrateurs Active Directory. Installez les autres outils ou scripts requis pour effectuer des tâches. Veillez à évaluer le risque d’exposition des informations d’identification sur les ordinateurs cibles avec tout outil avant de l’ajouter à un PAW. Accédez à [cette page](http://aka.ms/logontypes) pour obtenir plus d’informations sur l’évaluation des outils d’administration et des méthodes de connexion pour le risque d’exposition des informations d’identification. Veillez à obtenir tous les supports d’installation en utilisant les instructions de [Source propre pour support d’installation](http://aka.ms/cleansource).

   > [!NOTE]
   > L’utilisation d’un serveur de renvoi pour un emplacement central avec ces outils permet de réduire la complexité, même si cela ne constitue pas une barrière de sécurité.

10. (Facultatif) Téléchargez et installez le logiciel d’accès distant requis. Si les administrateurs utiliseront le PAW à distance pour l’administration, installez le logiciel d’accès à distance à l’aide du guide de sécurité de votre fournisseur de solutions d’accès à distance. Veillez à obtenir tous les supports d’installation en utilisant les instructions de Source propre pour support d’installation.

   > [!NOTE]
   > Étudiez attentivement tous les risques impliqués dans l’accès à distance via un PAW.  Si un PAW mobile permet de suivre plusieurs scénarios importants, dont le travail à domicile, le logiciel d’accès à distance peut être vulnérable aux attaques et compromettre un PAW.

11. Validez l’intégrité du système PAW en examinant et en confirmant que tous les paramètres appropriés sont en place à l’aide de la procédure ci-dessous :
   1. Confirmez que seules les stratégies de groupe propres au PAW sont appliquées au PAW
      1. Ouvrez une invite de commandes avec élévation de privilèges et entrez la commande suivante : `Gpresult /scope computer /r`
      2. Examinez la liste résultante et vérifiez que les seules stratégies de groupe qui s’affichent sont celles que vous avez créées précédemment.
   2. Vérifiez qu’aucun compte d’utilisateur supplémentaire n’est membres des groupes privilégiés sur le PAW à l’aide de la procédure ci-dessous :
      1. Ouvrez **Modifier les utilisateurs et groupes locaux** (lusrmgr.msc), sélectionnez **Groupes**, et vérifiez que seuls les membres du groupe Administrateurs local sont le compte Administrateur local et le groupe de sécurité global Maintenance des PAW.

         > [!NOTE]
         > Le groupe d’utilisateurs PAW ne doit pas être membre du groupe Administrateurs local.  Les seuls membres doivent être le compte Administrateur local et le groupe de sécurité global Maintenance de PAW (et les utilisateurs PAW ne doivent pas membres de ce groupe global non plus).

      2. De plus, utiliser **Modifier les utilisateurs et groupes locaux** garantit que les groupes suivants n’ont aucun membre : Opérateurs de sauvegarde opérateurs de chiffrement Hyper-V administrateurs réseau réplicateurs utilisateurs du Bureau à distance de Configuration opérateurs Power utilisateurs

12. (Facultatif) Si votre organisation utilise des informations de sécurité et de la solution de gestion (SIEM) des événements, vérifiez que le PAW [configuré pour transférer les événements sur le système à l’aide de transfert des événements Windows (WEF)](http://blogs.technet.com/b/jepayne/archive/2015/11/24/monitoring-what-matters-windows-event-forwarding-for-everyone-even-if-you-already-have-a-siem.aspx) ou enregistré avec le solution afin que le serveur SIEM reçoive activement les événements et des informations à partir du PAW.  Les détails de cette opération varient en fonction de votre solution SIEM.

   > [!NOTE]
   > Si votre solution SIEM nécessite un agent qui s’exécute en tant que système ou compte d’administration local sur les PAW, assurez-vous que les solutions SIEM sont gérées avec le même niveau de confiance que vos contrôleurs de domaine et systèmes d’identité.

13. (Facultatif) Si vous avez choisi de déployer LAPS pour gérer le mot de passe pour le compte d’administrateur local sur votre PAW, vérifiez que le mot de passe est enregistré avec succès.

   * Ouvrez **Utilisateurs et ordinateurs Active Directory** (dsa.msc) avec un compte disposant des autorisations pour lire les mots de passe gérés par LAPS.  Assurez-vous que l’option Fonctionnalités avancées est activée, puis cliquez sur l’objet ordinateur approprié.  Sélectionnez l’onglet Éditeur d’attribut et confirmez que la valeur de msSVSadmPwd est remplie avec un mot de passe.

### <a name="phase-2-extend-paw-to-all-administrators"></a>Phase 2 : Étendre les PAW à tous les administrateurs

Objectif : Tous les utilisateurs disposant de droits administratifs sur les applications stratégiques et les dépendances.  Cela doit inclure au moins les administrateurs de serveurs d’applications, les solutions de surveillance des solutions, de sécurité et d’intégrité opérationnelle, les systèmes de stockage et les appareils réseau.

> [!NOTE]
> Les instructions de cette phase supposent que la Phase 1 a été effectuée dans son intégralité.  Ne commencez pas la Phase 2 avant d’avoir terminé toutes les étapes de la Phase 1.

Après avoir confirmé que toutes les étapes ont été réalisées, suivez la procédure ci-dessous pour effectuer la Phase 2 :

#### <a name="recommended-enable-restrictedadmin-mode"></a>(Recommandé) Activer **RestrictedAdmin** mode

Activer cette fonctionnalité sur vos stations de travail et les serveurs existants, puis appliquez l’utilisation de cette fonctionnalité. Cette fonctionnalité nécessite que les serveurs cibles à exécuter Windows Server 2008 R2 ou version ultérieure et être en cours d’exécution Windows 7 ou version ultérieure des stations de travail cible.

1. Activez le mode **RestrictedAdmin** sur vos serveurs et stations de travail en suivant les instructions disponibles sur cette [page](http://aka.ms/rdpra).

   > [!NOTE]
   > Avant d’activer cette fonctionnalité pour les serveurs exposés à Internet, vous devez envisager le risque que des pirates parviennent à authentifier ces serveurs avec un hachage de mot de passe volé précédemment.

2. Créez un objet de stratégie de groupe (GPO) « RestrictedAdmin requis – Ordinateur ». Cette section crée un objet de stratégie de groupe qui applique l’utilisation du commutateur /RestrictedAdmin pour les connexions Bureau à distance sortantes, afin de protéger les comptes contre le vol d’informations d’identification sur les systèmes cible
   * Accédez à Configuration\Système\Délégation d’informations d’identification\Restreindre la délégation d’informations d’identification aux serveurs distants, et réglez la valeur sur **Activé**.
3. Liez **RestrictedAdmin** requis - Ordinateur aux appareils de niveau 1 et/ou niveau 2 appropriés en utilisant les options de stratégie ci-dessous :
   * Configuration PAW - Ordinateur
      * -> Emplacement du lien : Admin\Tier 0\Devices (existant)
   * Configuration PAW - Utilisateur
      * -> Emplacement du lien : Admin\Tier 0\Accounts
   * RestrictedAdmin requis - Ordinateur
      * -> Admin\Tier1\Devices ou -> Admin\Tier2\Devices (les deux sont facultatifs)

   > [!NOTE]
   > Cela n’est pas nécessaire pour les systèmes de niveau 0, ces systèmes ayant déjà le contrôle total de toutes les ressources dans l’environnement.

#### <a name="move-tier-1-objects-to-the-appropriate-ous"></a>Déplacer des objets de niveau 1 vers les unités d’organisation appropriées

1. Déplacez les groupes de niveau 1 vers l’unité d’organisation Admin\Tier 1\Groups. Recherchez tous les groupes qui octroient les droits d’administration suivants et déplacez-les dans cette unité d’organisation.
   * Administrateur local sur plusieurs serveurs
      * Accès administratif aux services cloud
      * Accès administratif aux applications d’entreprise
2. Déplacez les comptes de niveau 1 vers l’UO Admin\Tier 1\Accounts. Déplacez chaque compte membre des groupes de niveau 1 (y compris l’appartenance imbriquée) vers cette unité d’organisation.
3. Ajoutez les membres appropriés aux groupes pertinents
   * **Administrateurs de niveau 1** - Ce groupe contient les administrateurs de niveau 1 qui ne pourront pas se connecter à des hôtes de niveau 2. Ajoutez toutes vos groupes d’administration de niveau 1 qui disposent des privilèges d’administration sur les serveurs ou les services Internet.

      > [!NOTE]
      > Si le personnel d’administration a la responsabilité de gérer des ressources sur plusieurs niveaux, vous devrez créer un compte administratif distinct par niveau.

4. Activez la protection des informations d’identification pour réduire le risque de vol et de réutilisation d’informations d’identification.  La protection des informations d’identification est une nouvelle fonctionnalité de Windows 10 qui restreint l’accès des applications aux informations d’identification, pour empêcher les attaques par vol d’informations d’identification (notamment de type Pass-the-Hash).  La protection des informations d’identification est totalement transparente pour l’utilisateur final et nécessite seulement une configuration et des efforts minimaux.  Pour plus d’informations sur la protection des informations d’identification, y compris les étapes de déploiement et la configuration matérielle requise, reportez-vous à l’article [Protéger les informations d’identification de domaine avec la protection des informations d’identification](https://technet.microsoft.com/library/mt483740%28v=vs.85%29.aspx).

   > [!NOTE]
   > La protection des appareils doit être activée pour configurer et utiliser la protection des informations d’identification.  Toutefois, il n’est pas nécessaire de configurer les autres protections protection d’appareils pour pouvoir utiliser la protection des informations d’identification.

5. (Facultatif) Activer la connectivité aux Services Cloud. Cette étape permet la gestion des services cloud, comme Azure et Office 365, avec des garanties de sécurité appropriées. Cette étape est également requise pour que Microsoft Intune puisse gérer les PAW.

   > [!NOTE]
   > Ignorez cette étape si aucune connectivité cloud n’est requise pour l’administration de services cloud ou la gestion par Intune.

   * Ces étapes restreignent la communication sur Internet aux seuls services cloud autorisés (en excluant l’Internet public) et ajoutent des protections pour les navigateurs et autres applications qui traitent le contenu d’Internet. Ces PAW pour l’administration ne doivent jamais être utilisés pour des tâches utilisateur standard telles que les communications sur Internet et la productivité.
   * Pour activer la connectivité aux services PAW, procédez comme suit :

   1. Configurez PAW pour autoriser uniquement les destinations Internet autorisées.  Lorsque vous étendez votre déploiement PAW pour activer l’administration du cloud, vous devez permettre l’accès aux services autorisés en filtrant les accès à partir de l’Internet public, où des attaques peuvent être plus facilement lancées contre vos administrateurs.

      1. Créez un groupe **Administrateurs des services cloud** et ajoutez tous les comptes qui nécessitent un accès aux services cloud sur Internet.
      2. Téléchargez le fichier PAW *proxy.pac* dans [la Galerie TechNet](http://aka.ms/pawmedia) et publiez-le sur un site web interne.

         > [!NOTE]
         > Vous devez mettre à jour le fichier *proxy.pac* après téléchargement pour vous assurer qu’il est à jour et complet.  
         > Microsoft publie toutes les URL actuelles pour Office 365 et Azure dans le [Centre de support](https://support.office.com/en-us/article/Office-365-URLs-and-IP-address-ranges-8548a211-3fe7-47cb-abb1-355ea5aa88a2?ui=en-US&rs=en-US&ad=US) d’Office. Ces instructions supposent que vous utiliserez Internet Explorer (ou Microsoft Edge) pour l’administration d’Office 365, Azure et d’autres services cloud. Microsoft recommande de configurer des restrictions similaires pour les navigateurs tiers dont vous avez besoin pour l’administration. Les navigateurs web des PAW doivent uniquement servir pour l’administration des services cloud computing et jamais pour la navigation web générale.
         >
         > Vous devrez peut-être ajouter d’autres destinations Internet valides à cette liste pour les autres fournisseurs IaaS, mais n’ajoutez pas les sites de productivité, divertissements, actualités ou recherche à cette liste.
         >
         > Vous devrez peut-être aussi régler le fichier PAC pour configurer une adresse proxy valide à utiliser pour ces adresses.
         >
         > Vous pouvez également restreindre l’accès à partir du PAW avec un proxy web pour une défense plus profonde. Nous ne recommandons pas d’utiliser un tel proxy sans fichier PAC, car il ne restreindrait alors l’accès pour les PAW que lors de la connexion au réseau d’entreprise.

      3. Une fois que vous avez configuré le fichier *proxy.pac*, mettez à jour Configuration PAW - Objet de stratégie de groupe utilisateur.
         1. Allez dans configuration\preferences\paramètres windows\registre. Cliquez sur le Registre, sélectionnez **New** > **élément de Registre** et configurez les paramètres suivants :
            1. Action : Remplacer
            2. Ruche : HKEY_ CURRENT_USER
            3. Chemin de clé : Software\Microsoft\Windows\CurrentVersion\Internet Settings
            4. Nom de la valeur : AutoConfigUrl

               > [!NOTE]
               > Ne cochez pas la case **Par défaut** à gauche du nom de la valeur.

            5. Type de valeur : REG_SZ
            6. Données de la valeur : entrez l’URL complète vers le *proxy.pac* de fichiers, y compris http:// et le nom de fichier - par exemple http://proxy.fabrikam.com/proxy.pac.  L’URL peut également être une URL à intitulé unique, par exemple, http://proxy/proxy.pac

               > [!NOTE]
               > Le fichier PAC peut également être hébergé sur un partage de fichiers, avec la syntaxe file://server.fabrikan.com/share/proxy.pac, mais cela nécessite l’autorisation du protocole file://. Consultez le « Remarque : Section File://-based Proxy Scripts déconseillée » de ce [présentation de la Configuration Proxy Web](http://blogs.msdn.com/b/ieinternals/archive/2013/10/11/web-proxy-configuration-and-ie11-changes.aspx) blog pour plus d’informations sur la configuration de la valeur de Registre requises.

            7. Cliquez sur l’onglet **Commun** et sélectionnez **Supprimer cet élément lorsqu’il n’est plus appliqué**.
            8. Dans l’onglet **Commun**, sélectionnez **Ciblage du niveau d’élément** et cliquez sur **Ciblage**.
            9. Cliquez sur **Nouvel élément** et sélectionnez **Groupe de sécurité**.
            10. Sélectionnez le bouton «... » et recherchez le groupe **Administrateurs des services cloud**.
            11. Cliquez sur **Nouvel élément** et sélectionnez **Groupe de sécurité**.
            12. Sélectionnez le bouton «... » et recherchez le groupe **Utilisateurs de PAW**.
            13. Cliquez sur l’élément **Utilisateurs de PAW**, puis cliquez sur **Options d’élément**.
            14. Sélectionnez **N’est pas**.
            15. Cliquez sur **OK** dans la fenêtre de ciblage.
            16. Cliquez sur **OK** pour terminer la configuration de la stratégie du groupe **AutoConfigUrl**.
   2. Appliquez les lignes de base de sécurité de Windows 10 et l’accès au service cloud. Liez les lignes de base de sécurité pour Windows et pour l’accès aux services cloud (si nécessaire) aux bonnes unités d’organisation à l’aide de la procédure ci-dessous :
      1. Extrayez le contenu du fichier ZIP Windows 10 Security Baselines.
      2. Créez ces objets de stratégie de groupe, les paramètres [Importer la stratégie](https://technet.microsoft.com/library/cc753786.aspx) paramètres, et le [lien](https://technet.microsoft.com/library/cc732979.aspx) conformément à cette table. Liez chaque stratégie à chaque emplacement et vérifiez que l’ordre suit la table (les entrées inférieures dans la table doivent être appliquées ultérieurement et avec une priorité plus élevée) :

         **Stratégies :**

         |||
         |-|-|
         |CM Windows 10 - Sécurité de domaine|N/A - Ne pas lier maintenant|
         |SCM Windows 10 TH2 - Ordinateur|Admin\Tier 0\Devices|
         ||Admin\Tier 1\Devices|
         ||Admin\Tier 2\Devices|
         |SCM Windows 10 TH2- BitLocker|Admin\Tier 0\Devices|
         ||Admin\Tier 1\Devices|
         ||Admin\Tier 2\Devices|
         |SCM Windows 10 - Protection des informations d’identification|Admin\Tier 0\Devices|
         ||Admin\Tier 1\Devices|
         ||Admin\Tier 2\Devices|
         |SCM Internet Explorer - Ordinateur|Admin\Tier 0\Devices|
         ||Admin\Tier 1\Devices|
         ||Admin\Tier 2\Devices|
         |Configuration PAW - Ordinateur|Admin\Tier 0\Devices (existant)|
         ||Admin\Tier 1\Devices (nouveau lien)|
         ||Admin\Tier 2\Devices (nouveau lien)|
         |RestrictedAdmin requis - Ordinateur|Admin\Tier 0\Devices|
         ||Admin\Tier 1\Devices|
         ||Admin\Tier 2\Devices|
         |SCM Windows 10 - Utilisateur|Admin\Tier 0\Devices|
         ||Admin\Tier 1\Devices|
         ||Admin\Tier 2\Devices|
         |Internet Explorer SCM - Utilisateur|Admin\Tier 0\Devices|
         ||Admin\Tier 1\Devices|
         ||Admin\Tier 2\Devices|
         |Configuration PAW - Utilisateur|Admin\Tier 0\Devices (existant)|
         ||Admin\Tier 1\Devices (nouveau lien)|
         ||Admin\Tier 2\Devices (nouveau lien)|

         > [!NOTE]
         > L’objet de stratégie de groupe « SCM Windows 10 - Sécurité de domaine » peut être lié au domaine indépendamment du PAW, mais affecte l’ensemble du domaine.

6. (Facultatif) Installer les autres outils requis pour les administrateurs de niveau 1. Installez les autres outils ou scripts requis pour effectuer des tâches. Veillez à évaluer le risque d’exposition des informations d’identification sur les ordinateurs cibles avec tout outil avant de l’ajouter à un PAW. Visitez [cette page](http://aka.ms/logontypes) pour obtenir plus d’informations sur l’évaluation des outils d’administration et des méthodes de connexion pour le risque d’exposition des informations d’identification. Veillez à obtenir tous les supports d’installation en utilisant les instructions de Source propre pour support d’installation
7. Identifiez et obtenez en toute sécurité les logiciels et applications requis pour l’administration.  Cela est similaire au travail effectué en Phase 1, mais avec une portée plus large en raison de l’augmentation du nombre d’applications, de services et de systèmes sécurisés.

   > [!NOTE]
   > Veillez à protéger ces nouvelles applications (y compris les navigateurs web) en activant les protections fournies par Windows Defender Exploit Guard.

   Exemples d’applications et logiciels supplémentaires :

      * Microsoft Azure PowerShell
      * PowerShell pour Office 365 (également appelé Module Microsoft Online Services)
      * Logiciels de gestion des services ou applications basés sur la console MMC (Microsoft Management Console)
      * Logiciels de gestion des services ou applications propriétaires (non basées sur MMC)

         > [!NOTE]
         > De nombreuses applications sont désormais exclusivement gérées via les navigateurs web, y compris de nombreux services cloud.  Même si cela réduit le nombre d’applications qui doivent être installées sur un PAW, cela présente également des risques de problèmes d’interopérabilité avec les navigateurs.  Vous devrez peut-être déployer un navigateur web non Microsoft sur des instances spécifiques de PAW pour permettre l’administration de services spécifiques.  Si vous déployez un navigateur web supplémentaire, veillez à suivre tous les principes de source propre et à sécuriser le navigateur en suivant les instructions de sécurité du fournisseur.

8. (Facultatif) Téléchargez et installez des agents de gestion requis.

   > [!NOTE]
   > Si vous choisissez d’installer des agents de gestion supplémentaires (surveillance, sécurité, gestion de la configuration, etc.), il est essentiel de vérifier que les systèmes de gestion sont approuvés au même niveau que les contrôleurs de domaine et les systèmes d’identité. Pour plus d’informations, consultez Gestion et mise à jour des PAW.

9. Évaluez votre infrastructure pour identifier les systèmes qui nécessitent les protections de sécurité supplémentaires fournies par un PAW.  Assurez-vous de savoir exactement quels systèmes doivent être protégés.  Posez des questions essentielles relatives aux ressources, telles que :

   * Où sont les systèmes cibles qui doivent être gérés ?  Sont-ils collectés dans un seul emplacement physique, ou connectés à un seul sous-réseau bien défini ?
   * Combien de systèmes sont-ils présents ?
   * Ces systèmes dépendent-ils d’autres systèmes (virtualisation, stockage, etc.), et si c’est le cas, comment ces systèmes sont-ils gérés ?  Comment les systèmes critiques sont-ils exposés à ces dépendances, et quels sont les risques associés à ces dépendances ?
   * À quel point les services gérés sont-ils, et quelle est la perte attendue si ces services étaient compromis ?

      > [!NOTE]
      > Intégrez vos services cloud dans cette évaluation : les pirates ciblent de plus en plus les déploiements cloud non sécurisés, et il est essentiel que vous administriez ces services de façon aussi sécurisée que pour vos applications critiques locales.

        Utilisez cette évaluation pour identifier les systèmes qui nécessitent une protection supplémentaire, puis étendez votre programme PAW aux administrateurs de ces systèmes.  Des exemples courants de systèmes qui profitent grandement de l’administration basée sur un PAW comprennent SQL Server (en local et avec SQL Azure), les applications de ressources humaines, les logiciels financiers.

        > [!NOTE]
        > Si une ressource est gérée à partir d’un système Windows, elle peut être gérée avec un PAW, même si l’application elle-même s’exécute sur un système d’exploitation autre que Windows ou sur une plateforme cloud non Microsoft.  Par exemple, le propriétaire d’un abonnement Amazon Web Services doit uniquement utiliser un PAW pour administrer ce compte.

10. Développez une méthode de demande et de distribution pour le déploiement de PAW à l’échelle de votre organisation.  En fonction du nombre de PAW que vous choisissez de déployer en Phase 2, vous pourriez avoir à automatiser le processus.

   * Envisagez de développer un processus de demande et d’approbation officiel pour les administrateurs qui souhaitent obtenir un PAW.  Ce processus permet de normaliser le processus de déploiement, garantir la responsabilité pour les appareils PAW et vous aider à identifier les lacunes de déploiement de PAW.
   * Comme indiqué précédemment, cette solution de déploiement doit être distincte de méthodes d’automatisation existantes (qui ont déjà été compromises) et doit suivre les principes énoncés dans la Phase 1.

        > [!NOTE]
        > Tout système qui gère les ressources doit lui-même être géré au même niveau de confiance ou à un niveau supérieur.

11. Examinez et déployez d’autres profils matériels de PAW si nécessaire.  Le profil matériel que vous avez choisi pour le déploiement en Phase 1 peut ne pas convenir pour tous les administrateurs.  Examinez les profils matériels et sélectionnez éventuellement des profils matériels PAW supplémentaires pour répondre aux besoins des administrateurs.  Par exemple, le profil Matériel dédié (stations de travail PAW et d’utilisation quotidienne distinctes) peut être inapproprié pour un administrateur qui se déplace souvent ; dans ce cas, vous pouvez choisir de déployer le profil Utilisation simultanée (PAW avec machine virtuelle d’utilisateur) pour cet administrateur.
12. Pensez aux besoins de communication, de formation, culturels et opérationnels qui accompagnent un déploiement PAW étendu.   Un changement aussi significatif de modèle d’administration nécessite naturellement une gestion du changement, et il est essentiel d’intégrer cette question au projet de déploiement lui-même.  Envisagez au minimum les points suivants :

   * Comment communiquerez-vous les changements apportés à la direction pour assurer son soutien ?  Un projet sans soutien de la direction est probablement destiné à échouer, ou du moins difficile à financer et faire accepter.
   * Comment documenterez-vous le nouveau processus pour les administrateurs ?  Ces modifications doivent être documentées et communiquées non seulement aux administrateurs existants (qui doivent changer leurs habitudes et gérer les ressources d’une façon différente), mais aussi les nouveaux administrateurs (ceux qui sont promus dans l’organisation ou recrutés depuis l’extérieur).  Il est essentiel que la documentation soit claire et explique complètement l’importance des menaces, le rôle des PAW pour protéger les administrateurs, et comment utiliser les PAW correctement.

      > [!NOTE]
      > Cela est particulièrement important pour les rôles à rotation élevée, notamment le personnel du support technique, mais pas seulement.

   * Comment garantirez-vous la conformité au nouveau processus ?  Si le modèle PAW inclut un certain nombre de contrôles techniques pour éviter l’exposition d’informations d’identification privilégiées, il est impossible d’éviter totalement toute exposition possible uniquement à l’aide de contrôles techniques.  Par exemple, même s’il est possible d’empêcher un administrateur de se connecter avec succès sur le bureau d’un utilisateur avec des informations d’identification privilégiées, le simple fait de tenter l’ouverture de session peut exposer les informations d’identification aux logiciels malveillants installés sur l’ordinateur de bureau de cet utilisateur.  Il est donc essentiel de détailler non seulement les avantages du modèle PAW, mais aussi les risques de non-conformité.  Cela doit être complété par des audits et des alertes afin que les expositions d’informations d’identification puissent être détectées et résolues rapidement.

### <a name="phase-3-extend-and-enhance-protection"></a>Phase 3 : Étendre et améliorer la protection

Objectif : Ces protections améliorent les systèmes créés dans la Phase 1, en renforçant la protection de base avec des fonctionnalités avancées, notamment l’authentification multifacteur et règles d’accès réseau.

> [!NOTE]
> Cette phase peut être effectuée à tout moment une fois que la Phase 1 a été effectuée.  Elle ne dépend pas de la fin de la Phase 2 et peut donc être exécutée avant, en même temps que, ou après la Phase 2.

Suivez les étapes ci-dessous pour configurer cette phase :

1. **Activer l’authentification multifacteur pour les comptes privilégiés**.  L’authentification multifacteur renforce la sécurité des comptes en obligeant l’utilisateur à fournir un jeton physique en plus des informations d’identification.  L’authentification multifacteur s’ajoute très bien aux stratégies d’authentification, mais ne dépend pas des stratégies d’authentification pour le déploiement (et, de même, les stratégies d’authentification ne nécessitent pas l’authentification multifacteur).  Microsoft recommande d’utiliser une de ces formes d’authentification multifacteur :

   * **Carte à puce**: Une carte à puce est un appareil physique résistant aux falsifications et portable qui fournit une seconde vérification pendant le processus d’ouverture de session Windows.  En demandant à un individu de posséder une carte pour la connexion, vous pouvez réduire le risque de réutilisation d’informations d’identification volées à distance.  Pour plus d’informations sur la connexion avec carte à puce dans Windows, reportez-vous à l’article [Vue d’ensemble des cartes à puce](https://technet.microsoft.com/library/hh831433.aspx).
   * **Carte à puce virtuelle**:  Une carte à puce virtuelle fournit les mêmes avantages de sécurité comme les cartes à puce physiques, l’avantage d’être liées à un matériel spécifique.  Pour plus d’informations sur le déploiement et la configuration matérielle requise, reportez-vous aux articles [vue d’ensemble de carte à puce virtuelles](https://technet.microsoft.com/library/dn593708.aspx) et [bien démarrer avec les cartes à puce virtuelles : Guide pas à pas](https://technet.microsoft.com/library/dn579260.aspx).
   * **Windows Hello entreprise**: Windows Hello entreprise permet aux utilisateurs de s’authentifier auprès d’un compte Microsoft, d’un compte Active Directory, un compte Microsoft Azure Active Directory (Azure AD) ou un service non-Microsoft qui prend en charge l’authentification Fast ID Online (FIDO). Après une vérification initiale en deux étapes au cours de Windows Hello pour l’inscription d’entreprise, un Windows Hello entreprise est configuré sur le périphérique l’utilisateur et l’utilisateur définit un mouvement, ce qui peut être Windows Hello ou un code confidentiel. Windows Hello pour les informations d’identification de l’entreprise sont une paire de clés asymétriques peut être générée dans des environnements isolés de Modules de plateforme sécurisée (TPM).
      Pour plus d’informations sur Windows Hello pour la lecture de l’entreprise [Windows Hello entreprise](https://docs.microsoft.com/windows/security/identity-protection/hello-for-business/hello-identity-verification) article.
   * **Azure multi-factor authentication**:  Azure multi-factor authentication (MFA) fournit la sécurité d’un second facteur de vérification ainsi que la protection renforcée par la surveillance et machine learning-basée sur l’analyse.  L’authentification multifacteur Azure (MFA) peut sécuriser non seulement les administrateurs Azure, mais aussi de nombreuses autres solutions, notamment les applications web, Azure Active Directory et des solutions locales telles que l’accès à distance et le bureau à distance.  Pour plus d’informations sur l’authentification multifacteur Azure, consultez l’article [Multi-Factor Authentication](https://azure.microsoft.com/services/multi-factor-authentication).

2. **Les applications à l’aide de Windows Defender Application Control et/ou AppLocker approuvées en liste verte**.  En limitant la capacité du code non approuvé ou non signé à s’exécuter sur un PAW, vous réduisez encore la probabilité d’activités malveillantes de compromissions.  Windows comprend deux options principales pour le contrôle des applications :

   * **AppLocker**:  AppLocker permet aux administrateurs un contrôle dont les applications peuvent s’exécuter sur un système donné.  AppLocker peut être contrôlé de façon centrale via une stratégie de groupe et appliqué à des utilisateurs ou des groupes (pour une application ciblée aux utilisateurs de PAW).  Pour plus d’informations sur AppLocker, consultez l’article TechNet [Vue d’ensemble d’AppLocker](https://technet.microsoft.com/library/hh831440.aspx).
   * **Windows Defender Application Control**: la nouvelle fonctionnalité de Windows Defender Application Control fournit le contrôle d’application en fonction du matériel améliorée qui, contrairement à AppLocker, ne peut pas être substituée sur l’appareil concerné.  Comme AppLocker, Windows Defender Application Control peut être contrôlé via la stratégie de groupe et ciblé à des utilisateurs spécifiques.  Pour plus d’informations sur la limitation de l’utilisation des applications avec Windows Defender Application Control, reportez-vous à [Guide de déploiement de Windows Defender Application contrôle](https://docs.microsoft.com/en-gb/windows/security/threat-protection/windows-defender-application-control/windows-defender-application-control-deployment-guide).

3. **Utilisez les Utilisateurs protégés, les Stratégies d’authentification et les Silos d’authentification pour protéger davantage les comptes privilégiés**.  Les membres des Utilisateurs protégés sont soumis à des stratégies de sécurité supplémentaire qui protègent les informations d’identification stockées dans l’agent de sécurité local (LSA) et réduisent le risque de vol et de réutilisation des informations d’identification.  Les stratégies d’authentification et silos contrôlent la façon dont les utilisateurs privilégiés peuvent accéder aux ressources du domaine.  Collectivement, ces protections renforcent de façon spectaculaire la sécurité des comptes de ces utilisateurs privilégiés.  Pour plus d’informations sur ces fonctionnalités, reportez-vous à l’article web [Comment configurer des comptes protégés](https://technet.microsoft.com/library/dn518179.aspx).

   > [!NOTE]
   > Ces protections sont destinées à compléter, les mesures de sécurité de la Phase 1, sans les remplacer.  Les administrateurs doivent toujours utiliser des comptes distincts pour l’administration et l’utilisation générale.

## <a name="managing-and-updating"></a>La gestion et la mise à jour

Les PAW doivent avoir des fonctionnalités anti-programme malveillant, et les mises à jour doivent être appliquées rapidement pour conserver l’intégrité de ces stations de travail.

Vous pouvez également utiliser des fonctions de gestion de la configuration, de surveillance opérationnelle et de gestion de la sécurité supplémentaires avec les PAW, mais leur intégration doit être envisagée avec précaution, car chaque fonctionnalité de gestion présente également des risques de compromission de PAW à travers cet outil. La pertinence de l’ajout de fonctions de gestion avancées dépend de plusieurs facteurs, notamment :

* L’état de sécurité et les pratiques des capacités de gestion (notamment les pratiques relatives aux mises à jour logicielles pour l’outil, les rôles administratifs et les comptes pour ces rôles, les systèmes d’exploitation sur lesquels l’outil est hébergé ou à partir desquels il est géré, et toutes les autres dépendances matérielles ou logicielles de cet outil)
* La fréquence et la quantité des déploiements de logiciels et mises à jour sur vos PAW
* La configuration requise pour l’inventaire détaillé et les informations de configuration
* Conditions requises pour la surveillance de la sécurité
* Les normes organisationnelles et autres facteurs spécifiques à l’organisation

Selon le principe de source propre, tous les outils utilisés pour gérer ou surveiller les PAW doivent avoir un niveau d’approbation supérieur ou égal à celui des PAW. Pour cela, ces outils doivent généralement être gérés à partir d’un PAW afin d’assurer l’absence de dépendance de sécurité vis-à-vis des stations de travail à privilèges inférieurs.

Ce tableau décrit les différentes approches qui peuvent être utilisées pour gérer et surveiller les PAW :

|Approche|Observations|
|------|---------|
|Par défaut dans le PAW<br /><br />-   Windows Server Update Services<br />-   Windows Defender|-   Aucun coût supplémentaire<br />-   Exécute les fonctions de sécurité de base requise<br />-   Les instructions fournies dans ce guide|
|Gestion avec [Intune](https://technet.microsoft.com/library/jj676587.aspx)|<ul><li>Fournit le contrôle et la visibilité du cloud<br /><br /><ul><li>Déploiement de logiciel</li><li>o   Gérer les mises à jour logicielles</li><li>Gestion de stratégie du Pare-feu Windows</li><li>Protection anti-programme malveillant</li><li>Assistance à distance</li><li>Gestion des licences logicielles.</li></ul></li><li>Aucune infrastructure serveur requise</li><li>La procédure de la Phase 2 « Activer la connectivité aux services cloud » doit être suivie</li><li>Si l’ordinateur PAW n’est pas joint à un domaine, vous devez appliquer les lignes de base SCM aux images locales avec les outils fournis dans le téléchargement de ligne de base de sécurité.</li></ul>|
|Nouvelles instances de System Center pour gérer les PAW|-   Assure la visibilité et le contrôle de la configuration, du déploiement de logiciels et des mises à jour de sécurité<br />-   Nécessite une infrastructure serveur distincte, avec le niveau de sécurité des PAW et du personnel compétent pour les rôles à privilèges élevés|
|Gestion des PAW avec des outils de gestion existants|-Crée un risque significatif de compromission des Paw, sauf si l’infrastructure de gestion existante est affiché pour le niveau de sécurité de Paw **Remarque :**     Microsoft décourage généralement cette approche, sauf si votre organisation ait une raison spécifique pour l’utiliser. D’après notre expérience, il est généralement très coûteux de donner à tous ces outils (et leurs dépendances de sécurité) le niveau de sécurité des PAW.<br />-   La plupart de ces outils assurent la visibilité et le contrôle de la configuration, du déploiement de logiciels et des mises à jour de sécurité|
|Analyse de sécurité ou outils de surveillance nécessitant l’accès administrateur|Comprend un outil qui installe un agent ou requiert un compte disposant d’un accès administratif local.<br /><br />-   Nécessite de mettre la sécurité des outils au niveau de celle des PAW.<br />-   Peut nécessiter la réduction du cadre de sécurité des PAW pour prendre en charge les fonctionnalités des outils (en ouvrant les ports, installant Java ou d’autres intergiciels, etc.), ce qui constitue un compromis de sécurité.|
|Informations et événements gestion des événements (SIEM)|<ul><li>Si SIEM est sans agent<br /><br /><ul><li>Il est possible d’accéder aux événements sur les PAW sans accès administratif à l’aide d’un compte dans le groupe **Lecteurs des journaux d’événements**</li><li>Nécessite l’ouverture des ports de réseau pour autoriser le trafic entrant à partir des serveurs SIEM</li></ul></li><li>Si SIEM requiert un agent, consultez l’autre ligne **Analyse de sécurité ou outils de surveillance nécessitant l’accès administrateur**.</li></ul>|
|WEF (Windows Event Forwarding)|-   Fournit une méthode de transfert des événements de sécurité sans agent des PAW vers un collecteur externe ou SIEM<br />-   Il est possible d’accéder aux événements sur les PAW sans accès administratif<br />-   Ne nécessite pas l’ouverture des ports de réseau pour autoriser le trafic entrant à partir des serveurs SIEM|

## <a name="operating-paws"></a>Exploitation des PAW

La solution PAW doit être exploitée en respectant les normes des [Normes opérationnelles](http://aka.ms/securitystandards) basées sur le principe de source propre.

## <a name="related-topics"></a>Rubriques connexes

[Les Services de cybersécurité de Microsoft attrayantes](https://www.microsoft.com/en-us/microsoftservices/campaigns/cybersecurity-protection.aspx)

[Aperçu de Premier : Comment l’atténuer Pass-the-Hash et autres formes de vol d’informations d’identification](https://channel9.msdn.com/Blogs/Taste-of-Premier/Taste-of-Premier-How-to-Mitigate-Pass-the-Hash-and-Other-Forms-of-Credential-Theft)

[Microsoft Advanced Threat Analytique](http://aka.ms/ata)

[Protéger les informations d’identification de domaine dérivées avec Credential Guard](https://technet.microsoft.com/library/mt483740%28v=vs.85%29.aspx)

[Vue d’ensemble de Device Guard](https://technet.microsoft.com/library/dn986865(v=vs.85).aspx)

[Protection des ressources à haute valeur avec les stations de travail admin sécurisées](https://msdn.microsoft.com/en-us/library/mt186538.aspx)

[Mode utilisateur isolé dans Windows 10 avec Dave Probert (Channel 9)](https://channel9.msdn.com/Blogs/Seth-Juarez/Isolated-User-Mode-in-Windows-10-with-Dave-Probert)

[Isolé des processus en Mode utilisateur et les fonctionnalités de Windows 10 avec Logan Gabriel (Channel 9)](http://channel9.msdn.com/Blogs/Seth-Juarez/Isolated-User-Mode-Processes-and-Features-in-Windows-10-with-Logan-Gabriel)

[Plus sur les processus et les fonctionnalités en Mode utilisateur isolé de Windows 10 avec Dave Probert (Channel 9)](https://channel9.msdn.com/Blogs/Seth-Juarez/More-on-Processes-and-Features-in-Windows-10-Isolated-User-Mode-with-Dave-Probert)

[Atténuation de vol d’informations d’identification à l’aide de l’utilisateur isolé Mode Windows 10 (Channel 9)](https://channel9.msdn.com/Blogs/Seth-Juarez/Mitigating-Credential-Theft-using-the-Windows-10-Isolated-User-Mode)

[Activer la Validation KDC stricte dans Windows Kerberos](https://www.microsoft.com/en-us/download/details.aspx?id=6382)

[Quelles sont les nouveautés dans l’authentification Kerberos pour Windows Server 2012](https://technet.microsoft.com/library/hh831747.aspx)

[Assurance du mécanisme d’authentification pour les services AD DS dans le Guide pas à pas de Windows Server 2008 R2](https://technet.microsoft.com/library/dd378897(v=ws.10).aspx)

[Module de plateforme sécurisée](C:\sd\docs\p_ent_keep_secure\p_ent_keep_secure\trusted_platform_module_technology_overview.xml)
