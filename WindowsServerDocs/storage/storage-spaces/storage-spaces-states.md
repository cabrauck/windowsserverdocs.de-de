---
title: Integritäts-und Betriebsstatus direkte Speicherplätze
description: Erfahren Sie, wie Sie die verschiedenen Integritäts-und Betriebszustände von direkte Speicherplätze und Speicherplätzen (einschließlich physischer Datenträger, Pools und virtueller Datenträger) finden und verstehen können.
keywords: Speicherplätze, getrennt, virtueller Datenträger, physischer Datenträger, heruntergestuft
author: jasongerend
ms.author: jgerend
ms.date: 10/17/2018
ms.topic: article
ms.prod: windows-server
ms.technology: storage-spaces
manager: brianlic
ms.openlocfilehash: 4b525555333a8aeee416e9ab55981c17137a52ea
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71365988"
---
# <a name="troubleshoot-storage-spaces-direct-health-and-operational-states"></a>Behandeln von direkte Speicherplätze Integritäts-und Betriebszuständen

> Gilt für: Windows Server 2019, Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server (halbjährlicher Kanal), Windows 10, Windows 8.1

In diesem Thema werden die Integritäts-und Betriebszustände von Speicherpools, virtuellen Datenträgern (die sich unterhalb von Volumes in Speicherplätzen befinden) sowie Laufwerke in [direkte Speicherplätze](storage-spaces-direct-overview.md) und [Speicherplätze](overview.md)beschrieben. Diese Zustände können von Bedeutung sein, wenn Sie versuchen, verschiedene Probleme zu beheben, z. b. Warum Sie einen virtuellen Datenträger aufgrund einer schreibgeschützten Konfiguration nicht löschen können. Außerdem wird erläutert, warum ein Laufwerk nicht zu einem Pool hinzugefügt werden kann (cannotpoolreason).

Speicherplätze verfügen über drei primäre Objekte: *physische* Datenträger (Festplatten, SSDs usw.), die einem *Speicherpool*hinzugefügt werden, und virtualisieren des Speichers, sodass Sie *virtuelle* Datenträger aus freiem Speicherplatz im Pool erstellen können, wie hier gezeigt. Pool Metadaten werden auf jedes Laufwerk im Pool geschrieben. Volumes werden auf den virtuellen Datenträgern erstellt, und Ihre Dateien werden gespeichert, aber wir werden hier nicht über Volumes sprechen.

![Physische Datenträger werden einem Speicherpool hinzugefügt, und dann werden die virtuellen Datenträger aus dem Poolbereich erstellt.](media/storage-spaces-states/storage-spaces-object-model.png)

Sie können Integritäts-und Betriebszustände in Server-Manager oder PowerShell anzeigen. Im folgenden finden Sie ein Beispiel für eine Vielzahl von Integritäts-und Betriebszuständen in einem direkte Speicherplätze Cluster, in denen die meisten Cluster Knoten fehlen (Klicken Sie mit der rechten Maustaste auf die Spaltenüberschriften, um den **Betriebs Status**hinzuzufügen). Dabei handelt es sich nicht um einen glücklichen Cluster.

![Server-Manager, das die Ergebnisse von zwei fehlenden Knoten in einem direkte Speicherplätze Cluster anzeigt: viele fehlende physische Datenträger und virtuelle Datenträger in einem fehlerhaften Zustand.](media/storage-spaces-states/unhealthy-disks-in-server-manager.png)

## <a name="storage-pool-states"></a>Speicherpool Zustände

Jeder Speicherpool weist den Integritäts Status "fehlerfrei", " **Warnung**" oder " **unbekannt**"**auf, / Fehler** **Haft ist,** sowie einen oder mehrere Betriebszustände.

Verwenden Sie die folgenden PowerShell-Befehle, um herauszufinden, in welchem Zustand sich ein Pool befindet:

```PowerShell
Get-StoragePool -IsPrimordial $False | Select-Object HealthStatus, OperationalStatus, ReadOnlyReason
```

Im folgenden finden Sie eine Beispielausgabe, in der ein Speicherpool im unbekannten Integritäts Status mit dem schreibgeschützten Betriebsstatus angezeigt wird:

```
FriendlyName                OperationalStatus HealthStatus IsPrimordial IsReadOnly
------------                ----------------- ------------ ------------ ----------
S2D on StorageSpacesDirect1 Read-only         Unknown      False        True
```

In den folgenden Abschnitten werden die Integritäts-und Betriebszustände aufgeführt.

### <a name="pool-health-state-healthy"></a>Integritäts Status des Pools: Fehlerfrei

