---
title: "Vue d’ensemble des Services de domaine ActiveDirectory"
description: "Sécurité de Windows Server"
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.service: na
ms.suite: na
ms.technology: security-auditing
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6cfe9479-5d17-41d5-939a-891e5233fdca
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 3d0e849edbff3a481ffd28f83d7f14089030920d
ms.sourcegitcommit: 583355400f6b0d880dc0ac6bc06f0efb50d674f7
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/17/2017
---
# <a name="active-directory-domain-services-overview"></a>Vue d’ensemble des Services de domaine ActiveDirectory

>S’applique à: Windows Server (canal annuel un point-virgule), Windows Server2016
  
Un répertoire est une structure hiérarchique qui stocke des informations sur les objets sur le réseau. Un service d’annuaire, telles que les Services de domaine ActiveDirectory (ADDS), propose les méthodes de stockage des données d’annuaire et rendre ces données disponibles pour les administrateurs et utilisateurs du réseau. Par exemple, les services ADDS stocke des informations sur les comptes d’utilisateur, telles que des noms, les mots de passe, les numéros de téléphone et ainsi de suite et permet aux autres utilisateurs autorisés sur le même réseau accéder à ces informations.  
  
ActiveDirectory stocke des informations sur les objets sur le réseau et rend ces informations aux administrateurs et aux utilisateurs de trouver et utiliser facilement. ActiveDirectory utilise un magasin de données structurées comme base pour une organisation logique et hiérarchique des informations d’annuaire.  
  
Ce magasin de données, également connu sous le répertoire, contient des informations sur les objets ActiveDirectory. Ces objets incluent généralement des ressources partagées telles que des serveurs, des volumes, des imprimantes et les comptes d’utilisateur et l’ordinateur réseau. Pour plus d’informations sur le magasin de données ActiveDirectory, voir [magasin de données active](https://technet.microsoft.com/library/cc736627(v=ws.10).aspx).  
  
La sécurité est intégrée à ActiveDirectory par le biais de l’authentification de connexion et de contrôle d’accès aux objets dans l’annuaire. Avec une ouverture de session réseau unique, les administrateurs peuvent gérer les données d’annuaire et organisation tout au long de leur réseau, et les utilisateurs autorisés peuvent accéder aux ressources n’importe où sur le réseau. Administration basée sur une stratégie facilite la gestion du même réseau plus complexe. Pour plus d’informations sur la sécurité d’ActiveDirectory, voir vue d’ensemble de la sécurité.  
  
ActiveDirectory comprend également:  
* Un ensemble de règles, **le schéma**, qui définit les classes d’objets et attributs contenus dans le répertoire, les contraintes et les limites sur les instances de ces objets et le format de leurs noms. Pour plus d’informations sur le schéma, voir schéma.  
  
  
* Un **catalogue global** qui contient des informations sur chaque objet dans le répertoire. Cela permet aux utilisateurs et administrateurs pour trouver des informations de répertoire quel que soit le domaine dans le répertoire qui contient les données. Pour plus d’informations sur le catalogue global, voir le rôle du catalogue global.  
  
  
* Un **mécanisme de requête et d’index**, de sorte que les objets et leurs propriétés peuvent être publiées et détectées par les utilisateurs du réseau ou d’applications. Pour plus d’informations sur l’interrogation de l’annuaire, consultez Recherche d’informations de répertoire.  
  
  
* Un **service de réplication** qui distribue les données d’annuaire sur un réseau. Tous les contrôleurs de domaine dans un domaine participent à la réplication et contiennent une copie complète de toutes les informations d’annuaire de leur domaine. Toute modification apportée aux données d’annuaire est répliquée sur tous les contrôleurs de domaine dans le domaine. Pour plus d’informations sur la réplication ActiveDirectory, voir vue d’ensemble de la réplication.  
  
## <a name="understanding-active-directory"></a>Présentation d’ActiveDirectory  
 Cette section fournit des liens vers des concepts de base ActiveDirectory:  
   
* [Structure ActiveDirectory et les Technologies de stockage](https://technet.microsoft.com/library/cc759186(v=ws.10).aspx)  
* [Rôles de contrôleurs de domaines](https://technet.microsoft.com/library/cc786438(v=ws.10).aspx)   
* Schéma ActiveDirectory   
* [Présentation des approbations](https://technet.microsoft.com/library/cc771294(v=ws.10).aspx)   
* [Technologies de réplication ActiveDirectory](https://technet.microsoft.com/library/cc786438(v=ws.10).aspx)   
* [Recherche ActiveDirectory et les Technologies de Publication](https://technet.microsoft.com/library/cc775686(v=ws.10).aspx)   
* Il interagit avec DNS et stratégie de groupe   
* [Présentation du schéma](https://technet.microsoft.com/library/cc759402(v=ws.10).aspx)   
  
Pour obtenir une liste détaillée des concepts d’ActiveDirectory, voir [présentation ActiveDirectory](https://technet.microsoft.com/library/cc781408(v=ws.10).aspx).   

