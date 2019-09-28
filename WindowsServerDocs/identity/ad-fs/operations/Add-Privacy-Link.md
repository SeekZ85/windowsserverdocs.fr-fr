---
ms.assetid: 1ca6f87f-7272-4767-b609-3e295ac7d32f
title: Ajouter le lien de la déclaration de confidentialité
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: cd559e38c38e96d1417257fe7d6ff8ccfa180c6b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71358422"
---
# <a name="add-privacy-link"></a>Ajouter le lien de la déclaration de confidentialité 


Pour ajouter le lien de confidentialité affiché dans la page Sign @ no__t-0in, utilisez l’applet de commande Windows PowerShell et la syntaxe suivantes.  

![Ajouter un lien de confidentialité](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom2.png) 
  
 
`Set-AdfsGlobalWebContent -PrivacyLink https://fs1.contoso.com/privacy/ -PrivacyLinkText Privacy`  
 
  
> [!IMPORTANT]  
> Le paramètre `linkText` de cette applet de commande n'est nécessaire que si vous utilisez une valeur autre que la valeur par défaut (*Privacy*). L'avantage de l'utilisation de la valeur par défaut est que les pages sont localisées d'après tous les paramètres régionaux du client. Une fois la page Sign @ no__t-0in personnalisée, la personnalisation est prioritaire. par conséquent, vous devez personnaliser pour toutes les langues que vous souhaitez prendre en charge. Tout le contenu personnalisé prend un paramètre local. Quand vous configurez un contenu localisé, vous devez d’abord le configurer avec les paramètres régionaux Country @ no__t-0less, par exemple, « en », avant de configurer les paramètres régionaux Country et Region @ no__t-1specific, tels que « fr @ no__t-2us ».  

## <a name="additional-references"></a>Références supplémentaires 
[Personnalisation de la connexion de l’utilisateur AD FS](AD-FS-user-sign-in-customization.md)  
