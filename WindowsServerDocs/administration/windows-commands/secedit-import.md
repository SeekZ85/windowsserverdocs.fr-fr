---
title: 'secedit : import'
description: 'Rubrique relative aux commandes Windows pour * * * *- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1dd59d4c-9d48-444a-871b-b957eb682597
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: bb90096c3483b44cc1285fa3531f47b2bf5c6d2f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71384230"
---
# <a name="seceditimport"></a>secedit : import



Importe les paramètres de sécurité stockés dans un fichier INF précédemment exporté de la base de données configurée avec des modèles de sécurité. Pour obtenir des exemples d’utilisation de cette commande, consultez [exemples](#BKMK_Examples).

## <a name="syntax"></a>Syntaxe

```
Secedit /import /db <database file name> /cfg <configuration file name> [/overwrite] [/areas [securitypolicy | group_mgmt | user_rights | regkeys | filestore | services]] [/log <log file name>] [/quiet]
```

### <a name="parameters"></a>Paramètres

|Paramètre|Description|
|---------|-----------|
|bases|Obligatoire.</br>Spécifie le chemin d’accès et le nom de fichier d’une base de données qui contient la configuration stockée dans laquelle l’importation sera effectuée.</br>Si le nom de fichier spécifie une base de données qui n’a pas de modèle de sécurité (tel que représenté par le fichier `/cfg \<configuration file name>` de configuration) qui lui est associé, l’option de ligne de commande doit également être spécifiée.|
|overwrite|Facultatif.</br>Spécifie si le modèle de sécurité dans le paramètre/cfg doit remplacer tout modèle ou modèle composite qui est stocké dans la base de données au lieu d’ajouter les résultats au modèle stocké.</br>Cette option de ligne de commande est valide uniquement lorsque `/cfg \<configuration file name>` le paramètre est également utilisé. Si cette valeur n’est pas spécifiée, le modèle dans le paramètre/cfg est ajouté au modèle stocké.|
|cfg|Obligatoire.</br>Spécifie le chemin d’accès et le nom de fichier pour le modèle de sécurité qui sera importé dans la base de données à des fins d’analyse.</br>Cette option/cfg est valide uniquement lorsqu’elle est utilisée `/db \<database file name>` avec le paramètre. Si ce n’est pas spécifié, l’analyse est effectuée sur toute configuration déjà stockée dans la base de données.|
|overwrite|Facultatif.</br>Spécifie si le modèle de sécurité dans le paramètre/cfg doit remplacer tout modèle ou modèle composite qui est stocké dans la base de données au lieu d’ajouter les résultats au modèle stocké.</br>Cette option de ligne de commande est valide uniquement lorsque `/cfg \<configuration file name>` le paramètre est également utilisé. Si cette valeur n’est pas spécifiée, le modèle dans le paramètre/cfg est ajouté au modèle stocké.|
|Régions|Facultatif.</br>Spécifie les zones de sécurité à appliquer au système. Si ce paramètre n’est pas spécifié, tous les paramètres de sécurité définis dans la base de données sont appliqués au système. Pour configurer plusieurs zones, séparez chaque zone par un espace. Les zones de sécurité suivantes sont prises en charge :</br>-SecurityPolicy</br>    Stratégie locale et stratégie de domaine pour le système, y compris les stratégies de compte, les stratégies d’audit, les options de sécurité, etc.</br>- Group_Mgmt</br>    Paramètres de groupe restreints pour tous les groupes spécifiés dans le modèle de sécurité.</br>- User_Rights</br>    Droits d’ouverture de session utilisateur et octroi de privilèges.</br>- RegKeys</br>    Sécurité sur les clés de Registre locales.</br>-Cache de pages</br>    Sécurité sur le stockage de fichiers local.</br>-Services</br>    Sécurité pour tous les services définis.|
|Sign|Facultatif.</br>Spécifie le chemin d’accès et le nom du fichier journal pour le processus.|
|Silencieux|Facultatif.</br>Supprime la sortie de l’écran et du journal. Vous pouvez toujours afficher les résultats de l’analyse en utilisant le composant logiciel enfichable Configuration et analyse de la sécurité de la console MMC (Microsoft Management Console).|

## <a name="remarks"></a>Notes

Avant d’importer un fichier. inf sur un autre ordinateur, exécutez la commande secedit/generaterollback sur la base de données sur laquelle l’importation sera effectuée et secedit/Validate sur le fichier d’importation pour vérifier son intégrité.

Si le chemin d’accès du fichier journal n’est pas fourni, le fichier journal pardéfaut, (SystemRoot\*\Documents and Settings UserAccount<em>\*\Mes Documents\Security\Logs DatabaseName</em>. log), est utilisé.

Dans Windows Server 2008, `Secedit /refreshpolicy` a été remplacé par `gpupdate`. Pour plus d’informations sur la façon d’actualiser les paramètres de sécurité, consultez [gpupdate](gpupdate.md).

## <a name="BKMK_Examples"></a>Illustre

Exportez la base de données de sécurité et les stratégies de sécurité de domaine dans un fichier INF, puis importez ce fichier dans une autre base de données afin de répliquer les paramètres de stratégie de sécurité sur un autre ordinateur.
```
Secedit /export /db C:\Security\FY11\SecDbContoso.sdb /mergedpolicy /cfg NetworkShare\Policies\SecContoso.inf /log C:\Security\FY11\SecAnalysisContosoFY11.log /quiet
```
Importez uniquement la partie stratégies de sécurité du fichier dans une autre base de données sur un autre ordinateur.
```
Secedit /import /db C:\Security\FY12\SecDbContoso.sdb /cfg NetworkShare\Policies\SecContoso.inf /areas securitypolicy /log C:\Security\FY11\SecAnalysisContosoFY12.log /quiet
```

#### <a name="additional-references"></a>Références supplémentaires

-   [Secedit:export](secedit-export.md)
-   [Secedit:generaterollback](secedit-generaterollback.md)
-   [Secedit:validate](secedit-validate.md)
-   [Secedit](secedit.md)
-   [Clé de syntaxe de ligne de commande](command-line-syntax-key.md)