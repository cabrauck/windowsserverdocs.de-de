---
title: Planen der Verwendung von vrss
description: Sie können dieses Thema verwenden, um den virtuellen Computer und den Hyper-V-Host für die Verwendung von vrss in Windows Server 2016 vorzubereiten.
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: 695e6192-5e84-4ab4-b33e-8ebf6b8f5cbb
ms.localizationpriority: medium
manager: dougkim
ms.author: pashort
author: shortpatti
ms.date: 09/04/2018
ms.openlocfilehash: 3addb500a654ff9f23c56388fec3ef2c3855a1da
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71395821"
---
# <a name="plan-the-use-of-vrss"></a>Planen der Verwendung von vrss

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In Windows Server 2016 ist vrss standardmäßig aktiviert. Sie müssen jedoch Ihre Umgebung vorbereiten, damit vrss auf dem virtuellen Computer \(vm @ no__t-1 oder auf einem virtuellen Host Adapter \(vnic @ no__t-3 ordnungsgemäß funktioniert. In Windows Server 2012 R2 war vrss standardmäßig deaktiviert.

Wenn Sie die Verwendung von vrss planen und vorbereiten, stellen Sie Folgendes sicher:

- Der physische Netzwerkadapter ist mit Warteschlange für virtuelle Computer \(vmq @ no__t-1 kompatibel und weist eine Verbindungsgeschwindigkeit von 10 Gbit/s oder mehr auf.
- VMQ ist auf der physischen NIC und auf dem virtuellen Switch-Port von Hyper @ no__t-0V aktiviert.
- Für den virtuellen Computer ist kein Single root Input @ no__t-0output Virtualization \(sr @ no__t-2iov @ no__t-3 konfiguriert.
- Der NIC-Team Vorgang ist ordnungsgemäß konfiguriert.
- Der virtuelle Computer verfügt über mehrere logische Prozessoren \(lps @ no__t-1.

>[!NOTE]
>vrss ist standardmäßig auch für alle Host-vNICs aktiviert, für die RSS aktiviert ist.

Im folgenden finden Sie weitere Informationen, die Sie benötigen, um diese Vorbereitungsschritte abzuschließen.
  
1. **Kapazität des Netzwerkadapters**. Vergewissern Sie sich, dass der Netzwerkadapter mit Warteschlange für virtuelle Computer \(vmq @ no__t-1 kompatibel ist und eine Verbindungsgeschwindigkeit von 10 Gbit/s oder mehr aufweist. Wenn die Verbindungsgeschwindigkeit weniger als 10 Gbit/s beträgt, deaktiviert der virtuelle Hyper @ no__t-0V-Switch VMQ standardmäßig, obwohl VMQ weiterhin in den Ergebnissen des Windows PowerShell-Befehls **Get-netadaptervmq**als aktiviert angezeigt wird. Eine Methode, die Sie verwenden können, um zu überprüfen, ob VMQ aktiviert oder deaktiviert ist, besteht darin, den Befehl **Get-netadaptervmqqueue**zu verwenden.  Wenn VMQ deaktiviert ist, zeigen die Ergebnisse dieses Befehls, dass dem virtuellen Computer oder dem virtuellen Netzwerkadapter des Hosts keine QueueId zugewiesen ist. 
  
2. **Aktivieren Sie VMQ**. Überprüfen, Sie ob VMQ auf dem Hostcomputer aktiviert ist. vrss funktioniert nicht, wenn VMQ vom Host nicht unterstützt wird. Sie können überprüfen, ob VMQ aktiviert ist, indem Sie **Get-VMSwitch** ausführen und den Adapter suchen, der vom virtuellen Switch verwendet wird. Führen Sie als Nächstes **Get-NetAdapterVmq** aus, und stellen Sie sicher, dass der Adapter in den Ergebnissen angezeigt wird und dass VMQ für den Adapter aktiviert ist.
  
3. **Fehlende SR @ no__t-1iov**. Vergewissern Sie sich, dass eine einzelne Stamm Eingabe @ no__t-0output Virtualization \(sr @ no__t-2iov @ no__t-3 Virtual Function \(VF @ no__t-5 Driver nicht an die VM-Netzwerkschnittstelle angefügt ist. Dies können Sie mit dem Befehl **Get-netadaptersriov** überprüfen. Wenn ein VF-Treiber geladen wird, verwendet RSS die Skalierungs Einstellungen aus diesem Treiber anstelle der von vrss konfigurierten. Wenn der VF-Treiber RSS nicht unterstützt, wird vrss deaktiviert.
  
4. **Konfiguration des NIC**-Team Vorgangs. Wenn Sie NIC-Team Vorgänge verwenden, ist es wichtig, dass Sie VMQ ordnungsgemäß konfigurieren, damit Sie mit den NIC-Team Vorgangs Einstellungen arbeiten können. Ausführliche Informationen zur Bereitstellung und Verwaltung von NIC-Teaming finden Sie unter [NIC](https://docs.microsoft.com/windows-server/networking/technologies/nic-teaming/nic-teaming)-Team Vorgang.

5. **Anzahl der LPs**. Vergewissern Sie sich, dass der virtuelle Computer über mehrere logische Prozessoren verfügt \(lp @ no__t-1. vrss basiert auf RSS auf dem virtuellen Computer oder auf dem Hyper-V-Host, um einen Lastenausgleich für den empfangenen Datenverkehr auf mehrere LPs zur parallelen Verarbeitung durchzusetzen. Sie können die Anzahl der LPs Ihres virtuellen Computers beobachten, indem Sie den Windows PowerShell-Befehl **Get-vmprocessor** auf dem Host ausführen. Nachdem Sie den Befehl ausgeführt haben, können Sie den Eintrag für die Anzahl der-Spalten in der Anzahl der LPs beobachten.

Die Host-vNIC hat immer Zugriff auf alle physischen Prozessoren. um die Host-vNIC für die Verwendung einer bestimmten Anzahl von Prozessoren zu konfigurieren, verwenden Sie die Einstellungen **-baseprocessornumber** und **-maxprocessor** , wenn Sie den Windows PowerShell-Befehl **Set-netadapterrss** ausführen.

---