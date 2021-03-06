---
ms.assetid: 6ecf8d85-cd61-4c87-add8-00a679a6e3ff
title: Ajouter un serveur de fédération à une batterie de serveurs de fédération
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 57c59241c36ba4ed657b83e7c691931f57978a7c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408525"
---
# <a name="add-a-federation-server-to-a-federation-server-farm"></a>Ajouter un serveur de fédération à une batterie de serveurs de fédération


Après avoir installé le service de rôle service FS (Federation Service) et configuré les certificats requis sur un ordinateur, vous êtes prêt à configurer l’ordinateur pour qu’il devienne un serveur de Fédération. Vous pouvez utiliser la procédure suivante pour joindre un ordinateur à une nouvelle batterie de serveurs de fédération.  
  
Vous joignez un ordinateur à une batterie de serveurs à l’aide de l’Assistant Configuration du serveur de fédération AD FS. Lorsque vous utilisez cet Assistant pour joindre un ordinateur à une batterie de serveurs existante, l’ordinateur est configuré avec une copie en lecture\-seule de la base de données de configuration AD FS et il doit recevoir des mises à jour d’un serveur de Fédération principal.  
  
> [!NOTE]  
> Pour le\-de signature de\-unique Web fédéré sur \(conception de\) SSO, vous devez disposer d’au moins un serveur de Fédération dans l’organisation partenaire de compte et au moins un serveur de Fédération dans l’organisation partenaire de ressource. Pour plus d'informations, voir [Où placer un serveur de fédération](https://technet.microsoft.com/library/dd807127.aspx).  
  
Pour effectuer cette procédure, vous devez au minimum être membre du groupe **Administrateurs**ou d'un groupe équivalent sur l'ordinateur local.  Passez en revue les détails sur l’utilisation des comptes et des appartenances aux groupes appropriés dans les [groupes locaux et de domaine par défaut](https://go.microsoft.com/fwlink/?LinkId=83477) \(http :\/\/Go.Microsoft.com\/fwlink\/? LinkId\=83477\).   
  
### <a name="to-add-a-federation-server-to-a-federation-server-farm"></a>Pour ajouter un serveur de Fédération à une batterie de serveurs de Fédération  
  
1.  Il existe deux façons de démarrer l’Assistant Configuration du serveur de fédération AD FS. Pour démarrer l'Assistant, effectuez l'une des opérations suivantes :  
  
    -   Une fois l’installation du service de rôle service FS (Federation Service) terminée, ouvrez le composant logiciel enfichable Gestion des AD FS\-dans et cliquez sur le lien de l' **Assistant Configuration du serveur de fédération AD FS** dans la page **vue d’ensemble** ou dans le volet **actions** .  
  
    -   À chaque fois que l’Assistant installation est terminé, ouvrez l’Explorateur Windows, accédez au dossier **C :\\windows\\ADFS** , puis double\-cliquez sur **FsConfigWizard. exe**.  
  
2.  Sur la page **Bienvenue**, vérifiez que la case **Ajouter un serveur de fédération à un service de fédération** est activée, puis cliquez sur **Suivant**.  
  
3.  Si la base de données de AD FS que vous avez sélectionnée existe déjà, la page **base de données de Configuration AD FS détectée** apparaît. Si tel est le cas, cliquez sur **Supprimer la base de données**, puis cliquez sur **Suivant**.  
  
    > [!CAUTION]  
    > Sélectionnez cette option uniquement lorsque vous êtes sûr que les données de cette AD FS base de données ne sont pas importantes ou qu’elles ne sont pas utilisées dans une batterie de serveurs de Fédération de production.  
  
4.  Dans la page **Spécifiez le serveur de fédération principal et le compte de service**, sous **Nom du serveur de fédération principal**, tapez le nom d’ordinateur du serveur de fédération principal, puis cliquez sur**Parcourir**. Dans la boîte de dialogue **Parcourir**, recherchez le compte de domaine qui sera utilisé comme compte de service par tous les autres serveurs de fédération dans la nouvelle batterie de serveurs de fédération, puis cliquez sur **OK**. Tapez le mot de passe et confirmez-le, puis cliquez sur **suivant**:  
  
    > [!NOTE]  
    > Pour plus d’informations sur la spécification d’un compte de service pour une batterie de serveurs de Fédération, consultez [configurer manuellement un compte de service pour une batterie de serveurs de Fédération](Manually-Configure-a-Service-Account-for-a-Federation-Server-Farm.md). Chaque serveur de Fédération de la batterie de serveurs de Fédération doit spécifier le même compte de service pour que la batterie soit opérationnelle. Par exemple, si le compte de service créé était contoso\\ADFS2SVC, chaque ordinateur que vous configurez pour le rôle de serveur de Fédération et qui participera à la même batterie doit spécifier contoso\\ADFS2SVC à cette étape de l’Assistant Configuration du serveur de Fédération pour que la batterie soit opérationnelle.  
  
5.  Dans la page **Prêt à appliquer les paramètres**, vérifiez les paramètres définis. Si les paramètres semblent corrects, cliquez sur **suivant** pour commencer à configurer AD FS avec ces paramètres.  
  
6.  Dans la page **Résultats de la configuration**, examinez les résultats. Une fois toutes les étapes de configuration terminées, cliquez sur **Fermer** pour quitter l’Assistant.  
  
## <a name="additional-references"></a>Références supplémentaires  
[Liste de vérification : configuration d’un serveur de Fédération](Checklist--Setting-Up-a-Federation-Server.md)  
  

