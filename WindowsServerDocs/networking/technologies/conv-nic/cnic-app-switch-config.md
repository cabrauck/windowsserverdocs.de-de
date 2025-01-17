---
title: Konfiguration des physischen Switches für konvergierte NIC
description: In diesem Thema erhalten Sie Richtlinien für die Konfiguration physischer Switches.
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 6d53c797-fb67-4b9e-9066-1c9a8b76d2aa
manager: dougkim
ms.author: pashort
author: shortpatti
ms.date: 09/14/2018
ms.openlocfilehash: d10e8ca6e4689b89a8b9532f77613f17280282b1
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71355476"
---
# <a name="physical-switch-configuration-for-converged-nic"></a>Konfiguration des physischen Switches für konvergierte NIC

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In diesem Thema erhalten Sie Richtlinien für die Konfiguration physischer Switches. 


Dabei handelt es sich nur um Befehle und deren Verwendung. Sie müssen die Ports, mit denen die NICs verbunden sind, in Ihrer Umgebung bestimmen. 

>[!IMPORTANT]
>Stellen Sie sicher, dass die VLAN-und die No-Drop-Richtlinie für die Priorität festgelegt ist, über die SMB konfiguriert ist

## <a name="arista-switch-dcs-7050s-64-eos-4137m"></a>Arista Switch \(dcs @ no__t-17050s @ no__t-264, EOS @ no__t-34.13.7 m @ no__t-4

1.  en \(gehe zu Admin-Modus, fordert normalerweise ein Kennwort an (@ no__t-1).
2.  config \(to Enter into Configuration Mode @ no__t-1
3.  Ausführung anzeigen \(zeigt die aktuell aktive Konfiguration @ no__t-1
4.  Suchen Sie die Switchports, mit denen die NICs verbunden sind. In diesem Beispiel lauten Sie 14/1, 15/1, 16/1, 17/1.
5.  int ETH 14/1, 15/1, 16/1, 17/1 \(enter into config Mode für diese Ports @ no__t-1
6.  dcbx-Modus IEEE
7.  Prioritäts Fluss-Steuerungs Modus für
8.  Switchport-trunk natives VLAN 225
9.  Switchport-trunk zulässige VLAN 100-225
10. switchportmodus-trunk
11. Prioritäts Fluss-Steuerungs Priorität 3 nicht ablegen
12. QoS Trust COS
13. Run Show \(vergewissern Sie sich, dass die Konfiguration auf den Ports @ no__t-1 ordnungsgemäß eingerichtet ist.
14. WR \(, damit die Einstellungen über den switchneustart @ no__t-1 beibehalten werden.

### <a name="tips"></a>Chti
1.  Nein #Command # negiert einen Befehl.
2.  Vorgehensweise beim Hinzufügen eines neuen VLANs: int VLAN 100 \(if Storage Network on VLAN 100 @ no__t-1
3.  Überprüfen vorhandener VLANs: VLAN anzeigen
4.  Weitere Informationen zum Konfigurieren des Arista-Schalters finden Sie online nach: Arista EOS manuell
5.  Verwenden Sie diesen Befehl, um die PFC-Einstellungen zu überprüfen: Details der Prioritäts Fluss-Steuerungs Zähler anzeigen

--- 

## <a name="dell-switch-s4810-ftos-99-00"></a>Dell Switch \(s4810, f-9,9 \(0.0 @ no__t-2 @ no__t-3

    
    !
    dcb enable
    ! put pfc control on qos class 3
    configure
    dcb-map dcb-smb
    priority group 0 bandwidth 90 pfc on
    priority group 1 bandwidth 10 pfc off
    priority-pgid 1 1 1 0 1 1 1 1
    exit
    ! apply map to ports 0-31
    configure
    interface range ten 0/0-31
    dcb-map dcb-smb
    exit
    
--- 

## <a name="cisco-switch-nexus-3132-version-602u61"></a>Cisco Switch \(nexus 3132, Version 6.0 @ no__t-12 @ no__t-2u6 @ no__t-31 @ no__t-4 @ no__t-5

### <a name="global"></a>Global
    
    class-map type qos match-all RDMA
    match cos 3
    class-map type queuing RDMA
    match qos-group 3
    policy-map type qos QOS_MARKING
    class RDMA
    set qos-group 3
    class class-default
    policy-map type queuing QOS_QUEUEING
    class type queuing RDMA
    bandwidth percent 50
    class type queuing class-default
    bandwidth percent 50
    class-map type network-qos RDMA
    match qos-group 3
    policy-map type network-qos QOS_NETWORK
    class type network-qos RDMA
    mtu 2240
    pause no-drop
    class type network-qos class-default
    mtu 9216
    system qos
    service-policy type qos input QOS_MARKING
    service-policy type queuing output QOS_QUEUEING
    service-policy type network-qos QOS_NETWORK
    

### <a name="port-specific"></a>Port spezifisch

    
    switchport mode trunk
    switchport trunk native vlan 99
    switchport trunk allowed vlan 99,2000,2050   çuse VLANs that already exists
    spanning-tree port type edge
    flowcontrol receive on (not supported with PFC in Cisco NX-OS)
    flowcontrol send on (not supported with PFC in Cisco NX-OS)
    no shutdown
    priority-flow-control mode on
    
--- 

## <a name="related-topics"></a>Verwandte Themen

- [Konvergierte NIC-Konfiguration mit einem einzelnen Netzwerk Adapter](cnic-single.md)
- [Konvergierte NIC-Konfiguration mit Nic](cnic-datacenter.md)
- [Problembehandlung bei zusammen getauschten NIC](cnic-app-troubleshoot.md)

--- 