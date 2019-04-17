---
ms.assetid: e34622ff-b2d0-4f81-8d00-dacd5d6c215e
title: Service de temps Windows
description: 
author: shortpatti
ms.author: pashort
manager: brianlic
ms.date: 02/01/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adds
ms.openlocfilehash: c3c53db3839b5f33a87fe3789f2f7958f0bc42c2
ms.sourcegitcommit: 556361fe7c73c75d6cdc46a67dc88679fbe89c61
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 03/08/2018
---
# <a name="windows-time-service"></a>Service de temps Windows

>S’applique à: Windows Server2016, Windows Server2012R2, Windows Server2012
 
  
## <a name="w2k3tr_times_intro"></a>Référence technique du Service de temps Windows  
**Dans ce guide**  
  
* Où trouver les informations de Configuration de Service de temps Windows  
* Nouveautés du Service de temps Windows  
* Importance des protocoles de temps  
* Comment fonctionne le Service de temps Windows   
* Paramètres et outils de Service de temps Windows  
  
> [!NOTE]  
> Dans Windows Server 2003 et Microsoft Windows 2000 Server, le service d’annuaire est nommé service d’annuaire Active Directory. Dans Windows Server 2008 R2 et Windows Server 2008, le service d’annuaire est nommé Services de domaine Active Directory (AD DS). Le reste de cette rubrique fait référence aux services AD DS, mais les informations sont également applicables à des Services de domaine Active Directory dans Windows Server 2016.  
  
Le service de temps Windows, également appelée W32Time, synchronise la date et l’heure sur tous les ordinateurs dans un domaine AD DS. Synchronisation de l’heure est essentielle pour le bon fonctionnement de nombreux services Windows et les applications métier de. Le service de temps Windows utilise le protocole NTP (Network Time) pour synchroniser l’horloge de l’ordinateur sur le réseau afin qu’une valeur d’horloge précise, ou horodatage, peut être affecté à des demandes d’accès aux ressources et de validation du réseau. Le service s’intègre NTP et fournisseurs de temps, il effectue un service de temps fiable et évolutive pour les administrateurs d’entreprise.  
  
