---
title: rpcping
description: 'Rubrique de commandes de Windows pour ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 7382aa0d-90fc-47c0-84b3-15f52dd656d0
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: cfa1d08c81f8b26507a5cae5f688923a7b226e1d
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59829990"
---
# <a name="rpcping"></a>rpcping

>S'applique à : Windows Server (canal semi-annuel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Confirme la connectivité RPC entre l’ordinateur exécutant Microsoft Exchange Server et toutes les stations de travail Microsoft Exchange Client pris en charge sur le réseau. Cet utilitaire peut être utilisé pour vérifier si les services de Microsoft Exchange Server répondent aux demandes RPC à partir de stations de travail clientes via le réseau. 

## <a name="syntax"></a>Syntaxe
```
rpcping [/t <protseq>] [/s <server_addr>] [/e <endpoint>
        |/f <interface UUID>[,Majorver]] [/O <Interface Object UUID]
        [/i <#_iterations>] [/u <security_package_id>] [/a <authn_level>]
        [/N <server_princ_name>] [/I <auth_identity>] [/C <capabilities>]
        [/T <identity_tracking>] [/M <impersonation_type>]
        [/S <server_sid>] [/P <proxy_auth_identity>] [/F <RPCHTTP_flags>]
        [/H <RPC/HTTP_authn_schemes>] [/o <binding_options>]
        [/B <server_certificate_subject>] [/b] [/E] [/q] [/c]
        [/A <http_proxy_auth_identity>] [/U <HTTP_proxy_authn_schemes>]
        [/r <report_results_interval>] [/v <verbose_level>] [/d]
```

### <a name="parameters"></a>Paramètres

