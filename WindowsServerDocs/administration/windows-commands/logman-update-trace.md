---
title: Logman update trace
description: 'Rubrique de commandes de Windows pour ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b7111f7f-4162-4d1a-8e53-d766db0ede1f britw
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 30fe475fb6a8442558493dcd5a91ecb8fcee2de3
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59826430"
---
# <a name="logman-update-trace"></a>Logman update trace

>S'applique à : Windows Server (canal semi-annuel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Mettre à jour les propriétés d’un collecteur de données de trace événement existant.  
  
## <a name="syntax"></a>Syntaxe  
```  
logman update trace <[-n] <name>> [options]  
```  
## <a name="parameters"></a>Paramètres  
|Paramètre|Description|  
|-------|--------|  
|/?|Affiche l’aide contextuelle.|  
|-s <computer name>|Exécuter la commande sur l’ordinateur distant spécifié.|  
|-config <value>|Spécifie le fichier de paramètres contenant les options de commande.|  
|-ets|Envoyer des commandes aux Sessions de suivi d’événements directement sans enregistrement ni planification.|  
|[-n] <name>|Nom de l’objet cible.|  
|-f <bin&#124;bincirc&#124;csv&#124;tsv&#124;sql>|Spécifie le format de journal pour le collecteur de données.|  
|-u [-] < utilisateur [password] >|Spécifie l’utilisateur à exécuter en tant que. Entrer un * pour le mot de passe génère une invite pour le mot de passe. Le mot de passe n’est pas affichée lorsque vous le tapez à l’invite de mot de passe.|  
|-m < [start] [stop] [[start] [stop] [...]] >|Remplacez par démarrage manuel ou arrêter au lieu d’une heure de début ou de fin planifiée.|  
|-rf < [[hh :] mm :] ss >|Exécutez le collecteur de données pendant la période de temps spécifiée.|  
|-b <M/d/yyyy h:mm:ss[AM&#124;PM]>|Commencer à collecter les données à l’heure spécifiée.|  
|e - < j/aaaa h : mmss [AM&#124;PM] >|Terminer la collecte des données à l’heure spécifiée.|  
|-o <path&#124;dsn!log>|Spécifie que le fichier journal de sortie ou la source de données et le journal de nom de jeu dans une base de données SQL.|  
|-[-]r|Répétez le collecteur de données tous les jours au début spécifié et les heures de fin.|  
|-[-]a|ajouter à un fichier journal existant.|  
|-[-]ow|Remplacer un fichier journal existant.|  
|-[-]v <nnnnnn&#124;mmddhhmm>|joindre des informations de contrôle de version de fichier à la fin du nom du fichier journal.|  
|-[-] rc <task>|Exécutez la commande spécifiée chaque fois que le journal est fermé.|  
|-[-]max <value>|Taille du fichier journal maximale en Mo ou nombre maximal d’enregistrements des journaux SQL.|  
|-[-] cnf < [[hh :] mm :] ss >|Lors de l’heure est spécifiée, créez un nouveau fichier lorsque le délai imparti est écoulé. Lorsque le temps n’est pas spécifié, créez un nouveau fichier lorsque la taille maximale est dépassée.|  
|-y|Répondez Oui à toutes les questions sans demander confirmation.|  
|-ct < perf&#124;système&#124;cycle >|Spécifie le type d’horloge de Session de Trace d’événements.|  
|-ln < nom >|Spécifie le nom de l’enregistreur d’événements pour les Sessions de suivi d’événements.|  
|ft - < [[hh :] mm :] ss >|Spécifie l’horloge de vidage de Session de Trace d’événements.|  
|-[-] p < fournisseur [flags [level]] >|Spécifie un seul fournisseur de suivi d’événements pour l’activer.|  
|-pf <filename>|Spécifie un fichier listing plusieurs fournisseurs de suivi d’événements pour activer. Le fichier doit être un fichier texte contenant un seul fournisseur par ligne.|  
|-[-]rt|Exécuter la Session de suivi d’événements en mode en temps réel.|  
|-[-] ul|Exécuter la Session de suivi d’événements en mode utilisateur.|  
|-bs <value>|Spécifie la taille de mémoire tampon de Session de Trace d’événements dans la base de connaissances.|  
|-nb <min max>|Spécifie le nombre de mémoires tampons de Session de Trace d’événements.|  
|-mode <globalsequence&#124;localsequence&#124;pagedmemory>|Spécifie le mode d’enregistreur d’événements trace event session.<br /><br />**Globalsequence** Spécifie que le programme de suivi d’événements ajoute un numéro de séquence à chaque événement qu’il reçoit, quel que soit le traçage session a reçu l’événement.<br /><br />**Localsequence** Spécifie que le suivi de l’événement ajouter des numéros de séquence pour les événements envoyés à une session de trace spécifique. Lorsque le **localsequence** option est utilisée, les numéros de séquence en double peuvent exister dans toutes les sessions, mais seront uniques au sein de chaque session de trace.<br /><br />**Pagedmemory** Spécifie que le programme de suivi d’événements utilise la mémoire paginée plutôt que le pool de mémoire non paginée par défaut pour ses allocations de mémoire tampon interne.|  
## <a name="remarks"></a>Notes  
Si [-] est listé, un supplémentaire - inverse l’option.  
## <a name="BKMK_examples"></a>Exemples  
La commande suivante met à jour existant journal_perf collecteur des données, modification de la taille maximale du journal à 10 Mo, mise à jour le format de fichier journal au format CSV et ajout du contrôle de version de fichier dans le format mmddhhmm.  
```  
logman update perf_log -max 10 -f csv -v mmddhhmm  
```  
#### <a name="additional-references"></a>Références supplémentaires  
[logman](logman.md)  
[Logman créer trace](logman-create-trace.md)  