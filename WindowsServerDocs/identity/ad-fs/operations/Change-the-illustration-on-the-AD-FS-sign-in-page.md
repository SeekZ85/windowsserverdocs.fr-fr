---
ms.assetid: a4526500-24b3-423d-805c-24b0d8061aba
title: Modifier l’illustration de la page de connexion AD FS
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 3da7726ca625c32728fb0ae64d291ae599b6cd8d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71358290"
---
# <a name="change-the-illustration-on-the-ad-fs-sign-in-page"></a>Modifier l’illustration de la page de connexion AD FS

## <a name="change-the-illustration"></a>Modifier l’illustration  


Pour modifier l’illustration, le graphique sur la gauche, qui est affiché sur la page Sign\-in, utilisez l’applet de commande Windows PowerShell et la syntaxe suivantes.  

![modifier l’illustration](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom2.png)
  
> [!IMPORTANT]  
> Pour l'illustration, nous recommandons les dimensions 1420 x 1080 pixels, avec une résolution de 96 ppp et une taille de fichier inférieure ou égale à 200 Ko.  
  
 
    Set-AdfsWebTheme -TargetName default -Illustration @{path="c:\Contoso\illustration.png"}  

## <a name="additional-references"></a>Références supplémentaires 
[Personnalisation de la connexion de l’utilisateur AD FS](AD-FS-user-sign-in-customization.md)  
  
  
