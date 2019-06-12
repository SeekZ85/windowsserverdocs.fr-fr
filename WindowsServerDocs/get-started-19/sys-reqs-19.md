---
title: Configuration requise pour Windows Server 2019
description: Configuration minimale requise pour le stockage, processeur, réseau, mémoire RAM dans une nouvelle installation de Windows Server 2019.
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: server-general
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4a8b42d7-9fe5-4efe-9ea1-ace2131f860e
author: coreyp-at-msft
ms.author: coreyp
manager: jasgroce
ms.localizationpriority: medium
ms.openlocfilehash: d97ec0efee86165f82bdf99a316d24d9c39ec958
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66810719"
---
# <a name="system-requirements"></a>Configuration système

>S'applique à : Windows Server 2019 

Cette rubrique décrit la configuration minimale requise pour exécuter Windows Server&reg; 2019.

## <a name="review-system-requirements"></a>Passer en revue la configuration système requise  

Configuration système requise estimée Windows Server 2019 sont les suivantes : Si votre ordinateur ne possède pas la configuration minimale requise, vous ne pourrez pas installer ce produit correctement. La configuration requise réelle varie en fonction de la configuration de votre système et des applications et fonctionnalités que vous installez.

Sauf indication contraire, cette configuration minimale requise s’applique à toutes les options d’installation (installation minimale, Serveur avec Expérience utilisateur et Nano Server) et aux éditions Standard et Datacenter.  

> [!IMPORTANT]  
> Il serait irréaliste d’indiquer une configuration système requise « recommandée » susceptible d’être généralement applicable étant donné le nombre important des divers déploiements possibles. Consultez la documentation relative à chaque rôle de serveur que vous comptez déployer pour obtenir davantage de détails sur les besoins en ressource des rôles de serveur particuliers. Pour obtenir les meilleurs résultats, procédez à des déploiements tests afin de déterminer la configuration requise appropriée pour vos propres scénarios de déploiement.  

## <a name="processor"></a>Processeur  

Les performances du processeur dépendent non seulement de la fréquence d’horloge du processeur, mais également du nombre de cœurs de processeur et de la taille du cache de processeur. La configuration requise en matière de processeur pour ce produit est la suivante :  

**Minimum** :  
- Processeur 1,4 GHz 64 bits  
- Compatible avec le jeu d’instructions x64  
- Prend en charge NX et DEP  
- Prend en charge CMPXCHG16b, LAHF/SAHF et PrefetchW  
- Prend en charge la traduction d’adresse de second niveau (EPT ou NPT)  

