---
title: typeperf
description: 'Rubrique relative aux commandes Windows pour * * * *- '
ms.custom: na
ms.prod: windows-server-threshold
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 0c7ca89a-03b3-4626-afcf-ef8565e90043
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: cfcbac82b88c0c8d8bcc706ebfd807f96e359de7
ms.sourcegitcommit: af80963a1d16c0b836da31efd9c5caaaf6708133
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/31/2019
ms.locfileid: "66440778"
---
# <a name="typeperf"></a>typeperf



La commande **typeperf** écrit des données de performances dans la fenêtre commande ou dans un fichier journal. Pour arrêter **typeperf**, appuyez sur Ctrl + C.

Pour obtenir des exemples d’utilisation d' **typeperf**, consultez [exemples](#BKMK_EXAMPLES).

## <a name="syntax"></a>Syntaxe

```
typeperf <counter [counter ...]> [options]
typeperf -cf <filename> [options]
typeperf -q [object] [options]
typeperf -qx [object] [options]
```

## <a name="parameters"></a>Paramètres

|Paramètre|Description|
|---------|-----------|
|\<compteur [compteur [...]] >|Spécifie les compteurs de performance à surveiller.|

> [!NOTE]
> le > de compteur est le nom complet d’un compteur de performance au  *\\ \\format Computer\Object (instance) \Counter* , par exemple  **\<**  **\\ \\Server1\Processor (0)\%Heure**de l’utilisateur.

## <a name="options"></a>Options

|                   Option                   |                                                         Description                                                          |
|--------------------------------------------|------------------------------------------------------------------------------------------------------------------------------|
|                     -?                     |                                               Affiche l’aide contextuelle.                                               |
| -f \<&verbar;CSVbin&verbar;SQL> CSV&verbar; |                                    Spécifie le format du fichier de sortie. La valeur par défaut est CSV.                                     |
|              -CF \<nom du fichier >               |              Spécifie un fichier contenant une liste de compteurs de performances à surveiller, avec un compteur par ligne.               |
|             -Si < [[hh:] mm:] SS >             |                                  Spécifie l’intervalle d’échantillonnage. La valeur par défaut est d’une seconde.                                   |
|               -o \<filename >               |     Spécifie le chemin d’accès pour le fichier de sortie ou la base de données SQL. La valeur par défaut est STDOUT (écrit dans la fenêtre commande).      |
|                -q [objet]                 | Affiche la liste des compteurs installés (aucune instance). Pour répertorier les compteurs d’un objet, incluez le nom de l’objet. \*\*\*TELS |
|                -QX [objet]                |        Affiche la liste des compteurs installés avec des instances de. Pour répertorier les compteurs d’un objet, incluez le nom de l’objet.        |
|               -SC \<Samples >               |             Spécifie le nombre d’échantillons à collecter. La valeur par défaut consiste à collecter les données jusqu’à ce que CTRL + C soit enfoncé.              |
|            -nom \<de fichier de configuration >             |                                    Spécifie un fichier de paramètres contenant les options de commande.                                     |
|            -s \<nom_ordinateur >             |                   Spécifie un ordinateur distant à surveiller si aucun ordinateur n’est spécifié dans le chemin d’accès au compteur.                    |
|                     -y                     |                                        Répondez oui à toutes les questions sans demander confirmation.                                        |

## <a name="BKMK_EXAMPLES"></a>Illustre

- L’exemple suivant écrit les valeurs du temps processeur du processeur de compteur  **\\ \\de performance (_\% total)** de l’ordinateur local dans la fenêtre de commande à un intervalle d’échantillonnage par défaut de 1 seconde jusqu’à ce que CTRL + C soit enfoncé. .  
  ```
  typeperf "\Processor(_Total)\% Processor Time"
  ```  
- L’exemple suivant écrit les valeurs de la liste des compteurs dans le fichier **Counters. txt** dans le fichier délimité par des tabulations **domaine2. TSV** à un intervalle d’échantillonnage de 5 secondes jusqu’à ce que les exemples 50 aient été collectés.  
  ```
  typeperf -cf counters.txt -si 5 -sc 50 -f TSV -o domain2.tsv
  ```  
- L’exemple suivant interroge les compteurs installés avec des instances de l’objet de compteur **PhysicalDisk** et écrit la liste résultante dans le fichier **Counters. txt**.  
  ```
  typeperf -qx PhysicalDisk -o counters.txt
  ```
