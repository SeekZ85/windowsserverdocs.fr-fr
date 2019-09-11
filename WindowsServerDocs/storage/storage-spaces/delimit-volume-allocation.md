---
title: Délimiter l’allocation de volumes dans espaces de stockage direct
ms.author: cosmosdarwin
ms.manager: eldenc
ms.technology: storage-spaces
ms.topic: article
author: cosmosdarwin
ms.date: 03/29/2018
ms.openlocfilehash: faf9547833764e9075e86515d1f486a5a3f61ff8
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/10/2019
ms.locfileid: "70872079"
---
# <a name="delimit-the-allocation-of-volumes-in-storage-spaces-direct"></a>Délimiter l’allocation de volumes dans espaces de stockage direct
> S’applique à : Windows Server 2019

Windows Server 2019 introduit une option permettant de délimiter manuellement l’allocation des volumes dans espaces de stockage direct. Cela peut augmenter considérablement la tolérance aux pannes sous certaines conditions, mais impose des considérations et une complexité de gestion supplémentaires. Cette rubrique explique comment elle fonctionne et fournit des exemples dans PowerShell.

   > [!IMPORTANT]
   > Cette fonctionnalité est une nouveauté de Windows Server 2019. Elle n’est pas disponible dans Windows Server 2016. 

## <a name="prerequisites"></a>Prérequis

### <a name="green-checkmark-iconmediadelimit-volume-allocationsupportedpng-consider-using-this-option-if"></a>![Icône de coche verte.](media/delimit-volume-allocation/supported.png) Envisagez d’utiliser cette option si :

