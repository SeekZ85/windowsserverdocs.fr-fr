---
title: Activation de Windows Server 2019
description: Comment activer Windows Server 2019
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: server-general
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 99f7daa4-30ce-4d13-be65-0a4d55cca754
author: coreyp-at-msft
ms.author: coreyp
manager: jasgroce
ms.localizationpriority: medium
ms.openlocfilehash: 4cc669fee4fbd31edc8813f16761ecb9f90532df
ms.sourcegitcommit: 6ef4986391607bb28593852d06cc6645e548a4b3
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 06/07/2019
ms.locfileid: "66810919"
---
# <a name="windows-server-2019-activation"></a>Activation de Windows Server 2019

>S'applique à : Windows Server 2019, Windows Server 2016

Les informations suivantes soulignent les considérations de planification initiales que vous devez passer en revue pour l’activation des Services de gestion de clés (KMS) impliquant Windows Server 2019. Pour plus d’informations sur l’activation de KMS impliquant des systèmes d’exploitation plus anciens que ceux répertoriés ici, consultez [étape 1 : Passez en revue et sélectionner les méthodes d’Activation](https://technet.microsoft.com/library/jj134256(WS.11).aspx).

Le service KMS utilise un modèle client-serveur pour les clients actifs. Les clients KMS se connectent à un serveur KMS, nommé hôte KMS, pour l’activation. L’hôte KMS doit résider sur votre réseau local.

Les hôtes KMS n’ont pas besoin d’être des serveurs dédiés et le service KMS peut être co-hébergé avec d’autres services. Vous pouvez exécuter un hôte KMS sur n’importe quel système physique ou virtuel exécutant Windows 10, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows 8.1 ou Windows Server 2012.

Un hôte KMS qui s’exécute sur Windows 10 or Windows 8.1 peut uniquement activer des ordinateurs qui exécutent des systèmes d’exploitation clients.
Le tableau suivant récapitule les conditions d’hôte et le client KMS pour les réseaux qui incluent des clients Windows Server 2016, Windows Server 2019 et Windows 10.

> [!NOTE]
> - Des mises à jour peuvent être requises sur le serveur KMS pour prendre en charge l’activation d’un de ces clients plus récents. Si vous recevez des erreurs d’activation, vérifiez que vous disposez des mises à jour appropriées répertoriées dans le tableau ci-dessous.
> - Si vous travaillez avec des machines virtuelles, consultez [Automatic Virtual Machine Activation](vm-activation-19.md) pour plus d’informations et les clés AVMA.

|Groupe de clés de produit|Hébergement de KMS sur|Éditions de Windows activées par cet hôte KMS|  
|-----------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------|  
|Licence en volume pour Windows Server 2019|Windows Server 2012 R2<br /><br />Windows Server 2016<br /><br />Windows Server 2019<br /><br />|Canal semi-annuel Windows Server<br /><br />Windows Server 2019 (toutes éditions)<br /><br />Windows Server 2016 (toutes éditions)<br /><br />Windows 10 entreprise LTSC 2019 <br /><br />Windows 10 entreprise N LTSC 2019<br /><br />Windows 10 LTSB (2015 et 2016)<br /><br />Windows 10 Professionnel<br /><br />Windows 10 Entreprise<br /><br />Windows 10 Professionnel pour les stations de travail<br /><br />Windows 10 Éducation<br /><br />Windows Server 2012 R2 (toutes éditions)<br /><br />Windows 8.1 Professionnel<br /><br />Windows 8.1 Entreprise<br /><br />Windows Server 2012 (toutes éditions)<br /><br />Windows Server 2008 R2 (toutes éditions)<br /><br />Windows Server 2008 (toutes éditions)<br /><br />Windows 7 Professionnel<br /><br />Windows 7 Entreprise<br />| 
|Licence en volume pour Windows Server 2016|Windows Server 2012<br /><br />Windows Server 2012 R2<br /><br />Windows Server 2016<br /><br />|Canal semi-annuel Windows Server <br><br>Windows Server 2016 (toutes éditions)<br /><br />Windows 10 LTSB (2015 et 2016)<br /><br />Windows 10 Professionnel<br /><br />Windows 10 Entreprise<br /><br />Windows 10 Professionnel pour les stations de travail<br><br>Windows 10 Éducation<br><br>Windows Server 2012 R2 (toutes éditions)<br /><br />Windows 8.1 Professionnel<br /><br />Windows 8.1 Entreprise<br /><br />Windows Server 2012 (toutes éditions)<br /><br />Windows Server 2008 R2 (toutes éditions)<br /><br />Windows Server 2008 (toutes éditions)<br /><br />Windows 7 Professionnel<br /><br />Windows 7 Entreprise<br /><br />| 
|Licence en volume pour Windows 10|Windows 7<br /><br /> Windows 8.1<br /><br /> Windows 10|Windows 10 Professionnel<br /><br /> Windows 10 Professionnel N<br /><br /> Windows 10 Entreprise<br /><br /> Windows 10 Entreprise N<br /><br /> Windows 10 Éducation<br /><br /> Windows 10 Éducation N<br /><br /> Windows 10 entreprise LTSB (2015)<br /><br /> Windows 10 Enterprise LTSB N (2015)<br /><br /> Windows 10 Professionnel pour les stations de travail<br><br>Windows 8.1 Professionnel<br /><br /> Windows 8.1 Entreprise<br /><br /> Windows 7 Professionnel<br /><br /> Windows 7 Entreprise<br /><br />|  
|Licence en volume pour « Windows Server 2012 R2 pour Windows 10 »|Windows Server 2008 R2<br /><br /> Windows Server 2012 Standard<br /><br /> Windows Server 2012 Datacenter<br /><br /> Windows Server 2012 R2 Standard<br /><br />Windows Server2012R2 Datacenter|Windows 10 Professionnel<br /><br /> Windows 10 Entreprise<br /><br />Windows 10 entreprise LTSB (2015)<br><br>Windows 10 Professionnel pour les stations de travail<br><br>Windows 10 Éducation<br><br> Windows Server 2012 R2 (toutes éditions)<br /><br /> Windows 8.1 Professionnel<br /><br /> Windows 8.1 Entreprise<br /><br /> Windows Server 2012 (toutes éditions)<br /><br /> Windows Server 2008 R2 (toutes éditions)<br /><br /> Windows Server 2008 (toutes éditions)<br /><br />Windows 7 Professionnel<br /><br /> Windows 7 Entreprise|

> [!NOTE]  
> En fonction du système d’exploitation que votre serveur KMS exécute et des systèmes d’exploitation que vous souhaitez activer, il se peut que vous deviez installer une ou plusieurs de ces mises à jour :
> - Les installations du service de gestion de clés (KMS) sur Windows 7 ou Windows Server 2008 R2 doivent être mises à jour pour prendre en charge l’activation des clients qui exécutent Windows 10. Pour plus d’informations, consultez [mise à jour qui permet aux hôtes de Windows 7 et Windows Server 2008 R2 KMS d’activer Windows 10](https://support.microsoft.com/help/3079821/update-that-enables-windows-7-and-windows-server-2008-r2-kms-hosts-to-activate-windows-10).  
> - Les installations de KMS sur Windows Server 2012 doivent être mis à jour pour prendre en charge l’activation des clients qui exécutent Windows 10 et Windows Server 2016 ou Windows Server 2019, ou de client plus récent ou de systèmes d’exploitation serveur. Pour plus d’informations, consultez [correctif cumulatif de juillet 2016 pour Windows Server 2012](https://support.microsoft.com/help/3172615/july-2016-update-rollup-for-windows-server-2012). 
> - Les installations de KMS sur Windows 8.1 ou Windows Server 2012 R2 doivent être mis à jour pour prendre en charge l’activation des clients qui exécutent Windows 10 et Windows Server 2016 ou Windows Server 2019, ou de client plus récent ou de systèmes d’exploitation serveur. Pour plus d’informations, consultez [correctif cumulatif de juillet 2016 pour Windows 8.1 et Windows Server 2012 R2](https://support.microsoft.com/help/3172614/july-2016-update-rollup-for-windows-8.1-and-windows-server-2012-r2).  
> - Windows Server 2008 R2 ne peut pas être mis à jour pour prendre en charge l’activation des clients exécutant Windows Server 2016, Windows Server 2019 ou des systèmes d’exploitation plus récents. 

Un hôte KMS individuel peut prendre en charge un nombre illimité de clients KMS. Si vous possédez plus de 50 clients, nous vous recommandons d’utiliser au moins deux hôtes KMS au cas où le premier deviendrait indisponible. La plupart des organisations peuvent fonctionner avec pas plus de deux hôtes KMS pour leur infrastructure complète.

# <a name="addressing-kms-operational-requirements"></a>Prise en charge des conditions opérationnelles KMS
Le service KMS peut activer des ordinateurs physiques et virtuels, mais pour autoriser l’activation basée sur le service KMS, un réseau doit comporter un nombre minimal d’ordinateurs physiques (nommé seuil d’activation). Les clients KMS effectuent l’activation une fois seulement que ce seuil est atteint. Pour vérifier que ce seuil d’activation est atteint, un hôte KMS compte le nombre d’ordinateurs physiques qui demandent une activation sur le réseau.

Les hôtes KMS comptent les connexions plus récentes. Lorsqu'un client ou un serveur contacte l'hôte KMS, ce dernier ajoute l'ID de l'ordinateur à son comptage, puis renvoie cette valeur dans sa réponse. Le client ou le serveur s’active si ce nombre est assez élevé. Les clients s’activent si ce nombre est supérieur ou égal à 25. Les serveurs et les éditions en volume de produits Microsoft Office s’activent si ce nombre est supérieur ou égal à 5. Le service KMS ne compte que les connexions uniques dans les 30 derniers jours et ne stocke que les 50 contacts les plus récents.

Les activations KMS sont valides pendant 180 jours, une période appelée intervalle de validité de l'activation. Les clients KMS doivent renouveler leur activation en se connectant à l’hôte KMS au moins une fois tous les 180 jours pour rester activés. Par défaut, les ordinateurs clients KMS tentent de renouveler leur activation tous les sept jours. Une fois que l’activation d’un client a été renouvelée, l’intervalle de validité de l’activation est réinitialisé.

# <a name="addressing-kms-functional-requirements"></a>Prise en charge des conditions fonctionnelles KMS

L’activation basée sur le service KMS requiert la connectivité TCP/IP. Les clients et les hôtes KMS sont configurés par défaut pour utiliser le système DNS (Domain Name System). Par défaut, les hôtes KMS utilisent la mise à jour dynamique DNS pour publier automatiquement les informations que les clients KMS doivent trouver et s’y connecter. Vous pouvez accepter ces paramètres par défaut ou, si vous avez une configuration requise spéciale de sécurité et de réseau, vous pouvez configurer manuellement les clients et les hôtes KMS.

Une fois que le premier hôte KMS a été activé, la clé KMS utilisée sur le premier hôte peut être utilisée pour activer jusqu’à cinq hôtes KMS supplémentaires sur votre réseau. Une fois qu’un hôte KMS a été activé, les administrateurs peuvent réactiver le même hôte jusqu’à neuf fois avec la même clé.

Si votre organisation a besoin de plus de six hôtes KMS, vous devez demander des activations supplémentaires pour la clé KMS de votre organisation ; par exemple, si vous avez dix emplacements physiques sous un seul contrat de licence en volume et que vous voulez que chaque emplacement possède un hôte KMS local.

> [!NOTE] 
> Pour demander une telle exception, contactez votre centre d’appels d’activation. Pour plus d’informations, consultez [Licence en volume Microsoft](https://go.microsoft.com/fwlink/?LinkID=73076).

Les ordinateurs qui exécutent les éditions de licence en volume de Windows 10, Windows Server 2019, Windows Server 2016, Windows 8.1, Windows Server 2012 R2, Windows Server 2012, Windows 7, Windows Server 2008 R2 sont, par défaut, les clients KMS sans aucune configuration supplémentaire nécessaire.

Si vous convertissez un ordinateur ayant le statut d’hôte KMS, de clé d’activation multiple (MAK) ou d’une version commerciale de Windows en un client KMS, installez la clé de configuration de client KMS applicable. Pour plus d’informations, consultez [KMS Client Setup Keys](../get-started/KMSclientkeys.md). 
 

 
