---
ms.assetid: 026747c7-4c34-41c7-b7ea-27f9a7f64a35
title: Ajouter un enregistrement de ressource hôte (A) au DNS d’entreprise d’un serveur de fédération
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 132e71cec134d17dd73be998683c09f752fdc414
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71360330"
---
# <a name="add-a-host-a-resource-record-to-corporate-dns-for-a-federation-server"></a>Ajouter un enregistrement de ressource hôte (A) au DNS d’entreprise d’un serveur de fédération



Pour que les clients du réseau d’entreprise accèdent correctement à un serveur de Fédération à l’aide de l’authentification intégrée Windows, un enregistrement de ressource hôte \(A @ no__t-1 doit d’abord être créé dans le système de noms de domaine d’entreprise \(DNS @ no__t-3 qui résout le nom d’hôte du serveur de Fédération de compte @no__t 4for exemple, FS. fabrikam. com @ no__t-5 à l’adresse IP du serveur de Fédération ou du cluster de serveurs de Fédération. Vous pouvez utiliser la procédure suivante pour ajouter un enregistrement de ressource hôte \(A @ no__t-1 au DNS d’entreprise pour un serveur de Fédération.  
  
Pour mener à bien cette procédure, il faut appartenir au groupe **Administrateurs** ou à un groupe équivalent.  Examinez les informations relatives à l’utilisation des comptes et des appartenances au groupe appropriés dans la rubrique [Groupes locaux et de domaine par défaut](https://go.microsoft.com/fwlink/?LinkId=83477).   
  
### <a name="to-add-a-host-a-resource-record-to-corporate-dns-for-a-federation-server"></a>Pour ajouter un enregistrement de ressource hôte \(A @ no__t-1 au DNS d’entreprise pour un serveur de Fédération  
  
1.  Sur un serveur DNS du réseau d’entreprise, ouvrez le composant logiciel enfichable DNS @ no__t-0in.  
  
2.  Dans l’arborescence de la console, cliquez avec le bouton droit sur @ no__t-0click la zone de recherche directe applicable, puis cliquez sur **nouvel hôte \(A ou AAAA @ no__t-3**.  
  
3.  Dans **nom**, tapez uniquement le nom d’ordinateur du serveur de Fédération ou du cluster de serveurs de Fédération ; par exemple, pour le nom de domaine complet \(FQDN @ no__t-2 fs.fabrikam.com, tapez **FS**.  
  
4.  Dans **adresse IP**, tapez l’adresse IP du serveur de Fédération ou du cluster de serveurs de Fédération, par exemple, 192.168.1.4.  
  
5.  Cliquez sur **Ajouter un hôte**.  
  
## <a name="additional-references"></a>Références supplémentaires  
[Liste de vérification : Configuration d’un serveur de fédération](Checklist--Setting-Up-a-Federation-Server.md)  
  
[Exigences relatives à la résolution de noms pour les serveurs de fédération](https://technet.microsoft.com/library/dd807055.aspx)  
  

