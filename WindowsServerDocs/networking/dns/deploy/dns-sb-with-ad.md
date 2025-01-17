---
title: Verwenden von DNS-Richtlinien für Split Brain-DNS in Active Directory
description: Sie können dieses Thema verwenden, um die Funktionen zur Datenverkehrs Verwaltung von DNS-Richtlinien für Split-Brain-bereit Stellungen mit Active Directory integrierten DNS-Zonen in Windows Server 2016 zu nutzen.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-dns
ms.topic: article
ms.assetid: f9533204-ad7e-4e49-81c1-559324a16aeb
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 1a05bdcbf6205b8be7044c92e3dcf71a6e62bed6
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71356028"
---
# <a name="use-dns-policy-for-split-brain-dns-in-active-directory"></a>Verwenden von DNS-Richtlinien für Split Brain-DNS in Active Directory

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In diesem Thema können Sie die Datenverkehrs Verwaltungsfunktionen von DNS-Richtlinien für Split @ no__t-0brain-bereit Stellungen mit Active Directory integrierten DNS-Zonen in Windows Server 2016 nutzen.

In Windows Server 2016 wird die Unterstützung von DNS-Richtlinien auf Active Directory integrierte DNS-Zonen erweitert. Active Directory Integration bietet dem DNS-Server multiverfügbarkeits Funktionen mit mehreren @ no__t-0master. 

Bisher war es für dieses Szenario erforderlich, dass DNS-Administratoren zwei verschiedene DNS-Server verwalten, die jeweils Dienste für jede Gruppe von Benutzern bereitstellen, intern und extern. Wenn nur einige wenige Datensätze in der Zone Split @ no__t-0geschweiften oder beide Instanzen der Zone (intern und extern) an dieselbe übergeordnete Domäne delegiert wurden, wurde dies zu einer Verwaltungs-rückgängig gemacht.

> [!NOTE]
> - DNS-bereit Stellungen sind unterteilt @ no__t-0brain, wenn zwei Versionen einer einzelnen Zone, eine Version für interne Benutzer im Unternehmens Intranet und eine Version für externe Benutzer –, die üblicherweise Benutzer im Internet sind, vorhanden sind.
> - Das Thema [Verwenden der DNS-Richtlinie für Split-Brain-DNS-Bereitstellung](split-brain-DNS-deployment.md) erläutert, wie Sie DNS-Richtlinien und Zonen Bereiche zum Bereitstellen eines Split @ no__t-1brain-DNS-Systems auf einem einzelnen Windows Server 2016-DNS-Server verwenden können



##  <a name="example-split-brain-dns-in-active-directory"></a>Beispiel: Split @ no__t-0brain DNS in Active Directory

In diesem Beispiel wird ein fiktives Unternehmen ("") verwendet, das eine karrierewebsite unter www.Career.contoso.com verwaltet.

Der Standort verfügt über zwei Versionen: einen für die internen Benutzer, für den interne Auftrags Beiträge verfügbar sind. Diese interne Site ist unter der lokalen IP-Adresse 10.0.0.39 verfügbar. 

Die zweite Version ist die öffentliche Version der gleichen Site, die unter der öffentlichen IP-Adresse 65.55.39.10 verfügbar ist.

Wenn keine DNS-Richtlinie vorhanden ist, muss der Administrator diese beiden Zonen auf separaten Windows Server-DNS-Servern hosten und separat verwalten. 

Mithilfe von DNS-Richtlinien können diese Zonen jetzt auf demselben DNS-Server gehostet werden.

Wenn der DNS-Server für contoso.com Active Directory integriert ist und an zwei Netzwerkschnittstellen lauscht, kann der Configuration Manager-Administrator die Schritte in diesem Thema befolgen, um eine Split @ no__t-0brain-Bereitstellung zu erreichen.

Der DNS-Administrator konfiguriert die DNS-Server Schnittstellen mit den folgenden IP-Adressen.

- Der Netzwerkadapter mit Internet Zugriff wird mit einer öffentlichen IP-Adresse von 208.84.0.53 für externe Abfragen konfiguriert.
- Der Netzwerkadapter mit Intranetzugriff wird mit einer privaten IP-Adresse von 10.0.0.56 für interne Abfragen konfiguriert.

In der folgenden Abbildung ist dieses Szenario dargestellt.

![Integrierte DNS-Bereitstellung mit Split-Brain AD](../../media/DNS-SB-AD/DNS-SB-AD.jpg)

## <a name="how-dns-policy-for-split-brain-dns-in-active-directory-works"></a>Funktionsweise der DNS-Richtlinie für Split @ no__t-0brain-DNS in Active Directory

Wenn der DNS-Server mit den erforderlichen DNS-Richtlinien konfiguriert ist, wird jede Anforderung zur Namensauflösung mit den Richtlinien auf dem DNS-Server ausgewertet.