> [!IMPORTANT]  
> Avant Windows Server 2016, le service W32Time n’est pas conçu pour répondre aux besoins des applications sensibles à la fois.  Toutefois, les mises à jour vers Windows Server 2016 permettent désormais d’implémenter une solution pour 1 MS précision dans votre domaine.  Voir [Windows 2016 précis temps](accurate-time.md) et [limite de prise en charge pour configurer le service de temps Windows pour les environnements de grande précision](https://go.microsoft.com/fwlink/?LinkID=179459) pour plus d’informations.  
  
## <a name="BKMK_Config"></a>Où trouver les informations de Configuration de Service de temps Windows  
Ce guide est **pas** abordent la configuration du service de temps Windows. Il existe plusieurs rubriques différentes sur Microsoft TechNet et dans la Base de connaissances Microsoft qui expliquent les procédures pour configurer le service de temps Windows. Si vous avez besoin des informations de configuration, les rubriques suivantes devraient vous aider à trouver les informations appropriées.  
  
-   Pour configurer le service de temps Windows pour l’émulateur de contrôleur de domaine principal racine forêt, voir:  
  
    -   [Configurer le service de temps Windows sur l’émulateur de contrôleur de domaine principal dans le domaine racine de forêt](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731191%28v=ws.10%29) 
  
    -   [Configuration d’une source de temps pour la forêt](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc794823%28v%3dws.10%29) 
  
    -   L’article de la Base de connaissances Microsoft816042, [comment configurer un serveur de temps faisant autorité dans Windows Server](https://go.microsoft.com/fwlink/?LinkID=60402), qui décrit les paramètres de configuration pour les ordinateurs exécutant Windows Server2008R2, Windows Server2008, Windows Server2003, et Windows Server2003R2.  
  
-   Pour configurer le service de temps Windows sur les clients membres du domaine ou serveur ou même contrôleurs de domaine qui ne sont pas configurés en tant que l’émulateur de contrôleur de domaine principal de racine de forêt, voir [configurer un ordinateur client pour la synchronisation automatique de domaine de l’heure](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc816884%28v%3dws.10%29).  
  
    > [!WARNING]  
    > Certaines applications peuvent nécessiter leur ordinateur pour que les services au moment de grande précision. Si tel est le cas, vous pouvez choisir de configurer une source de temps manuelle, mais n’oubliez pas que le service de temps Windows n’a pas été conçu pour fonctionner en tant que source de temps extrêmement précises. Assurez-vous que vous connaissez les limitations de prise en charge pour les environnements de grande précision temps comme décrit dans l’article de la Base de connaissances Microsoft939322, [limite de prise en charge pour configurer le service de temps Windows pour les environnements de grande précision](https://go.microsoft.com/fwlink/?LinkID=179459).  
  
-   Pour configurer le service de temps Windows sur n’importe quel client ou serveur ordinateurs Windows qui sont configurés comme membres du groupe de travail au lieu des membres du domaine voir [configurer une source de temps manuelle pour un ordinateur client sélectionné](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc816656%28v%3dws.10%29).  
  
-   Pour configurer le service de temps Windows sur un ordinateur hôte qui exécute un environnement virtuel, voir l’article de la Base de connaissances Microsoft816042, [comment configurer un serveur de temps faisant autorité dans Windows Server](https://go.microsoft.com/fwlink/?LinkID=60402). Si vous travaillez avec un produit de virtualisation non Microsoft, assurez-vous de consulter la documentation du fournisseur de ce produit.  
  
-   Pour configurer le service de temps Windows sur un contrôleur de domaine qui est en cours d’exécution sur un ordinateur virtuel, il est recommandé de désactiver partiellement une synchronisation horaire entre le système et l’invité système d’exploitation hôte agissant comme un contrôleur de domaine. Cela permet à votre contrôleur de domaine invité synchroniser l’heure de la hiérarchie de domaine, mais il protège contre ayant un temps de décalage si elle est restaurée à partir d’un état enregistré. Pour plus d’informations, voir l’article de la Base de connaissances Microsoft976924, [vous recevez l’ID d’événement Service de temps Windows24, 29 et 38 sur un contrôleur de domaine virtualisé qui s’exécute sur un serveur hôte Windows Server2008 avec Hyper-V](https://go.microsoft.com/fwlink/?LinkID=192236) et [Considérations relatives au déploiement de contrôleurs de domaine virtualisés](https://go.microsoft.com/fwlink/?LinkID=192235).  
  
-   Pour configurer le service de temps Windows sur un contrôleur de domaine agissant en tant que l’émulateur de contrôleur de domaine principal racine forêt qui est également en cours d’exécution sur un ordinateur virtuel, suivez les mêmes instructions pour un ordinateur physique, comme décrit dans [configurer le service de temps Windows sur le contrôleur de domaine principal émulateur dans le domaine racine de forêt](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc731191%28v=ws.10%29).  
  
-   Pour configurer le service de temps Windows sur un serveur membre exécutant comme un ordinateur virtuel, utilisez la hiérarchie de temps du domaine, comme décrit dans ([configurer un ordinateur client pour la synchronisation automatique de domaine de l’heure](https://docs.microsoft.com/en-us/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc816884%28v%3dws.10%29).  
  
## <a name="BKMK_WTS"></a>Nouveautés du Service de temps Windows  
Le service de temps Windows (W32Time) fournit la synchronisation d’horloge de réseau pour les ordinateurs sans avoir besoin de configuration étendues.  
  
Le service de temps Windows est essentiel pour le bon fonctionnement de l’authentification Kerberos version 5 et, par conséquent, pour l’authentification par AD DS. N’importe quelle application prenant en charge Kerberos, y compris la plupart des services de sécurité, s’appuie sur la synchronisation entre les ordinateurs qui participent à la demande d’authentification. Contrôleurs de domaine AD DS doivent également avoir des horloges pour vous aider à garantir la réplication des données précises synchronisés.  
  
Le service de temps Windows est implémenté dans une bibliothèque de liens dynamiques appelée W32Time.dll. W32Time.dll est installé par défaut dans le **%Systemroot%\System32** dossier pendant l’installation et de configuration du système d’exploitation.  
  
W32Time.dll a été développé pour Windows 2000 Server prendre en charge une spécification par le protocole d’authentification Kerberos V5 nécessitant des horloges sur un réseau à synchroniser. À partir de Windows Server 2003, W32Time.dll fourni augmenté la précision de la synchronisation d’horloge de réseau sur le système d’exploitation Windows 2000 Server et, en outre, prise en charge des périphériques matériels et les protocoles de réseau au moyen de fournisseurs de temps. Bien qu’initialement conçue pour fournir la synchronisation de l’horloge pour l’authentification Kerberos, de nombreuses applications actuelles utilisent horodatages pour assurer la cohérence transactionnelle, pour enregistrer le temps d’événements importants et d’autres informations critiques, sensibles à la fois. Ces applications bénéficient de la synchronisation de l’heure entre des ordinateurs qui est fournie par le service de temps Windows.  
  
## <a name="BKMK_TimeProtocols"></a>Importance des protocoles de temps  
Protocoles de temps communiquent entre deux ordinateurs pour échanger des informations de temps, puis utiliser ces informations pour synchroniser leur horloge. Avec le protocole de temps de service de temps Windows, un client demande des informations de temps à partir d’un serveur et synchronise son horloge basée sur les informations reçues.  
  
Le service de temps Windows utilise le protocole NTP afin de synchroniser l’heure sur un réseau. NTP est un protocole de temps Internet qui inclut les algorithmes discipline nécessaires pour la synchronisation des horloges. NTP est un protocole de temps plus précis que le temps protocole SNTP (Simple Network) qui est utilisé dans certaines versions de Windows; Toutefois, W32Time continue de prendre en charge SNTP pour activer la compatibilité descendante avec les ordinateurs exécutant les services de temps SNTP base tels que Windows 2000.  
  
## <a name="see-also"></a>Voir aussi  
[Comment fonctionne le Service de temps Windows](How-the-Windows-Time-Service-Works.md)  
[Paramètres et outils de Service de temps Windows](Windows-Time-Service-Tools-and-Settings.md)  
[Article 902229 de la Base de connaissances Microsoft](https://go.microsoft.com/fwlink/?LinkId=186066)