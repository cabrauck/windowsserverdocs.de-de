---
title: WBADMIN-START SYSRECOVERY
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 95b8232f-7c42-452b-838e-15b0cf6faebe
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 9c653fa52a2a56267d6f0df169f8f9924f2aa94d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71362279"
---
# <a name="wbadmin-start-sysrecovery"></a>WBADMIN-START SYSRECOVERY



Führt eine Systemwiederherstellung (Bare-Metal-Recovery) mithilfe der Parameter aus, die Sie angeben.

> [!NOTE]
> Dieser Unterbefehl kann nur in der Windows-Wiederherstellungs Umgebung ausgeführt werden, und er ist standardmäßig nicht im Verwendungs Text von **Wbadmin**aufgeführt. Weitere Informationen finden Sie unter [Übersicht über die Windows-Wiederherstellungs Umgebung (Windows RE)](https://technet.microsoft.com/library/hh825173.aspx).

Wenn Sie mit diesem Unterbefehl eine Systemwiederherstellung durchführen möchten, müssen Sie Mitglied der Gruppe " **Sicherungs-Operatoren** " oder der Gruppe " **Administratoren** " sein, oder die entsprechenden Berechtigungen müssen an Sie delegiert worden sein.

Beispiele für die Verwendung dieses Unterbefehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
wbadmin start sysrecovery
-version:<VersionIdentifier>
-backupTarget:{<BackupDestinationVolume> | <NetworkShareHostingBackup>}
[-machine:<BackupMachineName>]
[-restoreAllVolumes]
[-recreateDisks]
[-excludeDisks]
[-skipBadClusterCheck]
[-quiet]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|-Version|Gibt den Versions Bezeichner für die wieder herzustellende Sicherung im Format mm/dd/yyyy-HH: mm an. Wenn Sie den Versions Bezeichner nicht kennen, geben Sie **Wbadmin Get Versions**ein.|
|-backupTarget|Gibt den Speicherort an, der die Sicherung oder Sicherungen enthält, die Sie wiederherstellen möchten. Dieser Parameter ist hilfreich, wenn sich der Speicherort von dem Speicherort unterscheidet, in dem die Sicherungen dieses Computers normalerweise gespeichert werden.|
|-Computer|Gibt den Namen des Computers an, den Sie wiederherstellen möchten. Dieser Parameter ist hilfreich, wenn mehrere Computer am gleichen Speicherort gesichert wurden. Sollte verwendet werden, wenn der **-backupTarget-** Parameter angegeben wird.|
|-restoreallvolumes|Stellt alle Volumes aus der ausgewählten Sicherung wieder her. Wenn dieser Parameter nicht angegeben wird, werden nur kritische Volumes (Volumes, die den Systemstatus und die Betriebssystemkomponenten enthalten) wieder hergestellt. Dieser Parameter ist hilfreich, wenn Sie während der Systemwiederherstellung nicht kritische Volumes wiederherstellen müssen.|
|-neu erstellte atedisks|Stellt eine Datenträger Konfiguration in dem Zustand wieder her, der beim Erstellen der Sicherung vorhanden war.</br>Warnung: Mit diesem Parameter werden alle Daten auf Volumes gelöscht, auf denen Betriebssystemkomponenten gehostet werden. Es können auch Daten aus Datenvolumes gelöscht werden.|
|-excluenddisks|Nur gültig, wenn der Parameter " **--Neuerstellung** " angegeben ist und als durch Trennzeichen getrennte Liste von Datenträger Bezeichnerzeichen eingegeben werden muss (wie in der Ausgabe von **Wbadmin Get Disks**aufgeführt). Ausgeschlossene Datenträger sind nicht partitioniert oder formatiert. Dieser Parameter hilft bei der Beibehaltung von Daten auf Datenträgern, die während des Wiederherstellungs Vorgangs nicht geändert werden sollen.|
|-skipbadclustercheck|Überspringt die Überprüfung der Wiederherstellungs Datenträger auf fehlerhafte Cluster Wenn Sie die Wiederherstellung auf einem alternativen Server oder auf einer anderen Hardware durchführen, wird empfohlen, diesen Parameter nicht zu verwenden. Sie können **chkdsk/b** jederzeit auf den Wiederherstellungs Datenträgern manuell ausführen, um Sie auf fehlerhafte Cluster zu überprüfen, und dann die Dateisystem Informationen entsprechend aktualisieren.</br>Warnung: Bis Sie **chkdsk** wie beschrieben ausführen, sind die in Ihrem wiederhergestellten System gemeldeten fehlerhaften Cluster möglicherweise nicht korrekt.|
|-quiet|Führt den Befehl ohne Aufforderungen an den Benutzer aus.|

## <a name="BKMK_examples"></a>Beispiele

Geben Sie Folgendes ein, um mit der Wiederherstellung der Informationen aus der Sicherung zu beginnen, die am 31. März, 2013 um 9:00 Uhr, auf Laufwerk d: ausgeführt wurde:
```
wbadmin start sysrecovery -version:03/31/2013-09:00 -backupTarget:d:
```
Geben Sie Folgendes ein, um mit der Wiederherstellung der Informationen aus der Sicherung zu beginnen, die am 2013 30. April um 9:00 Uhr ausgeführt wurde, die sich im freigegebenen Ordner \\ @ no__t-1servername\shared: für server01 befindet:
```
wbadmin start sysrecovery -version:04/30/2013-09:00 -backupTarget:\\servername\share -machine:server01
```

#### <a name="additional-references"></a>Weitere Verweise

-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
-   [Wbadmin](wbadmin.md)
-   Cmdlet " [Get-wbbaremetalrecovery](https://technet.microsoft.com/library/jj902461.aspx) "