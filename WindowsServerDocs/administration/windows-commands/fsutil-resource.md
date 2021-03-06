---
ms.assetid: b198d8ca-a5b7-430f-8911-5cbb9f50484c
title: Fsutil resource
ms.prod: windows-server
manager: dmoss
ms.author: toklima
author: toklima
ms.technology: storage
audience: IT Pro
ms.topic: article
ms.date: 10/16/2017
ms.openlocfilehash: 10f2847fd05658a481a10dfb5a1920a998559962
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71376820"
---
# <a name="fsutil-resource"></a>Fsutil resource
>S'applique à : Windows Server (canal semi-annuel), Windows Server 2016, Windows 10, Windows Server 2012 R2, Windows 8.1, Windows Server 2012, Windows 8, Windows Server 2008 R2, Windows 7, Windows 2008, Windows Vista

Crée un Gestionnaire des ressources transactionnel secondaire, démarre ou arrête un Gestionnaire des ressources transactionnel, ou affiche des informations sur un Gestionnaire des ressources transactionnel et modifie le comportement suivant :

-   Si un Gestionnaire des ressources transactionnel par défaut nettoie ses métadonnées transactionnelles au prochain montage

-   Le Gestionnaire des ressources transactionnel spécifié pour préférer la cohérence au niveau de la disponibilité

-   La transaction spécifiée Gestionnaire des ressources pour préférer la disponibilité à la cohérence

-   Caractéristiques d’un Gestionnaire des ressources transactionnel en cours d’exécution

Pour obtenir des exemples d’utilisation de cette commande, consultez [exemples](#BKMK_examples) .

## <a name="syntax"></a>Syntaxe

```
fsutil resource [create] <RmRootPathname>
fsutil resource [info] <RmRootPathname>
fsutil resource [setautoreset] {true|false} <DefaultRmRootPathname>
fsutil resource [setavailable] <RmRootPathname>
fsutil resource [setconsistent] <RmRootPathname>
fsutil resource [setlog] [growth {<Containers> containers|<Percent> percent} <RmRootPathname>] [maxextents <Containers> <RmRootPathname>] [minextents <Containers> <RmRootPathname>] [mode {full|undo} <RmRootPathname>] [rename <RmRootPathname>] [shrink <percent> <RmRootPathname>] [size <Containers> <RmRootPathname>]
fsutil resource [start] <RmRootPathname> [<RmLogPathname> <TmLogPathname>
fsutil resource [stop] <RmRootPathname>
```

### <a name="parameters"></a>Paramètres

|        Paramètre        |                                                                                                                                                                                                                                        Description                                                                                                                                                                                                                                         |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|         créer          |                                                                                                                                                                                                                    Crée un Gestionnaire des ressources transactionnel secondaire.                                                                                                                                                                                                                     |
|    <RmRootPathname>     |                                                                                                                                                                                                        Spécifie le chemin d’accès complet à un répertoire racine Gestionnaire des ressources transactionnel.                                                                                                                                                                                                         |
|          info           |                                                                                                                                                                                                            Affiche les informations de Gestionnaire des ressources transactionnelles spécifiées.                                                                                                                                                                                                            |
|      setautoreset       | Spécifie si un Gestionnaire des ressources transactionnel par défaut nettoie les métadonnées transactionnelles lors du montage suivant.<br /><br />-Affectez la valeur **true** au paramètre **setautoreset** pour spécifier que la transaction gestionnaire des ressources nettoiera les métadonnées transactionnelles lors du montage suivant, par défaut.<br />-Définissez le paramètre **setautoreset** sur **false** pour indiquer que la transaction gestionnaire des ressources ne nettoiera pas les métadonnées transactionnelles lors du montage suivant, par défaut. |
| <DefaultRmRootPathname> |                                                                                                                                                                                                                       Spécifie le nom du lecteur suivi d’un signe deux-points.                                                                                                                                                                                                                        |
|      setavailable       |                                                                                                                                                                                                 Spécifie qu’un Gestionnaire des ressources transactionnel préfèrera la disponibilité à la cohérence.                                                                                                                                                                                                 |
|      setconsistent      |                                                                                                                                                                                                 Spécifie qu’un Gestionnaire des ressources transactionnel préfèrera la cohérence au niveau de la disponibilité.                                                                                                                                                                                                 |
|         Growth          |                                                                                                                                                                                                  Modifie les caractéristiques d’un Gestionnaire des ressources transactionnel qui est déjà en cours d’exécution.                                                                                                                                                                                                  |
|         future          |                                                                                                  Spécifie le nombre de fois que le journal des Gestionnaire des ressources transactionnelles peut croître.<br /><br />Le paramètre Growth peut être spécifié comme suit :<br /><br />-Nombre de conteneurs en utilisant le format : _Conteneurs_ **conteneurs**<br />-Pourcentage en utilisant le format : _Pourcentage_ **pourcentage**                                                                                                   |
|      <containers>       |                                                                                                                                                                                                      Spécifie les objets de données utilisés par le Gestionnaire des ressources transactionnel.                                                                                                                                                                                                       |
|        maxextent        |                                                                                                                                                                                                Spécifie le nombre maximal de conteneurs pour le Gestionnaire des ressources transactionnel spécifié.                                                                                                                                                                                                |
|        minextent        |                                                                                                                                                                                                Spécifie le nombre minimal de conteneurs pour le Gestionnaire des ressources transactionnel spécifié.                                                                                                                                                                                                |
|  mode {annulation&#124;complète}  |                                                                                                                                                                                        Spécifie si toutes les transactions sont journalisées ( **complètes**) ou uniquement les événements restaurés (**annulation**).                                                                                                                                                                                         |
|         rename          |                                                                                                                                                                                                                  Modifie le GUID du Gestionnaire des ressources transactionnel.                                                                                                                                                                                                                  |
|         shrink          |                                                                                                                                                                                              Spécifie le pourcentage par lequel le journal des Gestionnaire des ressources transactionnelles peut diminuer automatiquement.                                                                                                                                                                                              |
|          size           |                                                                                                                                                                                              Spécifie la taille de la Gestionnaire des ressources transactionnelle sous la forme d’un nombre spécifié de *conteneurs*.                                                                                                                                                                                               |
|          start          |                                                                                                                                                                                                                    Démarre le Gestionnaire des ressources transactionnel spécifié.                                                                                                                                                                                                                    |
|          stop           |                                                                                                                                                                                                                    Arrête le Gestionnaire des ressources transactionnel spécifié.                                                                                                                                                                                                                     |

### <a name="BKMK_examples"></a>Illustre
Pour définir le journal pour le Gestionnaire des ressources transactionnel spécifié par c:\test, afin d’avoir une croissance automatique de cinq conteneurs, tapez :

```
fsutil resource setlog growth 5 containers c:test
```

Pour définir le journal pour le Gestionnaire des ressources transactionnel spécifié par c:\test, pour avoir une croissance automatique de deux pour cent, tapez :

```
fsutil resource setlog growth 2 percent c:test
```

Pour spécifier que le Gestionnaire des ressources transactionnel par défaut nettoie les métadonnées transactionnelles lors du montage suivant sur le lecteur C, tapez :

```
fsutil resource setautoreset true c:\  
```

### <a name="additional-references"></a>Références supplémentaires
[Clé de syntaxe de ligne de commande](Command-Line-Syntax-Key.md)

[Fsutil](Fsutil.md)

[NTFS transactionnel](https://go.microsoft.com/fwlink/?LinkID=165402)


