---
title: Améliorations du VPN Toujours actif (AlwaysOn)
description: VPN Always On présente de nombreux avantages sur les solutions VPN de Windows du passé. Principales améliorations apportées dans l’intégration, de sécurité, de connectivité, de contrôle de mise en réseau et de compatibilité alignent VPN Always On de la vision de Microsoft cloud-first, mobile-first.
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.assetid: ''
ms.author: pashort
author: shortpatti
ms.date: 11/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: d7844d93ac898316580123c82e08bb6f02d51a2b
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59836520"
---
# <a name="always-on-vpn-enhancements"></a>Améliorations du VPN Toujours actif (AlwaysOn)

>S'applique à : Windows Server (canal semi-annuel), Windows Server 2016, Windows 10

&#171;[ **Précédente :** En savoir plus sur les fonctionnalités de VPN Always On](../vpn-map-da.md)<br>
&#187;[ **Suivant :** En savoir plus sur la technologie VPN Always On](always-on-vpn-technology-overview.md)

VPN Always On présente de nombreux avantages sur les solutions VPN de Windows du passé. Les améliorations clées suivantes alignent VPN Always On de la vision de Microsoft cloud-first, mobile-first :

- **Intégration de plate-forme :** VPN Always On a une meilleure intégration avec le système d’exploitation de Windows et des solutions tierces pour fournir une plate-forme robuste pour les scénarios de connexion avancées innombrables.

