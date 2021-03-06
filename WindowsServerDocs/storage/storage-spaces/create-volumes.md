---
title: Création de volumes dans les espaces de stockage direct
description: Comment créer des volumes dans espaces de stockage direct à l’aide du centre d’administration Windows et de PowerShell.
ms.prod: windows-server
ms.reviewer: cosmosdarwin
author: cosmosdarwin
ms.author: cosdar
manager: eldenc
ms.technology: storage-spaces
ms.date: 02/25/2020
ms.openlocfilehash: fb53ae74e471d590f83e1017662f33bb5a4b7c1d
ms.sourcegitcommit: 92e0e4224563106adc9a7f1e90f27da468859d90
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 02/26/2020
ms.locfileid: "77608801"
---
# <a name="creating-volumes-in-storage-spaces-direct"></a>Création de volumes dans les espaces de stockage direct

> S’applique à : Windows Server 2019, Windows Server 2016

Cette rubrique explique comment créer des volumes sur un cluster espaces de stockage direct à l’aide du centre d’administration Windows et de PowerShell.

> [!TIP]
> Si vous ne l'avez pas encore fait, consultez d'abord [Planification des volumes dans les espaces de stockage direct](plan-volumes.md).

## <a name="create-a-three-way-mirror-volume"></a>Créer un volume miroir triple

Pour créer un volume miroir triple dans le centre d’administration Windows : 

1. Dans le centre d’administration Windows, connectez-vous à un cluster espaces de stockage direct, puis sélectionnez **volumes** dans le volet **Outils** .
2. Dans la page volumes, sélectionnez l’onglet **inventaire** , puis sélectionnez **créer un volume**.
3. Dans le volet **créer un volume** , entrez un nom pour le volume et laissez la **résilience** en **miroir triple**.
4. Dans **taille sur le disque dur**, spécifiez la taille du volume. Par exemple, 5 to (téraoctets).
5. Sélectionnez **Créer**.

Selon la taille, la création du volume peut prendre quelques minutes. Les notifications en haut à droite vous permettent de savoir quand le volume est créé. Le nouveau volume apparaît dans la liste Inventory.

Regardez une vidéo rapide sur la création d’un volume miroir triple.

