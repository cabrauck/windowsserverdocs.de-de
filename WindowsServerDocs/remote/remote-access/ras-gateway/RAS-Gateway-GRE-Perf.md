---
title: RAS-Gateway GRE-Tunneling Durchsatz und Leistung
description: Dieses Thema, das für IT-Experten gedacht ist, bietet Durchsatz-Leistungsinformationen zu den RAS-Tunneln (Generic Routing Kapselung) des RAS-Gateways.
manager: brianlic
ms.prod: windows-server
ms.date: ''
ms.technology: networking-ras
ms.topic: article
ms.assetid: c051b2ec-de0f-49d1-82b9-5742b259cd7c
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 79a6e822c3ff36f789a7a08b8cd56163014185a4
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71404684"
---
# <a name="ras-gateway-gre-tunnel-throughput-and-performance"></a>RAS-Gateway GRE-Tunneling Durchsatz und Leistung

>Gilt für: Windows Server \(halbjährlicher Kanal @ no__t-1

In diesem Thema erfahren Sie mehr über RAS-Server \(ras @ no__t-1 Gateway generische Routing Kapselung \(gre @ no__t-3-Tunnel Leistung unter Windows Server, Version 1709, in einem nicht von Software definierten Netzwerk \(sdn @ no__t-5-basierter Test Umgebung.

RAS-Gateway ist ein Software Router und ein Gateway, das Sie im Einzel Mandanten Modus oder im mehr Instanzen fähigen Modus verwenden können. In diesem Thema wird eine Konfiguration mit einem einzelnen Mandanten Modus mit hoher Verfügbarkeit und Failoverclustering behandelt. Die in diesem Thema dargestellten GRE-Tunnel Leistungsstatistiken gelten für das RAS-Gateway sowohl für den Singele-Mandanten als auch für den mehr Instanzen fähigen Modus.

>[!NOTE]
>Failoverclustering ist eine Windows Server-Funktion, mit der Sie mehrere Server in einem fehlertoleranten Cluster gruppieren können. Weitere Informationen finden Sie unter [Failover-Clustering](../../../failover-clustering/failover-clustering-overview.md) .

Der Einzel Mandanten Modus ermöglicht Organisationen beliebiger Größe das Bereitstellen des Gateways als Außendienst oder Internet @ no__t-0edge Virtual Private Network \(VPN @ no__t-2 Server. Im Einzel Mandanten Modus können Sie das RAS-Gateway auf einem physischen Server oder virtuellen Computer \(vm @ no__t-1 bereitstellen. In diesem Thema wird die Bereitstellung des RAS-Gateways auf zwei Virtual Machines \(vms @ no__t-1 beschrieben, die in einem Failovercluster konfiguriert sind.

>[!IMPORTANT]
>Da GRE-Tunnel Kapselung, aber keine Verschlüsselung bereitstellen, sollten Sie das mit GRE konfigurierte RAS-Gateway nicht als Internet Edge-Gateway verwenden. Informationen zu den besten Verwendungsmöglichkeiten für das RAS-Gateway mit GRE-Tunneln finden Sie unter [GRE-Tunnelung in Windows Server](gre-tunneling-windows-server.md).

GRE ist ein Lightweight-Tunnelingprotokoll, das eine Vielzahl von Protokollen der Netzwerkschicht innerhalb von virtuellen Punkten no__t-0bis @ no__t-1 Point-Links über ein Internet Protokoll-Internetzwerk Kapseln kann. Die Microsoft GRE-Implementierung kapselt sowohl IPv4 als auch IPv6.

Weitere Informationen finden Sie im Abschnitt **Bereitstellungs Szenarien für RAS-Gateways** im Thema [RAS-Gateway](https://docs.microsoft.com/windows-server/remote/remote-access/ras-gateway/ras-gateway#bkmk_deploy). 

In diesem Testszenario, das in der folgenden Abbildung dargestellt wird, wird der gemessene Daten Verkehrsfluss vom Unternehmens Intranet 2 in das Unternehmens Intranet 1 verlagert. Virtuelle Computer für die Arbeitsauslastung von Mandanten senden Netzwerk Datenverkehr von Intranet 2 an Intranet 1 mithilfe des RAS-Gateways.

![Übersicht über das RAS-tunneltest Szenario des RAS-Gateways](../../media/GRE-Tunnel-Perf/Gre-Infrastructure.jpg)

## <a name="test-environment-configuration"></a>Konfiguration der Test Umgebung

Dieser Abschnitt enthält Informationen über die Testumgebung und die Konfiguration des RAS-Gateways.

In der Testumgebung werden RAS-Gateway-VMS auf Hyper @ no__t-0V-Hosts in einem Failovercluster bereitgestellt, um Hochverfügbarkeit zu erhalten.

### <a name="hyper-v-host-configuration"></a>Hyper @ no__t-0V-Host Konfiguration

Zwei Hyper @ no__t-0V-Hosts werden so konfiguriert, dass das Testszenario auf folgende Weise unterstützt wird. 

- Zwei mit Dual @ no__t 0vernetzte physische Computer werden mit Windows Server, Version 1709, konfiguriert.
- Die beiden physischen Netzwerkadapter auf jedem der beiden Server sind mit unterschiedlichen Subnetzwerken verbunden, die beide Subnetze eines Unternehmensintranets darstellen. Sowohl Netzwerke als auch unterstützende Hardware verfügen über eine Kapazität von 10 Gbit/s.
- Hyperthreading auf den physischen Servern ist deaktiviert. Dies ermöglicht den maximalen Durchsatz von den physischen NICs.
- Die Hyper @ no__t-0V-Server Rolle wird auf beiden Servern installiert und mit zwei externen virtuellen Hyper @ no__t-1V-Switches konfiguriert, eine für jeden physischen Netzwerkadapter.
- Da beide Server mit demselben Intranet verbunden sind, können die Server miteinander kommunizieren.
- Die Hyper @ no__t-0V-Hosts werden in einem Failovercluster über das Intranet-Netzwerk konfiguriert. 

>[!NOTE]
>Weitere Informationen finden Sie unter [Hyper-V Virtual Switch](https://docs.microsoft.com/windows-server/virtualization/hyper-v-virtual-switch/hyper-v-virtual-switch).

### <a name="vm-configuration"></a>VM-Konfiguration

Zwei virtuelle Computer werden so konfiguriert, dass das Testszenario auf folgende Weise unterstützt wird.

- Auf jedem Server wird ein virtueller Computer installiert, auf dem Windows Server, Version 1709, ausgeführt wird. Jeder virtuelle Computer ist mit 10 Kernen und 8 GB RAM konfiguriert.
- Jeder virtuelle Computer wird auch mit zwei virtuellen Netzwerkadaptern konfiguriert. Ein virtueller Netzwerkadapter ist mit dem virtuellen Switch für intranet1 verbunden, und der andere virtuelle Netzwerkadapter ist mit dem virtuellen Switch für intranet2 verbunden.
- Auf jedem virtuellen Computer ist das RAS-Gateway installiert und als GRE @ no__t-0basierter VPN-Server konfiguriert.
- Die Gateway-VMS werden in einem Failovercluster konfiguriert. Wenn Sie gruppiert sind, ist eine VM aktiv, und die andere VM ist passiv.

### <a name="workload-hyper-v-hosts-and-vms"></a>Arbeitsauslastung Hyper @ no__t-0V-Hosts und-VMS

Für diesen Test werden zwei Arbeits Auslastungen vom Typ "Hyper @ no__t-0V" im Intranet installiert, und jeder Host verfügt über eine installierte VM. Wenn Sie diesen Test in ihrer eigenen Testumgebung duplizieren, können Sie so viele Arbeits Auslastungs Server und VMS installieren, wie es für Ihre Zwecke geeignet ist.

- Bei der Arbeitsauslastung von Hyper @ no__t-0V-Hosts ist ein physischer Netzwerkadapter installiert, der mit dem Unternehmens Intranet verbunden ist.
- In Hyper @ no__t-0V Virtual Switch wird ein virtueller Switch auf jedem Host erstellt. Der Switch ist extern und wird an den Netzwerkadapter gebunden, der mit dem Intranet verbunden ist.
- Die Arbeits Auslastungs-VMS werden mit 2 GB RAM und 2 Kernen konfiguriert.
- Die Arbeits Auslastungs-VMS verfügen jeweils über einen virtuellen Netzwerkadapter, der mit dem virtuellen Intranet-Switch verbunden ist.

### <a name="traffic-generator-tool"></a>Traffic Generator-Tool

Das Tool für den Datenverkehrs Generator, das in diesem Test verwendet wird, ist das ctstraffic-Tool. Das git-Repository für dieses Tool befindet sich auf [https://github.com/Microsoft/ctsTraffic](https://github.com/Microsoft/ctsTraffic).

## <a name="ras-gateway-performance"></a>Leistung des RAS-Gateways

In den Abbildungen in diesem Abschnitt werden die Task-Manager-anzeigen von GRE-Tunnel Durchsatz mit mehreren TCP-Verbindungen dargestellt.

Sie können einen Durchsatz von bis zu 2,0 Gbit/s auf virtuellen Computern mit mehreren @ no__t 0core erzielen, die als GRE-RAS-Gateways konfiguriert sind.

### <a name="gre-tunnel-performance-with-multiple-tcp-sessions"></a>GRE-Tunnel Leistung mit mehreren TCP-Sitzungen

Bei mehreren TCP-Sitzungen erreicht die CPU-Auslastung 100%, und der maximale Durchsatz im GRE-Tunnel beträgt 2,0 Gbit/s.

In der folgenden Abbildung wird die CPU-Auslastung für beide RAS-Gateway-VMS dargestellt. Die aktive VM, RAS-Gateway-VM-#1, befindet sich auf der linken Seite, während sich die passive VM, RAS-Gateway-VM #2, auf der rechten Seite befindet.

![CPU-Auslastung des Gateway-VM im Task-Manager](../../media/GRE-Tunnel-Perf/Gre-Tunnel-01.jpg)

In der folgenden Abbildung wird der Ethernet-Netzwerk Durchsatz auf den virtuellen RAS-Gateway-Computern dargestellt Die aktive VM, RAS-Gateway-VM-#1, befindet sich auf der linken Seite, während sich die passive VM, RAS-Gateway-VM #2, auf der rechten Seite befindet.

![Netzwerk Durchsatz für Gateway-VM-Ethernet im Task-Manager](../../media/GRE-Tunnel-Perf/Gre-Tunnel-02.jpg)


### <a name="gre-tunnel-performance-with-one-tcp-connection"></a>GRE-Tunnel Leistung mit einer TCP-Verbindung

Wenn die Testkonfiguration von mehreren TCP-Sitzungen in eine einzelne TCP-Sitzung geändert wurde, erreicht nur ein CPU-Kern die maximale Kapazität der RAS-Gateway-VMS.

Der maximale Durchsatz im GRE-Tunnel liegt zwischen 400-500 Mbit/s.

In der folgenden Abbildung wird die CPU-Auslastung für beide RAS-Gateway-VMS dargestellt. Die aktive VM, RAS-Gateway-VM-#1, befindet sich auf der linken Seite, während sich die passive VM, RAS-Gateway-VM #2, auf der rechten Seite befindet.

![CPU-Auslastung des Gateway-VM im Task-Manager](../../media/GRE-Tunnel-Perf/Gre-Tunnel-03.jpg)


In der folgenden Abbildung wird der Ethernet-Netzwerk Durchsatz auf den virtuellen RAS-Gateway-Computern dargestellt Die aktive VM, RAS-Gateway-VM-#1, befindet sich auf der linken Seite, während sich die passive VM, RAS-Gateway-VM #2, auf der rechten Seite befindet.

![Netzwerk Durchsatz für Gateway-VM-Ethernet im Task-Manager](../../media/GRE-Tunnel-Perf/Gre-Tunnel-04.jpg)

Weitere Informationen zur Leistung des RAS-Gateways finden Sie unter [HNV Gateway Performance Tuning in Software Defined Networks](https://docs.microsoft.com/windows-server/administration/performance-tuning/subsystem/software-defined-networking/hnv-gateway-performance).