|Betriebsstatus    |Beschreibung|
|---------            |---------  |
|OK|Der Speicherpool ist fehlerfrei.|

### <a name="pool-health-state-warning"></a>Integritäts Status des Pools: Warnung

Wenn sich der Speicherpool im **Warnungs** Integritäts Status befindet, bedeutet dies, dass der Pool zugänglich ist, aber mindestens ein Laufwerk fehlgeschlagen ist oder fehlt. Dadurch kann der Speicherpool die Resilienz verringern.

|Betriebsstatus    |Beschreibung|
|---------            |---------  |
|Verringert|Es sind fehlerhafte oder fehlende Laufwerke im Speicherpool vorhanden. Diese Bedingung tritt nur bei Laufwerken auf, die Pool-Metadaten Hosting. <br><br>**Aktion**: Überprüfen Sie den Zustand Ihrer Laufwerke, und ersetzen Sie alle fehlgeschlagenen Laufwerke, bevor weitere Fehler auftreten.|

### <a name="pool-health-state-unknown-or-unhealthy"></a>Integritäts Status des Pools: Unbekannt oder fehlerhaft

Wenn der Integritäts Status eines Speicher Pools unbekannt **oder Fehler** Haft ist, bedeutet dies, dass der Speicherpool schreibgeschützt ist und nicht geändert werden kann, bis der Pool wieder in den Zustand " **Warnung** " oder " **OK** " zurückversetzt wird.

|Betriebsstatus    |Schreib geschützter Grund |Beschreibung|
|---------            |---------       |--------   |
|Schreibgeschützt|Ständig|Dies kann vorkommen, wenn der Speicherpool sein [Quorum](understand-quorum.md)verliert, was bedeutet, dass die meisten Laufwerke im Pool ausgefallen sind oder aus irgendeinem Grund offline sind. Wenn ein Pool sein Quorum verliert, wird die Pool Konfiguration von Speicherplätzen automatisch auf schreibgeschützt festgelegt, bis genügend Laufwerke wieder verfügbar sind.<br><br>**Hinspiel** <br>1. Verbinden Sie fehlende Laufwerke erneut, und schalten Sie alle Server bei Verwendung von direkte Speicherplätze online. <br>2. Legen Sie den Pool auf Lese-/Schreibzugriff zurück, indem Sie eine PowerShell-Sitzung mit Administrator Berechtigungen öffnen und dann Folgendes eingeben:<br><br> <code> @ no__t-1 <PoolName> -IsPrimordial $False \| Set-StoragePool -IsReadOnly $false @ no__t-4|
||Richtlinie|Ein Administrator hat den Speicherpool als schreibgeschützt festgelegt.<br><br>**Hinspiel** Um einen Cluster Speicherpool in Failovercluster-Manager auf Lese-/Schreibzugriff festzulegen, wechseln Sie zu **Pools**, klicken Sie mit der rechten Maustaste auf den Pool, und wählen Sie dann **Online**schalten aus.<br><br>Öffnen Sie für andere Server und PCs eine PowerShell-Sitzung mit Administrator Berechtigungen, und geben Sie dann Folgendes ein:<br><br><code> @ no__t-1 <PoolName> \| Set-StoragePool -IsReadOnly $false @ no__t-4<br><br> |
||Starten|Speicherplätze werden gestartet, oder es wird darauf gewartet, dass Laufwerke im Pool verbunden werden. Dies sollte ein temporärer Zustand sein. Nachdem der Pool vollständig gestartet wurde, sollte er in einen anderen Betriebsstatus übergehen.<br><br>**Hinspiel** Wenn der Pool im *anfangs* Zustand bleibt, stellen Sie sicher, dass alle Laufwerke im Pool ordnungsgemäß verbunden sind.|

