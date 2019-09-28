---
ms.assetid: 693ab895-9d0c-47c1-9f52-df5cd287842a
title: Fsutil objectid
ms.prod: windows-server
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: 509e58b85842826b71cb1bfed72ae4c7e5337e25
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71376835"
---
# <a name="fsutil-objectid"></a>Fsutil objectid
>S'applique à : Windows Server (canal semi-annuel), Windows Server 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8, Windows Server 2008 R2, Windows 7

Gère les identificateurs d’objets (OID), qui sont des objets internes utilisés par le service client de suivi de lien distribué (DLT) et le service de réplication de fichiers (FRS) pour effectuer le suivi d’autres objets, tels que des fichiers, des répertoires et des liens. Les identificateurs d’objet sont invisibles pour la plupart des programmes et ne doivent jamais être modifiés.

> [!CAUTION]
> Ne supprimez pas, ne définissez pas ou ne modifiez pas un identificateur d’objet. La suppression ou la définition d’un identificateur d’objet peut entraîner la perte de données provenant de portions d’un fichier, jusqu’à et y compris des volumes entiers de données. En outre, vous risquez de provoquer un comportement négatif dans le service client de suivi des liaisons distribuées (DLT) et le service de réplication de fichiers (FRS).

Pour obtenir des exemples d’utilisation de cette commande, consultez [Exemples](#BKMK_examples).

## <a name="syntax"></a>Syntaxe

```
fsutil objectid [create] <FileName>
fsutil objectid [delete] <FileName>
fsutil objectid [query] <FileName>
fsutil objectid [set] <ObjectID> <BirthVolumeID> <BirthObjectID> <DomainID> <FileName>
```

## <a name="parameters"></a>Paramètres

|Paramètre|Description|
|-------------|---------------|
|créer|Crée un identificateur d’objet si le fichier spécifié n’en a pas déjà un. Si le fichier a déjà un identificateur d’objet, cette sous-commande est équivalente à la sous-commande de **requête** .|
|supprimer|Supprime un identificateur d’objet.|
|requête|Interroge un identificateur d’objet.|
|jeu|Définit un identificateur d’objet.|
|@no__t 0ObjectID >|Définit un identificateur hexadécimal à 16 octets propre au fichier qui est garanti comme étant unique au sein d’un volume. L’identificateur d’objet est utilisé par le service client de suivi de lien distribué (DLT) et le service de réplication de fichiers (FRS) pour identifier les fichiers.|
|@no__t 0BirthVolumeID >|Indique le volume sur lequel le fichier a été trouvé lors de la première obtention d’un identificateur d’objet. Cette valeur est un identificateur hexadécimal de 16 octets qui est utilisé par le service client DLT.|
|@no__t 0BirthObjectID >|Indique l’identificateur d’objet d’origine du fichier (l' *ObjectID* peut changer quand un fichier est déplacé). Cette valeur est un identificateur hexadécimal de 16 octets qui est utilisé par le service client DLT.|
|@no__t 0DomainID >|identificateur de domaine hexadécimal de 16 octets. Cette valeur n’est pas utilisée actuellement et doit être définie sur tous les zéros.|
|\<Nom de fichier >|Spécifie le chemin d’accès complet au fichier, y compris le nom de fichier et l’extension, par exemple C:\documents\filename.txt.|

## <a name="remarks"></a>Notes

-   Tout fichier qui a un identificateur d’objet a également un identificateur de volume de naissance, un identificateur d’objet de naissance et un identificateur de domaine. Lorsque vous déplacez un fichier, l’identificateur d’objet peut changer, mais les identificateurs d’objet volume de naissance et anniversaire restent les mêmes. Ce comportement permet au système d’exploitation Windows de toujours trouver un fichier, quel que soit l’endroit où il a été déplacé.

## <a name="BKMK_examples"></a>Illustre
Pour créer un identificateur d’objet, tapez :

`fsutil objectid create c:\temp\sample.txt`

Pour supprimer un identificateur d’objet, tapez :

`fsutil objectid delete c:\temp\sample.txt`

Pour interroger un identificateur d’objet, tapez :

`fsutil objectid query c:\temp\sample.txt`

Pour définir un identificateur d’objet, tapez :

`fsutil objectid set 40dff02fc9b4d4118f120090273fa9fc f86ad6865fe8d21183910008c709d19e 40dff02fc9b4d4118f120090273fa9fc 00000000000000000000000000000000 c:\temp\sample.txt`

#### <a name="additional-references"></a>Références supplémentaires
[Clé de syntaxe de ligne de commande](Command-Line-Syntax-Key.md)

[Fsutil](Fsutil.md)