|Paramètre|Description|
|-------|--------|
|/t \<protseq>|Spécifie la séquence de protocole à utiliser. Peut prendre l’une des séquences de protocole RPC standards, par exemple : ncacn_ip_tcp, ncacn_np, ou ncacn_http.<br /><br />Si non spécifié, la valeur par défaut est ncacn_ip_tcp.|
|/s \<server_addr>|Spécifie l’adresse du serveur. Si non spécifié, l’ordinateur local sera interrogée.|
|/e \<endpoint>|Spécifie le point de terminaison pour un test ping. Si aucun n’est spécifié, le mappeur de point de terminaison sur l’ordinateur cible sera interrogée.<br /><br />Cette option s’exclut mutuellement avec l’interface (**/f**) option.|
|/o \<binding_options>|Spécifie les options de liaison pour le test ping RPC.|
|/f \<UUID d’interface > [, Majorver]|Spécifie l’interface pour un test ping. Cette option s’exclut mutuellement avec l’option de point de terminaison. L’interface est spécifiée comme un UUID.<br /><br />Si le *Majorver* n’est pas spécifié, la version 1 de l’interface vous est demandée.<br /><br />Lors de l’interface est spécifiée, **rpcping** interrogera le mappeur de point de terminaison sur l’ordinateur cible pour récupérer le point de terminaison pour l’interface spécifiée. Le mappeur de point de terminaison doivent être interrogé à l’aide des options spécifiées dans la ligne de commande.|
|/ O \<UUID d’objet >|Spécifie l’UUID de l’objet si l’interface inscrit un.|
|/i \<#_iterations>|Spécifie le nombre d’appels à rendre. La valeur par défaut est 1. Cette option est utile pour mesurer la latence de connexion si plusieurs itérations sont spécifiées.|
|/u \<security_package_id>|Spécifie le package de sécurité (fournisseur de sécurité) utilisera pour effectuer l’appel RPC. Le package de sécurité est identifié comme un nombre ou un nom. Si un nombre est utilisé. il est le même nombre comme dans l’API RpcBindingSetAuthInfoEx. La liste ci-dessous affiche les noms et numéros. Les noms ne respectent pas la casse :<br /><br />-Par négociation / 9 ou une de nego, snego ou négocier<br />-NTLM / 10 ou NTLM<br />-SChannel / 14 ou SChannel<br />-Kerberos / 16 ou Kerberos<br />-Kernel / 20 ou noyau<br />    Si vous spécifiez cette option, vous devez spécifier le niveau d’authentification autre que none. Il n’existe aucune valeur par défaut pour cette option. S’il n’est pas spécifié, RPC n’utilisera pas la sécurité pour la commande ping.|
|/a \<authn_level>|Spécifie le niveau d’authentification à utiliser. Les valeurs possibles sont :<br /><br />-   connect<br />-appel<br />-   pkt<br />-   integrity<br />-confidentialité<br /><br />Si cette option est spécifiée, la sécurité des ID de package (/ u) doit également être spécifié. Il n’existe aucune valeur par défaut pour cette option.<br /><br />Si cette option n’est pas spécifiée, RPC n’utilisera pas la sécurité pour la commande ping.|
|/N \<server_princ_name>|Spécifie un nom de principal du serveur.<br /><br />Ce champ peut être utilisé uniquement lorsque le package de sécurité d’authentification sont sélectionnés.|
|/I \<auth_identity>|Permet de spécifier une autre identité pour se connecter au serveur. L’identité est l’utilisateur du formulaire, le domaine, le mot de passe. Si le nom d’utilisateur, le domaine ou le mot de passe ont les caractères spéciaux qui peuvent être interprétés par l’interpréteur de commandes, placez l’identité des guillemets doubles. Vous pouvez spécifier **\*** au lieu du mot de passe et le RPC vous invite à entrer le mot de passe sans l’afficher à l’écran. Si ce champ n’est pas spécifié, l’identité de l’utilisateur connecté sera utilisée.<br /><br />Ce champ peut être utilisé uniquement lorsque le package de sécurité d’authentification sont sélectionnés.|
|/C \<capabilities>|Spécifie un masque de bits hexadécimal d’indicateurs. Ce champ peut être utilisé uniquement lorsque le package de sécurité d’authentification sont sélectionnés.|
|/T \<identity_tracking >|Spécifie les statique ou dynamique. Si ce n’est pas spécifié, dynamique est la valeur par défaut.<br /><br />Ce champ peut être utilisé uniquement lorsque le package de sécurité d’authentification sont sélectionnés.|
|/M \<impersonation_type>|Spécifie les connexions anonymes, identifier, emprunter l’identité ou déléguer. Emprunter l’identité de la valeur par défaut.<br /><br />Ce champ peut être utilisé uniquement lorsque le package de sécurité d’authentification sont sélectionnés.|
|/S \<server_sid>|Spécifie le SID attendu du serveur.<br /><br />Ce champ peut être utilisé uniquement lorsque le package de sécurité d’authentification sont sélectionnés.|
|/P \<proxy_auth_identity>|Spécifie l’identité pour s’authentifier avec le proxy RPC/HTTP. A le même format que pour l’option /I. Vous devez spécifier le package de sécurité (/ u), niveau d’authentification (/ a) et les schémas d’authentification (/ H) pour pouvoir utiliser cette option.|
|/F \<RPCHTTP_flags>|Spécifie les indicateurs à passer pour l’authentification de serveur frontal RPC/HTTP. Les indicateurs peuvent être spécifiés en tant que nombres ou des noms, que les indicateurs actuellement reconnus sont :<br /><br />-Utiliser le protocole SSL / 1 ou ssl ou use_ssl<br />-Schéma d’authentification utilisation première / 2 ou premier ou use_first<br /><br />Vous devez spécifier le package de sécurité (/ u) et le niveau d’authentification (/) pour pouvoir utiliser cette option.|
|/H \<RPC/HTTP_authn_schemes>|Spécifie les schémas d’authentification à utiliser pour l’authentification de serveur frontal RPC/HTTP. Cette option est une liste de valeurs numériques ou de noms séparés par des virgules. Exemple : Basic, NTLM. Valeurs reconnues sont (les noms ne sont pas sensible à la casse) :<br /><br />-Base / 1 ou de base<br />-NTLM / 2 ou NTLM<br />-Certificats / 65536 ou certificat<br /><br />Vous devez spécifier le package de sécurité (/ u) et le niveau d’authentification (/) pour pouvoir utiliser cette option.|
|/B \<server_certificate_subject>|Spécifie l’objet du certificat serveur. Vous devez utiliser SSL pour cette option fonctionne.<br /><br />Vous devez spécifier le package de sécurité (/ u) et le niveau d’authentification (/) pour pouvoir utiliser cette option.|
|/b|Récupère l’objet du certificat serveur à partir du certificat envoyé par le serveur et l’imprime sur un écran ou un fichier journal. Valide uniquement lorsque le Proxy echo uniquement option (/ E) et l’utiliser les options SSL sont spécifiées.<br /><br />Vous devez spécifier le package de sécurité (/ u) et le niveau d’authentification (/) pour pouvoir utiliser cette option.|
|/R|Spécifie le serveur proxy HTTP. Si *aucun*, le proxy RPC est utilisé. La valeur *par défaut* signifie que les paramètres d’Internet Explorer dans votre ordinateur client. Toute autre valeur sera traitée en tant que le proxy HTTP explicit. Si vous ne spécifiez pas cet indicateur, la valeur par défaut est supposée, autrement dit, les paramètres d’Internet Explorer sont vérifiées. Cet indicateur est valide uniquement lorsque le **/E** (écho uniquement) l’indicateur est activé.|
|/E|Restreint la commande ping pour le proxy RPC/HTTP uniquement. La commande ping n’atteint pas le serveur. Utile lorsque vous tentez d’établir si le proxy RPC/HTTP est accessible. Pour spécifier un proxy HTTP, utilisez l’indicateur /R. Si un proxy HTTP est spécifié dans l’indicateur/o, cette option va être ignorée.<br /><br />Vous devez spécifier le package de sécurité (/ u) et le niveau d’authentification (/) pour pouvoir utiliser cette option.|
|/q|Spécifie le mode silencieux. Ne délivre pas les invites à l’exception des mots de passe. Suppose que *Y* réponse à toutes les requêtes. Utilisez cette option avec précaution.|
|/c|Utiliser le certificat de carte à puce. RpcPing invitera l’utilisateur de choisir une carte à puce.|
|/A|Spécifie l’identité avec laquelle s’authentifier sur le serveur proxy HTTP. A le même format que pour l’option /I.<br /><br />Vous devez spécifier les schémas d’authentification (/ U), package de sécurité (/ u) et le niveau d’authentification (/) pour pouvoir utiliser cette option.|
|/U|Spécifie les schémas d’authentification à utiliser pour l’authentification du proxy HTTP. Cette option est une liste de valeurs numériques ou de noms séparés par des virgules. Exemple : Basic, NTLM. Valeurs reconnues sont (les noms ne sont pas sensible à la casse) :<br /><br />-Base / 1 ou de base<br />-NTLM / 2 ou NTLM<br /><br />Vous devez spécifier le package de sécurité (/ u) et le niveau d’authentification (/) pour pouvoir utiliser cette option.|
|/r|Si plusieurs itérations sont spécifiées, cette option fera **rpcping** afficher les statistiques d’exécution actuel régulièrement à la place après le dernier appel. L’intervalle de rapport est donné en secondes. Valeur par défaut est 15.|
|/v|Indique à **rpcping** commentaires pour rendre la sortie. Valeur par défaut est 1. 2 et 3 fournissent plus de sortie de **rpcping**.|
|/d|Lancements RPC réseau de l’interface utilisateur de diagnostic.|
|/p|Spécifie pour demander les informations d’identification si l’authentification échoue.|
|/?|Affiche l'aide à l'invite de commandes.|

## <a name="BKMK_Examples"></a>Exemples
Pour savoir si votre serveur Exchange que vous vous connectez via RPC/HTTP est accessible, tapez :
```
rpcping /t ncacn_http /s exchange_server /o RpcProxy=front_end_proxy /P "username,domain,*" /H Basic /u NTLM /a connect /F 3
```

## <a name="additional-references"></a>Références supplémentaires
-   [Clé de la syntaxe de ligne de commande](command-line-syntax-key.md)