- **Sécurité :** VPN Always On dispose de fonctionnalités de nouveau la sécurité avancée pour restreindre le type de trafic, les applications peuvent utiliser la connexion VPN, et les méthodes d’authentification que vous pouvez utiliser pour lancer la connexion. Lorsque la connexion est active, la plupart du temps, il est particulièrement important de sécuriser la connexion. Pour plus d’informations, consultez [options d’authentification VPN](https://docs.microsoft.com/en-us/windows/security/identity-protection/vpn/vpn-authentication).

- **Connectivité VPN :** VPN Always On, avec ou sans périphériques Tunnel offre la possibilité de déclenchement automatique. Avant de VPN Always On, la possibilité de déclencher une connexion automatique à un utilisateur ou l’authentification des appareils n’était pas possible.  

- **Contrôle de la mise en réseau :** VPN Always On permet aux administrateurs de spécifier des stratégies de routage à un niveau plus granulaire, voire une l’application individuelle, ce qui est parfait pour les applications line of business (LOB) qui nécessitent un accès spécial à distance.  VPN Always On est également entièrement compatible avec les deux Internet Protocol version 4 (IPv4) et version 6 (IPv6). Contrairement à DirectAccess, il n’existe aucune dépendance spécifique sur IPv6.

  >[!Note]
  >Avant de commencer, assurez-vous d’activer IPv6 sur le serveur VPN. Sinon, Impossible d’établir une connexion et affiche un message d’erreur.
  
- **Configuration et la compatibilité :** VPN Always On peut être déployée et gérée de plusieurs façons, ce qui donne VPN Always On plusieurs avantages par rapport à l’autre logiciel de client VPN.

## <a name="platform-integration"></a>Intégration de plate-forme

Microsoft a introduit ou amélioré les fonctionnalités d’intégration suivantes dans VPN Always On :

| Amélioration des services clés | Description |
| ---- | ---- |
| **[Protection des informations Windows (WIP)](https://docs.microsoft.com/windows/threat-protection/windows-information-protection/protect-enterprise-data-using-wip)** | Intégration à WIP permet la mise en œuvre de la stratégie réseau déterminer si le trafic est autorisé à accéder via la connexion VPN. Si le profil utilisateur est actif et les stratégies de protection des informations Windows sont appliquées, VPN Always On est automatiquement déclenchée pour vous connecter. En outre, lorsque vous utilisez des travaux en cours, il est inutile de spécifier les règles AppTriggerList et TrafficFilterList séparément dans le profil VPN (sauf si vous souhaitez que configuration plus avancée), car les stratégies de protection des informations Windows et les listes d’applications automatiquement en vigueur. |
| **[Windows Hello entreprise](https://docs.microsoft.com/windows/access-protection/hello-for-business/hello-overview)** | VPN Always On en mode natif prend en charge Windows Hello for Business (en mode d’authentification par certificat) pour fournir une unique session expérience transparente pour les deux se connecter à l’ordinateur et connexion au VPN. Par conséquent, aucune authentification secondaire (informations d’identification de l’utilisateur) est nécessaire pour la connexion VPN, rendant ainsi possible d’utiliser une connexion Always On avec Windows Hello pour l’authentification d’entreprise. |
| **[Accès conditionnel de Microsoft Azure](https://docs.microsoft.com/azure/active-directory/active-directory-conditional-access-controls)** | Le client VPN Always On peut intégrer à la plateforme d’accès conditionnel Azure pour appliquer l’authentification multifacteur (MFA), la conformité des appareils ou une combinaison des deux. Lorsqu’elle est conforme aux stratégies d’accès conditionnel, Azure Active Directory (Azure AD) émet un certificat d’authentification IPsec (IP Security) courte durée de vie (par défaut, 60 minutes) qui peut ensuite être utilisé pour s’authentifier auprès de la passerelle VPN. Conformité de l’appareil utilise des stratégies de conformité System Center Configuration Manager/Intune, ce qui peuvent inclure l’état de l’attestation d’intégrité appareil dans le cadre de la vérification de conformité de connexion. |
| **Azure MFA** | Lorsqu’elles sont combinées avec les services d’authentification Dial-In Service RADIUS (Remote User) et l’extension de serveur NPS (Network Policy Server) pour Azure MFA, l’authentification VPN peut utiliser MFA fort. |
| **Plug-in de VPN tiers** | Avec la plateforme de Windows universelle (UWP), fournisseurs VPN tiers peuvent créer une application unique pour la plage complète de Windows 10 appareils. UWP fournit une couche de API de core garanti entre les périphériques, éliminant la complexité et les problèmes souvent associées avec l’écriture de pilotes au niveau du noyau. Actuellement, Windows 10 UWP VPN plug-ins existent pour [Pulse Secure](https://www.microsoft.com/p/pulse-secure/9nblggh3b0bp), [F5 accès](https://www.microsoft.com/p/f5-access/9wzdncrdsfn0), [VPN Check Point Capsule](https://www.microsoft.com/p/check-point-capsule-vpn/9wzdncrdjxtj), [FortiClient](https://www.microsoft.com/p/forticlient/9wzdncrdh6mc), [ SonicWall Mobile Connect](https://www.microsoft.com/p/sonicwall-mobile-connect/9wzdncrdsfkz), et [GlobalProtect](https://www.microsoft.com/p/globalprotect/9nblggh6bzl3); ne fait aucun doute, d’autres seront affiche dans le futur. |
---

## <a name="security"></a>Sécurité

Les améliorations de principales de sécurité sont les suivantes :

| Amélioration des services clés | Description |
| ---- | ---- |
| **Filtres de trafic** | Par le biais des filtres de trafic, vous pouvez spécifier des stratégies côté client qui déterminent quel trafic est autorisé dans le réseau d’entreprise. De cette façon, les administrateurs peuvent appliquer les restrictions d’application ou le trafic sur l’interface VPN, en limitant son utilisation pour des sources spécifiques, les ports de destination et les adresses IP. Deux types de règles de filtrage sont disponibles :<ul><li>**Règles en fonction des applications.** Règles de pare-feu en fonction des applications sont basées sur une liste d’applications spécifiées afin que seul le trafic provenant de ces applications sont autorisés à accéder via l’interface VPN.</li><li>**Règles de trafic.** Règles de pare-feu de trafic en fonction sont basées sur les exigences de réseau telles que les protocoles, adresses et ports. Utilisez ces règles uniquement pour le trafic qui correspond à ces conditions spécifiques sont autorisés à accéder via l’interface VPN.<p><p>_**Remarque.**_<br>Ces règles s’appliquent uniquement au trafic sortant à partir de l’appareil. Utilisation du trafic filtre bloque le trafic entrant à partir du réseau d’entreprise vers le client. </li></ul> |
| **VPN par application** | VPN par application revient à avoir un filtre de trafic basés sur l’application, mais il va plus loin pour combiner des déclencheurs d’application avec un filtre de trafic basés sur l’application afin que la connectivité VPN est limitée à une application spécifique, par opposition à toutes les applications sur le client VPN. La fonctionnalité lance automatiquement lorsque l’application démarre. |
| **Prise en charge des algorithmes de chiffrement IPsec personnalisés** | VPN Always On prend en charge l’utilisation de RSA et de courbe elliptique basée sur la cryptographie personnalisé algorithmes de chiffrement pour répondre aux administrations strictes ou stratégies de sécurité de l’organisation. |
| **Prise en charge native de protocole EAP (Extensible Authentication)** | VPN Always On prend nativement en charge EAP, qui vous permet d’utiliser un ensemble varié de Microsoft et les types EAP par des tiers dans le cadre du flux de travail de l’authentification. EAP fournit une authentification sécurisée basée sur les types d’authentification suivants :<ul><li>Nom d’utilisateur et mot de passe</li><li>Carte à puce (physique et virtuel)</li><li>Certificats d’utilisateur</li><li>Windows Hello Entreprise</li><li>Prise en charge MFA par le biais de l’intégration EAP RADIUS</li></ul>Le fournisseur de l’application contrôle les méthodes de plug-in d’authentification UWP VPN tierce, bien qu’ils ont un tableau des options disponibles, y compris les types d’informations d’identification personnalisées et prise en charge du secret à usage unique. |
---

## <a name="vpn-connectivity"></a>Connectivité VPN

Les améliorations principales dans la connectivité VPN Always On sont les suivantes :

| Amélioration des services clés | Description |
| ---- | ---- |
| **Always On** | Always On est une fonctionnalité de Windows 10 qui permet le profil VPN actif pour vous connecter automatiquement et de rester connecté basée sur des déclencheurs, à savoir, connexion de l’utilisateur, changement d’état de réseau ou écran active de l’appareil. Always On est également intégré à l’expérience de secours connecté afin d’optimiser la durée de la batterie. |
| **Déclenchement de l’application** | Vous pouvez configurer des profils VPN dans Windows 10 pour se connecter automatiquement au lancement d’un jeu spécifié d’applications. Vous pouvez configurer les applications de bureau et UWP pour déclencher une connexion VPN. |
| **En fonction du nom de déclenchement** | Avec VPN Always On, vous pouvez définir des règles afin que les requêtes de nom de domaine spécifique déclenchent la connexion VPN. Windows 10 prend désormais en charge en fonction du nom de déclenchement pour les ordinateurs joints au domaine et joints à un domaine (auparavant, seuls les ordinateurs joints à un domaine ont été gérés). |
| **Détection des réseaux approuvés** | VPN Always On comprend cette fonctionnalité pour vous assurer que connectivité VPN n’est pas déclenchée si un utilisateur est connecté à un réseau approuvé, dans les limites de l’entreprise. Vous pouvez combiner cette fonctionnalité avec une des méthodes de déclenchement mentionnés précédemment pour fournir une expérience utilisateur transparente de « se connecter uniquement lorsque nécessaire ». |
| **[Tunnel de l’appareil](../vpn-device-tunnel-config.md)** | VPN Always On vous donne la possibilité de créer un profil VPN dédié pour le périphérique ou ordinateur. Contrairement aux _utilisateur Tunnel_, qui se connecte uniquement après un utilisateur se connecte à l’appareil ou l’ordinateur, _appareil Tunnel_ permet la connexion VPN établir la connectivité avant la connexion de l’utilisateur. Tunnel de l’appareil et utilisateur Tunnel fonctionnent indépendamment avec leurs profils VPN peuvent être connectés en même temps et peuvent utiliser différentes méthodes d’authentification et d’autres paramètres de configuration de VPN comme il convient. |
---

## <a name="networking"></a>Mise en réseau

Voici quelques-unes des améliorations de mise en réseau dans les VPN Always On :

| Amélioration des services clés | Description |
| ---- | ---- |
| **Prise en charge double pile IPv4 et IPv6** | VPN Always On en mode natif prend en charge les deux protocoles IPv4 et IPv6 dans une approche à double pile. Il n’a aucune dépendance spécifique sur un protocole plutôt que l’autre, ce qui permet la compatibilité des applications IPv4/IPv6 maximale combinée avec prise en charge pour IPv6 futurs besoins de mise en réseau.<p>**_Remarque._** Avant de commencer, assurez-vous d’activer IPv6 sur le serveur VPN. Sinon, Impossible d’établir une connexion et affiche un message d’erreur.|
| **Spécifique à l’application des stratégies de routage** | Outre la définition globales stratégies de routage de connexion VPN pour la séparation du trafic internet et intranet, il est possible d’ajouter des stratégies de routage pour contrôler l’utilisation de tunnel fractionné ou forcer les configurations de tunneling sur chaque application. Cette option vous donne un contrôle plus précis sur lequel les applications sont autorisées à interagir avec les ressources via le tunnel VPN. |
| **Itinéraires d’exclusion** | VPN Always On prend en charge la possibilité de spécifier des itinéraires d’exclusion qui contrôlent le comportement de routage pour définir quel trafic doit traverser le VPN uniquement et pas établies via l’interface réseau physique en particulier.<p><p>_**Notes de publication.**_<br>-Exclusion les itinéraires actuellement fonctionnent pour le trafic au sein du même sous-réseau que le client, par exemple, LinkLocal.<br>-Les itinéraires d’exclusion fonctionnent uniquement dans une configuration de tunneling fractionné. |
---

## <a name="configuration-and-compatibility"></a>Configuration et la compatibilité 

Voici quelques-unes des améliorations de configuration et la compatibilité dans VPN Always On :

| Amélioration des services clés | Description |
| ---- | ---- |
| **Compatibilité de passerelle VPN tiers** | Le client VPN Always On ne nécessite pas l’utilisation d’une passerelle VPN basée sur Microsoft pour fonctionner. Via la prise en charge du protocole IKEv2, le client facilite l’interopérabilité avec les passerelles VPN tiers qui prennent en charge ce type de tunneling standard du secteur. Vous pouvez également obtenir l’interopérabilité avec les passerelles VPN tiers à l’aide d’un plug-in de VPN UWP combinées avec un type de tunneling personnalisé sans sacrifier les avantages et fonctionnalités de la plateforme VPN Always On.<p><p>_**Remarque.**_<br>Consultez votre fournisseur de matériel de serveur principal passerelle ou par des tiers sur les configurations et la compatibilité avec les VPN Always On et Tunnel de périphérique à l’aide d’IKEv2. |
| **Prise en charge du protocole standard de l’industrie VPN IKEv2** | Le client VPN Always On prend en charge IKEv2, un des aujourd'hui les plus répandues protocoles de tunneling standard. Cette compatibilité optimise l’interopérabilité avec les passerelles VPN tiers. |
| **Prise en charge de la plateforme** | Prend en charge VPN On AAlways joints au domaine, joint à un domaine (groupe de travail) ou appareils joint à un AD Azure pour permettre les deux entreprises et apportez votre propre appareil les scénarios (BYOD). En outre, le VPN Always On est disponible dans toutes les éditions de Windows. |
| **Divers mécanismes de déploiement et de gestion** | Vous pouvez utiliser plusieurs mécanismes de déploiement et de gestion pour gérer les paramètres de VPN (appelé un _profil VPN_), y compris Windows PowerShell, System Center Configuration Manager, Intune (ou outil de gestion [MDM] des appareils mobiles tiers) et le Concepteur de Configuration de Windows. Ces options de simplifient la configuration de VPN Always On, quel que soit les outils de gestion client que vous utilisez. |
| **Définition de profil VPN standardisée** | VPN Always On prend en charge la configuration à l’aide d’un profil XML standard (ProfileXML), en fournissant un modèle de format standard de configuration qui utilisent de la plupart des ensembles d’outils de déploiement et de gestion. |
---


## <a name="next-steps"></a>Étapes suivantes

- [En savoir plus sur certaines des fonctionnalités avancées VPN Always On](deploy/always-on-vpn-adv-options.md)

- [En savoir plus sur la technologie VPN Always On](always-on-vpn-technology-overview.md)

- [Commencer à planifier votre déploiement VPN Always On](deploy/always-on-vpn-deploy-deployment.md)



---