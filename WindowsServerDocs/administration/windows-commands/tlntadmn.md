---
title: tlntadmn
description: 'Rubrique relative aux commandes Windows pour * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 78b61e8d-b953-44bb-8d57-f3b42da9e7a8 vhorne
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 1218a0238f90403edcd04db447ceeac1e10a1fdf
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71385729"
---
# <a name="tlntadmn"></a>tlntadmn

>S’applique à : Windows Server (canal semi-annuel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Administre un ordinateur local ou distant qui exécute le service du serveur Telnet.   
## <a name="syntax"></a>Syntaxe  
```  
tlntadmn [<computerName>] [-u <UserName>] [-p <Password>] [{start | stop | pause | continue}] [-s {<SessionID> | all}] [-k {<SessionID> | all}] [-m {<SessionID> | all}  <Message>] [config [dom = <Domain>] [ctrlakeymap = {yes | no}] [timeout = <hh>:<mm>:<ss>] [timeoutactive = {yes | no}] [maxfail = <attempts>] [maxconn = <Connections>] [port = <Number>] [sec {+ | -}NTLM {+ | -}passwd] [mode = {console | stream}]] [-?]  
```  
### <a name="parameters"></a>Paramètres  

|                   Paramètre                    |                                                                                                                                                       Description                                                                                                                                                        |
|------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                \<computerName >                 |                                                                                                                    Spécifie le nom du serveur auquel se connecter. La valeur par défaut est l'ordinateur local.                                                                                                                    |
|         -u \<nom_utilisateur >-p \<mot de passe >          |                                                Spécifie les informations d’identification d’administration d’un serveur distant que vous voulez administrer. Ce paramètre est obligatoire si vous voulez administrer un serveur distant auquel vous n’êtes pas connecté avec des informations d’identification d’administration.                                                |
|                     start                      |                                                                                                                                            démarre le service du serveur Telnet.                                                                                                                                             |
|                      stop                      |                                                                                                                                             Arrête le service du serveur Telnet                                                                                                                                              |
|                     pause                      |                                                                                                                          suspend le service du serveur Telnet. Aucune nouvelle connexion n’est acceptée.                                                                                                                          |
|                    Pouvoir                    |                                                                                                                                            Reprend le service du serveur Telnet.                                                                                                                                            |
|          -s {\<SessionID > &#124; tout}          |                                                                                                                                             Affiche les sessions Telnet actives.                                                                                                                                             |
|          -k {\<SessionID > &#124; tout}          |                                                                                                        Met fin aux sessions Telnet. tapez l’ID de session pour mettre fin à une session spécifique, ou tapez All pour mettre fin à toutes les sessions.                                                                                                         |
|    -m {\<SessionID > &#124; tout} <Message>     |                                                   Envoie un message à une ou plusieurs sessions. tapez l’ID de session pour envoyer un message à une session spécifique, ou tapez tout pour envoyer un message à toutes les sessions. tapez le message que vous souhaitez envoyer entre guillemets.                                                   |
|             configuration DOM = \<> de domaine             |                                                                                                                                      Configure le domaine par défaut pour le serveur.                                                                                                                                       |
|      configuration ctrlakeymap = {oui &#124; non}      |                                                                                     Spécifie si vous souhaitez que le serveur Telnet interprète CTRL + A comme ALT. tapez **Oui** pour mapper la touche de raccourci ou tapez **non** pour empêcher le mappage.                                                                                     |
|       délai d’expiration de la configuration = \<HH >:\<mm >:\<SS >       |                                                                                                                                 Définit le délai d’attente en heures, minutes et secondes.                                                                                                                                 |
|     config timeoutactive = {oui &#124; non      |                                                                                                                                            Active le délai d’expiration de la session inactive.                                                                                                                                             |
|          configuration maxfail = \<tentatives >          |                                                                                                                          Définit le nombre maximal d’échecs de tentative de connexion avant la déconnexion.                                                                                                                          |
|        configuration maxconn = connexions \<>         |                                                                                                                                         Définit le nombre maximal de connexions.                                                                                                                                          |
|            port de configuration = < \nombre >             |                                                                                                                    Définit le port Telnet. Vous devez spécifier le port avec un entier inférieur à 1024.                                                                                                                    |
| configuration s {+ &#124; -} NTLM {+ &#124; -} passwd | Spécifie si vous souhaitez utiliser NTLM, un mot de passe ou les deux pour authentifier les tentatives de connexion. Pour utiliser un type particulier d’authentification, tapez un signe plus ( **+** ) avant ce type d’authentification. Pour empêcher l’utilisation d’un type particulier d’authentification, tapez un signe moins ( **-** ) avant ce type d’authentification. |
|     mode de configuration = { &#124; flux de console}      |                                                                                                                                             Spécifie le mode de fonctionnement.                                                                                                                                             |
|                       -?                       |                                                                                                                                           Affiche l'aide à l'invite de commandes.                                                                                                                                           |

## <a name="remarks"></a>Notes  
-   Pour afficher les paramètres du serveur, tapez **tlntadmn** sans aucun paramètre.  
-   Pour utiliser la commande **tlntadmn** , vous devez vous connecter à l’ordinateur local avec des informations d’identification d’administration. Pour administrer un ordinateur distant, vous devez également fournir des informations d’identification d’administration pour l’ordinateur distant. Pour ce faire, vous devez ouvrir une session sur l’ordinateur local avec un compte disposant d’informations d’identification d’administration pour l’ordinateur local et l’ordinateur distant. Si vous ne pouvez pas utiliser cette méthode, vous pouvez utiliser les paramètres **-u** et **-p** pour fournir les informations d’identification d’administration de l’ordinateur distant.  

## <a name="BKMK_Examples"></a>Illustre  
Configurez le délai d’expiration de la session inactive sur 30 minutes.  
```  
tlntadmn config timeout=0:30:0  
```  
Affiche les sessions Telnet actives.  
```  
tlntadmn -s  
```  

## <a name="additional-references"></a>Références supplémentaires  
-   [Guide des opérations Telnet](https://technet.microsoft.com/library/cc753164(v=ws.10).aspx)  
-   [Clé de syntaxe de ligne de commande](command-line-syntax-key.md)  
