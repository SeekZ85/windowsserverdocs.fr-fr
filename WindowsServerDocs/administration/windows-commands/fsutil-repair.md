---
ms.assetid: 62d77150-1d9e-4069-ab4a-299f33024912
title: Fsutil Repair
ms.prod: windows-server
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: 6e4e285bf8401d628f7e4bcbaeafb0c6defa3ad1
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71376911"
---
# <a name="fsutil-repair"></a>Fsutil Repair
>S’applique à : Windows Server (canal semi-annuel), Windows Server 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8, Windows Server 2008 R2, Windows 7

Administre et surveille les opérations de réparation d’auto-réparation NTFS.

Pour obtenir des exemples d’utilisation de cette commande, consultez [Exemples](#BKMK_examples).

## <a name="syntax"></a>Syntaxe

```
fsutil repair [enumerate] <volumepath> [<LogName>]
fsutil repair [initiate] <VolumePath> <FileReference>
fsutil repair [query] <VolumePath>
fsutil repair [set] <VolumePath> <Flags>
fsutil repair [wait][<WaitType>] <VolumePath>

```

## <a name="parameters"></a>Paramètres

|Paramètre|Description|
|-------------|---------------|
|énumérer|Énumère la totalité du journal de corruption d’un volume.|
|\<VolumePath >|Spécifie le volume en tant que nom de lecteur suivi d’un signe deux-points.|
|\<LogName >|$Corrupt : ensemble des endommagements confirmés dans le volume.<br />$Verify : un ensemble d’altérations potentielles non vérifiées dans le volume.|
|exécuter|Lance la réparation automatique NTFS.|
|\<de la méthode FileReference >|Spécifie l’ID de fichier NTFS spécifique au volume (numéro de référence du fichier). La référence de fichier comprend le numéro de segment du fichier.|
|requête|Interroge l’état de réparation automatique du volume NTFS.|
|set|Définit l’état de réparation automatique du volume.|
|Indicateurs de \<>|Spécifie la méthode de réparation à utiliser lors de la définition de l’état de réparation automatique du volume.<br /><br />Le paramètre **Flags** peut être défini sur trois valeurs :<br /><br />-   **0x01**: active la réparation générale.<br />-   **0x09**: avertit les pertes de données potentielles sans réparation.<br />-   **0x00**: désactive les opérations de réparation d’auto-réparation NTFS.|
|Département|Interroge l’état d’altération du système ou pour un volume donné.|
|qu'|Attend la fin de la ou des réparations. Si NTFS a détecté un problème sur un volume sur lequel il effectue des réparations, cette option permet au système d’attendre la fin de la réparation avant d’exécuter les scripts en attente.|
|[WaitType {0&#124;1}]|Indique s’il faut attendre la fin de la réparation en cours ou attendre la fin de toutes les réparations. *WaitType* peut être défini sur les valeurs suivantes :<br /><br />-   **0**: attend la fin de toutes les réparations. (valeur par défaut)<br />-   **1**: attend la fin de la réparation en cours.|

## <a name="remarks"></a>Notes

-   Le système de fichiers NTFS à réparation spontanée tente de corriger les altérations du système de fichiers NTFS en ligne, sans nécessiter l’exécution de **chkdsk. exe** . Cette fonctionnalité a été introduite dans Windows Server 2008. Pour plus d’informations, consultez l' [auto-réparation de NTFS](https://go.microsoft.com/fwlink/?LinkID=165401).

## <a name="BKMK_examples"></a>Illustre

Pour énumérer les endommagements confirmés d’un volume, tapez :

```
fsutil repair enumerate C: $Corrupt 
```

Pour activer la réparation de réparation spontanée sur le lecteur C, tapez :

```
fsutil repair set c: 1
```

Pour désactiver la réparation de réparation spontanée sur le lecteur C, tapez :

```
fsutil repair set c: 0
```

#### <a name="additional-references"></a>Références supplémentaires
[Clé de syntaxe de ligne de commande](Command-Line-Syntax-Key.md)

[Fsutil](Fsutil.md)

[NTFS de réparation automatique](https://go.microsoft.com/fwlink/?LinkID=165401)


