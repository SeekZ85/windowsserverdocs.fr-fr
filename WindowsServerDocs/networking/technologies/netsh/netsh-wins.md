---
title: Exemple de fichier de commandes d'environnement réseau (Netsh)
description: Vous pouvez utiliser cette rubrique pour apprendre à créer un fichier de commandes qui effectue plusieurs tâches à l’aide de la commande netsh dans Windows Server 2016.
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: c94e37a4-3637-4613-9eb5-ed604e831eca
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 86fbe66978f7c09a332bba16a27a13fa029cb5a6
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/27/2019
ms.locfileid: "71401921"
---
# <a name="network-shell-netsh-example-batch-file"></a>Exemple de fichier de commandes Network Shell \(Netsh @ no__t-1

S'applique à : Windows Server 2016

Vous pouvez utiliser cette rubrique pour apprendre à créer un fichier de commandes qui effectue plusieurs tâches à l’aide de la commande netsh dans Windows Server 2016. Dans cet exemple de fichier de commandes, le contexte **netsh WINS** est utilisé.

## <a name="example-batch-file-overview"></a>Exemple de vue d’ensemble du fichier batch

Vous pouvez utiliser les commandes netsh pour Windows Internet Name Service \(WINS @ no__t-1 dans des fichiers de commandes et d’autres scripts pour automatiser des tâches. L’exemple de fichier de commandes suivant montre comment utiliser les commandes netsh pour WINS pour effectuer diverses tâches connexes.

Dans cet exemple de fichier de commandes, WINS @ no__t-0A est un serveur WINS avec l’adresse IP 192.168.125.30 et WINS @ no__t-1B est un serveur WINS avec l’adresse IP 192.168.0.189.

L’exemple de fichier de commandes effectue les tâches suivantes.

- Ajoute un enregistrement de nom dynamique avec l’adresse IP 192.168.0.205, mon @ no__t-0RECORD \[04h @ no__t-2, à WINS @ no__t-3A
- Définit WINS @ no__t-0B comme partenaire de réplication push/pull de WINS @ no__t-1A
- Se connecte à WINS @ no__t-0B, puis définit WINS @ no__t-1A comme partenaire de réplication push/pull de WINS @ no__t-2B
- Lance une réplication push de WINS @ no__t-0A vers WINS @ no__t-1B
- Se connecte à WINS @ no__t-0B pour vérifier que le nouvel enregistrement, MY @ no__t-1RECORD, a été correctement répliqué

## <a name="netsh-example-batch-file"></a>Exemple de fichier de commandes netsh

Dans l’exemple de fichier de commandes suivant, les lignes qui contiennent des commentaires sont précédées de la mention « rem ». Netsh ignore les commentaires.

    rem: Begin example batch file.
    
    rem two WINS servers:
    
    rem (WINS-A) 192.168.125.30
    
    rem (WINS-B) 192.168.0.189
    
    rem 1. Connect to (WINS-A), and add the dynamic name MY\_RECORD \[04h\] to the (WINS-A) database.
    
    netsh wins server 192.168.125.30 add name Name=MY\_RECORD EndChar=04 IP={192.168.0.205}
    
    rem 2. Connect to (WINS-A), and set (WINS-B) as a push/pull replication partner of (WINS-A).
    
    netsh wins server 192.168.125.30 add partner Server=192.168.0.189 Type=2
    
    rem 3. Connect to (WINS-B), and set (WINS-A) as a push/pull replication partner of (WINS-B).
    
    netsh wins server 192.168.0.189 add partner Server=192.168.125.30 Type=2
    
    rem 4. Connect back to (WINS-A), and initiate a push replication to (WINS-B).
    
    netsh wins server 192.168.125.30 init push Server=192.168.0.189 PropReq=0
    
    rem 5. Connect to (WINS-B), and check that the record MY\_RECORD \[04h\] was replicated successfully.
    
    netsh wins server 192.168.0.189 show name Name=MY\_RECORD EndChar=04
    
    rem 6. End example batch file.

## <a name="netsh-wins-commands-used-in-the-example-batch-file"></a>Commandes netsh WINS utilisées dans l’exemple de fichier de commandes

La section suivante répertorie les commandes **WINS netsh** utilisées dans cet exemple de procédure.

- **serveur**. Déplace le contexte de commande WINS @ no__t-0line actuel vers le serveur spécifié par son nom ou son adresse IP.
- **Ajouter un nom**. Inscrit un nom sur le serveur WINS.
- **Ajoutez un partenaire**. Ajoute un partenaire de réplication sur le serveur WINS.
- **init push**. Lance et envoie un déclencheur Push à un serveur WINS.
- **afficher le nom**. Affiche des informations détaillées pour un enregistrement particulier dans la base de données du serveur WINS.  

Pour plus d’informations, consultez [Network Shell (Netsh)](netsh.md).
