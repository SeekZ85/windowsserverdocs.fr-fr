---
ms.assetid: 638c89bd-87e6-484b-9d2e-8ae2a74227e5
title: Définir un certificat de communication du service
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: d0464853c73f88ed76545921ffc8a4bf8551c800
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408320"
---
# <a name="set-a-service-communications-certificate"></a>Définir un certificat de communication du service


Les serveurs de Fédération dans Services ADFS \(AD FS @ no__t-1 utilisent le certificat de communication du service pour sécuriser le trafic des services Web pour la communication protocole SSL \(SSL @ no__t-3 avec les clients Web ou avec le serveur de Fédération proxys.

> [!NOTE]  
> Le certificat de communication du service n’est pas le même qu’un certificat SSL. Pour modifier le certificat SSL AD FS, vous devez utiliser PowerShell. Suivez les instructions de cet [article](https://docs.microsoft.com/windows-server/identity/ad-fs/operations/manage-ssl-certificates-ad-fs-wap).


Vous pouvez utiliser la procédure suivante pour modifier le certificat de communication du service avec le composant logiciel enfichable de gestion de AD FS no__t-0in.  

> [!NOTE]  
> Le composant logiciel enfichable de gestion AD FS @ no__t-0in fait référence aux certificats d’authentification serveur pour les serveurs de Fédération en tant que certificats de communication de service.  

Pour effectuer cette procédure, vous devez au minimum être membre du groupe **Administrateurs**ou d'un groupe équivalent sur l'ordinateur local.  Passez en revue les détails sur l’utilisation des comptes et des appartenances aux groupes appropriés dans les\/ \( [groupes locaux et de domaine par défaut](https://go.microsoft.com/fwlink/?LinkId=83477) http :\/Go.Microsoft.com\/fwlink\/? LinkId\=83477\).   

### <a name="to-set-a-service-communications-certificate"></a>Pour définir un certificat de communication de service  

1.  Dans l’écran d' **Accueil** , tapez**AD FS Management**, puis appuyez sur entrée.  

2.  Dans l’arborescence de la console, double @ no__t-0click **service**, puis cliquez sur **certificats**.  

3.  Dans le volet **actions** , cliquez sur le lien **définir le certificat de communication du service** .  

4.  Dans la boîte de dialogue **Sélectionner un certificat de communication du service** , accédez au fichier de certificat que vous souhaitez définir en tant que certificat de communication du service, sélectionnez le fichier de certificat, puis cliquez sur **ouvrir**.  

## <a name="additional-references"></a>Références supplémentaires  
[Liste de vérification : Configuration d’un serveur de fédération](Checklist--Setting-Up-a-Federation-Server.md)  

[Certificats requis pour les serveurs de fédération](https://technet.microsoft.com/library/dd807040.aspx)  
