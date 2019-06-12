---
title: Logman mise à jour cfg
description: 'Rubrique de commandes de Windows pour ***- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9da4e8b4-3be5-42d3-b0b4-c429630c35c4 britw
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7ff7cd9d21596b6a40a750374087427cf688cd64
ms.sourcegitcommit: eaf071249b6eb6b1a758b38579a2d87710abfb54
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 05/31/2019
ms.locfileid: "66437623"
---
# <a name="logman-update-cfg"></a>Logman mise à jour cfg

>S'applique à : Windows Server (canal semi-annuel), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Mettre à jour les propriétés d’un collecteur de données de configuration existant.  

## <a name="syntax"></a>Syntaxe  
```  
logman update cfg <[-n] <name>> [options]  
```  
## <a name="parameters"></a>Paramètres  

|                    Paramètre                     |                                                                               Description                                                                               |
|--------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|                        /?                        |                                                                    Affiche l’aide contextuelle.                                                                     |
|                -s <computer name>                |                                                          Exécuter la commande sur l’ordinateur distant spécifié.                                                          |
|                 -config <value>                  |                                                         Spécifie le fichier de paramètres contenant les options de commande.                                                         |
|                   [-n] <name>                    |                                                                       Nom de l’objet cible.                                                                        |
| -f <bin&#124;bincirc&#124;csv&#124;tsv&#124;sql> |                                                            Spécifie le format de journal pour le collecteur de données.                                                             |
|             -u [-] < utilisateur [password] >              | Spécifie l’utilisateur à exécuter en tant que. Entrer un \* pour le mot de passe génère une invite pour le mot de passe. Le mot de passe n’est pas affichée lorsque vous le tapez à l’invite de mot de passe. |
|    -m < [start] [stop] [[start] [stop] [...]] >    |                                                Remplacez par démarrage manuel ou arrêter au lieu d’une heure de début ou de fin planifiée.                                                 |
|                -rf < [[hh :] mm :] ss >                |                                                        Exécutez le collecteur de données pendant la période de temps spécifiée.                                                         |
|        -b <M/d/yyyy h:mm:ss[AM&#124;PM]>         |                                                              Commencer à collecter les données à l’heure spécifiée.                                                               |
|        e - < j/aaaa h : mmss [AM&#124;PM] >         |                                                               Terminer la collecte des données à l’heure spécifiée.                                                                |
|                -si < [[hh :] mm :] ss >                |                                                 Spécifie l’intervalle d’échantillonnage pour les collecteurs de données de compteur de performances.                                                  |
|              -o <path&#124;dsn!log>              |                                              Spécifie que le fichier journal de sortie ou la source de données et le journal de nom de jeu dans une base de données SQL.                                               |
|                      -[-]r                       |                                                  Répétez le collecteur de données tous les jours au début spécifié et les heures de fin.                                                  |
|                      -[-]a                       |                                                                     ajouter à un fichier journal existant.                                                                     |
|                      -[-]ow                      |                                                                     Remplacer un fichier journal existant.                                                                     |
|           -[-]v <nnnnnn&#124;mmddhhmm>           |                                                   joindre des informations de contrôle de version de fichier à la fin du nom du fichier journal.                                                   |
|                  -[-] rc <task>                   |                                                         Exécutez la commande spécifiée chaque fois que le journal est fermé.                                                          |
|                 -[-]max <value>                  |                                                 Taille du fichier journal maximale en Mo ou nombre maximal d’enregistrements des journaux SQL.                                                  |
|              -[-] cnf < [[hh :] mm :] ss >              |     Lors de l’heure est spécifiée, créez un nouveau fichier lorsque le délai imparti est écoulé. Lorsque le temps n’est pas spécifié, créez un nouveau fichier lorsque la taille maximale est dépassée.     |
|                        -y                        |                                                             Répondez Oui à toutes les questions sans demander confirmation.                                                              |
|                      -[-]ni                      |                                                         Activer (-ni) ou désactiver (-ni) requête d’interface réseau.                                                          |
|             reg - < chemin d’accès [[...]] >             |                                                                 Spécifie l’ou les valeurs de Registre à collecter.                                                                 |
|            -mgt < requête [[...]] >            |                                                      Spécifie l’ou les objets WMI à collecter à l’aide du langage de requête SQL.                                                       |
|             -ftc < chemin d’accès [[...]] >             |                                                           Spécifie le chemin complet vers l’ou les fichiers à collecter.                                                            |

## <a name="remarks"></a>Notes  
Si [-] est listé, un supplémentaire - inverse l’option.  
## <a name="BKMK_examples"></a>Exemples  
La commande suivante met à jour le cfg_log de collecteur de données configuration existant pour collecter la clé de Registre HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\Currentverion\\.  
```  
logman update cfg cfg_log -reg "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\Currentverion\"  
```  
#### <a name="additional-references"></a>Références supplémentaires  
[logman](logman.md)  
[Logman créer cfg](logman-create-cfg.md)  
