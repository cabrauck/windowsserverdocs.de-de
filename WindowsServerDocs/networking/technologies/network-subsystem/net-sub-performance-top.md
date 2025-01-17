---
title: Leistungsoptimierung für das Netzwerksubsystem
description: Dieses Thema ist Teil des Handbuch zur Leistungsoptimierung des Netzwerk Subsystems für Windows Server 2016.
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 45217fce-bfb9-47e8-9814-88ffdb3c7b7d
manager: brianlic
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 02a1abc9de04926740309081397e0bd92fe74b88
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71401901"
---
# <a name="network-subsystem-performance-tuning"></a>Leistungsoptimierung für das Netzwerksubsystem

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In diesem Thema finden Sie eine Übersicht über das Netzwerk Subsystem und Links zu anderen Themen in diesem Handbuch.

>[!NOTE]
>Zusätzlich zu diesem Thema enthalten die folgenden Abschnitte dieses Handbuchs Empfehlungen zur Leistungsoptimierung für Netzwerkgeräte und den Netzwerk Stapel.
> - [Auswählen eines Netzwerkadapters](net-sub-choose-nic.md)
> - [Konfigurieren der Reihenfolge von Netzwerkschnittstellen](net-sub-interface-metric.md)
> - [Leistungsoptimierung für Netzwerkadapter](net-sub-performance-tuning-nics.md)
> - [Netzwerkbezogene Leistungsindikatoren](net-sub-performance-counters.md)
> - [Leistungstools für Netzwerkworkloads](net-sub-performance-tools.md)

Die Leistungsoptimierung des Netzwerk Subsystems, insbesondere für Netzwerk intensive Workloads, kann jede Schicht der Netzwerkarchitektur beinhalten, die auch als Netzwerk Stapel bezeichnet wird. Diese Ebenen sind weitgehend in die folgenden Abschnitte unterteilt.

1. **Netzwerkschnittstelle**. Dies ist die niedrigste Ebene im Netzwerk Stapel und enthält den Netzwerktreiber, der direkt mit dem Netzwerkadapter kommuniziert.

2. **Network Driver Interface Specification (NDIS)** . NDIS macht Schnittstellen für den darunter liegenden Treiber und für die Ebenen oberhalb, z. b. den Protokollstapel, verfügbar.
  
3. **Protokollstapel**. Der Protokollstapel implementiert Protokolle wie TCP/IP und UDP/IP. Diese Ebenen machen die Transportschicht Schnittstelle für Ebenen oberhalb verfügbar.
  
4. **System Treiber**. Dabei handelt es sich in der Regel um Clients, die eine Schnittstelle für Transportdaten Erweiterung (TDX) oder Winsock Kernel (WSK) verwenden, um Schnittstellen für Benutzermodusanwendungen bereitzustellen Die WSK-Schnittstelle wurde in Windows Server 2008 und Windows @ no__t-0 Vista eingeführt und wird von Afd. sys bereitgestellt. Die-Schnittstelle verbessert die Leistung, indem der Wechsel zwischen Benutzermodus und Kernel Modus entfällt.
  
5. **Benutzermodusanwendungen**. Dies sind in der Regel Microsoft-Lösungen oder benutzerdefinierte Anwendungen.

Die folgende Tabelle enthält eine vertikale Darstellung der Ebenen des Netzwerk Stapels, einschließlich Beispielen für Elemente, die auf jeder Ebene ausgeführt werden.  

![Netzwerk Stapel Schichten](../../media/Network-Subsystem/network-layers.jpg)

