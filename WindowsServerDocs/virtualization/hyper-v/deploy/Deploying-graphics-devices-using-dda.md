---
title: Bereitstellen von Grafik Geräten mithilfe der diskreten Geräte Zuweisung
description: Erfahren Sie, wie Sie mit DDA Grafikgeräte in Windows Server bereitstellen.
ms.prod: windows-server
ms.service: na
ms.technology: hyper-v
ms.tgt_pltfrm: na
ms.topic: article
author: chrishuybregts
ms.author: chrihu
ms.assetid: 67a01889-fa36-4bc6-841d-363d76df6a66
ms.openlocfilehash: 3b37abaf5a2341aff66ff0064ecc4f52faf47f06
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71392994"
---
# <a name="deploy-graphics-devices-using-discrete-device-assignment"></a>Bereitstellen von Grafik Geräten mithilfe der diskreten Geräte Zuweisung

>Gilt für: Microsoft Hyper-V Server 2016, Windows Server 2016, Windows Server 2019 Microsoft Hyper-V Server 2019  

Ab Windows Server 2016 können Sie eine diskrete Geräte Zuweisung oder DDA verwenden, um ein gesamtes PCIe-Gerät an eine VM zu übergeben.  Dadurch wird ein hoher Leistungs Zugriff auf Geräte wie [nvme-Speicher](./Deploying-storage-devices-using-dda.md) oder Grafikkarten innerhalb eines virtuellen Computers ermöglicht, während die Gerätesystem eigene Treiber genutzt werden können.  Weitere Informationen zu den einzelnen Geräten, zu den möglichen Auswirkungen auf die Sicherheit usw. finden Sie unter Planen der Bereitstellung von [Geräten mit diskreter Geräte Zuweisung](../plan/Plan-for-Deploying-Devices-using-Discrete-Device-Assignment.md) .

Die Verwendung eines Geräts mit diskreter Geräte Zuweisung umfasst drei Schritte:
-   Konfigurieren der VM für die diskrete Geräte Zuweisung
-   Aufheben der Einbindung des Geräts von der Host Partition
-   Zuweisen des Geräts zum virtuellen Gastcomputer

Der Befehl "alle" kann auf dem Host in einer Windows PowerShell-Konsole als Administrator ausgeführt werden.

## <a name="configure-the-vm-for-dda"></a>Konfigurieren des virtuellen Computers für DDA
Bei der diskreten Geräte Zuweisung gelten einige Einschränkungen für die VMs, und der folgende Schritt muss ausgeführt werden.

1.  Konfigurieren Sie die Aktion "automatisches Abbrechen" eines virtuellen Computers, um durch Ausführen von

```
Set-VM -Name VMName -AutomaticStopAction TurnOff
```

### <a name="some-additional-vm-preparation-is-required-for-graphics-devices"></a>Für Grafikgeräte sind einige zusätzliche VM-Vorbereitung erforderlich.