- Votre cluster compte six serveurs ou plus ; les
- Votre cluster utilise uniquement [la résilience miroir triple](storage-spaces-fault-tolerance.md#mirroring)

### <a name="red-x-iconmediadelimit-volume-allocationunsupportedpng-do-not-use-this-option-if"></a>![Icône X rouge.](media/delimit-volume-allocation/unsupported.png) N’utilisez pas cette option dans les cas suivants :

- Votre cluster contient moins de six serveurs ; ni
- Votre cluster utilise la [parité](storage-spaces-fault-tolerance.md#parity) ou la résilience [de parité à accélération miroir](storage-spaces-fault-tolerance.md#mirror-accelerated-parity)

## <a name="understand"></a>Comprendre

### <a name="review-regular-allocation"></a>Révision : allocation régulière

Avec la mise en miroir triple régulière, le volume est divisé en plusieurs petits « dalles » qui sont copiés trois fois et répartis uniformément sur chaque lecteur de chaque serveur du cluster. Pour plus d’informations, consultez [ce blog approfondi](https://blogs.technet.microsoft.com/filecab/2016/11/21/deep-dive-pool-in-spaces-direct/).

![Diagramme montrant que le volume est divisé en trois piles de dalles et répartis uniformément sur chaque serveur.](media/delimit-volume-allocation/regular-allocation.png)

Cette allocation optimise les lectures et écritures parallèles, ce qui permet de meilleures performances et est attrayante dans sa simplicité : chaque serveur est également occupé, chaque lecteur est tout aussi plein et tous les volumes restent en ligne ou sont mis hors connexion ensemble. Chaque volume est assuré de survivre à deux échecs simultanés, comme illustré dans [ces exemples](storage-spaces-fault-tolerance.md#examples) .

Toutefois, avec cette allocation, les volumes ne peuvent pas survivre à trois échecs simultanés. Si trois serveurs basculent en même temps, ou si les lecteurs de trois serveurs échouent en même temps, les volumes deviennent inaccessibles car au moins certaines dalles ont été (avec une très grande probabilité) allouées aux trois lecteurs ou serveurs qui ont échoué.

Dans l’exemple ci-dessous, les serveurs 1, 3 et 5 échouent en même temps. Bien que de nombreux dalles soient restées en copie, certaines ne le sont pas :

![Diagramme montrant trois des six serveurs mis en surbrillance en rouge et le volume global est rouge.](media/delimit-volume-allocation/regular-does-not-survive.png)

Le volume est mis hors connexion et devient inaccessible jusqu’à ce que les serveurs soient récupérés.

### <a name="new-delimited-allocation"></a>Nouveau : allocation délimitée

Avec l’allocation délimitée, vous spécifiez un sous-ensemble de serveurs à utiliser (trois au minimum pour un miroir triple). Le volume est divisé en dalles copiées trois fois, comme avant, mais au lieu d’allouer sur chaque serveur, **les tablettes sont allouées uniquement au sous-ensemble de serveurs que vous spécifiez**.

![Diagramme montrant que le volume est divisé en trois piles de tablettes et distribué uniquement à trois des six serveurs.](media/delimit-volume-allocation/delimited-allocation.png)

#### <a name="advantages"></a>Avantages

Avec cette allocation, le volume est susceptible de survivre à trois échecs simultanés : en fait, sa probabilité de survie augmente de 0% (avec une allocation régulière) à 95% (avec allocation délimitée) dans ce cas. Intuitivement, cela est dû au fait qu’il ne dépend pas des serveurs 4, 5 ou 6, de sorte qu’il n’est pas affecté par leurs échecs.

Dans l’exemple ci-dessus, les serveurs 1, 3 et 5 échouent en même temps. Étant donné que l’allocation délimitée a permis de garantir que le serveur 2 contient une copie de chaque dalle, chaque dalle a une copie survivante et le volume reste en ligne et accessible :

![Diagramme montrant trois des six serveurs mis en surbrillance en rouge, alors que le volume global est vert.](media/delimit-volume-allocation/delimited-does-survive.png)

La probabilité de survie dépend du nombre de serveurs et d’autres facteurs. pour plus d’informations, consultez [analyse](#analysis) .

#### <a name="disadvantages"></a>Inconvénients

L’allocation délimitée impose des considérations et une complexité de gestion supplémentaires :

1. Il incombe à l’administrateur de délimiter l’allocation de chaque volume pour équilibrer l’utilisation du stockage entre les serveurs et respecter une forte probabilité de survie, comme décrit dans la section [meilleures pratiques](#best-practices) .

2. Avec une allocation délimitée, réserver l’équivalent d' **un lecteur de capacité par serveur (sans maximum)** . C’est plus que la [recommandation publiée](plan-volumes.md#choosing-the-size-of-volumes) pour l’allocation régulière, qui atteignent à quatre unités de capacité au total.

3. Si un serveur tombe en panne et doit être remplacé, comme décrit dans [supprimer un serveur et ses lecteurs](remove-servers.md#remove-a-server-and-its-drives), l’administrateur est responsable de la mise à jour de la délimitation des volumes affectés en ajoutant le nouveau serveur et en supprimant l’exemple d’échec 1-ci-dessous.

## <a name="usage-in-powershell"></a>Utilisation dans PowerShell

Vous pouvez utiliser l' `New-Volume` applet de commande pour créer des volumes dans espaces de stockage direct.

Par exemple, pour créer un volume miroir triple standard :

```PowerShell
New-Volume -FriendlyName "MyRegularVolume" -Size 100GB
```

### <a name="create-a-volume-and-delimit-its-allocation"></a>Créer un volume et délimiter son allocation

Pour créer un volume miroir triple et délimiter son allocation :

1. Affectez d’abord les serveurs de votre cluster à `$Servers`la variable :

    ```PowerShell
    $Servers = Get-StorageFaultDomain -Type StorageScaleUnit | Sort FriendlyName
    ```

   > [!TIP]
   > Dans espaces de stockage direct, le terme « unité d’échelle de stockage » fait référence à l’ensemble du stockage brut attaché à un serveur, y compris les lecteurs à attachement direct et les boîtiers externes à connexion directe avec les lecteurs. Dans ce contexte, il est identique à « Server ».

2. Spécifiez les serveurs à utiliser avec le `-StorageFaultDomainsToUse` nouveau paramètre et en indexant `$Servers`. Par exemple, pour délimiter l’allocation aux premier, deuxième et troisième serveurs (index 0, 1 et 2) :

    ```PowerShell
    New-Volume -FriendlyName "MyVolume" -Size 100GB -StorageFaultDomainsToUse $Servers[0,1,2]
    ```

### <a name="see-a-delimited-allocation"></a>Afficher une allocation délimitée

Pour voir comment *MyVolume* est alloué, utilisez le `Get-VirtualDiskFootprintBySSU.ps1` script figurant dans l' [annexe](#appendix):

```PowerShell
PS C:\> .\Get-VirtualDiskFootprintBySSU.ps1

VirtualDiskFriendlyName TotalFootprint Server1 Server2 Server3 Server4 Server5 Server6
----------------------- -------------- ------- ------- ------- ------- ------- -------
MyVolume                300 GB         100 GB  100 GB  100 GB  0       0       0      
```

Notez que seuls Server1, Server2 et Server3 contiennent des dalles de *MyVolume*.

### <a name="change-a-delimited-allocation"></a>Modifier une allocation délimitée

Utilisez les applets `Remove-StorageFaultDomain` de commande New `Add-StorageFaultDomain` et pour modifier la façon dont l’allocation est délimitée.

Par exemple, pour déplacer *MyVolume* sur un serveur :

1. Spécifiez que le quatrième serveur **peut** stocker des tablettes de *MyVolume*:

    ```PowerShell
    Get-VirtualDisk MyVolume | Add-StorageFaultDomain -StorageFaultDomains $Servers[3]
    ```

2. Spécifiez que le premier serveur **ne peut pas** stocker de tablettes de *MyVolume*:

    ```PowerShell
    Get-VirtualDisk MyVolume | Remove-StorageFaultDomain -StorageFaultDomains $Servers[0]
    ```

3. Rééquilibrer le pool de stockage pour que la modification prenne effet :

    ```PowerShell
    Get-StoragePool S2D* | Optimize-StoragePool
    ```

![Diagramme montrant les dalles migrer en-massive des serveurs 1, 2 et 3 vers les serveurs 2, 3 et 4.](media/delimit-volume-allocation/move.gif)

Vous pouvez surveiller la progression du rééquilibrage avec `Get-StorageJob`.

Une fois l’opération terminée, vérifiez que *MyVolume* a été déplacé `Get-VirtualDiskFootprintBySSU.ps1` en exécutant à nouveau.

```PowerShell
PS C:\> .\Get-VirtualDiskFootprintBySSU.ps1

VirtualDiskFriendlyName TotalFootprint Server1 Server2 Server3 Server4 Server5 Server6
----------------------- -------------- ------- ------- ------- ------- ------- -------
MyVolume                300 GB         0       100 GB  100 GB  100 GB  0       0      
```

Notez que Server1 ne contient plus de dalles de *MyVolume* , à la place, Server04.

## <a name="best-practices"></a>Bonnes pratiques

Voici les meilleures pratiques à suivre lors de l’utilisation de l’allocation de volume délimitée :

### <a name="choose-three-servers"></a>Choisir trois serveurs

Délimitez chaque volume miroir triple à trois serveurs, et pas plus.

### <a name="balance-storage"></a>Équilibrer le stockage

Équilibrez la quantité de stockage allouée à chaque serveur, en tenant compte de la taille du volume.

### <a name="every-delimited-allocation-unique"></a>Toutes les allocations délimitées uniques

Pour optimiser la tolérance de panne, augmentez l’allocation de chaque volume, ce qui signifie qu’il ne partage pas *tous* ses serveurs avec un autre volume (une partie du chevauchement est acceptée). Avec N serveurs, il existe « N Choose 3 » combinaisons uniques : Voici ce que cela signifie pour certaines tailles de cluster courantes :

| Nombre de serveurs (N) | Nombre d’allocations délimitées uniques (N Choose 3) |
|-----------------------|-----------------------------------------------------|
| 6\.                     | 20                                                  |
| 8                     | 56                                                  |
| 12                    | 220                                                 |
| 16                    | 560                                                 |

   > [!TIP]
   > Envisagez cet examen utile de [combinatorics et choisissez la notation](https://betterexplained.com/articles/easy-permutations-and-combinations/).

Voici un exemple qui optimise la tolérance aux pannes : chaque volume a une allocation unique délimitée :

![allocation unique](media/delimit-volume-allocation/unique-allocation.png)

À l’inverse, dans l’exemple suivant, les trois premiers volumes utilisent la même allocation délimitée (aux serveurs 1, 2 et 3) et les trois derniers volumes utilisent la même allocation délimitée (aux serveurs 4, 5 et 6). Cela n’optimise pas la tolérance de panne : si trois serveurs échouent, plusieurs volumes peuvent passer en mode hors connexion et devenir inaccessibles simultanément.

![allocation non unique](media/delimit-volume-allocation/non-unique-allocation.png)

## <a name="analysis"></a>Analysis

Cette section détaille la probabilité mathématique qu’un volume reste en ligne et accessible (ou, de manière équivalente, la fraction attendue de stockage global qui reste en ligne et accessible) en tant que fonction du nombre d’échecs et de la taille du cluster.

   > [!NOTE]
   > Cette section est une lecture facultative. Si vous êtes en train de voir les maths, lisez ! Mais dans le cas contraire, ne vous inquiétez pas : [L’utilisation de PowerShell](#usage-in-powershell) et des [meilleures pratiques](#best-practices) est tout ce dont vous avez besoin pour implémenter l’allocation délimitée avec succès.

### <a name="up-to-two-failures-is-always-okay"></a>Jusqu’à deux échecs sont toujours corrects

Chaque volume miroir triple peut survivre simultanément à deux défaillances, comme illustré dans [ces exemples](storage-spaces-fault-tolerance.md#examples) , quelle que soit son allocation. Si deux lecteurs échouent, ou si deux serveurs échouent, ou l’un de chacun, chaque volume miroir triple reste en ligne et accessible, même avec une allocation régulière.

### <a name="more-than-half-the-cluster-failing-is-never-okay"></a>Plus de la moitié de l’échec du cluster n’est jamais OK

À l’inverse, dans le cas extrême où plus de la moitié des serveurs ou lecteurs du cluster échouent simultanément, le [quorum est perdu](understand-quorum.md) et chaque volume miroir triple est mis hors connexion et devient inaccessible, quelle que soit son allocation.

### <a name="what-about-in-between"></a>Qu’en est-il de entre ?

Si au moins trois échecs se produisent à la fois, mais qu’au moins la moitié des serveurs et des lecteurs est toujours en service, les volumes avec une allocation délimitée peuvent rester en ligne et accessibles, en fonction des serveurs qui présentent des erreurs. Nous allons exécuter les nombres pour déterminer les chances précises.

Par souci de simplicité, supposons que les volumes sont distribués de manière indépendante et identique (IID) conformément aux meilleures pratiques ci-dessus, et que suffisamment de combinaisons uniques sont disponibles pour que chaque allocation de volume soit unique. La probabilité qu’un volume donné subsiste est également la fraction attendue du stockage global qui survit par la linéarité de l’attente. 

Étant donné que les **N** serveurs dont **F** rencontrent des défaillances, un volume alloué à **3** de ceux-ci sont hors connexion si les **3** sont dans le **f** avec des échecs. Il existe des méthodes **(N Choose f)** pour les échecs **f** , dont **(f Choose 3)** entraînent la mise hors connexion du volume et son inaccessibilité. La probabilité peut être exprimée comme suit :

![P_offline = FC3/NcF](media/delimit-volume-allocation/probability-volume-offline.png)

Dans tous les autres cas, le volume reste en ligne et accessible :

![P_online = 1 – (FC3/NcF)](media/delimit-volume-allocation/probability-volume-online.png)

Les tableaux suivants évaluent la probabilité pour certaines tailles de cluster courantes et jusqu’à 5 échecs, révélant que l’allocation délimitée augmente la tolérance de panne par rapport à l’allocation régulière dans tous les cas considérés.

### <a name="with-6-servers"></a>Avec 6 serveurs

| Allocation                           | Probabilité de survivant 1 défaillance | Probabilité de survie de 2 échecs | Probabilité de survie de 3 échecs | Probabilité de survie de 4 échecs | Probabilité de survie de 5 échecs |
|--------------------------------------|------------------------------------|-------------------------------------|-------------------------------------|-------------------------------------|-------------------------------------|
| Régulier, réparti sur les 6 serveurs | 100%                               | 100%                                | entre                                  | entre                                  | entre                                  |
| Délimité à 3 serveurs uniquement          | 100%                               | 100%                                | 95,0%                               | entre                                  | entre                                  |

   > [!NOTE]
   > Après plus de 3 échecs sur 6 serveurs au total, le cluster perd le quorum.

### <a name="with-8-servers"></a>Avec 8 serveurs

| Allocation                           | Probabilité de survivant 1 défaillance | Probabilité de survie de 2 échecs | Probabilité de survie de 3 échecs | Probabilité de survie de 4 échecs | Probabilité de survie de 5 échecs |
|--------------------------------------|------------------------------------|-------------------------------------|-------------------------------------|-------------------------------------|-------------------------------------|
| Régulier, réparti sur les 8 serveurs | 100%                               | 100%                                | entre                                  | entre                                  | entre                                  |
| Délimité à 3 serveurs uniquement          | 100%                               | 100%                                | 98,2%                               | 94.3%                               | entre                                  |

   > [!NOTE]
   > Après plus de 4 échecs de 8 serveurs au total, le cluster perd le quorum.

### <a name="with-12-servers"></a>Avec 12 serveurs

| Allocation                            | Probabilité de survivant 1 défaillance | Probabilité de survie de 2 échecs | Probabilité de survie de 3 échecs | Probabilité de survie de 4 échecs | Probabilité de survie de 5 échecs |
|---------------------------------------|------------------------------------|-------------------------------------|-------------------------------------|-------------------------------------|-------------------------------------|
| Régulier, réparti sur les 12 serveurs | 100%                               | 100%                                | entre                                  | entre                                  | entre                                  |
| Délimité à 3 serveurs uniquement           | 100%                               | 100%                                | 99,5%                               | 99,2%                               | 98,7%                               |

### <a name="with-16-servers"></a>Avec 16 serveurs

| Allocation                            | Probabilité de survivant 1 défaillance | Probabilité de survie de 2 échecs | Probabilité de survie de 3 échecs | Probabilité de survie de 4 échecs | Probabilité de survie de 5 échecs |
|---------------------------------------|------------------------------------|-------------------------------------|-------------------------------------|-------------------------------------|-------------------------------------|
| Normal, réparti sur les 16 serveurs | 100%                               | 100%                                | entre                                  | entre                                  | entre                                  |
| Délimité à 3 serveurs uniquement           | 100%                               | 100%                                | 99,8%                               | 99,8%                               | 99,8%                               |

## <a name="frequently-asked-questions"></a>Questions fréquentes (FAQ)

### <a name="can-i-delimit-some-volumes-but-not-others"></a>Puis-je délimiter certains volumes, mais pas d’autres ?

Oui. Vous pouvez choisir par volume de délimiter l’allocation.

### <a name="does-delimited-allocation-change-how-drive-replacement-works"></a>L’allocation délimitée change-t-elle le fonctionnement du disque de remplacement ?

Non, il est identique à l’allocation régulière.

## <a name="see-also"></a>Voir aussi

- [Présentation de espaces de stockage direct](storage-spaces-direct-overview.md)
- [Tolérance de panne dans espaces de stockage direct](storage-spaces-fault-tolerance.md)

## <a name="appendix"></a>Annexe

Ce script vous permet de voir comment vos volumes sont alloués.

Pour l’utiliser comme décrit ci-dessus, copiez/collez et enregistrez sous `Get-VirtualDiskFootprintBySSU.ps1`.

```PowerShell
Function ConvertTo-PrettyCapacity {
    Param (
        [Parameter(
            Mandatory = $True,
            ValueFromPipeline = $True
            )
        ]
    [Int64]$Bytes,
    [Int64]$RoundTo = 0
    )
    If ($Bytes -Gt 0) {
        $Base = 1024
        $Labels = ("bytes", "KB", "MB", "GB", "TB", "PB", "EB", "ZB", "YB")
        $Order = [Math]::Floor( [Math]::Log($Bytes, $Base) )
        $Rounded = [Math]::Round($Bytes/( [Math]::Pow($Base, $Order) ), $RoundTo)
        [String]($Rounded) + " " + $Labels[$Order]
    }
    Else {
        "0"
    }
    Return
}

Function Get-VirtualDiskFootprintByStorageFaultDomain {

    ################################################
    ### Step 1: Gather Configuration Information ###
    ################################################

    Write-Progress -Activity "Get-VirtualDiskFootprintByStorageFaultDomain" -CurrentOperation "Gathering configuration information..." -Status "Step 1/4" -PercentComplete 00

    $ErrorCannotGetCluster = "Cannot proceed because 'Get-Cluster' failed."
    $ErrorNotS2DEnabled = "Cannot proceed because the cluster is not running Storage Spaces Direct."
    $ErrorCannotGetClusterNode = "Cannot proceed because 'Get-ClusterNode' failed."
    $ErrorClusterNodeDown = "Cannot proceed because one or more cluster nodes is not Up."
    $ErrorCannotGetStoragePool = "Cannot proceed because 'Get-StoragePool' failed."
    $ErrorPhysicalDiskFaultDomainAwareness = "Cannot proceed because the storage pool is set to 'PhysicalDisk' fault domain awareness. This cmdlet only supports 'StorageScaleUnit', 'StorageChassis', or 'StorageRack' fault domain awareness."

    Try  {
        $GetCluster = Get-Cluster -ErrorAction Stop
    }
    Catch {
        throw $ErrorCannotGetCluster
    }

    If ($GetCluster.S2DEnabled -Ne 1) {
        throw $ErrorNotS2DEnabled
    }

    Try  {
        $GetClusterNode = Get-ClusterNode -ErrorAction Stop
    }
    Catch {
        throw $ErrorCannotGetClusterNode
    }

    If ($GetClusterNode | Where State -Ne Up) {
        throw $ErrorClusterNodeDown
    }

    Try {
        $GetStoragePool = Get-StoragePool -IsPrimordial $False -ErrorAction Stop
    }
    Catch {
        throw $ErrorCannotGetStoragePool
    }

    If ($GetStoragePool.FaultDomainAwarenessDefault -Eq "PhysicalDisk") {
        throw $ErrorPhysicalDiskFaultDomainAwareness
    }

    ###########################################################
    ### Step 2: Create SfdList[] and PhysicalDiskToSfdMap{} ###
    ###########################################################

    Write-Progress -Activity "Get-VirtualDiskFootprintByStorageFaultDomain" -CurrentOperation "Analyzing physical disk information..." -Status "Step 2/4" -PercentComplete 25

    $SfdList = Get-StorageFaultDomain -Type ($GetStoragePool.FaultDomainAwarenessDefault) | Sort FriendlyName # StorageScaleUnit, StorageChassis, or StorageRack

    $PhysicalDiskToSfdMap = @{} # Map of PhysicalDisk.UniqueId -> StorageFaultDomain.FriendlyName
    $SfdList | ForEach {
        $StorageFaultDomain = $_
        $_ | Get-StorageFaultDomain -Type PhysicalDisk | ForEach {
            $PhysicalDiskToSfdMap[$_.UniqueId] = $StorageFaultDomain.FriendlyName
        }
    }

    ##################################################################################################
    ### Step 3: Create VirtualDisk.FriendlyName -> { StorageFaultDomain.FriendlyName -> Size } Map ###
    ##################################################################################################

    Write-Progress -Activity "Get-VirtualDiskFootprintByStorageFaultDomain" -CurrentOperation "Analyzing virtual disk information..." -Status "Step 3/4" -PercentComplete 50

    $GetVirtualDisk = Get-VirtualDisk | Sort FriendlyName

    $VirtualDiskMap = @{}

    $GetVirtualDisk | ForEach {
        # Map of PhysicalDisk.UniqueId -> Size for THIS virtual disk
        $PhysicalDiskToSizeMap = @{}
        $_ | Get-PhysicalExtent | ForEach {
            $PhysicalDiskToSizeMap[$_.PhysicalDiskUniqueId] += $_.Size
        }
        # Map of StorageFaultDomain.FriendlyName -> Size for THIS virtual disk
        $SfdToSizeMap = @{}
        $PhysicalDiskToSizeMap.keys | ForEach {
            $SfdToSizeMap[$PhysicalDiskToSfdMap[$_]] += $PhysicalDiskToSizeMap[$_]
        }
        # Store
        $VirtualDiskMap[$_.FriendlyName] = $SfdToSizeMap
    }

    #########################
    ### Step 4: Write-Out ###
    #########################

    Write-Progress -Activity "Get-VirtualDiskFootprintByStorageFaultDomain" -CurrentOperation "Formatting output..." -Status "Step 4/4" -PercentComplete 75

    $Output = $GetVirtualDisk | ForEach {
        $Row = [PsCustomObject]@{}

        $VirtualDiskFriendlyName = $_.FriendlyName
        $Row | Add-Member -MemberType NoteProperty "VirtualDiskFriendlyName" $VirtualDiskFriendlyName

        $TotalFootprint = $_.FootprintOnPool | ConvertTo-PrettyCapacity
        $Row | Add-Member -MemberType NoteProperty "TotalFootprint" $TotalFootprint

        $SfdList | ForEach {
            $Size = $VirtualDiskMap[$VirtualDiskFriendlyName][$_.FriendlyName] | ConvertTo-PrettyCapacity
            $Row | Add-Member -MemberType NoteProperty $_.FriendlyName $Size
        }

        $Row
    }

    # Calculate width, in characters, required to Format-Table
    $RequiredWindowWidth = ("TotalFootprint").length + 1 + ("VirtualDiskFriendlyName").length + 1
    $SfdList | ForEach {
        $RequiredWindowWidth += $_.FriendlyName.Length + 1
    }

    $ActualWindowWidth = (Get-Host).UI.RawUI.WindowSize.Width

    If (!($ActualWindowWidth)) {
        # Cannot get window width, probably ISE, Format-List
        Write-Warning "Could not determine window width. For the best experience, use a Powershell window instead of ISE"
        $Output | Format-Table
    }
    ElseIf ($ActualWindowWidth -Lt $RequiredWindowWidth) {
        # Narrower window, Format-List
        Write-Warning "For the best experience, try making your PowerShell window at least $RequiredWindowWidth characters wide. Current width is $ActualWindowWidth characters."
        $Output | Format-List
    }
    Else {
        # Wider window, Format-Table
        $Output | Format-Table
    }
}

Get-VirtualDiskFootprintByStorageFaultDomain
```