Die Server Schnittstelle wird in diesem Beispiel als Kriterium für die Unterscheidung zwischen den internen und externen Clients verwendet.

Wenn die Server Schnittstelle, auf der die Abfrage empfangen wird, mit einer der Richtlinien übereinstimmt, wird der zugehörige Zonen Bereich verwendet, um auf die Abfrage zu antworten. 

In unserem Beispiel erhalten die DNS-Abfragen für www.Career.contoso.com, die auf der privaten IP-Adresse (10.0.0.56) empfangen werden, eine DNS-Antwort, die eine interne IP-Adresse enthält. und die DNS-Abfragen, die an der öffentlichen Netzwerkschnittstelle empfangen werden, erhalten eine DNS-Antwort, die die öffentliche IP-Adresse im Standard Zonen Bereich enthält (entspricht der normalen Abfrage Auflösung).  

Die Unterstützung für dynamische DNS-\(ddns @ no__t-1 Updates und Bereinigung wird nur im Standard Zonen Bereich unterstützt. Da die internen Clients vom Standard Zonen Bereich bedient werden, können die DNS-Administratoren von Administratoren die vorhandenen Mechanismen (Dynamic DNS oder static) weiterhin verwenden, um die Datensätze in contoso.com zu aktualisieren. Für nicht-@ no__t-0default-Zonen Bereiche \(, wie z. b. der externe Bereich in diesem Beispiel, ist @ no__t, DDNS oder die Unterstützung von Bereinigung nicht verfügbar.

### <a name="high-availability-of-policies"></a>Hohe Verfügbarkeit von Richtlinien

DNS-Richtlinien sind nicht Active Directory integriert. Aus diesem Grund werden DNS-Richtlinien nicht auf die anderen DNS-Server repliziert, die dieselbe Active Directory integrierte Zone hosten. 

DNS-Richtlinien werden auf dem lokalen DNS-Server gespeichert. Sie können DNS-Richtlinien mithilfe der folgenden Windows PowerShell-Beispiel Befehle problemlos von einem Server zu einem anderen exportieren.

    $policies = Get-DnsServerQueryResolutionPolicy -ZoneName "contoso.com" -ComputerName Server01
    
    $policies |  Add-DnsServerQueryResolutionPolicy -ZoneName "contoso.com" -ComputerName Server02

Weitere Informationen finden Sie in den folgenden Windows PowerShell-Referenz Themen.

- [Get-dnsserverqueryresolutionpolicy](https://docs.microsoft.com/powershell/module/dnsserver/get-dnsserverqueryresolutionpolicy?view=win10-ps)
- [Add-dnsserverqueryresolutionpolicy](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverqueryresolutionpolicy?view=win10-ps)


## <a name="how-to-configure-dns-policy-for-split-brain-dns-in-active-directory"></a>Konfigurieren der DNS-Richtlinie für Split @ no__t-0brain DNS in Active Directory

Zum Konfigurieren der DNS Split-Brain-Bereitstellung mithilfe der DNS-Richtlinie müssen Sie die folgenden Abschnitte verwenden, die ausführliche Konfigurations Anweisungen bereitstellen.

### <a name="add-the-active-directory-integrated-zone"></a>Hinzufügen der integrierten Zone Active Directory

Sie können den folgenden Beispiel Befehl verwenden, um dem DNS-Server die Active Directory integrierte Zone contoso.com hinzuzufügen.

    Add-DnsServerPrimaryZone -Name "contoso.com" -ReplicationScope "Domain" -PassThru

Weitere Informationen finden Sie unter [Add-dnsserverprimaryzone](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverprimaryzone?view=win10-ps).

### <a name="create-the-scopes-of-the-zone"></a>Erstellen der Bereiche der Zone

Sie können diesen Abschnitt verwenden, um die Zone contoso.com zu partitionieren und einen externen Zonen Bereich zu erstellen.

Ein Zonen Bereich ist eine eindeutige Instanz der Zone. Eine DNS-Zone kann über mehrere Zonen Bereiche verfügen, wobei jeder Zonen Bereich einen eigenen Satz von DNS-Einträgen enthält. Derselbe Datensatz kann in mehreren Bereichen mit unterschiedlichen IP-Adressen oder den gleichen IP-Adressen vorhanden sein. 

Da Sie diesen neuen Zonen Bereich in einer Active Directory integrierten Zone hinzufügen, werden der Zonen Bereich und die darin enthaltenen Datensätze über Active Directory auf andere Replikat Server in der Domäne repliziert.

Standardmäßig ist ein Zonen Bereich in jeder DNS-Zone vorhanden. Dieser Zonen Bereich hat denselben Namen wie die Zone, und ältere DNS-Vorgänge funktionieren in diesem Bereich. Dieser Standard Zonen Bereich hostet die interne Version von www.Career.contoso.com.

Sie können den folgenden Beispiel Befehl verwenden, um den Zonen Bereich auf dem DNS-Server zu erstellen.

    Add-DnsServerZoneScope -ZoneName "contoso.com" -Name "external"

Weitere Informationen finden Sie unter [Add-dnsserverzonescope](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverzonescope?view=win10-ps).

### <a name="add-records-to-the-zone-scopes"></a>Hinzufügen von Datensätzen zu den Zonen Bereichen

Der nächste Schritt besteht darin, die Datensätze, die den Webserver Host darstellen, in die beiden Zonen Bereiche "extern" und "Standard" \(für interne Clients @ no__t-1 hinzuzufügen. 

Im Standardbereich der internen Zone wird der Datensatz www.Career.contoso.com mit der IP-Adresse 10.0.0.39 hinzugefügt. Dies ist eine private IP-Adresse. im Bereich der externen Zone wird der gleiche Datensatz @no__t -0www. Karriere. "no__t-1" mit der öffentlichen IP-Adresse 65.55.39.10 hinzugefügt. 

Die Datensätze \(im internen Standard Zonen Bereich und der externe Zonen Bereich @ no__t-1 werden automatisch über die Domäne mit ihren jeweiligen Zonen Bereichen repliziert.

Sie können den folgenden Beispiel Befehl verwenden, um Datensätze zu den Zonen Bereichen auf dem DNS-Server hinzuzufügen.

    Add-DnsServerResourceRecord -ZoneName "contoso.com" -A -Name "www.career" -IPv4Address "65.55.39.10" -ZoneScope "external"
    
    Add-DnsServerResourceRecord -ZoneName "contoso.com" -A -Name "www.career" -IPv4Address "10.0.0.39”

> [!NOTE]
> Der **– zonescope** -Parameter ist nicht eingeschlossen, wenn der Datensatz dem Standard Zonen Bereich hinzugefügt wird. Diese Aktion ist mit dem Hinzufügen von Datensätzen zu einer normalen Zone identisch.

Weitere Informationen finden Sie unter [Add-dnsserverresourcerecord](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverresourcerecord?view=win10-ps).

### <a name="create-the-dns-policies"></a>Erstellen der DNS-Richtlinien

Nachdem Sie die Server Schnittstellen für das externe Netzwerk und das interne Netzwerk ermittelt und die Zonen Bereiche erstellt haben, müssen Sie DNS-Richtlinien erstellen, mit denen die internen und externen Zonen Bereiche verbunden werden.

> [!NOTE]
> In diesem Beispiel wird die Server Schnittstelle \(the-serverInterface-Parameter im Beispiel Befehl unten @ no__t-1 als Kriterium für die Unterscheidung zwischen den internen und externen Clients verwendet. Eine andere Methode zur Unterscheidung zwischen externen und internen Clients besteht darin, Clientsubnetze als Kriterium zu verwenden. Wenn Sie die Subnetze ermitteln können, zu denen die internen Clients gehören, können Sie die DNS-Richtlinie so konfigurieren, dass Sie basierend auf dem clientsubnetz unterschieden wird Informationen zum Konfigurieren der Datenverkehrs Verwaltung mithilfe von clientsubnetzkriterien finden Sie unter [Verwenden der DNS-Richtlinie für die georedundanzbasierte Datenverkehrs Verwaltung mit primären Servern](primary-geo-location.md).

Nachdem Sie Richtlinien konfiguriert haben, wird die Antwort vom externen Bereich der Zone zurückgegeben, wenn eine DNS-Abfrage an der öffentlichen Schnittstelle empfangen wird. 

> [!NOTE]
> Zum Mapping des standardmäßigen internen Zonen Bereichs sind keine Richtlinien erforderlich. 

    Add-DnsServerQueryResolutionPolicy -Name "SplitBrainZonePolicy" -Action ALLOW -ServerInterface "eq,208.84.0.53" -ZoneScope "external,1" -ZoneName contoso.com

> [!NOTE]
> 208.84.0.53 ist die IP-Adresse der öffentlichen Netzwerkschnittstelle.

Weitere Informationen finden Sie unter [Add-dnsserverqueryresolutionpolicy](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverqueryresolutionpolicy?view=win10-ps).

Nun wird der DNS-Server mit den erforderlichen DNS-Richtlinien für einen Split-Brain-Namen Server mit einer Active Directory integrierten DNS-Zone konfiguriert.

Sie können Tausende von DNS-Richtlinien gemäß Ihren Anforderungen für die Datenverkehrs Verwaltung erstellen, und alle neuen Richtlinien werden dynamisch angewendet, ohne dass der DNS-Server bei eingehenden Abfragen neu gestartet wird. 
