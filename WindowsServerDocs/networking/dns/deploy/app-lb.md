---
title: Verwenden der DNS-Richtlinie für den Anwendungslastenausgleich
description: Dieses Thema ist Teil des DNS-Richtlinien szenariohandbuchs für Windows Server 2016.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-dns
ms.topic: article
ms.assetid: f9c313ac-bb86-4e48-b9b9-de5004393e06
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 356c61c2cc5b60f43a69f17966c97f3c69d05cda
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71356041"
---
# <a name="use-dns-policy-for-application-load-balancing"></a>Verwenden der DNS-Richtlinie für den Anwendungslastenausgleich

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In diesem Thema erfahren Sie, wie Sie eine DNS-Richtlinie für den Anwendungs Lastenausgleich konfigurieren.

In früheren Versionen von Windows Server-DNS wurde nur ein Lastenausgleich mithilfe von Roundrobin-Antworten bereitgestellt. mit DNS in Windows Server 2016 können Sie jedoch die DNS-Richtlinie für den Anwendungs Lastenausgleich konfigurieren.

Wenn Sie mehrere Instanzen einer Anwendung bereitgestellt haben, können Sie die DNS-Richtlinie verwenden, um die Auslastung des Datenverkehrs zwischen den verschiedenen Anwendungs Instanzen auszugleichen, wodurch die Auslastung des Datenverkehrs für die Anwendung dynamisch zugeordnet wird.

## <a name="example-of-application-load-balancing"></a>Beispiel für den Anwendungs Lastenausgleich

Im folgenden finden Sie ein Beispiel für die Verwendung der DNS-Richtlinie für den Anwendungs Lastenausgleich.

In diesem Beispiel wird ein fiktives Unternehmen mit der Bezeichnung "contosogiftservices.com" verwendet, das Online-gifing-Dienste bereitstellt und über eine Website mit dem Namen "" verfügt.

Die contosogiftservices.com-Website wird in mehreren Rechenzentren gehostet, die jeweils über unterschiedliche IP-Adressen verfügen.

In Nordamerika, der der primäre Markt für die Dienstleistungen von "Configuration Manager" ist, wird die Website in drei Rechenzentren gehostet: Chicago, IL, Dallas, TX und Seattle, WA.

Der Seattle-Webserver verfügt über die beste Hardwarekonfiguration und kann doppelt so viel Last wie die anderen beiden Standorte verarbeiten. Der Anwendungs Datenverkehr wird von den Dienstleistungen von "Configuration Manager" wie folgt gesteuert.

- Da der Seattle-Webserver weitere Ressourcen enthält, werden die Hälfte der Client Clients an diesen Server weitergeleitet.
- Ein Viertel der Clients der Anwendung wird an das Dallas, TX Datacenter, geleitet.
- Ein Viertel der Clients der Anwendung wird an Chicago, IL, Datacenter geleitet.

In der folgenden Abbildung ist dieses Szenario dargestellt.

![DNS-Anwendungs Lastenausgleich mit DNS-Richtlinie](../../media/Dns-App-Lb/dns-app-lb.jpg)


### <a name="how-application-load-balancing-works"></a>Funktionsweise des Anwendungs Lastenausgleichs

Nachdem Sie den DNS-Server mit der DNS-Richtlinie für den Anwendungs Lastenausgleich unter Verwendung dieses Beispiel Szenarios konfiguriert haben, antwortet der DNS-Server 50% der Zeit mit der Adresse des Webservers in Seattle, 25% der Zeit mit der Adresse des Dallas-Webservers und 25% der Zeit mit die Adresse des Chicago-Webservers.

Für alle vier Abfragen, die der DNS-Server empfängt, antwortet der DNS-Server daher mit zwei Antworten für Seattle und einem einzelnen für Dallas und Chicago.

Ein mögliches Problem beim Lastenausgleich mit der DNS-Richtlinie ist die Zwischenspeicherung von DNS-Einträgen durch den DNS-Client und die Konflikt Löser/ldns, die den Lastenausgleich beeinträchtigen können, da der Client oder der Konflikt Löser keine Abfrage an den DNS-Server sendet.

Sie können die Auswirkung dieses Verhaltens verringern, indem Sie für die DNS-Einträge, für die ein Lastenausgleich ausgeführt werden soll, einen Wert für den Wert "niedrige Zeit @ no__t-0to @ no__t-1Live \(ttl @ no__t-3" verwenden.

### <a name="how-to-configure-application-load-balancing"></a>Konfigurieren des Anwendungs Lastenausgleichs

In den folgenden Abschnitten wird gezeigt, wie Sie die DNS-Richtlinie für den Anwendungs Lastenausgleich konfigurieren.

#### <a name="create-the-zone-scopes"></a>Erstellen der Zonen Bereiche

Sie müssen zunächst die Bereiche der Zone contosogiftservices.com für die Rechenzentren erstellen, in denen Sie gehostet werden.

