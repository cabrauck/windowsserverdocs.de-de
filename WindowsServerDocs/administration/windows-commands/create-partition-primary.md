---
title: create partition primary
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6d652d8e-3935-4a91-8ced-b17c0e7937be
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9c690119ad97db563e165e43716ede0e57bdc19a
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71378923"
---
# <a name="create-partition-primary"></a>create partition primary

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

erstellt eine primäre Partition auf dem Basis Datenträger mit dem Fokus.  
  
> [!CAUTION]  
  
  
  
## <a name="syntax"></a>Syntax  
  
```  
create partition primary [size=<n>] [offset=<n>] [id={ <byte> | <guid> }] [align=<n>] [noerr]  
```  
  
## <a name="parameters"></a>Parameter  
  
|          Parameter           |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           Beschreibung                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
|------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|          Size @ no__t-0 @ no__t-1           |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              Gibt die Größe der Partition in Megabyte \(MB @ no__t-1 an. Wenn keine Größe angegeben wird, wird die Partition so lange fortgesetzt, bis nicht mehr zugewiesener Speicherplatz in der aktuellen Region vorhanden ist.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              |
|         Offset @ no__t-0 @ no__t-1          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 Der Offset in Kilobyte \(KB @ no__t-1, bei dem die Partition erstellt wird. Wenn kein Offset angegeben wird, wird die Partition am Anfang des größten Datenträger Blocks gestartet, der groß genug ist, um Sie zu speichern.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
|          align @ no__t-0 @ no__t-1          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              Richtet alle Partitions Blöcke an die nächstgelegene Ausrichtungs Grenze aus. Wird in der Regel mit der Hardware-RAID-Nummer \(lun @ no__t-1 verwendet, um die Leistung zu verbessern. <n> ist die Anzahl der Kilobyte \( KB @ no__t-2 vom Anfang des Datenträgers bis zur nächstgelegenen Ausrichtungs Grenze.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                               |
| ID @ no__t-0 {<byte> &#124; <guid>} | Gibt den Partitionstyp an. Dieser Parameter ist für den ursprünglichen Gerätehersteller gedacht \(oem @ no__t-1 nur verwenden. Mit diesem Parameter können beliebige Byte-oder GUID-Partitionstypen angegeben werden. DiskPart überprüft den Partitionstyp nicht auf Gültigkeit, außer um sicherzustellen, dass es sich um ein Byte in Hexadezimal Form oder eine GUID handelt. **Vorsicht:** Das Erstellen von Partitionen mit diesem Parameter kann dazu führen, dass der Computer ausfällt oder nicht gestartet werden kann. Wenn Sie kein OEM-oder IT-Experte mit GPT-Datenträgern sind, erstellen Sie keine Partitionen auf GPT-Datenträgern mithilfe dieses Parameters. Verwenden Sie stattdessen immer den Befehl **create partition efi** zum Erstellen von EFI-System Partitionen, den Befehl **create partition msr** , um reservierte Microsoft-Partitionen zu erstellen, und den Befehl **create partition primary** \(without the  **ID @ no__t-5 {Byte&#124;GUID}** Parameter @ no__t-7 zum Erstellen primärer Partitionen auf GPT-Datenträgern.<br /><br />**Datenträger für Master Boot Record**<br /><br />für Master Boot Record \(mbr @ no__t-1-Datenträgern geben Sie für die Partition ein Byte vom Typ Partitionstyp (in Hexadezimal Form) an. Wenn dieser Parameter für einen MBR-Datenträger nicht angegeben wird, erstellt der Befehl eine Partition des Typs 0x06, die angibt, dass ein Dateisystem nicht installiert ist. Dazu gehören:<br /><br />-LDM-Daten Partition: 0x42<br />-Wiederherstellungs Partition: 0x27<br />-Erkannte OEM-Partition: 0x12, 0x84, 0xde, 0xFE, 0xa0<br /><br />**GUID-Partitionstabellen-Datenträger**<br /><br />für die GUID-Partitionstabelle \(gpt @ no__t-1-Datenträger können Sie eine GUID für den Partitionstyp für die Partition angeben, die Sie erstellen möchten. Zu den erkannten GUIDs zählen:<br /><br />-EFI-Systempartition: c12a7328 @ no__t-0f81f @ no__t-111d2 @ no__t-2ba4b @ no__t-300a0c93ec93b<br />-Microsoft Reserved Partition: e3c9e316 @ no__t-00b5c @ no__t-14db8 @ no__t-2817d @ no__t-3F 92 df00215ae<br />-Basic Data Partition: ebd0a0a2 @ no__t-0b9e5 @ no__t-14433 @ no__t-287c0 @ no__t-368b6b72699c7<br />-LDM-Metadatenpartition auf einem dynamischen Datenträger: 5808c8aa @ no__t-07e8f @ no__t-142e0 @ no__t-285d2 @ no__t-3e1e90434cfb3<br />-LDM-Daten Partition auf einem dynamischen Datenträger: af9b60a0 @ no__t-01431 @ no__t-14f 62 @ no__t-2bc68 @ no__t-33311714a69ad<br />-Wiederherstellungs Partition: de94bba4 @ no__t-006d1 @ no__t-14d40 @ no__t-2a16a @ no__t-3BF d50179d6ac<br /><br />Wenn dieser Parameter für einen GPT-Datenträger nicht angegeben wird, erstellt der Befehl eine grundlegende Daten Partition. |
|            Noerr             |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            Nur für Skripterstellung. Wenn ein Fehler auftritt, verarbeitet DiskPart weiterhin Befehle so, als ob der Fehler nicht aufgetreten ist. Ohne den Noerr-Parameter bewirkt ein Fehler, dass DiskPart mit einem Fehlercode beendet wird.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
  
## <a name="remarks"></a>Hinweise  
  
-   Nachdem Sie die Partition erstellt haben, wird der Fokus automatisch auf die neue Partition verlagert.  
  
-   Die Partition erhält keinen Laufwerk Buchstaben. Sie müssen den **assign** -Befehl in DiskPart verwenden, um der Partition einen Laufwerk Buchstaben zuzuweisen.  
  
-   Ein Basis Datenträger muss ausgewählt werden, damit dieser Vorgang erfolgreich ausgeführt wird. Verwenden Sie den Befehl Datenträger **auswählen** , um einen Basis Datenträger auszuwählen und den Fokus darauf zu verschieben.  
  
## <a name="BKMK_examples"></a>Beispiele  
Geben Sie Folgendes ein, um eine primäre Partition mit einer Größe von 1000 Megabyte zu erstellen:  
  
```  
create partition primary size=1000  
```  
  
#### <a name="additional-references"></a>Weitere Verweise  
[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
  

  