> [!VIDEO https://www.youtube-nocookie.com/embed/o66etKq70N8]

## <a name="create-a-mirror-accelerated-parity-volume"></a>Créer un volume de parité à accélération miroir

La parité avec accélération miroir réduit l’encombrement du volume sur le disque dur. Par exemple, un volume miroir triple signifie que pour chaque taille de 10 téraoctets, vous aurez besoin de 30 téraoctets comme empreinte. Pour réduire la surcharge d’encombrement, créez un volume avec une parité à accélération miroir. Cela réduit l’encombrement de 30 téraoctets à seulement 22 téraoctets, même avec seulement 4 serveurs, par la mise en miroir des 20% de données les plus actifs et l’utilisation de la parité, qui est plus efficace pour stocker le reste. Vous pouvez ajuster ce ratio de parité et de miroir pour améliorer les performances par rapport à la capacité pour votre charge de travail. Par exemple, une parité de 90% et une mise en miroir de 10% entraînent moins de performances, mais simplifient encore davantage l’encombrement.

Pour créer un volume avec parité à accélération miroir dans le centre d’administration Windows :

1. Dans le centre d’administration Windows, connectez-vous à un cluster espaces de stockage direct, puis sélectionnez **volumes** dans le volet **Outils** .
2. Dans la page volumes, sélectionnez l’onglet **inventaire** , puis sélectionnez **créer un volume**.
3. Dans le volet **créer un volume** , entrez un nom pour le volume.
4. Dans **résilience**, sélectionnez **parité avec accélération miroir**.
5. Dans **pourcentage de parité**, sélectionnez le pourcentage de parité.
6. Sélectionnez **Créer**.

Regardez une vidéo rapide sur la création d’un volume de parité à accélération miroir.

> [!VIDEO https://www.youtube-nocookie.com/embed/R72QHudqWpE]

## <a name="open-volume-and-add-files"></a>Ouvrir le volume et ajouter des fichiers

Pour ouvrir un volume et ajouter des fichiers au volume dans le centre d’administration Windows :

1. Dans le centre d’administration Windows, connectez-vous à un cluster espaces de stockage direct, puis sélectionnez **volumes** dans le volet **Outils** .
2. Dans la page volumes, sélectionnez l’onglet **inventaire** .
2. Dans la liste des volumes, sélectionnez le nom du volume que vous souhaitez ouvrir.

    Sur la page Détails du volume, vous pouvez voir le chemin d’accès au volume.

4. En haut de la page, sélectionnez **ouvrir**. L’outil fichiers est lancé dans le centre d’administration Windows.
5. Accédez au chemin d’accès du volume. Ici, vous pouvez parcourir les fichiers du volume.
6. Sélectionnez **Télécharger**, puis sélectionnez un fichier à charger.
7. Utilisez le bouton **précédent** du navigateur pour revenir au volet outils du centre d’administration Windows.

Regardez une vidéo rapide sur l’ouverture d’un volume et l’ajout de fichiers.

> [!VIDEO https://www.youtube-nocookie.com/embed/j59z7ulohs4]

## <a name="turn-on-deduplication-and-compression"></a>Activer la déduplication et la compression

La déduplication et la compression sont gérées par volume. La déduplication et la compression utilisent un modèle de publication, ce qui signifie que vous ne verrez aucune économie tant qu’elle n’est pas exécutée. Dans ce cas, il fonctionnera sur tous les fichiers, y compris sur ceux qui étaient déjà présents.

1. Dans le centre d’administration Windows, connectez-vous à un cluster espaces de stockage direct, puis sélectionnez **volumes** dans le volet **Outils** .
2. Dans la page volumes, sélectionnez l’onglet **inventaire** .
3. Dans la liste des volumes, sélectionnez le nom du volume que vous souhaitez gérer.
4. Sur la page Détails du volume, cliquez sur le commutateur **déduplication et compression**.
5. Dans le volet activer la déduplication, sélectionnez le mode de déduplication.

    Au lieu de paramètres complexes, le centre d’administration Windows vous permet de choisir entre des profils prêts à l’emploi pour différentes charges de travail. Si vous n’en êtes pas sûr, utilisez le paramètre par défaut.

6. Sélectionnez **Activer**.

Regardez une vidéo rapide sur la façon d’activer la déduplication et la compression.

> [!VIDEO https://www.youtube-nocookie.com/embed/PRibTacyKko]

## <a name="create-volumes-using-powershell"></a>Créer des volumes à l’aide de PowerShell

Nous vous recommandons d’utiliser l'applet de commande **New-Volume** pour créer des volumes pour les espaces de stockage direct. Il fournit l’expérience la plus rapide et la plus simple. Cet applet de commande unique crée et formate automatiquement le disque virtuel et les partitions, crée le volume avec le nom correspondant et l’ajoute aux volumes partagés de cluster – le tout en une seule étape facile.

L'applet de commande **New-Volume** inclut quatre paramètres que vous devez toujours renseigner :

- **FriendlyName :** une chaîne de votre choix, par exemple *« Volume1 »*
- **FileSystem :** soit **CSVFS_ReFS** (recommandé), soit **CSVFS_NTFS**
- **StoragePoolFriendlyName :** le nom de votre pool de stockage, par exemple *« S2D sur ClusterName »*
- **Size :** la taille du volume, par exemple *« 10 To »*

   > [!NOTE]
   > Windows, y compris PowerShell, calcule à l'aide de nombres binaires (base-2), tandis que les lecteurs sont souvent étiquetés à l’aide de nombres décimaux (base-10). Cela explique pourquoi un lecteur d'une capacité égale à « un téraoctet » (soit 1 000 000 000 000 octets) affiche une capacité d'environ « 909 Go » dans Windows. Ce comportement est normal. Lors de la création de volumes à l’aide de **New-Volume**, vous devez spécifier le paramètre **Size** à l'aide de nombres binaires (base-2). Par exemple, si vous spécifiez « 909 Go » ou « 0,909495 To », le volume créé sera d'environ 1 000 000 000 000 octets.

### <a name="example-with-2-or-3-servers"></a>Exemple : avec 2 ou 3 serveurs

Pour plus de simplicité, si votre déploiement possède uniquement deux serveurs, les espaces de stockage direct utiliseront automatiquement une mise en miroir double pour la résilience. Si votre déploiement possède uniquement trois serveurs, ils utiliseront automatiquement la mise en miroir triple.

```PowerShell
New-Volume -FriendlyName "Volume1" -FileSystem CSVFS_ReFS -StoragePoolFriendlyName S2D* -Size 1TB
```

### <a name="example-with-4-servers"></a>Exemple : avec 4 serveurs ou plus

Si vous possédez quatre serveurs ou plus, vous pouvez utiliser le paramètre facultatif **ResiliencySettingName** pour choisir votre type de résilience.

-   **ResiliencySettingName :** **Miroir** ou **Parité**.

Dans l’exemple suivant, *« Volume2 »* utilise la mise en miroir triple et *« Volume3 »* utilise la double parité (souvent appelée « codage d’effacement »).

```PowerShell
New-Volume -FriendlyName "Volume2" -FileSystem CSVFS_ReFS -StoragePoolFriendlyName S2D* -Size 1TB -ResiliencySettingName Mirror
New-Volume -FriendlyName "Volume3" -FileSystem CSVFS_ReFS -StoragePoolFriendlyName S2D* -Size 1TB -ResiliencySettingName Parity
```

### <a name="example-using-storage-tiers"></a>Exemple : utilisation de niveaux de stockage

Dans les déploiements qui font appel à trois types de lecteurs, un volume peut s’étendre au niveau des disques SSD et du disque dur afin de résider en partie sur chacun d'entre eux. De la même façon, dans les déploiements faisant appel à quatre serveurs ou plus, un volume peut combiner la mise en miroir et la double parité afin de résider en partie sur chacun d'entre eux.

Pour vous aider à créer des volumes de ce type, les espaces de stockage direct fournissent des modèles de niveau par défaut appelés *Performances* et *Capacité*. Ils encapsulent les définitions pour la mise en miroir triple sur les lecteurs à capacité plus rapide (le cas échéant) et pour la double parité sur les lecteurs à capacité plus lente (le cas échéant).

Vous pouvez les afficher en exécutant l'applet de commande **Get-StorageTier**.

```PowerShell
Get-StorageTier | Select FriendlyName, ResiliencySettingName, PhysicalDiskRedundancy
```

![Capture d'écran PowerShell des niveaux de stockage](media/creating-volumes/storage-tiers-screenshot.png)

Pour créer des volumes à plusieurs niveaux de stockage, référencez ces modèles de niveau à l'aide des paramètres **StorageTierFriendlyNames** et **StorageTierSizes** de l'applet de commande **New-Volume**. Par exemple, l’applet de commande suivant crée un volume qui mélange la mise en miroir triple et la double parité dans des proportions 30 : 70.

```PowerShell
New-Volume -FriendlyName "Volume4" -FileSystem CSVFS_ReFS -StoragePoolFriendlyName S2D* -StorageTierFriendlyNames Performance, Capacity -StorageTierSizes 300GB, 700GB
```

C’est terminé ! Si nécessaire, répétez la procédure pour créer plusieurs volumes.

## <a name="see-also"></a>Voir aussi

- [Présentation de espaces de stockage direct](storage-spaces-direct-overview.md)
- [Planification des volumes dans espaces de stockage direct](plan-volumes.md)
- [Extension des volumes dans espaces de stockage direct](resize-volumes.md)
- [Suppression de volumes dans espaces de stockage direct](delete-volumes.md)
