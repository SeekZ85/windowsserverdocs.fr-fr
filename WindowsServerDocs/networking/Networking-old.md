---
title: Mise en réseau
description: Cette rubrique fournit une vue d’ensemble des technologies de mise en réseau SDN (Software Defined Networking) et de plateforme réseau qui sont disponibles dans Windows Server 2016.
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.date: 05/08/2018
ms.assetid: daaf6b61-5953-4c2d-b6b8-7c885b552646
manager: dougkim
ms.author: pashort
author: shortpatti
ms.localizationpriority: medium
ms.openlocfilehash: 1cc30f239f1c4c9107ce0afcfb70647d43384949
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71356786"
---
# <a name="networking"></a>Mise en réseau

>S’applique à : Windows Server (Canal semi-annuel), Windows Server 2016

>[!TIP]
> Vous recherchez des informations sur des versions plus anciennes de Windows Server ? Consultez nos autres [bibliothèques Windows Server](/previous-versions/windows/) sur docs.microsoft.com. Vous pouvez également [rechercher dans ce site](https://docs.microsoft.com/search/index?search=Windows+Server&dataSource=previousVersions) des informations spécifiques.

<img src="../media/landing-icons/network.png" style='float:left; padding:.5em;' alt="Icon depicting two networked computers"> La mise en réseau est une partie fondamentale de la plateforme \(SDDC\) du centre de donnes, et Windows Server 2016 fournit des technologies \(de\) mise en réseau SDN nouvelles et améliorées pour vous aider à passer à une solution SDDC entièrement réalisée pour votre organisation.

Lorsque vous gérez des réseaux en tant que ressource définie par un logiciel, vous pouvez décrire une fois les exigences de l’infrastructure d’une application, puis choisir l’emplacement d’exécution de l’application (localement ou dans le Cloud). 

Cette cohérence signifie que vos applications sont désormais plus faciles à mettre à l’échelle ; vous pouvez exécuter des applications en toute transparence, n’importe où, en sachant que la sécurité, les performances, la qualité de service et la disponibilité seront toujours aussi fiables.

>[!Note]
> Pour télécharger Windows Server, accédez à [Windows Server - Évaluations](https://www.microsoft.com/evalcenter/evaluate-windows-server-technical-preview).

Windows Server 2016 ajoute les nouvelles technologies de mise en réseau suivantes :

- Mise en réseau définie par le logiciel : Le Contrôleur de réseau offre une fonction d’automatisation programmable et centralisée pour gérer, configurer, analyser et dépanner l’infrastructure réseau virtuelle et physique dans votre centre de données. Le contrôleur de réseau vous permet d’utiliser la virtualisation de fonction réseau pour déployer \(facilement\) des machines virtuelles \(de\) machines virtuelles pour l’équilibrage de charge de logiciels SLB afin d’optimiser les charges de trafic réseau pour vos locataires, et Ras Des passerelles pour fournir aux locataires les options de connectivité dont ils ont besoin entre Internet, local et les ressources de Cloud. Ce Contrôleur vous permet également de gérer le pare-feu du centre de données sur les machines virtuelles et les hôtes Hyper-V.

- Plateforme réseau : À l’aide de nouvelles fonctionnalités pour les technologies de plateforme réseau existantes, vous pouvez utiliser une stratégie DNS pour personnaliser les réponses de votre serveur DNS aux requêtes, utiliser une carte réseau convergée qui gère le trafic d’accès \(direct à la mémoire à distance combiné RDMA\) et le trafic Ethernet. \(, utilisez Switch Embedded Teaming\) Set pour créer des commutateurs virtuels Hyper-V connectés à des cartes réseau RDMA et \(utilisez\) la gestion des adresses IP IPAM pour gérer les zones et les serveurs DNS, ainsi que les adresses DHCP et IP.

Pour en savoir plus, voir [Scénarios de réseaux pris en charge par Windows Server](windows-server-supported-networking-scenarios.md).

Les sections suivantes fournissent des informations sur les technologies SDN et les technologies de plateforme réseau.

## <a name="software-defined-networking-technologies"></a>Technologies de mise en réseau SDN (Software-Defined Networking)

### <a name="software-defined-networking-40sdn41sdnsoftware-defined-networkingmd"></a>[SDN de mise &#40;en réseau définie par logiciel&#41;](sdn/software-defined-networking.md)

Vous pouvez utiliser cette rubrique pour découvrir les technologies de mise en réseau SDN (Software-Defined Networking) offertes par Windows Server, System Center et Microsoft Azure.

>[!NOTE]
>Pour les ordinateurs hôtes Hyper-V et \(les\) machines virtuelles qui exécutent des serveurs d’infrastructure SDN, tels que des nœuds de contrôleur de réseau et d’équilibrage de la charge logicielle, vous devez installer Windows Server 2016 Datacenter Edition. Pour les ordinateurs hôtes Hyper-V qui contiennent uniquement des machines virtuelles de charge\-de travail client connectées à des réseaux contrôlés SDN, vous pouvez exécuter Windows Server 2016 Standard Edition.

### <a name="deploy-a-software-defined-network-infrastructure-using-scriptssdndeploydeploy-a-software-defined-network-infrastructure-using-scriptsmd"></a>[Déployer une infrastructure réseau définie par logiciel à l’aide de scripts](sdn/deploy/Deploy-a-Software-Defined-Network-infrastructure-using-scripts.md)
Ce guide fournit des instructions permettant de déployer le Contrôleur réseau via des passerelles et des réseaux virtuels dans un environnement de laboratoire de test.

### <a name="network-controllersdntechnologiesnetwork-controllernetwork-controllermd"></a>[Contrôleur de réseau](sdn/technologies/network-controller/Network-Controller.md)

Le Contrôleur de réseau offre une fonction d’automatisation programmable et centralisée pour gérer, configurer, analyser et dépanner l’infrastructure réseau virtuelle et physique dans votre centre de données.

### <a name="software-load-balancing-40slb41-for-sdnsdntechnologiesnetwork-function-virtualizationsoftware-load-balancing-for-sdnmd"></a>[Équilibrage &#40;de charge logiciel&#41; SLB pour Sdn](sdn/technologies/network-function-virtualization/software-load-balancing-for-sdn.md)

Les fournisseurs \(de services\) Cloud CSP et les entreprises qui déploient la mise en réseau SDN (Software Defined Networking) dans Windows \(Server 2016 peuvent utiliser l’équilibrage de charge logiciel SLB\) pour distribuer uniformément le locataire et le locataire le trafic réseau des clients entre les ressources du réseau virtuel. La fonctionnalité d’équilibrage de charge de Windows Server vous permet d’activer plusieurs serveurs pour héberger la même charge de travail, ce qui garantit évolutivité et haute disponibilité.

### <a name="ras-gateway-for-sdnsdntechnologiesnetwork-function-virtualizationras-gateway-for-sdnmd"></a>[Passerelle du serveur d’accès à distance pour SDN](sdn/technologies/network-function-virtualization/RAS-Gateway-for-SDN.md)

La passerelle RAS, qui est un routeur basé sur le logiciel, multi \(-\) locataire Border Gateway Protocol BGP dans Windows Server 2016, est conçue\) pour les fournisseurs \(de services Cloud et les entreprises qui hébergent réseaux virtuels à plusieurs locataires utilisant la virtualisation de réseau Hyper-V. 

### <a name="network-function-virtualizationsdntechnologiesnetwork-function-virtualizationnetwork-function-virtualizationmd"></a>[Virtualisation de fonction réseau](sdn/technologies/network-function-virtualization/Network-Function-Virtualization.md)

Dans les centres de développement logiciels, les fonctions réseau qui sont effectuées par les \(Appliances matérielles, telles que les équilibreurs de charge, les pare-feu\) , les routeurs, les commutateurs, etc., sont de plus en plus virtualisées en tant qu’Appliances virtuelles. Cette « virtualisation des fonctions réseau » est une évolution naturelle de la virtualisation des serveurs et des réseaux.

### <a name="datacenter-firewall-overviewsdntechnologiesnetwork-function-virtualizationdatacenter-firewall-overviewmd"></a>[Présentation du pare-feu de centre de données](sdn/technologies/network-function-virtualization/Datacenter-Firewall-Overview.md)

Le pare-feu de centre de données est un pare-feu de couche réseau, 5-tuple (protocole, numéros de port source et de destination, adresses IP source et de destination) avec état et multi-locataire.

## <a name="bkmk_networking"></a>Technologies de mise en réseau

Le tableau suivant fournit des liens vers certaines technologies de mise en réseau de Windows Server 2016.

### <a name="whats-new-in-networkingnetworkingwhat-s-new-in-networkingmd"></a>[Nouveautés en matière de mise en réseau](../networking/What-s-New-in-Networking.md)

Les sections suivantes vous permettent de découvrir les nouvelles technologies de mise en réseau et les nouvelles fonctionnalités des technologies existantes dans Windows Server 2016.

### <a name="branchcachebranchcachebranchcachemd"></a>[BranchCache](branchcache/BranchCache.md)

BranchCache est une technologie d’optimisation \(de\) la bande passante du réseau étendu. Pour optimiser la bande passante d’un réseau étendu lorsque des utilisateurs accèdent à du contenu sur des serveurs distants, BranchCache extrait le contenu des serveurs de contenu de votre siège social ou du cloud hébergé et le met en cache sur les systèmes des filiales, permettant ainsi aux ordinateurs clients des filiales d’accéder localement au contenu au lieu de passer par le réseau étendu.

### <a name="core-network-guide-for-windows-server-2016core-network-guidecore-network-guide-windows-servermd"></a>[Guide du réseau de base pour Windows Server 2016](core-network-guide/core-network-guide-windows-server.md)

Découvrez comment déployer un réseau Windows Server avec le Guide du réseau de base, ainsi que comment ajouter des fonctionnalités à votre déploiement de réseau avec les Guides d’accompagnement du réseau de base.

### <a name="directaccessremoteremote-accessdirectaccessdirectaccessmd"></a>[DirectAccess](../remote/remote-access/directaccess/DirectAccess.md)

DirectAccess assure la connectivité entre les utilisateurs distants et les ressources réseau de l'organisation. 

La documentation de DirectAccess se trouve désormais dans la section [Accès à distance et gestion de serveur](https://docs.microsoft.com/windows-server/remote/) de la table des matières de Windows Server 2016, sous [Accès à distance](https://docs.microsoft.com/windows-server/remote/remote-access/remote-access). Pour plus d’informations, voir [DirectAccess](../remote/remote-access/directaccess/DirectAccess.md).

### <a name="domain-name-system-40dns41dnsdns-topmd"></a>[DNS DNS ( &#40;Domain Name System)&#41;](dns/dns-top.md)

Le système \(DNS\) fait partie d’une série de protocoles répondant aux normes du secteur, qui inclut le protocole TCP/IP standard. Lorsqu’ils sont associés, le client DNS et le serveur DNS fournissent des services de résolution des noms pour le mappage des noms d’ordinateurs et des adresses IP aux utilisateurs et aux ordinateurs.

### <a name="dynamic-host-configuration-protocol-40dhcp41technologiesdhcpdhcp-topmd"></a>[DHCP DHCP (Dynamic &#40;Host Configuration Protocol)&#41;](technologies/dhcp/dhcp-top.md)

La fonction Dynamic Host Configuration Protocol \(DHCP\) est un protocole client/serveur qui fournit automatiquement une adresse Internet Protocol \(IP\) et d’autres informations de configuration pertinentes à un hôte IP (par exemple, masque de sous-réseau et passerelle par défaut).

### <a name="hyper-v-network-virtualizationsdntechnologieshyper-v-network-virtualizationhyper-v-network-virtualizationmd"></a>[Virtualisation de réseau Hyper-V](sdn/technologies/hyper-v-network-virtualization/Hyper-V-Network-Virtualization.md)

La fonction de virtualisation de réseau Hyper-V \(HNV\) permet la virtualisation des réseaux des clients sur une infrastructure réseau physique partagée.

### <a name="hyper-v-virtual-switchvirtualizationhyper-v-virtual-switchhyper-v-virtual-switchmd"></a>[Commutateur virtuel Hyper-V](../virtualization/hyper-v-virtual-switch/Hyper-V-Virtual-Switch.md)

Le commutateur virtuel Hyper-V désigne un commutateur réseau Ethernet de couche 2 logiciel disponible dans le Gestionnaire Hyper-V lorsque vous installez le rôle serveur Hyper-V. Le commutateur offre des fonctionnalités gérées par programme et extensibles pour connecter des machines virtuelles aux réseaux virtuels et au réseau physique à la fois. Qui plus est, le commutateur virtuel Hyper-V assure l’application de la stratégie de sécurité et d’isolement, ainsi que des niveaux de service. 

La documentation du commutateur virtuel Hyper\-V se trouve désormais dans la section **Virtualisation** de la table des matières de Windows Server 2016. Pour plus d’informations, voir [Commutateur virtuel Hyper\-V](../virtualization/hyper-v-virtual-switch/Hyper-V-Virtual-Switch.md).

### <a name="ip-address-management-40ipam41technologiesipamipam-topmd"></a>[Gestion &#40;des adresses IP IPAM&#41;](technologies/ipam/ipam-top.md)

La fonction de gestion des adresses IP \(IPAM\) est une suite d’outils intégrés permettant d’activer la planification, le déploiement, la gestion et la surveillance de bout en bout de votre infrastructure d’adresses IP, avec une expérience utilisateur enrichie. IPAM Découvre automatiquement les serveurs d’infrastructure d’adresses IP et les serveurs \(DNS\) du système de noms de domaine sur votre réseau et vous permet de les gérer à partir d’une interface centrale.

### <a name="network-load-balancingtechnologiesnetwork-load-balancingmd"></a>[Équilibrage de la charge réseau](technologies/Network-Load-Balancing.md)

L’équilibrage de la charge réseau ou Network Load Balancing \(NLB\) répartit le trafic sur plusieurs serveurs à l’aide du protocole réseau TCP/IP. Dans le cas de déploiements qui ne sont pas de type SDN, l’équilibrage de la charge réseau s’assure que les applications sans état, par exemple les serveurs web qui exécutent Internet Information Services \(IIS\), sont évolutives, via l’ajout de serveurs supplémentaires au fur et à mesure de l’augmentation de la charge.

### <a name="high-performance-networkingtechnologieshpnhpn-topmd"></a>[Mise en réseau hautes performances](technologies/hpn/hpn-top.md)

Les technologies de déchargement et d’optimisation du réseau dans Windows Server 2016 incluent des fonctions et des technologies purement logicielles, des fonctions et des technologies intégrées à la fois logicielles et matérielles, ainsi que des fonctions et des technologies purement matérielles.

La documentation suivante sur les technologies de déchargement et d’optimisation est également disponible.

- [Guide de configuration de la carte d’interface réseau (NIC) convergée](technologies/conv-nic/cnic-top.md)
- [Data Center Bridging (DCB)](technologies/dcb/dcb-top.md)
- [Mise à l’échelle côté réception virtuelle (vRSS, Virtual Receive Side Scaling)](technologies/vrss/vrss-top.md)


### <a name="network-policy-servertechnologiesnpsnps-topmd"></a>[NPS (Network Policy Server)](technologies/nps/nps-top.md)

Un serveur NPS \(Network Policy Server\) vous permet de créer et d’appliquer des stratégies d’accès réseau valides pour toute l’organisation, qui régissent les demandes d’authentification et l’autorisation des demandes de connexion.

### <a name="network-shell-netshtechnologiesnetshnetshmd"></a>[Environnement réseau (Netsh)](technologies/netsh/netsh.md)

Vous pouvez utiliser l’utilitaire réseau \(netsh\) de Network Shell pour gérer les technologies de mise en réseau dans Windows Server 2016 et Windows 10.

### <a name="network-subsystem-performance-tuningtechnologiesnetwork-subsystemnet-sub-performance-topmd"></a>[Réglage des performances du sous-système réseau](technologies/network-subsystem/net-sub-performance-top.md)

Cette rubrique fournit des informations sur le choix de la carte réseau appropriée pour la charge de travail de votre serveur, la commande des interfaces réseau, les compteurs de performances liés au réseau et le réglage des performances des cartes réseau et des technologies de mise en réseau associées, telles que Réception de la mise \(à\)l’échelle côté réception \(RSS\), réception de la fusion côté réception de RSC et autres.

### <a name="nic-teamingtechnologiesnic-teamingnic-teamingmd"></a>[Association de cartes réseau](technologies/nic-teaming/NIC-Teaming.md)

La fonction d’association de cartes réseau vous permet de regrouper plusieurs cartes réseau Ethernet physiques dans une ou plusieurs cartes réseau virtuelle à définition logicielle. Ces cartes réseau virtuelles fournissent des performances élevées et une tolérance de panne importante en cas de défaillance de la carte réseau.

### <a name="quality-of-service-qos-policytechnologiesqosqos-policy-topmd"></a>[Stratégie de qualité de service (QoS)](technologies/qos/qos-policy-top.md)

Vous pouvez utiliser une stratégie de qualité de service comme pilier de la gestion de bande passante réseau dans toute votre infrastructure Active Directory, en créant des profils de qualité de service dont les paramètres sont distribués à l’aide de la stratégie de groupe.

### <a name="remote-accessremoteremote-accessremote-accessmd"></a>[Accès à distance](../remote/remote-access/remote-access.md)

Vous pouvez utiliser les technologies d’accès à distance, telles que DirectAccess et \(VPN\) de réseau privé virtuel pour permettre aux employés distants de se connecter aux ressources réseau internes. En outre, vous pouvez utiliser l’accès à distance pour le \(routage\) LAN du réseau local et pour le proxy d’application Web. Celui-ci fournit la fonctionnalité de proxy inverse pour les applications web au sein de votre réseau d’entreprise pour permettre aux utilisateurs d’y accéder à partir de n’importe quel appareil depuis l’extérieur du réseau d’entreprise.

La documentation de l’accès à distance se trouve désormais dans la section [Accès à distance et gestion de serveur](https://docs.microsoft.com/windows-server/remote/) de la table des matières de Windows Server 2016. Pour plus d’informations, voir [Accès à distance](../remote/remote-access/remote-access.md).

Pour plus d’informations sur le proxy d’application web, qui est un service de rôle du rôle serveur Accès à distance, voir [Proxy d’application web dans Windows Server 2016](https://docs.microsoft.com/windows-server/remote/remote-access/web-application-proxy/web-application-proxy-windows-server).

### <a name="virtual-private-networking-vpnremoteremote-accessvpnvpn-topmd"></a>[Réseau privé virtuel (VPN)](../remote/remote-access/vpn/vpn-top.md)

Dans Windows Server 2016, **DirectAccess et VPN** un service du rôle serveur **Accès à distance**.

Lorsque vous installez l’accès à distance en tant que serveur VPN, vous pouvez utiliser \(le\) VPN de réseau privé virtuel pour fournir à vos employés distants des connexions au réseau de votre organisation via Internet, tout en conservant les informations confidentialité avec les connexions chiffrées.

Avec un VPN Accès à distance Windows Server 2016 \(et des ordinateurs clients Windows 10\), vous avez la possibilité de déployer un VPN Toujours actif (AlwaysOn). Un VPN Toujours actif (AlwaysOn) vous donne la possibilité de gérer les clients VPN distants qui sont connectés en permanence, tout en se montrant très pratique pour les collaborateurs distants qui n’ont plus besoin de se connecter ou déconnecter manuellement du VPN du réseau de votre organisation.

Pour plus d’informations, voir [Guide de déploiement de l’accès à distance Toujours actif sur VPN pour Windows Server 2016 et Windows 10](https://docs.microsoft.com/windows-server/remote/remote-access/vpn/always-on-vpn/deploy/always-on-vpn-deploy).

>[!NOTE]
>La documentation VPN se trouve désormais dans la section [Accès à distance et gestion de serveur](https://docs.microsoft.com/windows-server/remote/) de la table des matières de Windows Server 2016, sous [Accès à distance](https://docs.microsoft.com/windows-server/remote/remote-access/remote-access).

Pour plus d’informations sur le VPN, voir [Virtual Private Networking (VPN)](https://docs.microsoft.com/windows-server/remote/remote-access/vpn/vpn-top).

### <a name="windows-container-networkinghttpsdocsmicrosoftcomvirtualizationwindowscontainersmanage-containerscontainer-networking"></a>[Mise en réseau de conteneurs Windows](https://docs.microsoft.com/virtualization/windowscontainers/manage-containers/container-networking)

La mise en réseau de conteneurs Windows vous permet de créer et gérer des réseaux de manière à connecter les points de terminaison de conteneur, aussi bien aux hôtes Windows 10 et Windows Server à l’aide d’outils conformes aux normes du secteur et de flux de travail. Les réseaux de conteneurs Windows prennent en charge plusieurs topologies, notamment privée, à plat-couche 2 et routé-couche 3.

Les superpositions que vous pouvez créer localement sur l’hôte sont également prises en charge à l’aide de dockr, Kubernetes ou Windows PowerShell via les plug-ins \(qui\)communiquent avec le service de mise en réseau d’ordinateurs hôtes Windows. Vous pouvez créer et gérer des\-réseaux de clusters à plusieurs nœuds via des systèmes d’orchestration de niveau supérieur en communiquant via un agent local à chaque HNS de nœud.

### <a name="windows-internet-name-service-winstechnologieswinswins-topmd"></a>[Service WINS Windows Internet Name Service)](technologies/wins/wins-top.md)

Le service WINS (Windows Internet Name Service) représente un service hérité d’inscription et de résolution de noms d’ordinateurs qui mappe les noms NetBIOS d’ordinateurs à des adresses IP. Il est recommandé d'utiliser DNS plutôt que WINS.

## <a name="additional-resources"></a>Ressources complémentaires

Vous trouverez des ressources de mise en réseau pour les systèmes antérieurs à Windows Server 2016 aux emplacements suivants.

- [Vue d’ensemble de la mise en réseau](https://technet.microsoft.com/library/hh831357.aspx) Windows Server 2012 et Windows Server 2012 R2
- [Mise en réseau](https://technet.microsoft.com/library/cc753940) Windows Server 2008 et Windows Server 2008 R2
- Contenu retiré de Windows Server 2003 [Windows server 2003/2003 R2](https://www.microsoft.com/download/details.aspx?id=53314)