Ein Zonen Bereich ist eine eindeutige Instanz der Zone. Eine DNS-Zone kann über mehrere Zonen Bereiche verfügen, wobei jeder Zonen Bereich einen eigenen Satz von DNS-Einträgen enthält. Derselbe Datensatz kann in mehreren Bereichen mit unterschiedlichen IP-Adressen oder den gleichen IP-Adressen vorhanden sein.

>[!NOTE]
>In den DNS-Zonen ist standardmäßig ein Zonen Bereich vorhanden. Dieser Zonen Bereich hat denselben Namen wie die Zone, und ältere DNS-Vorgänge funktionieren in diesem Bereich.

Sie können die folgenden Windows PowerShell-Befehle verwenden, um Zonen Bereiche zu erstellen.
    
    Add-DnsServerZoneScope -ZoneName "contosogiftservices.com" -Name "SeattleZoneScope"
    
    Add-DnsServerZoneScope -ZoneName "contosogiftservices.com" -Name "DallasZoneScope"
    
    Add-DnsServerZoneScope -ZoneName "contosogiftservices.com" -Name "ChicagoZoneScope"

Weitere Informationen finden Sie unter [Add-dnsserverzonescope](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverzonescope?view=win10-ps) .

#### <a name="bkmk_records"></a>Hinzufügen von Datensätzen zu den Zonen Bereichen

Nun müssen Sie die Datensätze, die den Webserver Host darstellen, zu den Zonen Bereichen hinzufügen.

Sie können in " **czonescope**" den Datensatz www.contosogiftservices.com mit der IP-Adresse 192.0.0.1 hinzufügen, die sich im Daten Center Seattle befindet.

In " **chicagozonescope**" können Sie denselben Datensatz hinzufügen @no__t -1www. Conto sogiftservices. com @ no__t-2 with IP Address 182.0.0.1 im Chicago Datacenter.

Auf ähnliche Weise können Sie in **dallaszonescope**einen Datensatz @no__t -1www. Conto sogiftservices. com @ no__t-2 mit IP-Adresse 162.0.0.1 im Chicago-Daten Center hinzufügen.

Sie können die folgenden Windows PowerShell-Befehle verwenden, um Datensätze zu den Zonen Bereichen hinzuzufügen.
    
    Add-DnsServerResourceRecord -ZoneName "contosogiftservices.com" -A -Name "www" -IPv4Address "192.0.0.1" -ZoneScope "SeattleZoneScope
    
    Add-DnsServerResourceRecord -ZoneName "contosogiftservices.com" -A -Name "www" -IPv4Address "182.0.0.1" -ZoneScope "ChicagoZoneScope"
    
    Add-DnsServerResourceRecord -ZoneName "contosogiftservices.com" -A -Name "www" -IPv4Address "162.0.0.1" -ZoneScope "DallasZoneScope"
    

Weitere Informationen finden Sie unter [Add-dnsserverresourcerecord](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverresourcerecord?view=win10-ps).

#### <a name="bkmk_policies"></a>Erstellen der DNS-Richtlinien

Nachdem Sie die Partitionen (Zonen Bereiche) erstellt und Datensätze hinzugefügt haben, müssen Sie DNS-Richtlinien erstellen, die die eingehenden Abfragen über diese Bereiche verteilen, damit 50% der Abfragen für contosogiftservices.com mit der IP-Adresse für das Web beantwortet werden. der Server im Daten Center Seattle und der Rest sind gleichmäßig auf die Daten Center Chicago und Dallas verteilt.

Mithilfe der folgenden Windows PowerShell-Befehle können Sie eine DNS-Richtlinie erstellen, die den Anwendungs Datenverkehr in diesen drei Rechenzentren ausgleicht.

>[!NOTE]
>Im Beispiel Befehl unten ist der Ausdruck "– zonescope", 2; Chicagozonescope, 1; Dallaszonescope, 1 "konfiguriert den DNS-Server mit einem Array, das die Parameter Kombination \<zonescope @ no__t-1, \<weight @ no__t-3 enthält.
    
    Add-DnsServerQueryResolutionPolicy -Name "AmericaPolicy" -Action ALLOW -ZoneScope "SeattleZoneScope,2;ChicagoZoneScope,1;DallasZoneScope,1" -ZoneName "contosogiftservices.com"
    

Weitere Informationen finden Sie unter [Add-dnsserverqueryresolutionpolicy](https://docs.microsoft.com/powershell/module/dnsserver/add-dnsserverqueryresolutionpolicy?view=win10-ps).  

Sie haben nun erfolgreich eine DNS-Richtlinie erstellt, die den Anwendungs Lastenausgleich über Webserver in drei verschiedenen Rechenzentren hinweg ermöglicht.

Sie können Tausende von DNS-Richtlinien gemäß Ihren Anforderungen für die Datenverkehrs Verwaltung erstellen, und alle neuen Richtlinien werden dynamisch angewendet, ohne dass der DNS-Server bei eingehenden Abfragen neu gestartet wird.
