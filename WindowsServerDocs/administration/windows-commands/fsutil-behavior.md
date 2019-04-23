---
title: Comportement de Fsutil
ms.prod: windows-server-threshold
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 10/16/2017
ms.assetid: 84eaba2c-c0af-49e1-bbbd-2ed2928e5e4b
ms.openlocfilehash: 4593739f25c356e72ea39947c67f3e1301573137
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59838270"
---
# <a name="fsutil-behavior"></a>Comportement de Fsutil

>S'applique à : Windows Server (canal semi-annuel), Windows Server 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8, Windows Server 2008 R2, Windows 7

Les requêtes ou définit le comportement de volume NTFS, notamment :

-   La création de noms de fichiers de longueur en caractères 8.3

-   Utilisation de caractères étendus dans les noms de fichiers courts de longueur en caractères au format 8.3 sur les volumes NTFS

-   La mise à jour de l’horodatage de l’heure du dernier accès lorsque les répertoires sont répertoriés sur les volumes NTFS

-   La fréquence avec un quota quels événements sont écrits dans le journal système et au format NTFS réserve paginée pool et les niveaux de cache de mémoire de réserve non paginée NTFS

-   La taille de la zone de table de fichiers principale (MFT Zone)

-   En mode silencieux la suppression de données lorsque le système rencontre une corruption sur un volume NTFS.

-   Notification de suppression de fichier (également appelé trim ou annulez ses mappages)

