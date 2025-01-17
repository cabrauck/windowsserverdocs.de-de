---
title: Neues in DHCP
description: Dieses Thema enthält eine Übersicht über die neuen Features für DHCP (Dynamic Host Configuration Protocol) in Windows Server 2016.
manager: brianlic
ms.prod: windows-server
ms.technology: networking-dhcp
ms.topic: get-started-article
ms.assetid: c6f36998-5b64-45d1-b1f0-0f0d6604dbe3
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 8032b7c8e78170d57b0367775672577d9fd900e2
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71355451"
---
# <a name="whats-new-in-dhcp"></a>Neues in DHCP

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In diesem Thema werden die DHCP-Funktionen (Dynamic Host Configuration Protocol) beschrieben, die in Windows Server 2016 neu oder geändert wurden.
  
DHCP ist ein IETF (Internet Engineering Task Force)-Standard, der den Verwaltungsaufwand und die Komplexität beim Konfigurieren von Hosts in einem TCP/IP @ no__t-basierten Netzwerk, wie z. b. einem privaten Intranet, reduziert. Der DHCP-Serverdienst führt den Konfigurationsprozess für TCP/IP auf DHCP-Clients automatisch durch.

In den folgenden Abschnitten finden Sie Informationen zu neuen Features und Funktionsänderungen für DHCP.

## <a name="dhcp-subnet-selection-options"></a>Optionen für das DHCP-subnetzauswahl

DHCP unterstützt nun die Optionen 118 und 82 \(sub-Option 5 @ no__t-1. Mithilfe dieser Optionen können Sie DHCP-Proxy Clients und Relay-Agents gestatten, eine IP-Adresse für ein bestimmtes Subnetz und einen bestimmten IP-Adressbereich und-Bereich anzufordern.


Wenn Sie einen DHCP-Relay-Agent verwenden, der mit der DHCP-Option 82, Sub @ no__t-0option 5 konfiguriert ist, kann der Relay-Agent eine IP-Adress Lease für DHCP-Clients von einem bestimmten IP-Adressbereich anfordern.

Weitere Informationen finden Sie unter [Auswahl Optionen für das DHCP-Subnetz](dhcp-subnet-options.md).

## <a name="new-logging-events-for-dns-registration-failures-by-the-dhcp-server"></a>Neue Protokollierungs Ereignisse für DNS-Registrierungsfehler durch den DHCP-Server

DHCP umfasst nun Protokollierungs Ereignisse für Situationen, in denen DHCP-Server-DNS-Einträge auf dem DNS-Server fehlschlagen.

Weitere Informationen finden Sie unter [DHCP-Protokollierungs Ereignisse für DNS-Daten Satz Registrierungen](dhcp-dns-events.md).

## <a name="dhcp-nap-is-not-supported-in-windows-server-2016"></a>DHCP-NAP wird in Windows Server 2016 nicht unterstützt.

Der Netzwerk Zugriffsschutz \(nap @ no__t-1 ist in Windows Server 2012 R2 veraltet, und in Windows Server 2016 unterstützt die DHCP-Server Rolle NAP nicht mehr. Weitere Informationen finden Sie unter [in Windows Server 2012 R2 entfernte oder veraltete Features](https://technet.microsoft.com/library/dn303411.aspx).  
  
Die NAP-Unterstützung wurde mit Windows Server 2008 in die DHCP-Server Rolle eingeführt und wird in Windows-Client-und Server Betriebssystemen vor Windows 10 und Windows Server 2016 unterstützt. In der folgenden Tabelle wird die Unterstützung für NAP in Windows Server zusammengefasst.  
  
|Betriebssystem|NAP-Unterstützung|  
|--------------------|---------------|  
| WindowsServer 2008 |Unterstützt|  
| Windows Server 2008 R2 |Unterstützt|  
| Windows Server 2012 |Unterstützt|  
| Windows Server 2012 R2 |Unterstützt|  
| Windows Server 2016|Nicht unterstützt.|  
  
In einer NAP-Bereitstellung kann ein DHCP-Server mit einem Betriebssystem, das NAP unterstützt, als NAP-Erzwingungs Punkt für die NAP-Erzwingungs Methode fungieren. Weitere Informationen zu DHCP in NAP finden Sie unter [checkliste: Implementieren eines DHCP-Erzwingungs Entwurfs @ no__t-0.  
  
In Windows Server 2016 erzwingen DHCP-Server keine NAP-Richtlinien, und DHCP-Bereiche können nicht NAP @ no__t-0aktiviert werden. DHCP-Client Computer, die auch NAP-Clients sind, senden ein Statement of Health-\(soh @ no__t-1 mit der DHCP-Anforderung. Wenn auf dem DHCP-Server Windows Server 2016 ausgeführt wird, werden diese Anforderungen so verarbeitet, als ob kein SoH vorhanden ist. Der DHCP-Server gewährt dem Client eine normale DHCP-Lease. 

Wenn Server, auf denen Windows Server 2016 ausgeführt wird, RADIUS-Proxys sind, die Authentifizierungsanforderungen an einen Netzwerk Richtlinien Server weiterleiten \(nps @ no__t-1, der NAP unterstützt, werden diese NAP-Clients von NPS als nicht-NAP @ no__t-fähig ausgewertet, und die NAP-Verarbeitung schlägt fehl.
  
## <a name="see-also"></a>Siehe auch  
  
-   [Dynamic Host Configuration-Protokoll (DHCP)](Dynamic-Host-Configuration-Protocol--DHCP-.md)  
  

