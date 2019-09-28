---
title: DNS (Domain Name System)
description: Cette rubrique fournit une vue d’ensemble du DNS dans Windows Server 2016
manager: brianlic
ms.prod: windows-server
ms.technology: networking-dns
ms.topic: article
ms.assetid: 1324ba18-4e28-4b9d-bbe7-75707e6d30ab
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 6ad3b66ff0b271c3b6f6134a96aaf6b5171bc7d4
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71406170"
---
# <a name="domain-name-system-dns"></a>DNS (Domain Name System)

>S’applique à : Windows Server (Canal semi-annuel), Windows Server 2016

Le système DNS (Domain Name System) est l’une des gammes de protocoles standard qui composent le protocole TCP/IP, et le client DNS et le serveur DNS fournissent des services de résolution de noms de nom d’ordinateur à adresse IP aux ordinateurs et aux utilisateurs.  
  
> [!NOTE]  
> En plus de cette rubrique, le contenu DNS suivant est disponible.  
>   
> -   [Nouveautés du client DNS](What-s-New-in-DNS-Client.md)  
> -   [Nouveautés du serveur DNS](What-s-New-in-DNS-Server.md)  
> -   [Guide du scénario de stratégie DNS](deploy/DNS-Policy-Scenario-Guide.md)  
> -   Vidéo : @no__t 0Windows Server 2016 : Gestion du service DNS dans IPAM @ no__t-0  
  
Dans Windows Server 2016, DNS est un rôle serveur que vous pouvez installer à l’aide de Gestionnaire de serveur ou de commandes Windows PowerShell. Si vous installez une nouvelle forêt et un nouveau domaine Active Directory, DNS est automatiquement installé avec Active Directory en tant que serveur de catalogue global pour la forêt et le domaine.  
  
Active Directory Domain Services (AD DS) utilise DNS en tant que mécanisme d’emplacement du contrôleur de domaine. Lorsque l’une des opérations de Active Directory principal est effectuée, telles que l’authentification, la mise à jour ou la recherche, les ordinateurs utilisent le DNS pour localiser Active Directory contrôleurs de domaine. En outre, les contrôleurs de domaine utilisent DNS pour les localiser les uns les autres.  
  
Le service client DNS est inclus dans toutes les versions client et serveur du système d’exploitation Windows et s’exécute par défaut lors de l’installation du système d’exploitation. Quand vous configurez une connexion réseau TCP/IP avec l’adresse IP d’un serveur DNS, le client DNS interroge le serveur DNS pour détecter les contrôleurs de domaine et résoudre les noms d’ordinateurs en adresses IP. Par exemple, lorsqu’un utilisateur réseau disposant d’un compte d’utilisateur Active Directory se connecte à un domaine Active Directory, le service client DNS interroge le serveur DNS pour trouver un contrôleur de domaine pour le domaine Active Directory. Lorsque le serveur DNS répond à la requête et fournit l’adresse IP du contrôleur de domaine au client, le client contacte le contrôleur de domaine et le processus d’authentification peut commencer.  
  
Le serveur DNS Windows Server 2016 et les services du client DNS utilisent le protocole DNS inclus dans la suite de protocoles TCP/IP. DNS fait partie de la couche application du modèle de référence TCP/IP, comme indiqué dans l’illustration suivante.  
  
![DNS dans TCP/IP](../media/Domain-Name-System--DNS-/dns_in_tcpip.jpg)  
  

