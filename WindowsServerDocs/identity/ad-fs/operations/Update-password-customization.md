---
ms.assetid: 7e804590-6d6c-4cca-ac14-02d4dff06cec
title: Personnalisation de mot de passe de mise à jour
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: identity-adfs
ms.openlocfilehash: 4b06992bfb398b66988ad4882217a8a83738365e
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59876570"
---
# <a name="update-password-customization"></a>Personnalisation de mot de passe de mise à jour 

>S'applique à : Windows Server 2016, Windows Server 2012 R2

Dans certaines situations, les utilisateurs ne peuvent pas se connecter au réseau d'entreprise pour modifier le mot de passe de leur compte. Cela peut être gênant, notamment pour les employés distants qui habitent loin du bureau de l'entreprise le plus proche. Dans ces cas, l'utilisateur doit se connecter à Internet pour utiliser la page de mise à jour du mot de passe.  
  
Vous pouvez personnaliser la page de mise à jour du mot de passe en fournissant votre propre description pour la page.  
  
> Pour activer la page de mise à jour du mot de passe, accédez à Gestion AD FS sous Points de terminaison. Le point de terminaison pour la mise à jour du mot de passe se trouve en bas, sous Autre - /adfs/portal/updatepassword/. Après avoir activé le point de terminaison, vous devez redémarrer le service AD FS manuellement. Vous pouvez ensuite accéder à l'adresse https://<fqdn>/adfs/portal/updatepassword/ depuis un appareil joint à un espace de travail ; la page de mise à jour du mot de passe doit normalement apparaître.  
  
![mise à jour](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom5.png)  
  
## <a name="customize-the-update-password-page-description"></a>Personnaliser la description de la page de mise à jour du mot de passe  
Pour personnaliser la description mise à jour de la page mot de passe, utilisez l’applet de commande Windows PowerShell suivante et la syntaxe.  
  

    Set-AdfsGlobalWebContent -UpdatePasswordPageDescriptionText "This is the Contoso Update Password page."  

## <a name="additional-references"></a>Références supplémentaires 
[AD FS Sign-in personnalisation de l’utilisateur](AD-FS-user-sign-in-customization.md)  