Pour obtenir des exemples d’utilisation de cette commande, consultez [Exemples](#BKMK_examples).

## <a name="syntax"></a>Syntaxe

```
fsutil behavior query {allowextchar | bugcheckoncorrupt | disable8dot3 [<VolumePath>] | disablecompression | disablecompressionlimit | disableencryption | disablefilemetadataoptimization | disablelastaccess | disablespotcorruptionhandling | disabletxf | disablewriteautotiering | encryptpagingfile | mftzone | memoryusage | quotanotify | symlinkevaluation | disabledeletenotify}

fsutil behavior set {allowextchar {1|0} | bugcheckoncorrupt {1|0} | disable8dot3 [ <Value> | [<VolumePath> {1|0}] ] | disablecompression {1|0} | disablecompressionlimit {1|0} | disableencryption {1|0} | disablefilemetadataoptimization {1|0} | disablelastaccess {1|0} | disablespotcorruptionhandling {1|0} | disabletxf {1|0} | disablewriteautotiering {1|0} | encryptpagingfile {1|0} | mftzone <Value> | memoryusage <Value> | quotanotify <Frequency> | symlinkevaluation <SymbolicLinkType> | disabledeletenotify {1|0}}
```

## <a name="parameters"></a>Paramètres

|Paramètre|Description|
|-------------|---------------|
|requête|Interroge les paramètres de comportement de système de fichiers.|
|jeu|Modifie les paramètres de comportement de système de fichiers.|
|allowextchar {1&#124;0}|Permet de (**1**) ou interdit (**0**) caractères à partir du caractère étendu défini (y compris les caractères diacritiques) à utiliser dans les noms de fichiers courts de longueur en caractères au format 8.3 sur les volumes NTFS.<br /><br />Vous devez redémarrer votre ordinateur pour que ce paramètre prenne effet.|
|Bugcheckoncorrupt {1&#124;0}|Permet de (**1**) ou interdit (**0**) génération d’une vérification de bogue lorsqu’il existe une altération sur un volume NTFS. Cette fonctionnalité peut être utilisée pour empêcher la suppression en mode silencieux des données lorsqu’il est utilisé avec la fonctionnalité de réparation spontanée NTFS NTFS.<br /><br />Vous devez redémarrer votre ordinateur pour que ce paramètre prenne effet.<br /><br />Ce paramètre s’applique à :  Windows Server 2008 R2 et Windows 7.|
|disable8dot3 [<VolumePath>] {1&#124;0}|Désactive (**1**) ou active (**0**) la création d’une longueur de caractère de 8.3 nom sur les volumes FAT et NTFS formatées. Si vous le souhaitez, avec le préfixe le *VolumePath* spécifié comme un nom de lecteur suivi d’un signe deux-points ou d’un GUID.|
|disablecompression {1&#124;0}|Désactive **(1)** ou Active **(0)** la compression NTFS.<br /><br />Vous devez redémarrer votre ordinateur pour que ce paramètre prenne effet.|
|disablecompressionlimit {1&#124;0}| Désactive **(1)** ou Active **(0)** limite de la compression NTFS sur un volume NTFS. Quand un fichier compressé atteint un certain niveau de fragmentation, plutôt que d’échouer étendre le fichier, NTFS arrête la compression des étendues supplémentaires du fichier. Cela a été effectuée pour permettre d’être plus volumineux qu’ils seraient normalement les fichiers compressés. La valeur TRUE désactive cette fonctionnalité qui limite la taille des fichiers compressés sur le système. Nous vous déconseillons de désactiver cette fonctionnalité.<br /><br />Vous devez redémarrer votre ordinateur pour que ce paramètre prenne effet.|
|disableencryption {1&#124;0}|Désactive **(1)** ou Active **(0)** le cryptage des dossiers et fichiers sur les volumes NTFS.<br /><br />Vous devez redémarrer votre ordinateur pour que ce paramètre prenne effet.|
|disablefilemetadataoptimization {1&#124;0}|Désactive **(1)** ou Active **(0)** optimisation des métadonnées de fichiers. NTFS a une limite sur un fichier donné peut avoir des extensions combien. Compressé et les fichiers de pièces de rechange peuvent devenir très fragmentés. Par défaut, NTFS compresse périodiquement ses structures de métadonnées internes pour permettre des fichiers plus fragmentés. La valeur TRUE désactive cette optimisation interne. Nous vous déconseillons de désactiver cette fonctionnalité.<br /><br />Vous devez redémarrer votre ordinateur pour que ce paramètre prenne effet.|
|disablelastaccess {1&#124;0}|Désactive (**1**) ou active (**0**) met à jour à la dernière date et heure d’accès sur chaque répertoire lorsque les répertoires sont répertoriés sur un volume NTFS.<br /><br />Vous devez redémarrer votre ordinateur pour que ce paramètre prenne effet.|
|disablespotcorruptionhandling {1&#124;0}|Désactive **(1)** ou Active **(0)** gestion d’altération directs. Une des nouvelles fonctionnalités introduites dans Windows 8 et Windows Server 2012 est une nouvelle forme de haute disponibilité de CHKDSK. Cette fonctionnalité permet aux administrateurs de système d’exécuter CHKDSK pour analyser l’état d’un volume sans mettre hors connexion. Nous vous déconseillons de désactiver cette fonctionnalité.<br /><br />Vous devez redémarrer votre ordinateur pour que ce paramètre prenne effet.|
|disabletxf {1&#124;0}|Désactive **(1)** ou Active **(0)** txf sur le volume NTFS spécifié. TxF est une fonctionnalité NTFS qui fournit la transaction comme sémantique pour les opérations de système de fichier. TxF est actuellement deprected bien que la fonctionnalité soit toujours disponible. Nous vous déconseillons de désactiver cette fonctionnalité sur le volume C:.<br /><br />Vous devez redémarrer votre ordinateur pour que ce paramètre prenne effet.|
|disablewriteautotiering {1&#124;0}|Désactive la logique hiérarchisation automatique v2 ReFS pour les volumes hiérarchisés.<br /><br />Vous devez redémarrer votre ordinateur pour que ce paramètre prenne effet.|
|encryptpagingfile {1&#124;0}|Chiffre (**1**) ou ne pas chiffrer (**0**) le fichier de pagination de mémoire dans le système d’exploitation Windows.<br /><br />Vous devez redémarrer votre ordinateur pour que ce paramètre prenne effet.|
|mftzone <Value>|Définit la taille de la Zone MFT et est exprimée sous la forme d’un multiple d’unités de 200 Mo. Définissez *valeur* à un nombre compris entre **1** (valeur par défaut est 200 Mo) à **4** (valeur maximale est de 800 Mo).<br /><br />Vous devez redémarrer votre ordinateur pour que ce paramètre prenne effet.|
|memoryusage <Value>|Configure les niveaux de cache interne de-paginée NTFS et de la mémoire de réserve non paginée NTFS. La valeur **1** ou **2**. Lorsque la valeur **1** (la valeur par défaut), NTFS utilise la quantité par défaut de la mémoire de réserve paginée. Lorsque la valeur **2**, NTFS augmente la taille de ses listes en parallèle et les seuils de mémoire. (Une liste en parallèle est un pool de mémoires tampons de taille fixe de mémoire que les noyau et pilotes de périphérique créez lors de la mémoire privée met en cache pour les opérations de système de fichiers, telles que la lecture d’un fichier.)<br /><br />Vous devez redémarrer votre ordinateur pour que ce paramètre prenne effet.|
|quotanotify <Frequency>|Configure la fréquence à laquelle les violations de quota NTFS sont signalées dans le journal système. Les valeurs valides pour sont dans la plage 0-4294967295. La fréquence par défaut est 3 600 secondes (une heure).<br /><br />Vous devez redémarrer votre ordinateur pour que ce paramètre prenne effet.|
|symlinkevaluation <SymbolicLinkType>|Contrôle le type de liens symboliques qui peuvent être créés sur un ordinateur. Les choix valides sont :<br /><br />1.  Local vers les liens symboliques locales, L2L : {0&#124;1}<br />2.  Local vers les liens symboliques à distance, L2R : {0&#124;1}<br />3.  À distance vers les liens symboliques locales, R2R : {0&#124;1}<br />4.  À distance aux liens symboliques à distance, R2L : {0&#124;1}|
|DisableDeleteNotify|Désactive \( **1** \) ou Active \( **0** \) supprimer les notifications. Supprimer la notification \(également appelé trim ou annulez ses mappages\) est l’opération de suppression d’une fonctionnalité qui notifie le dispositif de stockage sous-jacent de clusters qui ont été libérés en raison d’un fichier. En outre :<br /><br />-Pour les systèmes à l’aide des références v2, trim est désactivée par défaut. S’applique à Windows Server 2016.<br />-Pour les systèmes à l’aide des références v1, trim est activé par défaut. S’applique à Windows Server 2012, Windows Server 2012 R2 et Windows Server 2016.<br />-Pour les systèmes à l’aide de NTFS, trim est activée par défaut, sauf si un administrateur désactive.<br />-Si votre lecteur de disque dur ou un SAN signale qu’il ne prend pas en charge trim, votre lecteur de disque dur et les réseaux SAN n’obtiennent pas de notifications de découpage.<br />-Activation ou désactivation ne nécessite pas un redémarrage.<br />-Trim est efficace lorsque annuler le mappage de la prochaine commande est émise.<br />-Des e/s ne sont pas affectées par la modification du Registre en cours d’exécution.<br />-Exige un redémarrage du service lorsque vous activez ou désactivez trim.<br /><br />Ce paramètre a été introduit dans Windows Server 2008 R2 et Windows 7. | 

## <a name="remarks"></a>Notes

-   La Zone MFT est un espace réservé qui permet à la table de fichiers principale (MFT) pour développer en fonction des besoins afin d’éviter la fragmentation de la MFT. Si la taille moyenne des fichiers sur le volume est de 2 Ko ou moins, il peut être avantageux de définir la **mftzone** valeur 2. Si la taille moyenne des fichiers sur le volume est de 1 Ko ou moins, il peut être avantageux de définir la **mftzone** valeur à 4.

-   Lorsque **disable8dot3** a la valeur **0**, chaque fois que vous créez un fichier avec un nom de fichier long, NTFS crée une deuxième entrée de fichier qui a un nom de 8.3 fichier de longueur en caractères. Lorsque NTFS crée des fichiers dans un répertoire, il doit rechercher les noms de fichiers de longueur en caractères 8.3 qui sont associés à des noms de fichier longs. Ce paramètre met à jour le **HKLM\SYSTEM\CurrentControlSet\Control\FileSystem\NtfsDisable8dot3NameCreation** clé de Registre.

-   Le **allowextchar** mises à jour du paramètre le **HKLM\SYSTEM\CurrentControlSet\Control\FileSystem\NtfsAllowExtendedCharacterIn8dot3Name** clé de Registre.

-   Le **disablelastaccess** paramètre réduit l’impact des mises à jour de la journalisation à l’horodatage de l’heure du dernier accès sur les fichiers et répertoires. La désactivation de la **heure du dernier accès** fonctionnalité améliore la vitesse d’accès de fichier et répertoire. Ce paramètre met à jour le **HKLM\SYSTEM\CurrentControlSet\Control\FileSystem\NtfsDisableLastAccessUpdate** clé de Registre.

    Remarques :

    -   Basé sur fichier **heure du dernier accès** requêtes sont exactes, même si toutes les valeurs sur disque ne sont pas en cours. NTFS retourne la valeur correcte sur les requêtes, car la valeur exacte est stockée en mémoire.

    -   Une heure est la quantité maximale de temps NTFS diffère de la mise à jour **heure du dernier accès** sur le disque. Si NTFS met à jour les autres attributs de fichier tel que **heure de dernière modification**et un **heure du dernier accès** mise à jour est en attente, les mises à jour NTFS **heure du dernier accès** avec les autres mises à jour sans impact sur les performances supplémentaires.

    -   Le **disablelastaccess** paramètre peut affecter des programmes tels que la sauvegarde et le stockage étendu qui reposent sur cette fonctionnalité.

-   Augmenter la mémoire physique n’augmente pas toujours la quantité de mémoire de réserve paginée disponible au format NTFS. Paramètre **memoryusage** à **2** augmente la limite de mémoire de réserve paginée. Cela peut améliorer les performances si votre système s’ouvre et ferme de nombreux fichiers dans le même fichier et n'est pas déjà à l’aide de grandes quantités de mémoire système pour d’autres applications ou pour le cache. Si votre ordinateur utilise déjà des grandes quantités de mémoire système pour d’autres applications ou pour le cache, augmenter la limite de NTFS réserve paginée et une mémoire non paginée réduit la mémoire du pool disponible pour d’autres processus. Cela peut réduire les performances globales du système. Ce paramètre met à jour le **HKLM\SYSTEM\CurrentControlSet\Control\FileSystem\NtfsMemoryUsage** clé de Registre.

-   La valeur spécifiée dans le **mftzone** paramètre est une approximation de la taille initiale de la MFT ainsi que la Zone MFT sur un nouveau volume, et elle est définie au moment de montage pour chaque système de fichiers. Comme l’espace sur le volume est utilisé, NTFS ajuste l’espace réservé pour une croissance future MFT. Si la Zone MFT est déjà grande, la taille totale de la Zone MFT n’est pas réservée à nouveau. Étant donné que la Zone MFT est basée sur la plage contiguë après la fin de la MFT, elle diminue à mesure que l’espace est utilisé.

    Le système de fichiers ne détermine pas le nouvel emplacement de la Zone MFT jusqu'à ce que la Zone MFT actuelle est complètement utilisée. Notez que cela ne se produit jamais sur un système classique.

-   Certains appareils peuvent rencontrer une dégradation des performances lorsque la fonctionnalité de notification de suppression est activée. Dans ce cas, utilisez le **disabledeletenotify** option pour désactiver la fonctionnalité de notification.

### <a name="BKMK_examples"></a>Exemples
Pour obtenir le comportement de noms 8dot3 disable pour un volume de disque spécifié avec le GUID, {928842df-5a01-11de-a85c-806e6f6e6963}, tapez :

```
fsutil behavior query disable8dot3 Volume{928842df-5a01-11de-a85c-806e6f6e6963}
```

Vous pouvez également interroger le comportement de noms 8dot3 à l’aide de la **8dot3name** sous-commande.

Pour interroger le système pour voir si la fonction TRIM est activée ou non, tapez :

```
fsutil behavior query DisableDeleteNotify
```
Il en résulte une sortie similaire à ceci :

    NTFS DisableDeleteNotify = 1
    ReFS DisableDeleteNotify is not currently set

Pour substituer le comportement par défaut TRIM \(disabledeletenotify\) pour ReFS v2, tapez :

```
fsutil behavior set DisableDeleteNotify ReFS 0
```

Pour substituer le comportement par défaut TRIM \(disabledeletenotify\) pour v1 NTFS et ReFS, tapez :
```
fsutil behavior set DisableDeleteNotify 1
```

#### <a name="additional-references"></a>Références supplémentaires
[Clé de la syntaxe de ligne de commande](Command-Line-Syntax-Key.md)

[Fsutil](Fsutil.md)

[fsutil 8dot3name](Fsutil-8dot3name.md)


