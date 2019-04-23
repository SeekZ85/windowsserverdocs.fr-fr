---
ms.assetid: 6086947f-f9ef-4e18-9f07-6c7c81d7002c
title: Paramètres et outils du service de temps Windows
description: ''
author: shortpatti
ms.author: pashort
manager: dougkim
ms.date: 10/16/2018
ms.topic: article
ms.prod: windows-server-threshold
ms.technology: networking
ms.openlocfilehash: 7cf3b3f2bb9a2c9f95c50aa6a7b7690f89cdd0af
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59840660"
---
# <a name="windows-time-service-tools-and-settings"></a>Paramètres et outils du service de temps Windows
>S’applique à : Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows 10 ou version ultérieure

Dans cette rubrique, vous en savoir plus sur les outils et paramètres pour le service de temps de Windows (W32Time). 

Si vous souhaitez uniquement synchroniser l’heure pour un ordinateur client joint au domaine, consultez [configurer un ordinateur client pour la synchronisation date / heure automatique domaine](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-r2-and-2008/cc816884%28v%3dws.10%29). Pour accéder aux rubriques sur la configuration du service de temps de Windows, consultez [où trouver des informations Windows temps Service Configuration](https://docs.microsoft.com/windows-server/networking/windows-time-service/windows-time-service-top).  
  
>[!CAUTION]  
>Vous ne devez pas utiliser la commande Net time pour configurer ou définir la durée d’exécution lorsque le service de temps de Windows.  
>
>En outre, sur les anciens ordinateurs qui exécutent Windows XP ou versions antérieures, le /querysntp de Net time commande affiche le nom d’un serveur de protocole NTP (Network Time) avec laquelle un ordinateur est configuré pour synchroniser, mais ce serveur NTP est utilisé uniquement lorsque le client avant de l’ordinateur est configuré comme NTP ou AllSync. Cette commande a depuis été déconseillée.  
  
La plupart des ordinateurs membres du domaine sont de type client heure NT5DS, ce qui signifie que lorsqu’ils synchronisent à temps à partir de la hiérarchie de domaine. L’exception à cette règle uniquement classique est le contrôleur de domaine qui fonctionne comme le principal (PDC) émulateur maître d’opérations PDC du domaine racine de forêt, qui est généralement configuré pour synchroniser l’heure avec une source externe. Pour afficher la configuration du client de temps d’un ordinateur, exécutez la commande de configuration W32tm /query à partir d’une invite de commandes avec élévation de privilèges dans à compter de Windows Server 2008 et Windows Vista et lisez le **Type** ligne dans la sortie de commande. Pour plus d’informations, consultez [Windows temps Service fonctionnement](https://docs.microsoft.com/windows-server/networking/windows-time-service/How-the-Windows-Time-Service-Works). Vous pouvez exécuter la commande **reg query HKLM\SYSTEM\CurrentControlSet\Services\W32Time\Parameters** et lire la valeur de **NtpServer** dans la sortie de commande.  
  
> [!IMPORTANT]  
> Avant Windows Server 2016, le service W32Time n’est pas conçu pour répondre aux besoins de l’application de la contrainte de temps.  Toutefois, les mises à jour vers Windows Server 2016 maintenant vous permettent d’implémenter une solution de 1 MS précision dans votre domaine.  Consultez [Windows 2016 précise temps](accurate-time.md) et [limite de prise en charge pour configurer le service de temps de Windows pour les environnements de haute-précision](https://docs.microsoft.com/windows-server/networking/windows-time-service/support-boundary) pour plus d’informations.  
  
## <a name="windows-time-service-tools"></a>Outils de Service de temps Windows  
Les outils suivants sont associés avec le service de temps de Windows.  
  
#### <a name="w32tmexe-windows-time"></a>W32tm.exe : Horloge Windows  
**Catégorie**  

Cet outil est installé en tant que partie de Windows XP, Windows Vista, Windows 7, Windows Server 2003, Windows Server 2003 R2, Windows Server 2008 et installations par défaut de Windows Server 2008 R2.  
  
**Compatibilité des versions**  
  
Cet outil fonctionne sur Windows XP, Windows Vista, Windows 7, Windows Server 2003, Windows Server 2003 R2, Windows Server 2008 et installations par défaut de Windows Server 2008 R2.  
  
W32tm.exe est utilisé pour configurer les paramètres de service de temps de Windows. Il peut également servir à diagnostiquer les problèmes avec le service de temps. W32tm.exe est l’outil de ligne de commande par défaut pour la configuration, la surveillance ou la résolution des problèmes du service de temps de Windows.  
  
Les tableaux suivants décrivent les paramètres qui sont utilisés avec W32tm.exe.  
  
**Paramètres du principal W32tm.exe**  
  
|Paramètre|Description|  
|-------------|---------------|  
|W32tm / ?|Aide de la ligne de commande w32tm|  
|W32tm /register|Inscrit le service de temps à s’exécuter en tant que service et ajoute la configuration par défaut dans le Registre.|  
|W32tm / annuler l’inscription|Annule l’inscription du service de temps et supprime toutes les informations de configuration à partir du Registre.|  
|w32tm /monitor<br /><br />[/ domaine :<domain name>] [/ ordinateurs :<name>[,<name>[,<name>...]]] [/ threads :<num>]|domaine - spécifie le domaine à surveiller. Si aucun nom de domaine est attribué, ou option ni le domaine ou ordinateurs n’est spécifiée, le domaine par défaut est utilisé. Cette option peut être utilisée plusieurs fois.<br /><br />ordinateurs - surveille la liste donnée d’ordinateurs. Noms d’ordinateur sont séparés par des virgules, sans espaces. Si un nom est préfixé avec un ' *', il est traité comme un contrôleur de domaine principal. Cette option peut être utilisée plusieurs fois.<br /><br />threads : Spécifie le nombre d’ordinateurs à analyser simultanément. La valeur par défaut est 3. Plage autorisée est 1-50.|  
|w32tm /ntte <NT time epoch>|Convertir une heure système NT, de (10 ^ -7) intervalles s à partir de 0 h - 1 janvier 1601, dans un format lisible.|  
|w32tm /ntpte <NTP time epoch>|Convertir un temps NTP, en (2 ^ -32) intervalles s à partir de 0 h 1 - janvier 1900, dans un format lisible.|  
|w32tm /resync<br /><br />[/ ordinateur :<computer>]<br /><br />[/nowait]<br /><br />[/rediscover]<br /><br />[/soft]|Indique à un ordinateur qu’il devrait resynchroniser son horloge dès que possible, en vidant toutes les statistiques d’erreur accumulées.<br /><br />ordinateur :<computer> -Spécifie l’ordinateur qui doit effectuer la synchronisation. Si non spécifié, l’ordinateur local est resynchronisé.<br /><br />NOWAIT - n’attendent pas que le se resynchronisent se produise ; retourner immédiatement. Sinon, attendez que le se resynchronisent à effectuer avant de retourner.<br /><br />redécouvrir : détecter la configuration du réseau et redécouvrir les sources du réseau, puis resynchroniser.<br /><br />Soft - resynchroniser à l’aide de statistiques d’erreurs existant. Pas utile, fourni pour la compatibilité.|  
|w32tm /stripchart<br /><br />/ Computer :<target><br /><br />[/ période :<refresh>]<br /><br />[/dataonly]<br /><br />[/ samples :<count>]<br/><br/>[/rdtsc]<br/>|Afficher un graphique de la bande du décalage entre cet ordinateur et un autre ordinateur.<br /><br />ordinateur :<target> -mesurer les décalages de l’ordinateur.<br /><br />période :<refresh> - le délai entre les échantillons, en secondes. La valeur par défaut est 2 s.<br /><br />dataonly - afficher uniquement les données sans graphismes.<br /><br />exemples :<count> : collectez <count> échantillons, puis arrêter. Si non spécifié, les échantillons seront collectés jusqu'à **Ctrl + C** est enfoncé.<br/><br/>RDTSC : pour chaque exemple, cette option imprime les valeurs séparées par des virgules, ainsi que les en-têtes RdtscStart, RdtscEnd, FileTime, RoundtripDelay, NtpOffset au lieu de l’image de texte.<br/><ul><li>[RdtscStart – RDTSC (compteur d’horodatage de lecture)](https://en.wikipedia.org/wiki/Time_Stamp_Counter) valeur collectée juste avant que la demande NTP a été générée.</li><li>RdtscEnd – valeur RDTSC (compteur d’horodatage de lecture) collecté uniquement une fois que la réponse NTP a été reçue et traitée.</li><li>FileTime – valeur FILETIME Local utilisé dans la demande NTP.</li><li>RoundtripDelay – le temps écoulé en secondes entre la génération de la demande NTP et traitement de la réponse NTP reçue, calculée en fonction des calculs d’aller-retour NTP.</li><li>NTPOffset – en secondes entre l’ordinateur local et le serveur NTP, du décalage horaire calculé selon les calculs de décalage NTP.</li></ul>|
|w32tm /config<br /><br />[/ ordinateur :<target>]<br /><br />[/update]<br /><br />[/manualpeerlist:<peers>]<br /><br />[/ syncfromflags :<source>]<br /><br />[/ LocalClockDispersion :<seconds>]<br /><br />[/ reliable : (Oui&#124;non)]<br /><br />[/largephaseoffset:<milliseconds>]|ordinateur :<target> -ajuste la configuration de <target>. Si non spécifié, la valeur par défaut est l’ordinateur local.<br /><br />mise à jour : avertit le service de temps que la configuration a changé, l’origine des modifications entrent en vigueur.<br /><br />manualpeerlist :<peers> -définit la liste d’homologues manuelle de <peers>, qui est une liste délimitée par des adresses DNS et/ou IP. Lorsque vous spécifiez plusieurs homologues, cette option doit être entre guillemets.<br /><br />syncfromflags :<source> -définit les sources du client NTP doit se synchroniser à partir de. <source> doit être une liste séparée par des virgules de ces mots clés (non sensible à la casse) :<br /><br />MANUAL - inclure les homologues dans la liste d’homologues manuelle.<br /><br />DOMHIER - synchroniser à partir d’un contrôleur de domaine (DC) dans la hiérarchie de domaine.<br /><br />LocalClockDispersion :<seconds> -configure la précision de l’horloge interne W32Time supposera que lorsqu’il ne peut pas acquérir le temps à partir de ses sources configurés.<br /><br />fiable : (Oui&#124;non) - définir si cet ordinateur est une source de temps fiable.<br /><br />Ce paramètre n’est significatif sur les contrôleurs de domaine.<br /><br />Oui - cet ordinateur est un service de temps fiable.<br /><br />NON - cet ordinateur n’est pas un service de temps fiable.<br /><br />LargePhaseOffset :<milliseconds> -définit la différence de temps entre local et réseau de temps qui W32Time considère un pic.|  
|w32tm /tz|Afficher les paramètres de fuseau horaire actuel.|  
|w32tm /dumpreg<br /><br />[/ sous-clé :<key>]<br /><br />[/ ordinateur :<target>]|Afficher les valeurs associées à une clé de Registre donnée.<br /><br />La clé par défaut est HKLM\System\CurrentControlSet\Services\W32Time<br /><br />(la clé racine pour le service de temps).<br /><br />sous-clé :<key> -affiche les valeurs associées de sous-clé <key> de la clé par défaut.<br /><br />ordinateur :<target> -interroge les paramètres du Registre pour l’ordinateur <target>|  
|w32tm /query [/computer:<target>] {/source &#124; /configuration &#124; /peers &#124; /status} [/verbose]|Ce paramètre a été tout d’abord mis à disposition dans les temps de Windows client les versions de Windows Vista et Windows Server 2008.<br /><br />Afficher les informations de service de temps de Windows d’un ordinateur.<br /><br />**ordinateur :<target>**  -interroger les informations de **<target>**. Si non spécifié, la valeur par défaut est l’ordinateur local.<br /><br />**Source** -afficher la source de temps.<br /><br />**Configuration** -afficher la configuration d’exécution et où le paramètre provenance. En mode documenté, afficher le non défini ou non utilisés aussi un paramètre.<br /><br />**homologues** -afficher la liste des homologues et leur état.<br /><br />**état** -état de service de temps d’affichage Windows.<br /><br />**verbose** -définir le mode détaillé pour afficher plus d’informations.|  
|w32tm /debug {/disable &#124; {/enable /file:<name> /size:<bytes> /entries:<value> [/truncate]}}|Ce paramètre a été tout d’abord mis à disposition dans les temps de Windows client les versions de Windows Vista et Windows Server 2008.<br /><br />Activer ou désactiver l’ordinateur local Windows service privé journal.<br /><br />**désactiver** -désactiver le journal privé.<br /><br />**activer** -activer le journal privé.<br /><br />-   **fichier :<name>**  -spécifiez le nom de fichier absolu.<br />-   **taille :<bytes>**  -spécifiez la taille maximale pour la journalisation circulaire.<br />-   **entrées :<value>**  -contient une liste d’indicateurs, spécifiée par le numéro et séparés par des virgules, qui spécifient les types d’informations qui doivent être journalisées. Les nombres valides sont 0 à 300. Une plage de nombres est valide, en plus des nombres uniques, par exemple, 0-100,103, 106. La valeur 0 à 300 est pour toutes les informations de connexion.<br /><br />**tronquer** -tronquer le fichier s’il existe.|  

---  
Pour plus d’informations sur **W32tm.exe**, consultez le centre d’aide et Support dans Windows XP, Windows Vista, Windows 7, Windows Server 2003, Windows Server 2003 R2, Windows Server 2008 et Windows Server 2008 R2.  
  
## <a name="windows-time-service-registry-entries"></a>Entrées de Registre du Service de temps Windows  
Les entrées de Registre suivantes sont associées avec le service de temps de Windows.  
  
Ces informations sont fournies en tant que référence pour une utilisation dans la résolution des problèmes ou de vérifier que les paramètres requis sont appliquées. Il est recommandé que vous ne modifiez pas directement le Registre, sauf si il n’existe aucune alternative. Modifications du Registre ne sont pas validées par l’Éditeur du Registre ou par Windows avant qu’ils sont appliqués, et par conséquent, les valeurs incorrectes peuvent être stockées. Cela peut entraîner des erreurs irrécupérables dans le système.  
  
Si possible, utilisez la stratégie de groupe ou d’autres outils de Windows, tels que Microsoft Management Console (MMC), pour accomplir les tâches plutôt que de modifier le Registre directement. Si vous devez modifier le Registre, soyez très vigilant.  
  
> [!WARNING]  
> Certaines des valeurs prédéfinies qui sont configurés dans le fichier de modèle d’administration système (System.adm) pour les paramètres d’objet de stratégie de groupe diffèrent des entrées de Registre par défaut correspondantes. Si vous envisagez d’utiliser un objet de stratégie de groupe pour configurer les paramètres d’heure de Windows, n’oubliez pas que vous passez en revue [les valeurs de présélection pour les paramètres de stratégie de groupe de service de temps de Windows sont différentes dans les entrées de Registre de service Windows temps correspondantes dans Windows Server 2003 ](https://go.microsoft.com/fwlink/?LinkId=186066). Ce problème s’applique à Windows Server 2008 R2, Windows Server 2008, Windows Server 2003 R2 et Windows Server 2003.  
  
Nombre d’entrées de Registre pour le service de temps de Windows est les mêmes que le paramètre de stratégie de groupe du même nom. Les paramètres de stratégie de groupe correspondent aux entrées de Registre du même nom situé dans :  
  
>**HKLM\SYSTEM\CurrentControlSet\Services\W32Time\\**

  
Il existe plusieurs clés de Registre à cet emplacement de Registre. Les paramètres d’heure de Windows sont stockées dans les valeurs dans l’ensemble de ces clés :
* [Paramètres](#Parameters)
* [Config](#Configuration)
* [NtpClient](#NtpClient)
* [NtpServer](#NtpServer)
  

Plusieurs des valeurs dans la section W32Time du Registre sont utilisés en interne par W32Time pour stocker des informations. Ces valeurs ne doivent pas être modifiées manuellement à tout moment. Ne modifiez pas les paramètres dans cette section, sauf si vous êtes familiarisé avec le paramètre et que vous êtes certain que la nouvelle valeur fonctionne comme prévu. Les entrées de Registre suivantes se trouvent sous :

**HKLM\SYSTEM\CurrentControlSet\Services\W32Time**  

Lorsque vous créez une stratégie, les paramètres sont configurés à l’emplacement suivant, qui n’est pas prioritaire sur l’emplacement suivant :

**HKLM\SOFTWARE\Policies\Microsoft\Windows\W32time**

La clé W32time est créée avec la stratégie.  Lorsque vous supprimez la stratégie, puis cette clé est également supprimée.

L’autre emplacement par défaut :

**HKLM\SYSTEM\CurrentControlSet\Services\W32time**

Certains des paramètres sont stockés dans des battements d’horloge dans le Registre et certaines sont exprimées en secondes. Pour convertir l’heure à partir de battements d’horloge secondes :  
  
-   1 minute = 60 sec  
  
-   1 s = 1 000 ms  
  
-   1 ms = 10 000 battements d’horloge sur un système Windows, comme décrit dans [DateTime.Ticks Property](https://docs.microsoft.com/dotnet/api/system.datetime.ticks?redirectedfrom=MSDN&view=netframework-4.7.2#System_DateTime_Ticks).  
  
Par exemple, 5 minutes deviendrait 5 * 60\*1000\*10000 = 3000000000 battements d’horloge. 

Toutes les versions incluent Windows 7, Windows 8, Windows 10, Windows Server 2008 et Windows Server 2008 R2, Windows Server 2012, Windows Server 2012 R2, Windows Server 2016.  Certaines entrées sont uniquement disponibles sur les versions de Windows plus récentes.


#### <a name="hklmsystemcurrentcontrolsetservicesw32timeparameters"></a>HKLM\SYSTEM\CurrentControlSet\Services\W32Time\Parameters

|Entrée de Registre|Version|Description|
|------------------------------------|---------------|----------------------------|
|AllowNonstandardModeCombinations|Tous|Entrée indique que les combinaisons de mode non standard sont autorisées dans la synchronisation entre homologues. La valeur par défaut pour les membres du domaine est 1. La valeur par défaut pour les clients et serveurs autonomes est 1.|
|NtpServer|Tous|Entrée spécifie une liste délimitée par des homologues à partir de laquelle un ordinateur obtient des horodatages, consistant en un ou plusieurs noms DNS ou adresses IP par ligne. Chaque nom DNS ou l’adresse IP doit être unique. Ordinateurs connectés à un domaine doivent synchroniser avec une source de temps plus fiable, tels que l’horloge de temps américain officiel.  <ul><li>0 x 01 SpecialInterval </li><li>0x02 UseAsFallbackOnly</li><li>0 x 04 SymmetricActive - pour plus d’informations sur ce mode, consultez [serveur de temps Windows : 3.3 les modes de fonctionnement](https://go.microsoft.com/fwlink/?LinkId=208012).</li><li>0 x 08 client</li></ul><br />Il n’existe aucune valeur par défaut pour cette entrée de Registre sur les membres du domaine. La valeur par défaut sur les clients et serveurs autonomes est time.windows.com,0x1.<br /><br />Remarque: Pour plus d’informations sur les serveurs NTP disponibles, consultez [l’article de la Base de connaissances Microsoft 262680 - une liste des serveurs de temps de protocole SNTP (Simple Network Time Protocol) qui sont disponibles sur Internet](https://go.microsoft.com/fwlink/?LinkId=186067)|
|ServiceDll|Tous|Entrée est conservée par W32Time. Il contient des données réservé qui sont utilisées par le système d’exploitation Windows, et les modifications apportées à ce paramètre peuvent entraîner des résultats imprévisibles. L’emplacement par défaut pour cette DLL sur les serveurs et de clients autonomes et les membres du domaine est % windir%\System32\W32Time.dll.  |
|ServiceMain|Tous|Entrée est conservée par W32Time. Il contient des données réservé qui sont utilisées par le système d’exploitation Windows, et les modifications apportées à ce paramètre peuvent entraîner des résultats imprévisibles. La valeur par défaut sur les membres du domaine est SvchostEntry_W32Time. La valeur par défaut sur les clients et serveurs autonomes est SvchostEntry_W32Time.  "|
|Type|Tous|Entrée indique laquelle homologues pour accepter la synchronisation à partir de :  <ul><li>**NoSync**. Le service de temps ne synchronise pas avec d’autres sources.</li><li>**NTP.** Le service de temps synchronise à partir des serveurs spécifiés dans le **NtpServer**. entrée de Registre.</li><li>**NT5DS**. Le service de temps synchronise à partir de la hiérarchie de domaine.  </li><li>**AllSync**. Le service de temps utilise les mécanismes de synchronisation disponibles.  </li></ul>La valeur par défaut sur les membres du domaine est **NT5DS**. La valeur par défaut sur les clients et serveurs autonomes est **NTP**.   |
---
#### <a name="hklmsystemcurrentcontrolsetservicesw32timeconfig"></a>HKLM\SYSTEM\CurrentControlSet\Services\W32Time\Config

|Entrée de Registre|Version|Description|
|------------------------------------|---------------|----------------------------|
|AnnounceFlags|Tous|Entrée de contrôle si cet ordinateur est marqué comme un serveur de temps fiable. Un ordinateur n’est pas marqué comme fiables, sauf si elle est également marqué comme un serveur de temps.<br /> -0 x 00 pas un serveur de temps  <br /> -serveur de temps toujours 0 x 01  <br /> -serveur de temps automatique de 0 x 02  <br /> -serveur de temps fiable toujours 0 x 04  <br /> -serveur de temps fiable automatique 0 x 08  <br />La valeur par défaut pour les membres du domaine est 10. La valeur par défaut pour les clients et serveurs autonomes est 10.|
|EventLogFlags|Tous|Entrée de contrôle les événements qui enregistre le service de temps.  <br />-Heure saut : 0x1  <br />-Modification de la source : 0x2  <br />La valeur par défaut sur les membres du domaine est 2. La valeur par défaut sur les clients et serveurs autonomes est 2.  |
|FrequencyCorrectRate|Tous|Entrée contrôle la fréquence à laquelle l’horloge est corrigée. Si cette valeur est trop petite, l’horloge est instable et overcorrects. Si la valeur est trop grande, l’horloge prend beaucoup de temps à synchroniser. La valeur par défaut sur les membres du domaine est 4. La valeur par défaut sur les clients et serveurs autonomes est 4.  <br /><br />Notez que 0 est une valeur non valide pour l’entrée de Registre FrequencyCorrectRate. Sur Windows Server 2003, Windows Server 2003 R2, Windows Server 2008 et les ordinateurs Windows Server 2008 R2, si la valeur est définie sur 0 le service de temps de Windows sera automatiquement Remplacez-le par 1.  |
|HoldPeriod|Tous|Entrée contrôle la période de temps pour lequel pic détection est désactivée, faire en sorte que l’horloge locale en synchronisation rapidement. Un pic est un exemple de temps indiquant ce temps est désactivé un nombre de secondes et est généralement reçu après que les exemples de bon moment ont été retournés régulièrement. La valeur par défaut sur les membres du domaine est 5. La valeur par défaut sur les clients et serveurs autonomes est 5.  |
|LargePhaseOffset|Tous|Entrée spécifie qu’une durée décalage supérieure ou égale à cette valeur dans les 10<sup>-7</sup> secondes est considéré comme un pic. Une interruption du réseau comme une grande quantité de trafic peut provoquer un pic. Un pic sera ignoré, sauf si elle persiste pendant une longue période de temps. La valeur par défaut sur les membres du domaine est 50000000. La valeur par défaut sur les clients et serveurs autonomes est 50000000.  |
|LastClockRate|Tous|Entrée est conservée par W32Time. Il contient des données réservé qui sont utilisées par le système d’exploitation Windows, et les modifications apportées à ce paramètre peuvent entraîner des résultats imprévisibles. La valeur par défaut sur les membres du domaine est 156250. La valeur par défaut sur les clients et serveurs autonomes est 156250.  |
|LocalClockDispersion|Tous|Entrée contrôle la dispersion (en secondes) que vous devez considérer lorsque le seul moment où la source est l’horloge CMOS intégré. La valeur par défaut sur les membres du domaine est 10. La valeur par défaut sur les clients et serveurs autonomes est 10.|
|MaxAllowedPhaseOffset|Tous|Entrée spécifie le décalage maximal (en secondes) pendant laquelle W32Time essaie d’ajuster l’horloge de l’ordinateur à l’aide de la fréquence d’horloge. Lorsque le décalage est supérieur à ce taux, W32Time définit directement l’horloge de l’ordinateur. La valeur par défaut pour les membres du domaine est 300. La valeur par défaut pour les clients et serveurs autonomes est 1.  [Voir ci-dessous pour plus d’informations](#MaxAllowedPhaseOffset).|
|MaxClockRate|Tous|Entrée est conservée par W32Time. Il contient des données réservé qui sont utilisées par le système d’exploitation Windows, et les modifications apportées à ce paramètre peuvent entraîner des résultats imprévisibles. La valeur par défaut pour les membres du domaine est 155860. La valeur par défaut pour les clients et serveurs autonomes est 155860.  |
|MaxNegPhaseCorrection|Tous|Entrée spécifie la plus grande correction de temps négatif en quelques secondes que le service effectue. Si le service détermine qu’une modification supérieure est nécessaire, il consigne un événement à la place. Cas particulier : 0xFFFFFFFF signifie toujours faire une correction de temps. La valeur par défaut pour les membres du domaine est 0xFFFFFFFF. La valeur par défaut pour les clients et serveurs autonomes est 54 000 (15 heures).  |
|MaxPollInterval|Tous|Entrée spécifie l’intervalle le plus grand, en secondes de log2, autorisée pour l’intervalle d’interrogation du système. Notez que pendant un système doit interroger en fonction de l’intervalle planifié, un fournisseur peut refuser produire des exemples de la demande. La valeur par défaut pour les contrôleurs de domaine est 10. La valeur par défaut pour les membres du domaine est 15. La valeur par défaut pour les clients et serveurs autonomes est 15.  |
|MaxPosPhaseCorrection|Tous|Entrée spécifie la plus grande correction de temps positif en secondes que le service effectue. Si le service détermine qu’une modification supérieure est nécessaire, il consigne un événement à la place. Cas particulier : 0xFFFFFFFF signifie toujours faire une correction de temps. La valeur par défaut pour les membres du domaine est 0xFFFFFFFF. La valeur par défaut pour les clients et serveurs autonomes est 54 000 (15 heures).  |
|MinClockRate|Tous|Entrée est conservée par W32Time. Il contient des données réservé qui sont utilisées par le système d’exploitation Windows, et les modifications apportées à ce paramètre peuvent entraîner des résultats imprévisibles. La valeur par défaut pour les membres du domaine est 155860. La valeur par défaut pour les clients et serveurs autonomes est 155860.  |
|MinPollInterval|Tous|Entrée spécifie l’intervalle le plus faible, en secondes de log2, autorisée pour l’intervalle d’interrogation du système. Notez que pendant un système ne demande pas les échantillons plus fréquemment, un fournisseur peut produire des exemples parfois autre que l’intervalle planifié. La valeur par défaut pour les contrôleurs de domaine est 6. La valeur par défaut pour les membres du domaine est 10. La valeur par défaut pour les clients et serveurs autonomes est 10.  |
|PhaseCorrectRate|Tous|Entrée contrôle la fréquence à laquelle l’erreur de phase a été corrigée. En spécifiant une valeur faible corrige l’erreur de phase rapidement, mais peut entraîner l’horloge de devenir instable. Si la valeur est trop grande, elle prend plus de temps pour corriger l’erreur de phase. <br /><br />La valeur par défaut sur les membres du domaine est 1. La valeur par défaut sur les clients et serveurs autonomes est 7.<br /><br />Remarque: 0 est une valeur non valide pour l’entrée de Registre PhaseCorrectRate. Sur Windows Server 2003, Windows Server 2003 R2, Windows Server 2008 et les ordinateurs Windows Server 2008 R2, si la valeur est définie sur 0, le service de temps de Windows modifie automatiquement en fonction à 1.  |
|PollAdjustFactor|Tous|Entrée contrôle la décision pour augmenter ou diminuer l’intervalle d’interrogation pour le système. Plus la valeur est grande, plus la quantité d’erreurs qui provoque l’intervalle d’interrogation être réduit. La valeur par défaut sur les membres du domaine est 5. La valeur par défaut sur les clients et serveurs autonomes est 5. |
|SpikeWatchPeriod|Tous|Entrée spécifie la durée pendant laquelle un décalage suspect doit persister avant d’être accepté comme correcte (en secondes). La valeur par défaut sur les membres du domaine est 900. La valeur par défaut sur les clients autonomes et les stations de travail est de 900.  |
|TimeJumpAuditOffset|Tous|Entier non signé qui indique le seuil d’audit de saut de temps, en secondes. Si le service de temps ajuste l’horloge locale en définissant l’horloge directement, et la correction de temps dépasse cette valeur, le service de temps consigne un événement d’audit.|
|UpdateInterval|Tous|Entrée spécifie le nombre de battements d’horloge entre les ajustements de correction de phase. La valeur par défaut pour les contrôleurs de domaine est 100. La valeur par défaut pour les membres du domaine est de 30 000. La valeur par défaut pour les clients et serveurs autonomes est 360 000.  <br /><br />**REMARQUE** : Zéro est une valeur non valide pour l’entrée de Registre UpdateInterval. Sur les ordinateurs exécutant Windows Server 2003, Windows Server 2003 R2, Windows Server 2008 et Windows Server 2008 R2, si la valeur est définie sur 0 le service de temps de Windows modifie automatiquement en fonction à 1.<br /><br />Les entrées de trois Registre suivantes ne font pas partie de la configuration par défaut W32Time mais peuvent être ajoutées dans le Registre pour obtenir des fonctionnalités de journalisation accrue. Les informations consignées dans le journal des événements système peuvent être modifiées en modifiant la valeur du paramètre EventLogFlags dans l’éditeur d’objet de stratégie de groupe. Par défaut, le service de temps crée un journal dans l’Observateur d’événements chaque fois qu’il bascule vers une nouvelle source de temps.<br /><br />**AVERTISSEMENT** : Certaines des valeurs prédéfinies qui sont configurés dans le fichier de modèle d’administration système (System.adm) pour les paramètres d’objet de stratégie de groupe diffèrent des entrées de Registre par défaut correspondantes. Si vous envisagez d’utiliser un objet de stratégie de groupe pour configurer les paramètres d’heure de Windows, n’oubliez pas que vous passez en revue [les valeurs de présélection pour les paramètres de stratégie de groupe de service de temps de Windows sont différentes dans les entrées de Registre de service Windows temps correspondantes dans Windows Server 2003 ](https://go.microsoft.com/fwlink/?LinkId=186066). Ce problème s’applique à Windows Server 2008 R2, Windows Server 2008, Windows Server 2003 R2 et Windows Server 2003. |
|UtilizeSslTimeData|Valider la build 1511 de Windows 10|Entrée de 1 indique que le W32Time utilise plusieurs horodateurs SSL pour amorcer une horloge est certes approximative.|
---
Les entrées de Registre suivantes doivent être ajoutées afin d’activer la journalisation de W32Time :  

|Entrée de Registre|Version|Description|
|------------------------------------|---------------|----------------------------|
|FileLogEntries|Tous|Entrée contrôle la quantité d’entrées créées dans le fichier journal Windows. La valeur par défaut est none, ce qui n’enregistre pas de toute activité au moment de Windows. Les valeurs valides sont 0 à 300. Cette valeur n’affecte pas les entrées de journal des événements normalement créées par heure de Windows|
|FileLogName|Tous|Entrée contrôle l’emplacement et le nom de fichier du journal de temps de Windows. La valeur par défaut est vide et ne doit pas être modifiée, sauf si **FileLogEntries** est modifiée. Une valeur valide est un chemin d’accès complet et le nom de fichier Windows temps utilisera pour créer le fichier journal. Cette valeur n’affecte pas les entrées de journal des événements normalement créées par heure de Windows.  |
|FileLogSize|Tous|Entrée de contrôle le comportement de l’enregistrement circulaire des fichiers journaux au moment de Windows. Lorsque **FileLogEntries** et **FileLogName** sont définis, entrée définit la taille, en octets, pour permettre le fichier journal à atteindre avant de remplacer les entrées de journal plus ancien avec de nouvelles entrées. Utilisez 1000000 ou plus grande valeur pour ce paramètre. Cette valeur n’affecte pas les entrées de journal des événements normalement créées par heure de Windows.  |

---

#### <a name="hklmsystemcurrentcontrolsetservicesw32timetimeprovidersntpclient"></a>HKLM\SYSTEM\CurrentControlSet\Services\W32Time\TimeProviders\NtpClient

|Entrée de Registre|Version|Description|
|------------------------------------|---------------|----------------------------|
|AllowNonstandardModeCombinations|Tous|Entrée indique que les combinaisons de mode non standard sont autorisées dans la synchronisation entre homologues. La valeur par défaut pour les membres du domaine est 1. La valeur par défaut pour les clients et serveurs autonomes est 1.|
|CompatibilityFlags|Tous|Entrée spécifie les indicateurs de compatibilité suivants et les valeurs : <br /><br />-DispersionInvalid : 0x00000001  <br />-   IgnoreFutureRefTimeStamp: 0x00000002  <br /> -   AutodetectWin2K: 0x80000000  <br />-AutodetectWin2KStage2 : 0x40000000  <br /><br />La valeur par défaut pour les membres du domaine est 0 x 80000000. La valeur par défaut pour les clients et serveurs autonomes est 0 x 80000000.  |
|CrossSiteSyncFlags|Tous|Détermine si le service choisit des partenaires de synchronisation en dehors du domaine de l’ordinateur. Les options et les valeurs sont :  <br /><br />-None : 0  <br />-   PdcOnly: 1  <br />-Toutes les : 2  <br /><br />Cette valeur est ignorée si la valeur NT5DS n’est pas définie. La valeur par défaut pour les membres du domaine est 2. La valeur par défaut pour les clients et serveurs autonomes est 2.  |
|DllName|Tous|Entrée spécifie l’emplacement de la DLL pour le fournisseur de temps.  <br /><br />L’emplacement par défaut pour cette DLL sur les serveurs et de clients autonomes et les membres du domaine est % windir%\System32\W32Time.dll.|
|Enabled|Tous|Entrée indique si le fournisseur de NtpClient est activé dans le Service de temps actuelle.  <br /><ul><li>Oui 1</li><li>N° 0</li></ul>La valeur par défaut sur les membres du domaine est 1. La valeur par défaut sur les clients et serveurs autonomes est 1.|
|EventLogFlags|Tous|Entrée spécifie les événements consignés par le service de temps de Windows.<ul><li>modifications de l’accessibilité de 0 x 1</li><li>0 x 2 échantillon de grande taille décalage (cela s’applique à Windows Server 2003, Windows Server 2003 R2, Windows Server 2008 et Windows Server 2008 R2 uniquement)</li></ul>La valeur par défaut sur les membres du domaine est 0 x 1. La valeur par défaut sur les clients et serveurs autonomes est 0 x 1.|
|InputProvider|Tous|Entrée indique s’il faut activer NtpClient comme un InputProvider, qui obtient des informations au moment de la NtpServer. Le NtpServer est un serveur de temps qui répond aux demandes client sur le réseau en retournant des exemples qui sont utiles pour la synchronisation de l’horloge locale. <ul><li>1 = Oui  </li><li>No = 0 </li></ul><p>Valeur par défaut pour les membres du domaine et les clients autonomes : 1  |
|LargeSampleSkew|Tous|Entrée indique l’inclinaison de l’échantillon de grande taille pour la journalisation en secondes. Pour être conforme aux spécifications de sécurité et d’Exchange Commission (s), cela doit être défini sur trois secondes. Les événements seront enregistrés pour ce paramètre uniquement lorsque EventLogFlags est explicitement configuré pour un décalage des échantillons importants 0 x 2. La valeur par défaut sur les membres du domaine est 3. La valeur par défaut sur les clients et serveurs autonomes est 3.  |
|ResolvePeerBackOffMaxTimes|Tous|Entrée spécifie le nombre maximal de fois de doubler le délai d’attente lorsque répété tente de localiser un homologue pour se synchroniser avec échec. Une valeur égale à zéro signifie que le délai d’attente est toujours la valeur minimale. La valeur par défaut sur les membres du domaine est 7. La valeur par défaut sur les clients et serveurs autonomes est 7. |
|ResolvePeerBackoffMinutes|Tous|Entrée spécifie l’intervalle d’attente, en minutes, avant de tenter de localiser un homologue pour se synchroniser avec initial. La valeur par défaut sur les membres du domaine est 15. La valeur par défaut sur les clients et serveurs autonomes est 15.  |
|SpecialPollInterval|Tous|Entrée spécifie l’intervalle d’interrogation spécial en secondes pour les homologues manuels. Lorsque l’indicateur SpecialInterval 0 x 1 est activé, W32Time utilise cet intervalle d’interrogation au lieu d’un intervalle d’interrogation déterminer par le système d’exploitation. La valeur par défaut sur les membres du domaine est 3 600. La valeur par défaut sur les clients et serveurs autonomes est 604 800.<br/><br/>Nouveau pour la version 1702, SpecialPollInterval est contenu par les valeurs de Registre MinPollInterval et MaxPollInterval Config.|
|SpecialPollTimeRemaining|Tous|Entrée est conservée par W32Time. Il contient des données réservé qui sont utilisées par le système d’exploitation Windows. Il spécifie la durée en secondes avant W32Time resynchronisera après avoir redémarré l’ordinateur. Les modifications apportées à ce paramètre peuvent entraîner des résultats imprévisibles. La valeur par défaut, les deux membres du domaine et sur les serveurs et clients autonomes est vide.  |

---

#### <a name="hklmsystemcurrentcontrolsetservicesw32timetimeprovidersntpserver"></a>HKLM\SYSTEM\CurrentControlSet\Services\W32Time\TimeProviders\NtpServer

|Entrée de Registre|Version|Description|
|------------------------------------|---------------|----------------------------|
|AllowNonstandardModeCombinations|Tous|Entrée indique que les combinaisons de mode non standard sont autorisées dans la synchronisation entre les clients et serveurs. La valeur par défaut pour les membres du domaine est 1. La valeur par défaut pour les clients et serveurs autonomes est 1.|
|DllName|Tous|Entrée spécifie l’emplacement de la DLL pour le fournisseur de temps.<br /><br />L’emplacement par défaut pour cette DLL sur les serveurs et de clients autonomes et les membres du domaine est % windir%\System32\W32Time.dll.  |
|Enabled|Tous|Entrée indique si le fournisseur NtpServer est activé dans le Service de temps actuelle. <ul><li>Oui 1</li><li>N° 0</li></ul>La valeur par défaut sur les membres du domaine est 1. La valeur par défaut sur les clients et serveurs autonomes est 1.  |
|InputProvider|Tous|Entrée indique s’il faut activer NtpClient comme un InputProvider, qui obtient des informations au moment de la NtpServer. Le NtpServer est un serveur de temps qui répond aux demandes client sur le réseau en retournant des exemples qui sont utiles pour la synchronisation de l’horloge locale. <ul><li>1 = Oui  </li><li>No = 0 </li></ul><p>Valeur par défaut pour les membres du domaine et les clients autonomes : 1  |

---

#### <a name="maxallowedphaseoffset-information"></a>Informations de MaxAllowedPhaseOffset
Dans l’ordre pour W32Time définir l’horloge de l’ordinateur progressivement, le décalage doit être inférieure à la **MaxAllowedPhaseOffset** valeur et de répondre à l’équation suivante en même temps :  

```  
|CurrentTimeOffset| / (PhaseCorrectRate*UpdateInterval) < SystemClockRate / 2  
``` 
Le CurrentTimeOffset est mesurée en battements d’horloge, où 1 MS = 10 000 battements sur un système Windows d’horloge.  
  
SystemClockRate et PhaseCorrectRate sont également mesurés en battements d’horloge. Pour obtenir le SystemClockRate, vous pouvez utiliser la commande suivante et convertissez-le de quelques secondes à l’aide de la formule de secondes de battements d’horloge * 1000\*10000 :  
  
```  
W32tm /query /status /verbose  
ClockRate: 0.0156000s  
```  
  
SystemclockRate est la vitesse de l’horloge sur le système. À l’aide de 156000 secondes par exemple, le SystemclockRate serait être = 0.0156000 * 1000 \* 10000 = 156000 battements d’horloge.  
  
MaxAllowedPhaseOffset est également en secondes. Pour convertir en battements d’horloge, multipliez MaxAllowedPhaseOffset * 1000\*10000.  
  
Les deux exemples suivants montrent comment appliquer  
  
**Exemple 1** : Heure diffère de 4 minutes (par exemple, votre temps est 11 h 05 et reçue d’un homologue de l’échantillon de temps et considérée comme étant correcte est 11:09:00).  
```
phasecorrectRate = 1  
  
UpdateInterval = 30000 (clock ticks)  
  
systemclockRate = 156000 (clock ticks)  
  
MaxAllowedPhaseOffset = 10min = 600 seconds = 600*1000\*10000=6000000000 clock ticks  
  
|currentTimeOffset| = 4mins = 4*60\*1000\*10000 = 2400000000 ticks  
  
Is CurrentTimeOffset < MaxAllowedPhaseOffset?  
  
2400000000 < 6000000000 = TRUE  
```
ET ne répond pas à l’équation ci-dessus ? 
```
(|CurrentTimeOffset| / (PhaseCorrectRate*UpdateInterval) < SystemClockRate / 2)  
  
Is 2,400,000,000 / (30000*1) < 156000/2  
  
Is 80,000 < 78,000  
  
NO/FALSE  
```  
Par conséquent W32tm serait reculez l’horloge immédiatement.  
  
> [!NOTE]  
> Dans ce cas, si vous souhaitez définir l’horloge précédent lentement, vous devez ajuster les valeurs de PhaseCorrectRate ou updateInterval dans le Registre ainsi pour garantir les résultats de l’équation dans la valeur TRUE.  
  
**Exemple 2** : Heure diffère de 3 minutes.  
```  
phasecorrectRate = 1  
  
UpdateInterval = 30000 (clock ticks)  
  
systemclockRate = 156000 (clock ticks)  
  
MaxAllowedPhaseOffset = 10min = 600 seconds = 600*1000\*10000=6000000000 clock ticks  
  
currentTimeOffset = 3mins = 3*60\*1000\*10000 = 1800000000 clock ticks  
  
Is CurrentTimeOffset < MaxAllowedPhaseOffset?  
  
1800000000 < 6000000000 = TRUE  
```  
ET ne répond pas à l’équation ci-dessus ?
```
(|CurrentTimeOffset| / (PhaseCorrectRate*UpdateInterval) < SystemClockRate / 2)  
  
Is 3 mins (1,800,000,000) / (30000*1) < 156000/2  
  
Is 60,000 < 78,000  
  
YES/TRUE  
```  
Dans ce cas l’horloge retrouvent lentement.  
  
## <a name="windows-time-service-group-policy-settings"></a>Paramètres de stratégie de groupe de Service de temps Windows  
Vous pouvez configurer la plupart des paramètres W32Time à l’aide de l’éditeur d’objets de stratégie de groupe. Cela inclut la configuration d’un ordinateur pour être NTPServer ou NTPClient, le mécanisme de synchronisation de temps de configuration et configuration d’un ordinateur pour pouvoir être une source de temps fiable.  
  
> [!NOTE]  
> Paramètres de stratégie de groupe pour le service de temps de Windows peuvent être configurés sur les contrôleurs de domaine Windows Server 2003, Windows Server 2003 R2, Windows Server 2008 et Windows Server 2008 R2 et peuvent être appliquées uniquement aux ordinateurs exécutant Windows Server 2003, Windows Server 2003 R2, Windows Server 2008 et Windows Server 2008 R2.  
  
Vous pouvez trouver la stratégie de groupe de paramètres utilisés pour configurer W32Time dans le composant logiciel enfichable Éditeur d’objets de stratégie de groupe dans les emplacements suivants :  
  
-   Service de temps d’ordinateur Configuration ordinateur\Modèles Templates\System\Windows  
  
    Configurer **les paramètres de Configuration globaux** ici.  
  
-   Ordinateur Configuration ordinateur\Modèles Templates\System\Windows temps Service\Time fournisseurs  
  
    Configurer **Windows NTP Client** paramètres ici.  
  
    Activer **Windows NTP Client** ici.  
  
    Activer **Windows NTP Server** ici.  
  
> [!WARNING]  
> Certaines des valeurs prédéfinies qui sont configurés dans le fichier de modèle d’administration système (System.adm) pour les paramètres d’objet de stratégie de groupe diffèrent des entrées de Registre par défaut correspondantes. Si vous envisagez d’utiliser un objet de stratégie de groupe pour configurer les paramètres d’heure de Windows, n’oubliez pas que vous passez en revue [les valeurs de présélection pour les paramètres de stratégie de groupe de service de temps de Windows sont différentes dans les entrées de Registre de service Windows temps correspondantes dans Windows Server 2003 ](https://go.microsoft.com/fwlink/?LinkId=186066). Ce problème s’applique à Windows Server 2008 R2, Windows Server 2008, Windows Server 2003 R2 et Windows Server 2003.  
  
Le tableau suivant répertorie les paramètres de stratégie de groupe globaux qui sont associés avec le service de temps de Windows et la valeur prédéfinie associée à chaque paramètre. Pour plus d’informations sur chaque paramètre, consultez les entrées de Registre correspondantes dans «[entrées de Registre du Service de temps Windows](#w2k3tr_times_tools_uhlp)» plus haut dans ce sujet. Les paramètres suivants sont contenus dans un seul GPO appelé **les paramètres de Configuration globaux**.  
  
**Paramètres de stratégie de groupe global associés à des temps de Windows**  
  
|Paramètre de stratégie de groupe|Valeur prédéfinie|  
|------------------------|------------------|  
|AnnounceFlags|10|  
|EventLogFlags|2|  
|FrequencyCorrectRate|4|  
|HoldPeriod|5|  
|LargePhaseOffset|1280000|  
|LocalClockDispersion|10|  
|MaxAllowedPhaseOffset|300|  
|MaxNegPhaseCorrection|54 000 (15 heures)|  
|MaxPollInterval|15|  
|MaxPosPhaseCorrection|54 000 (15 heures)|  
|MinPollInterval|10|  
|PhaseCorrectRate|7|  
|PollAdjustFactor|5|  
|SpikeWatchPeriod|90|  
|UpdateInterval|100|  
  
Le tableau suivant répertorie les paramètres disponibles pour le **configurer Windows NTP Client** GPO et les valeurs prédéfinies qui sont associées avec le service de temps de Windows. Pour plus d’informations sur chaque paramètre, consultez les entrées de Registre correspondantes dans «[entrées de Registre du Service de temps Windows](#w2k3tr_times_tools_uhlp)» plus haut dans ce sujet.  
  
**Paramètres de stratégie de groupe du Client NTP associés aux temps de Windows**  
  
|Paramètre de stratégie de groupe|Valeur par défaut|  
|------------------------|-----------------|  
|NtpServer|time.windows.com,0x1|  
|Type|Options par défaut :<br /><br />-   **NTP.** Utiliser sur les ordinateurs qui ne sont pas joints à un domaine.<br />-   **NT5DS.** Utiliser sur les ordinateurs qui sont joints à un domaine.|  
|CrossSiteSyncFlags|2|  
|ResolvePeerBackoffMinutes|15|  
|ResolvePeerBackoffMaxTimes|7|  
|SpecialPollInterval|3600|  
|EventLogFlags|0|  
  
## <a name="network-ports-used-by-the-windows-time-service"></a>Ports réseau utilisés par le Service de temps Windows  
Heure de Windows suit la spécification NTP, ce qui nécessite l’utilisation du port UDP 123 pour toutes les communications de synchronisation de temps. Ce port est réservé par heure de Windows et reste réservée à tout moment. Chaque fois que l’ordinateur synchronise son horloge ou fournit le temps vers un autre ordinateur, cette communication est effectuée sur le port UDP 123.  
  
> [!NOTE]  
> Si vous avez un ordinateur avec plusieurs cartes réseau (également appelés un ordinateur multirésident), vous ne pouvez pas activer le service de temps de Windows en fonction de la carte réseau.  
  
## <a name="related-information"></a>Informations connexes  
Les ressources suivantes contiennent des informations supplémentaires qui se rapportent à cette section.  
  
-   RFC *1305* dans la base de données de la norme IETF RFC  