[Coreinfo](https://technet.microsoft.com/sysinternals/cc835722.aspx) est un outil que vous pouvez utiliser pour les capacités votre processeur a de confirmer.

## <a name="ram"></a>RAM  
La configuration requise en matière de mémoire vive (RAM) pour ce produit est la suivante :  

**Minimum** :  
- 512 Mo (2 Go pour l’option d’installation Serveur avec Expérience utilisateur)
- Type d’ECC (Error Correcting Code) ou une technologie similaire pour les déploiements de l’hôte physique

> [!IMPORTANT]  
> Si vous créez un ordinateur virtuel avec les paramètres matériel minimum pris en charge (1 processeur et 512 Mo de RAM), puis essayez d’installer cette version sur l’ordinateur virtuel, le programme d’installation échouera.  
>   
> Pour éviter ceci, effectuez l’une des opérations suivantes :  
>   
> -   Allouez plus de 800 Mo de RAM à l’ordinateur virtuel sur lequel vous voulez installer cette version. Une fois le programme d’installation terminé, vous pouvez réduire l’allocation à 512 Mo de RAM, en fonction de la configuration du serveur.  
> -   Interrompez le processus de démarrage de cette version sur l’ordinateur virtuel en appuyant sur Maj+F10. Dans l’invite de commandes qui s’ouvre, utilisez Diskpart.exe pour créer et formater une partition d’installation. Exécutez **Wpeutil createpagefile /path=C:\pf.sys** (C: étant la partition d’installation créée). Fermez l’invite de commandes et poursuivez le programme d’installation.  

## <a name="storage-controller-and-disk-space-requirements"></a>Contrôleur de stockage et espace disque requis  
Les ordinateurs qui exécutent Windows Server 2019 doivent inclure une carte de stockage qui est conforme à la spécification de l’architecture PCI Express. Les dispositifs de stockage persistant sur les serveurs classés en tant que lecteurs de disque dur ne doivent pas être PATA. Windows Server 2019 n’autorise pas ATA/PATA/IDE/EIDE pour les lecteurs de données, de démarrage ou de page.  

L’espace disque requis **minimal** approximatif pour la partition système est le suivant.  

**Minimum** : 32 Go  

> [!NOTE]
> Gardez à l’esprit que 32 Go doivent être considérés comme une valeur *minimale absolue* pour une installation réussie. Cette valeur minimale doit vous permettre d’installer Windows Server 2019 en mode Server Core, avec le rôle de serveur Web Services (IIS). Un serveur en mode d’installation minimale nécessite environ 4 Go d’espace disque de moins que le même serveur en mode Serveur avec une interface graphique utilisateur. 
> 
> La partition système aura besoin d’espace supplémentaire dans chacun des cas suivants :  
> 
> -   Si vous installez le système sur un réseau.  
> -   Les ordinateurs disposant de plus de 16 Go de RAM peuvent avoir besoin d’un espace disque supplémentaire pour les fichiers de pagination, de mise en veille prolongée et d’image mémoire.  

## <a name="network-adapter-requirements"></a>Conditions requises pour les cartes réseau  

Les cartes réseau utilisées avec cette version doivent inclure les fonctionnalités suivantes :  

**Minimum** :  
- Carte réseau Ethernet capable d’au moins un débit en gigabits  
- Conforme à la spécification de l’architecture PCI Express.  

Une carte réseau qui prend en charge le débogage réseau (KDNet) est utile, mais ne constitue pas une condition minimale requise.   

Une carte réseau que prend en charge l’environnement d’exécution de prédémarrage (PXE) est utile, mais pas une configuration minimale requise.

## <a name="other-requirements"></a>Autres conditions requises pour la configuration  
Les ordinateurs exécutant cette version doivent également disposer des éléments suivants :  

-   Lecteur de DVD (si vous comptez installer le système d’exploitation à partir d’un DVD)  

Les éléments suivants ne sont pas strictement obligatoires, mais sont nécessaires pour certaines fonctionnalités :  

- Microprogramme et système UEFI 2.3.1c prenant en charge le démarrage sécurisé  
- Module de plateforme sécurisée  

-   Périphérique graphique et moniteur capable d’une résolution Super VGA (1024 x 768) ou supérieure  

-   Clavier et souris Microsoft&reg; (ou tout autre dispositif de pointage compatible)  

-   Accès Internet (frais possibles)  

> [!NOTE]  
> Une puce de module de plateforme sécurisée n’est pas strictement nécessaire pour installer cette version, même si elle est requise pour pouvoir utiliser certaines fonctionnalités telles que le chiffrement de lecteur BitLocker. Si votre ordinateur utilise le module de plateforme sécurisée, il doit répondre à ces exigences :  
>  
> - Les modules de plateforme sécurisée matériels doivent implémenter la version 2.0 de la spécification de module de plateforme sécurisée.  
> - Les modules de plateforme sécurisée qui implémentent la version 2.0 doivent avoir un certificat EK préconfiguré pour le module de plateforme sécurisée par le fournisseur de matériel ou capable d’être récupéré par l’appareil pendant le premier démarrage.  
> - Les modules de plateforme sécurisée qui implémentent la version 2.0 doivent être livrés avec des banques de registre de configuration de plateforme (PCR) SHA-256 et implémenter les PCR 0 à 23 pour SHA-256. Il est acceptable de livrer des modules de plateforme sécurisée avec une seule banque PCR commutable qui peut être utilisée pour les deux mesures SHA-1 et SHA-256.  
> - Une option UEFI pour désactiver le module de plateforme sécurisée n’est pas obligatoire.  