Weitere Informationen finden [Sie unter Ändern eines Speicherpools, der eine schreibgeschützte Konfiguration aufweist](https://social.technet.microsoft.com/wiki/contents/articles/14861.modifying-a-storage-pool-that-has-a-read-only-configuration.aspx).

## <a name="virtual-disk-states"></a>Virtuelle Datenträger Zustände

Bei Speicherplätzen werden Volumes auf virtuellen Datenträgern (Speicherplätzen) platziert, die aus freiem Speicherplatz in einem Pool aufgeteilt sind. Jeder virtuelle Datenträger hat den Integritäts Status "fehlerfrei" **, "** **Warnung** **", "** fehlerhaft" oder " **unbekannt** " sowie einen oder mehrere Betriebszustände.

Verwenden Sie die folgenden PowerShell-Befehle, um herauszufinden, in welchem Zustand die virtuellen Datenträger sich befinden:

```PowerShell
Get-VirtualDisk | Select-Object FriendlyName,HealthStatus, OperationalStatus, DetachedReason
```

Im folgenden finden Sie ein Beispiel für die Ausgabe eines getrennten virtuellen Datenträgers und eines herunter gestuften/unvollständigen virtuellen Datenträgers:

```
FriendlyName HealthStatus OperationalStatus      DetachedReason
------------ ------------ -----------------      --------------
Volume1      Unknown      Detached               By Policy
Volume2      Warning      {Degraded, Incomplete} None
```

In den folgenden Abschnitten werden die Integritäts-und Betriebszustände aufgeführt.

### <a name="virtual-disk-health-state-healthy"></a>Integritäts Status des virtuellen Datenträgers: Fehlerfrei

|Betriebsstatus    |Beschreibung|
|---------            |---------          |
|OK    |Der virtuelle Datenträger ist fehlerfrei.|
|Suboptimalen    |Daten werden nicht gleichmäßig auf die Laufwerke geschrieben. <br><br>**Aktion**: Optimieren Sie die Laufwerk Auslastung im Speicherpool, indem Sie das Cmdlet " [optimieren-storagepool](https://technet.microsoft.com/itpro/powershell/windows/storage/optimize-storagepool) " ausführen.|

### <a name="virtual-disk-health-state-warning"></a>Integritäts Status des virtuellen Datenträgers: Warnung

Wenn sich der virtuelle Datenträger in einem **Warnungs** Integritäts Status befindet, bedeutet dies, dass eine oder mehrere Kopien Ihrer Daten nicht verfügbar sind. Speicherplätze können aber trotzdem mindestens eine Kopie Ihrer Daten lesen.

|Betriebsstatus    |Beschreibung|
|---------            |---------          |
|In Dienst            |Windows repariert den virtuellen Datenträger, z. b. nach dem Hinzufügen oder Entfernen eines Laufwerks. Nach Abschluss der Reparatur sollte der virtuelle Datenträger in den Integritäts Status OK zurückkehren.|
|Ständig           |Die Resilienz des virtuellen Datenträgers wird verringert, weil mindestens ein Laufwerk ausgefallen ist oder nicht vorhanden ist. Die fehlenden Laufwerke enthalten jedoch aktuelle Kopien Ihrer Daten.<br><br> **Aktion**: <br>1. Verbinden Sie fehlende Laufwerke erneut, ersetzen Sie alle fehlgeschlagenen Laufwerke, und schalten Sie, wenn Sie direkte Speicherplätze verwenden, alle Server Online, die offline sind. <br>2. Wenn Sie direkte Speicherplätze nicht verwenden, reparieren Sie die virtuelle Festplatte als nächstes mithilfe des Cmdlets [Repair-virtualdisk](https://technet.microsoft.com/itpro/powershell/windows/storage/repair-virtualdisk) .<br> Direkte Speicherplätze automatisch eine Reparatur startet, wenn dies nach dem erneuten Verbinden oder Austauschen eines Laufwerks erforderlich ist.|
|Verringert             |Die Resilienz des virtuellen Datenträgers wird verringert, weil mindestens ein Laufwerk ausgefallen ist oder nicht vorhanden ist und auf diesen Laufwerken veraltete Kopien Ihrer Daten vorhanden sind. <br><br>**Aktion**: <br> 1. Verbinden Sie fehlende Laufwerke erneut, ersetzen Sie alle fehlgeschlagenen Laufwerke, und schalten Sie, wenn Sie direkte Speicherplätze verwenden, alle Server Online, die offline sind. <br> 2. Wenn Sie direkte Speicherplätze nicht verwenden, reparieren Sie die virtuelle Festplatte als nächstes mithilfe des Cmdlets [Repair-virtualdisk](https://technet.microsoft.com/itpro/powershell/windows/storage/repair-virtualdisk) . <br>Direkte Speicherplätze automatisch eine Reparatur startet, wenn dies nach dem erneuten Verbinden oder Austauschen eines Laufwerks erforderlich ist.|

### <a name="virtual-disk-health-state-unhealthy"></a>Integritäts Status des virtuellen Datenträgers: Unhealthy

Wenn sich ein virtueller Datenträger in **einem Fehler** haften Integritäts Status befindet, ist der Zugriff auf einige oder alle Daten auf dem virtuellen Datenträger derzeit nicht möglich.

|Betriebsstatus    |Beschreibung|
|---------            |--------   |
|Keine Redundanz|Der virtuelle Datenträger hat Daten verloren, weil zu viele Laufwerke fehlgeschlagen sind.<br><br>**Aktion**: Ersetzen Sie die fehlerhaften Laufwerke, und stellen Sie die Daten dann aus der Sicherung|

### <a name="virtual-disk-health-state-informationunknown"></a>Integritäts Status des virtuellen Datenträgers: Informationen/unbekannt

Der virtuelle Datenträger kann sich auch im Integritäts Status des Zustands (wie im System Steuerungselement "Speicherplätze" gezeigt) oder in einem **unbekannten** Integritäts Status (wie in PowerShell gezeigt) befinden, wenn ein Administrator den virtuellen **Daten** Träger offline geschaltet hat oder der virtuelle Datenträger zu ab.

|Betriebsstatus    |Getrennter Grund |Beschreibung|
|---------            |---------       |--------   |
|„Getrennt“             |Nach Richtlinie            |Ein Administrator hat den virtuellen Datenträger offline geschaltet oder den virtuellen Datenträger so festgelegt, dass er eine manuelle Anlage erfordert. in diesem Fall müssen Sie den virtuellen Datenträger bei jedem Neustart von Windows manuell anfügen.<br><br>**Aktion**: Schalten Sie den virtuellen Datenträger wieder online. Um dies zu tun, wenn sich der virtuelle Datenträger in einem Cluster Speicherpool befindet, wählen Sie in Failovercluster-Manager **Speicher** > **Pools** > **virtuelle**Datenträger auswählen den virtuellen Datenträger aus, der den **Offline** Status anzeigt, und wählen Sie dann die Option **Bring Online**. <br><br>Um einen virtuellen Datenträger wieder online zu schalten, wenn er sich nicht in einem Cluster befinden, öffnen Sie eine PowerShell-Sitzung als Administrator, und versuchen Sie es dann mit dem folgenden Befehl:<br><br> <code>Get-VirtualDisk \| Where-Object -Filter { $_.OperationalStatus -eq "Detached" } \| Connect-VirtualDisk</code><br><br>Um alle nicht gruppierten virtuellen Datenträger nach dem Neustart von Windows automatisch anzufügen, öffnen Sie eine PowerShell-Sitzung als Administrator, und verwenden Sie dann den folgenden Befehl:<br><br> <code>Get-VirtualDisk \| Set-VirtualDisk -ismanualattach $false</code>|
|            |Mehrheits Datenträger |Zu viele von dieser virtuellen Festplatte verwendete Laufwerke konnten nicht ausgeführt werden, fehlen oder haben veraltete Daten.   <br><br>**Aktion**: <br> 1. Verbinden Sie fehlende Laufwerke erneut, und schalten Sie, wenn Sie direkte Speicherplätze verwenden, alle Server Online, die offline sind. <br> 2. Wenn alle Laufwerke und Server online sind, ersetzen Sie alle fehlgeschlagenen Laufwerke. Weitere Informationen finden Sie unter [Integritätsdienst](../../failover-clustering/health-service-overview.md) . <br>Direkte Speicherplätze automatisch eine Reparatur startet, wenn dies nach dem erneuten Verbinden oder Austauschen eines Laufwerks erforderlich ist.<br>3. Wenn Sie direkte Speicherplätze nicht verwenden, reparieren Sie die virtuelle Festplatte als nächstes mithilfe des Cmdlets [Repair-virtualdisk](https://technet.microsoft.com/itpro/powershell/windows/storage/repair-virtualdisk) .  <br><br>Wenn mehr Datenträger fehlschlagen, als Sie Kopien Ihrer Daten haben und der virtuelle Datenträger nicht zwischen Fehlern repariert wurde, gehen alle Daten auf dem virtuellen Datenträger dauerhaft verloren. Löschen Sie in diesem unglücklichen Fall den virtuellen Datenträger, erstellen Sie einen neuen virtuellen Datenträger, und stellen Sie dann eine Wiederherstellung von einer Sicherung durch.|
|                     |Ständig |Zum Lesen der virtuellen Festplatte sind nicht genügend Laufwerke vorhanden.    <br><br>**Aktion**: <br> 1. Verbinden Sie fehlende Laufwerke erneut, und schalten Sie, wenn Sie direkte Speicherplätze verwenden, alle Server Online, die offline sind. <br> 2. Wenn alle Laufwerke und Server online sind, ersetzen Sie alle fehlgeschlagenen Laufwerke. Weitere Informationen finden Sie unter [Integritätsdienst](../../failover-clustering/health-service-overview.md) . <br>Direkte Speicherplätze automatisch eine Reparatur startet, wenn dies nach dem erneuten Verbinden oder Austauschen eines Laufwerks erforderlich ist.<br>3. Wenn Sie direkte Speicherplätze nicht verwenden, reparieren Sie die virtuelle Festplatte als nächstes mithilfe des Cmdlets [Repair-virtualdisk](https://technet.microsoft.com/itpro/powershell/windows/storage/repair-virtualdisk) .<br><br>Wenn mehr Datenträger fehlschlagen, als Sie Kopien Ihrer Daten haben und der virtuelle Datenträger nicht zwischen Fehlern repariert wurde, gehen alle Daten auf dem virtuellen Datenträger dauerhaft verloren. Löschen Sie in diesem unglücklichen Fall den virtuellen Datenträger, erstellen Sie einen neuen virtuellen Datenträger, und stellen Sie dann eine Wiederherstellung von einer Sicherung durch.|
| |Timeout|Das Anfügen des virtuellen Datenträgers hat zu lange gedauert. <br><br> **Hinspiel** Dies sollte nicht häufig vorkommen, weshalb Sie möglicherweise versuchen, festzustellen, ob die Bedingung rechtzeitig verstrichen ist. Sie können auch versuchen, den virtuellen Datenträger mit dem [Disconnect-virtualdisk-](https://docs.microsoft.com/powershell/module/storage/disconnect-virtualdisk?view=win10-ps) Cmdlet zu trennen und dann das [Connect-virtualdisk-](https://docs.microsoft.com/powershell/module/storage/connect-virtualdisk?view=win10-ps) Cmdlet zum erneuten Verbinden zu verwenden. |

## <a name="drive-physical-disk-states"></a>Zustände des Laufwerks (physischer Datenträger)

In den folgenden Abschnitten werden die Integritäts Zustände eines Laufwerks beschrieben. Laufwerke in einem Pool werden in PowerShell als *physische* Datenträger Objekte dargestellt.

### <a name="drive-health-state-healthy"></a>Laufwerks Integritäts Status: Fehlerfrei

|Betriebsstatus    |Beschreibung|
|---------            |---------          |
|OK|Das Laufwerk ist fehlerfrei.|
|In Dienst|Das Laufwerk führt einige interne Betriebs Vorgänge aus. Wenn die Aktion beendet ist, sollte das Laufwerk in den Integritäts Status *OK* zurückkehren.|

### <a name="drive-health-state-warning"></a>Laufwerks Integritäts Status: Warnung

Ein Laufwerk im Warnungs Status kann Daten erfolgreich lesen und schreiben, weist jedoch ein Problem auf.

|Betriebsstatus    |Beschreibung|
|---------            |---------          |
|Verlorene Kommunikation|Das Laufwerk fehlt. Wenn Sie direkte Speicherplätze verwenden, könnte dies daran liegen, dass ein Server herunter ist.<br><br>**Aktion**: Wenn Sie direkte Speicherplätze verwenden, schalten Sie alle Server wieder online. Wenn dies nicht behoben werden kann, verbinden Sie das Laufwerk erneut, ersetzen Sie es, oder führen Sie ausführliche Diagnoseinformationen zu diesem Laufwerk aus, indem Sie die Schritte unter Problembehandlung mithilfe Windows-Fehlerberichterstattung > physischen Datenträgers durch [führen](../../failover-clustering/troubleshooting-using-wer-reports.md#physical-disk-timed-out).|
|Entfernen aus Pool|Speicherplätze entfernen gerade das Laufwerk aus dem Speicherpool. <br><br> Dies ist ein temporärer Zustand. Wenn das Laufwerk nach Abschluss des Entfernens noch an das System angefügt ist, wechselt es in einem ursprünglichen Pool in einen anderen Betriebsstatus (normalerweise OK).|
|Starten des Wartungsmodus|Bei Speicherplätzen wird das Laufwerk in den Wartungsmodus versetzt, nachdem ein Administrator das Laufwerk in den Wartungsmodus versetzt hat. Dies ist ein temporärer Zustand: das Laufwerk sollte sich bald im *Wartungsmodus* befindet.|
|Im Wartungsmodus|Ein Administrator hat das Laufwerk in den Wartungsmodus versetzt, wobei Lese-und Schreibvorgänge vom Laufwerk angehalten werden. Dies erfolgt in der Regel vor dem Aktualisieren der Laufwerks Firmware oder beim Testen von Fehlern.<br><br>**Aktion**: Wenn Sie das Laufwerk aus dem Wartungsmodus entfernen möchten, verwenden Sie das Cmdlet " [Deaktivierte storagemaintenancemode](https://technet.microsoft.com/itpro/powershell/windows/storage/disable-storagemaintenancemode) ".|
|Beenden des Wartungsmodus|Ein Administrator hat das Laufwerk aus dem Wartungsmodus genommen, und Speicherplätze werden gerade wieder online geschaltet. Dies ist ein temporärer Zustand: das Laufwerk sollte bald in einem anderen Zustand sein *, idealerweise*fehlerfrei.|
|Vorhersagefehler|Das Laufwerk hat gemeldet, dass es sich in der Nähe des Fehlers befindet.<br><br>**Aktion**: Ersetzen Sie das Laufwerk.|
|IO-Fehler|Vorübergehender Fehler beim Zugriff auf das Laufwerk.<br><br>**Aktion**: <br>1. Wenn das Laufwerk nicht wieder in den Zustand **OK** wechselt, können Sie versuchen, das Laufwerk mithilfe des [Reset-PhysicalDisk-](https://docs.microsoft.com/powershell/module/storage/reset-physicaldisk) Cmdlets zurückzusetzen. <br> 2. Verwenden Sie [Repair-virtualdisk](https://docs.microsoft.com/powershell/module/storage/repair-virtualdisk) , um die Resilienz der betroffenen virtuellen Datenträger wiederherzustellen. <br>3. Wenn dies der Fall ist, ersetzen Sie das Laufwerk.|
|Vorübergehender Fehler|Temporärer Fehler beim Laufwerk. Dies bedeutet in der Regel, dass das Laufwerk nicht reagiert, aber auch bedeutet, dass die Schutz Partition der Speicherplätze nicht ordnungs mäßig vom Laufwerk entfernt wurde. <br><br>**Aktion**: <br>1. Wenn das Laufwerk nicht wieder in den Zustand **OK** wechselt, können Sie versuchen, das Laufwerk mithilfe des [Reset-PhysicalDisk-](https://docs.microsoft.com/powershell/module/storage/reset-physicaldisk) Cmdlets zurückzusetzen. <br> 2. Verwenden Sie [Repair-virtualdisk](https://docs.microsoft.com/powershell/module/storage/repair-virtualdisk) , um die Resilienz der betroffenen virtuellen Datenträger wiederherzustellen. <br>3. Wenn dies der Fall ist, ersetzen Sie das Laufwerk, oder führen Sie ausführliche Diagnoseinformationen zu diesem Laufwerk aus, indem Sie die Schritte unter Problembehandlung mithilfe Windows-Fehlerberichterstattung > physischer Datenträger [konnte nicht online](../../failover-clustering/troubleshooting-using-wer-reports.md#physical-disk-failed-to-come-online)geschaltet werden.|
|Ungewöhnliche Latenz|Das Laufwerk führt langsam aus, gemessen an der Integritätsdienst in direkte Speicherplätze.<br><br>**Aktion**: Wenn dies der Fall ist, ersetzen Sie das Laufwerk, sodass es nicht die Leistung von Speicherplätzen als Ganzes verringert.

### <a name="drive-health-state-unhealthy"></a>Laufwerks Integritäts Status: Unhealthy

Auf ein Laufwerk im fehlerhaften Zustand kann derzeit nicht geschrieben werden oder es kann nicht darauf zugegriffen werden.

|Betriebsstatus    |Beschreibung|
|---------            |---------          |
|Nicht verwendbar|Dieses Laufwerk kann nicht von Speicherplätzen verwendet werden. Weitere Informationen finden Sie unter [direkte Speicherplätze Hardwareanforderungen](storage-spaces-direct-hardware-requirements.md). Wenn Sie direkte Speicherplätze nicht verwenden, finden Sie weitere Informationen unter [Übersicht über Speicherplätze](https://technet.microsoft.com/library/hh831739(v=ws.11).aspx#Requirements).|
|Getrennt|Das Laufwerk wurde vom Pool getrennt.<br><br>**Aktion**: Setzen Sie das Laufwerk zurück, löschen Sie alle Daten vom Laufwerk, und fügen Sie es als leeres Laufwerk wieder zum Pool hinzu. Öffnen Sie hierzu eine PowerShell-Sitzung als Administrator, führen Sie das Cmdlet [Reset-PhysicalDisk](https://technet.microsoft.com/itpro/powershell/windows/storage/reset-physicaldisk) aus, und führen Sie dann [Repair-virtualdisk](https://technet.microsoft.com/itpro/powershell/windows/storage/repair-virtualdisk)aus. <br><br>Um ausführliche Diagnoseinformationen zu diesem Laufwerk zu erhalten, führen Sie die Schritte unter Problembehandlung mithilfe Windows-Fehlerberichterstattung aus, > physischer Datenträger [nicht online](../../failover-clustering/troubleshooting-using-wer-reports.md#physical-disk-failed-to-come-online)geschaltet werden konnte.|
|Veraltete Metadaten|Auf dem Laufwerk wurden alte Metadaten gefunden.<br><br>**Aktion**: Dies sollte ein temporärer Zustand sein. Wenn das Laufwerk nicht wieder in OK übergeht, können Sie [Repair-virtualdisk](https://technet.microsoft.com/itpro/powershell/windows/storage/repair-virtualdisk) ausführen, um einen Reparaturvorgang auf betroffenen virtuellen Datenträgern zu starten. Wenn das Problem nicht behoben wird, können Sie das Laufwerk mit dem Cmdlet " [Reset-PhysicalDisk](https://technet.microsoft.com/itpro/powershell/windows/storage/reset-physicaldisk) " zurücksetzen, alle Daten vom Laufwerk löschen und dann " [Repair-virtualdisk](https://technet.microsoft.com/itpro/powershell/windows/storage/repair-virtualdisk)" ausführen.|
|Unbekannte Metadaten|Speicherplätze haben unbekannte Metadaten auf dem Laufwerk gefunden. Dies bedeutet in der Regel, dass das Laufwerk über Metadaten aus einem anderen Pool verfügt.<br><br>**Aktion**: Wenn Sie das Laufwerk zurücksetzen und dem aktuellen Pool hinzufügen möchten, setzen Sie das Laufwerk zurück. Öffnen Sie zum Zurücksetzen des Laufwerks eine PowerShell-Sitzung als Administrator, führen Sie das Cmdlet [Reset-PhysicalDisk](https://technet.microsoft.com/itpro/powershell/windows/storage/reset-physicaldisk) aus, und führen Sie dann [Repair-virtualdisk](https://technet.microsoft.com/itpro/powershell/windows/storage/repair-virtualdisk)aus.|
|Fehlerhafte Medien|Das Laufwerk ist fehlgeschlagen und wird nicht mehr von Speicherplätzen verwendet.<br><br>**Aktion**: Ersetzen Sie das Laufwerk. <br><br>Um ausführliche Diagnoseinformationen zu diesem Laufwerk zu erhalten, führen Sie die Schritte unter Problembehandlung mithilfe Windows-Fehlerberichterstattung aus, > physischer Datenträger [nicht online](../../failover-clustering/troubleshooting-using-wer-reports.md#physical-disk-failed-to-come-online)geschaltet werden konnte.|
|Gerätehardware Fehler|Auf diesem Laufwerk ist ein Hardwarefehler aufgetreten. <br><br>**Aktion**: Ersetzen Sie das Laufwerk.|
|Aktualisieren der Firmware|Die Firmware auf dem Laufwerk wird von Windows aktualisiert. Dies ist ein temporärer Zustand, der in der Regel weniger als eine Minute dauert und während der andere Laufwerke im Pool alle Lese-und Schreibvorgänge verarbeiten. Weitere Informationen finden Sie unter [Aktualisieren der Laufwerks Firmware](../update-firmware.md).|
|Starten|Das Laufwerk ist betriebsbereit. Dies sollte ein temporärer Status sein. nach Abschluss des Vorgangs sollte das Laufwerk in einen anderen Betriebsstatus übergehen.|

## <a name="reasons-a-drive-cant-be-pooled"></a>Gründe für das poolte eines Laufwerks

Einige Laufwerke sind nur in einem Speicherpool bereit. Sie können herausfinden, warum ein Laufwerk nicht für das Pooling geeignet ist, indem Sie sich die `CannotPoolReason`-Eigenschaft eines physischen Datenträgers ansehen. Im folgenden finden Sie ein Beispiel für ein PowerShell-Skript zum Anzeigen der cannotpoolreason-Eigenschaft:

```PowerShell
Get-PhysicalDisk | Format-Table FriendlyName,MediaType,Size,CanPool,CannotPoolReason
```

Im folgenden finden Sie eine Beispielausgabe:

```
FriendlyName          MediaType          Size CanPool CannotPoolReason
------------          ---------          ---- ------- ----------------
ATA MZ7LM120HCFD00D3  SSD        120034123776   False Insufficient Capacity
Msft Virtual Disk     SSD         10737418240    True
Generic Physical Disk SSD        119990648832   False In a Pool
```

In der folgenden Tabelle werden die einzelnen Gründe ausführlicher erläutert.

|Grund|Beschreibung|
|---|---|
|In einem Pool|Das Laufwerk gehört bereits zu einem Speicherpool. <br><br>Laufwerke können jeweils nur zu einem einzelnen Speicherpool gehören. Um dieses Laufwerk in einem anderen Speicherpool zu verwenden, entfernen Sie zunächst das Laufwerk aus dem vorhandenen Pool, das Speicherplätze anweist, die Daten auf dem Laufwerk auf andere Laufwerke im Pool zu verschieben. Oder setzen Sie das Laufwerk zurück, wenn das Laufwerk vom Pool getrennt wurde, ohne Speicherplätze zu benachrichtigen. <br><br>Verwenden Sie zum sicheren Entfernen eines Laufwerks aus einem Speicherpool [Remove-PhysicalDisk](https://technet.microsoft.com/itpro/powershell/windows/storage/remove-physicaldisk), oder wechseln Sie zu Server-Manager > **Datei-und Speicherdienste** > -**Speicherpools**, > **physischen**Datenträgern, klicken Sie mit der rechten Maustaste auf das Laufwerk, und wählen Sie dann entfernen aus.  **Datenträger.**<br><br>Verwenden Sie zum Zurücksetzen eines Laufwerks [Reset-PhysicalDisk](https://technet.microsoft.com/itpro/powershell/windows/storage/reset-physicaldisk).|
|Nicht fehlerfrei|Das Laufwerk befindet sich nicht in einem fehlerfreien Zustand und muss möglicherweise ersetzt werden.|
|Wechselmedien|Das Laufwerk ist als Wechsel Datenträger klassifiziert. <br><br>Speicherplätze unterstützen keine Medien, die von Windows als Wechselmedien erkannt werden, z. b. Blu-ray-Laufwerke. Obwohl sich viele Festplattenlaufwerke in Wechsel Datenträgern befinden, sind Medien, die von Windows als Wechsel Datenträger *klassifiziert* werden, nicht für die Verwendung mit Speicherplätzen geeignet.|
|Wird vom Cluster verwendet|Das Laufwerk wird zurzeit von einem Failovercluster verwendet.|
|Offline|Das Laufwerk ist offline. <br><br>Um alle Offline Laufwerke Online zu schalten und auf Lese-/Schreibzugriff festzulegen, öffnen Sie eine PowerShell-Sitzung als Administrator, und verwenden Sie die folgenden Skripts:<br><br><code>Get-Disk \| Where-Object -Property OperationalStatus -EQ "Offline" \| Set-Disk -IsOffline $false</code><br><br><code>Get-Disk \| Where-Object -Property IsReadOnly -EQ $true \| Set-Disk -IsReadOnly $false</code>|
|Unzureichende Kapazität|Dies tritt normalerweise auf, wenn Partitionen den freien Speicherplatz auf dem Laufwerk einnehmen. <br><br>**Aktion**: Löschen Sie alle Volumes auf dem Laufwerk, und löschen Sie alle Daten auf dem Laufwerk. Eine Möglichkeit hierfür ist die Verwendung des PowerShell-Cmdlets [Clear-Disk](https://docs.microsoft.com/powershell/module/storage/clear-disk?view=win10-ps) .|
|Überprüfung wird durchgeführt|Der [Integritätsdienst](../../failover-clustering/health-service-overview.md#supported-components-document) überprüft, ob das Laufwerk oder die Firmware auf dem Laufwerk für die Verwendung durch den Server Administrator genehmigt ist.|
|Überprüfung fehlgeschlagen|Der [Integritätsdienst](../../failover-clustering/health-service-overview.md#supported-components-document) konnte nicht überprüfen, ob das Laufwerk oder die Firmware auf dem Laufwerk für die Verwendung durch den Server Administrator genehmigt ist.|
|Firmware nicht kompatibel|Die Firmware auf dem physischen Laufwerk ist nicht in der Liste der genehmigten Firmwarerevisionen enthalten, die vom Server Administrator mithilfe des [Integritätsdienst](../../failover-clustering/health-service-overview.md#supported-components-document)angegeben werden. |
|Hardware nicht kompatibel|Das Laufwerk ist nicht in der Liste der genehmigten Speicher Modelle enthalten, die vom Server Administrator mithilfe des [Integritätsdienst](../../failover-clustering/health-service-overview.md#supported-components-document)angegeben werden.|

## <a name="see-also"></a>Siehe auch

- [Direkte Speicherplätze](storage-spaces-direct-overview.md)
- [Direkte Speicherplätze Hardwareanforderungen](storage-spaces-direct-hardware-requirements.md)
- [Grundlegendes zum Cluster- und Poolquorum](understand-quorum.md)