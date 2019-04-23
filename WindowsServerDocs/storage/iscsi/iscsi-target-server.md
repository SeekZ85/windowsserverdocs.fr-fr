---
title: iSCSI Target Server Overview
TOCTitle: iSCSI Target Server
ms.prod: windows-server-threshold
ms.technology: storage-iscsi
ms.topic: article
author: JasonGerend
manager: dougkim
ms.author: jgerend
ms.date: 09/11/2018
ms.openlocfilehash: 14dd373b71c1be2f1a4ff157b9c631530532fc80
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59837940"
---
# <a name="iscsi-target-server-overview"></a>vue d’ensemble du serveur cible iSCSI

S'applique à : Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Cette rubrique fournit une vue d’ensemble du serveur cible iSCSI, un service de rôle dans Windows Server qui vous permet de rendre le stockage disponible via le protocole iSCSI. Cela est utile pour fournir l’accès au stockage sur votre serveur Windows pour les clients qui ne peut pas communiquer via le protocole SMB de partage de fichiers de Windows natif.

Le serveur cible iSCSI est idéal pour les opérations suivantes :

* **Démarrage réseau et sans disque**   à l’aide de cartes réseau prenant en charge de démarrage ou un chargeur de logiciel, vous pouvez déployer des centaines de serveurs sans disque. Avec le serveur cible iSCSI, le déploiement est rapide. Dans les tests internes de Microsoft, 256 ordinateurs ont été déployés en 34 minutes. En utilisant des disques durs virtuels de différenciation, vous pouvez économiser jusqu’à 90 % de l’espace de stockage utilisé pour les images de système d’exploitation. Cette approche est idéale pour les déploiements à grande échelle d’images de système d’exploitation identiques, par exemple sur des machines virtuelles exécutant Hyper-V ou dans des clusters HPC (High-Performance Computing).

* **Stockage d’applications serveur**   certaines applications requièrent un stockage de bloc. Le serveur cible iSCSI peut fournir à ces applications un stockage par blocs disponible en continu. Dans la mesure où le stockage est accessible à distance, il peut également consolider le stockage par blocs pour des emplacements centraux ou des filiales.

* **Stockage hétérogène**   le serveur cible iSCSI prend en charge les initiateurs iSCSI non non-Microsoft, facilitant le partage du stockage sur les serveurs dans un environnement logiciel mixte.

* **Les environnements de développement, de test, de démonstration et de laboratoire**   lorsque le serveur cible iSCSI est activé, un ordinateur exécutant le système d’exploitation Windows Server devient un dispositif de stockage de bloc accessible via le réseau. Cela peut s’avérer utile pour tester des applications avant de les déployer sur un périphérique de stockage SAN.

## <a name="block-storage-requirements"></a>Configuration requise pour le stockage par blocs

L’activation du serveur cible iSCSI visant à offrir du stockage par blocs permet de tirer parti de votre réseau Ethernet existant. Aucun matériel supplémentaire n’est requis. Si une haute disponibilité est un critère important, créez un cluster de haute disponibilité. Vous avez besoin d’un stockage partagé pour le cluster haute disponibilité, soit un stockage matériel Fibre Channel, soit un groupe de stockage SAS (Serial Attached SCSI).

Si vous activez le clustering invité, vous devez fournir une fonctionnalité de stockage par blocs. Les serveurs qui exécutent des logiciels avec le serveur cible iSCSI peuvent fournir la fonctionnalité de stockage par blocs.

## <a name="see-also"></a>Voir aussi

[Stockage cible iSCSI bloc, comment](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh848268(v%3dws.11))  
[Quelles sont les nouveautés dans le serveur cible iSCSI dans Windows Server](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn305893(v%3dws.11))