Einige Hardware Leistung ist besser, wenn der virtuelle Computer auf eine bestimmte Art und Weise konfiguriert ist.  Weitere Informationen dazu, ob Sie die folgenden Konfigurationen für Ihre Hardware benötigen, wenden Sie sich an den Hardwarehersteller. Weitere Informationen finden Sie unter Planen der Bereitstellung [von Geräten mithilfe der diskreten Geräte Zuweisung](../plan/Plan-for-Deploying-Devices-using-Discrete-Device-Assignment.md) und in diesem [Blogbeitrag.](https://techcommunity.microsoft.com/t5/Virtualization/Discrete-Device-Assignment-GPUs/ba-p/382266)

1. Aktivieren der Schreibweise auf der CPU
   ```
   Set-VM -GuestControlledCacheTypes $true -VMName VMName
   ```
2. Konfigurieren des 32-Bit-MMIO-Speicherplatzes
   ```
   Set-VM -LowMemoryMappedIoSpace 3Gb -VMName VMName
   ```
3. Mehr als 32-Bit-MMIO-Speicherplatz konfigurieren
   ```
   Set-VM -HighMemoryMappedIoSpace 33280Mb -VMName VMName
   ```
   > [!TIP] 
   > Die obigen MMIO-Speicherplatz Werte sind sinnvolle Werte, die für das Experimentieren mit einem einzelnen GPU festgelegt werden.  Wenn nach dem Starten des virtuellen Computers ein Fehler im Zusammenhang mit nicht ausreichenden Ressourcen gemeldet wird, müssen Sie diese Werte wahrscheinlich ändern. Weitere Informationen zur genauen Berechnung von MMIO-Anforderungen finden Sie unter Planen der Bereitstellung [von Geräten mit diskreter Geräte Zuweisung](../plan/Plan-for-Deploying-Devices-using-Discrete-Device-Assignment.md) .

## <a name="dismount-the-device-from-the-host-partition"></a>Aufheben der Einbindung des Geräts von der Host Partition
### <a name="optional---install-the-partitioning-driver"></a>Optional: Installieren des Partitionierungs Treibers
Die diskrete Geräte Zuweisung bietet Hardware-Hersteller die Möglichkeit, einen Sicherheits Entschärfungs Treiber für Ihre Geräte bereitzustellen.  Beachten Sie, dass dieser Treiber nicht mit dem Gerätetreiber identisch ist, der auf der Gast-VM installiert wird.  Es liegt an dem Ermessen des Hardware Anbieters, diesen Treiber bereitzustellen. Wenn Sie ihn jedoch bereitstellen, installieren Sie ihn, bevor Sie das Gerät von der Host Partition trennen.  Wenden Sie sich an den Hardwarehersteller, um weitere Informationen darüber zu erhalten, ob ein Entschärfungs Treiber vorhanden ist.
> Wenn kein Partitionierungs Treiber bereitgestellt wird, müssen Sie während der Aufhebung `-force` der Bereitstellung die-Option verwenden, um die Sicherheitswarnung zu umgehen. Weitere Informationen zu den Sicherheits Implikationen finden Sie unter Planen der Bereitstellung von [Geräten mit diskreter Geräte Zuweisung](../plan/Plan-for-Deploying-Devices-using-Discrete-Device-Assignment.md).

### <a name="locating-the-devices-location-path"></a>Suchen des Speicher Orts des Geräts
Der PCI-Speicherort Pfad ist erforderlich, um das Gerät vom Host zu entfernen und zu binden.  Ein Beispiel für einen Speicherort Pfad sieht wie `"PCIROOT(20)#PCI(0300)#PCI(0000)#PCI(0800)#PCI(0000)"`folgt aus:.  Weitere Informationen zum Speicherort Pfad finden Sie hier: [Planen Sie die Bereitstellung von Geräten mit diskreter Geräte Zuweisung](../plan/Plan-for-Deploying-Devices-using-Discrete-Device-Assignment.md).

### <a name="disable-the-device"></a>Deaktivieren des Geräts
Stellen Sie mithilfe von Geräte-Manager oder PowerShell sicher, dass das Gerät "deaktiviert" ist.  

### <a name="dismount-the-device"></a>Aufheben der Einbindung des Geräts
Abhängig davon, ob der Anbieter einen Entschärfungs Treiber bereitgestellt hat, müssen Sie entweder die Option "-Force" verwenden oder nicht.
- Bei Installation eines Entschärfungs Treibers
  ```
  Dismount-VMHostAssignableDevice -LocationPath $locationPath
  ```
- Wenn ein Entschärfungs Treiber nicht installiert wurde
  ```
  Dismount-VMHostAssignableDevice -force -LocationPath $locationPath
  ```

## <a name="assigning-the-device-to-the-guest-vm"></a>Zuweisen des Geräts zum virtuellen Gastcomputer
Der letzte Schritt besteht darin, Hyper-V mitzuteilen, dass ein virtueller Computer Zugriff auf das Gerät haben soll.  Zusätzlich zu dem oben gefundenen Speicherort Pfad müssen Sie den Namen des virtuellen Computers kennen.

```
Add-VMAssignableDevice -LocationPath $locationPath -VMName VMName
```

## <a name="whats-next"></a>Was kommt als nächstes
Nachdem ein Gerät erfolgreich auf einem virtuellen Computer bereitgestellt wurde, können Sie diesen virtuellen Computer starten und mit dem Gerät interagieren, wie Sie es normalerweise bei einem Bare-Metal-System ausführen würden.  Dies bedeutet, dass Sie jetzt die Treiber des Hardware Anbieters auf dem virtuellen Computer installieren können und Anwendungen sehen können, dass die Hardware vorhanden ist.  Sie können dies überprüfen, indem Sie in der Gast-VM den Geräte-Manager öffnen und sehen, dass die Hardware jetzt angezeigt wird.

## <a name="removing-a-device-and-returning-it-to-the-host"></a>Entfernen eines Geräts und Zurückgeben des Geräts an den Host
Wenn Sie das Gerät wieder in den ursprünglichen Zustand zurücksetzen möchten, müssen Sie den virtuellen Computer unterbinden und folgendes ausgeben:
```
#Remove the device from the VM
Remove-VMAssignableDevice -LocationPath $locationPath -VMName VMName
#Mount the device back in the host
Mount-VMHostAssignableDevice -LocationPath $locationPath
```
Anschließend können Sie das Gerät im Geräte-Manager erneut aktivieren, und das Host Betriebssystem kann erneut mit dem Gerät interagieren.

## <a name="examples"></a>Beispiele

### <a name="mounting-a-gpu-to-a-vm"></a>Einbinden einer GPU an einen virtuellen Computer
In diesem Beispiel verwenden wir PowerShell, um einen virtuellen Computer mit dem Namen "ddatest1" zu konfigurieren, mit dem die erste von der Hersteller-NVIDIA verfügbare GPU übernommen und der VM zugewiesen wird.  
```
#Configure the VM for a Discrete Device Assignment
$vm =   "ddatest1"
#Set automatic stop action to TurnOff
Set-VM -Name $vm -AutomaticStopAction TurnOff
#Enable Write-Combining on the CPU
Set-VM -GuestControlledCacheTypes $true -VMName $vm
#Configure 32 bit MMIO space
Set-VM -LowMemoryMappedIoSpace 3Gb -VMName $vm
#Configure Greater than 32 bit MMIO space
Set-VM -HighMemoryMappedIoSpace 33280Mb -VMName $vm

#Find the Location Path and disable the Device
#Enumerate all PNP Devices on the system
$pnpdevs = Get-PnpDevice -presentOnly
#Select only those devices that are Display devices manufactured by NVIDIA
$gpudevs = $pnpdevs |where-object {$_.Class -like "Display" -and $_.Manufacturer -like "NVIDIA"}
#Select the location path of the first device that's available to be dismounted by the host.
$locationPath = ($gpudevs | Get-PnpDeviceProperty DEVPKEY_Device_LocationPaths).data[0]
#Disable the PNP Device
Disable-PnpDevice  -InstanceId $gpudevs[0].InstanceId

#Dismount the Device from the Host
Dismount-VMHostAssignableDevice -force -LocationPath $locationPath

#Assign the device to the guest VM.
Add-VMAssignableDevice -LocationPath $locationPath -VMName $vm
```
