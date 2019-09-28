---
ms.assetid: da035189-e87f-4597-9933-49bf391a8d5d
title: Ajouter le lien de la page d'accueil
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: e5f1fad340629304fdf960139be05b8dbc2690e0
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407775"
---
# <a name="add-home-link"></a>Ajouter le lien de la page d'accueil 

Pour ajouter le lien d’hébergement affiché sur la page Sign @ no__t-0in, utilisez l’applet de commande Windows PowerShell et la syntaxe suivantes. 


![Ajouter un lien d’hébergement](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom2.png) 
  

`Set-AdfsGlobalWebContent -HomeLink https://fs1.contoso.com/home/ -HomeLinkText Home ` 
 
  
> [!IMPORTANT]  
> Le paramètre `linkText` de cette applet de commande n'est nécessaire que si vous utilisez une valeur autre que la valeur par défaut (*Home*). L'avantage de l'utilisation de la valeur par défaut est que les pages sont localisées d'après tous les paramètres régionaux du client. Une fois la page Sign @ no__t-0in personnalisée, la personnalisation est prioritaire. par conséquent, vous devez personnaliser pour toutes les langues que vous souhaitez prendre en charge.

## <a name="additional-references"></a>Références supplémentaires 
[Personnalisation de la connexion de l’utilisateur AD FS](AD-FS-user-sign-in-customization.md)  
