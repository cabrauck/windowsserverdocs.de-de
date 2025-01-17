---
title: cleanmgr
description: Erfahren Sie, wie Sie mithilfe von Befehlszeilenoptionen das Tool für die Datenträger Bereinigung (cleanmgr. exe) so konfigurieren, dass bestimmte Dateien automatisch bereinigt werden.
ms.prod: windows-server
ms.reviewer: cosmosdarwin
author: iangpgh
ms.author: jgerend
manager: daveba
ms.technology: storage-spaces
ms.date: 06/20/2019
ms.openlocfilehash: 20bc60abc747e6bab0ef59f38d0a392f18d75abe
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71379375"
---
# <a name="cleanmgr"></a>cleanmgr

> Gilt für: Windows Server 2019, Windows Server 2016, Windows Server 2012, Windows Server 2008 R2, Windows Server (halbjährlicher Kanal)

Löscht unnötige Dateien von der Festplatte Ihres Computers. Sie können Befehlszeilenoptionen verwenden, um anzugeben, dass cleanmgr temporäre Dateien, Internet Dateien, heruntergeladene Dateien und Papierkorb Dateien bereinigt. Anschließend können Sie die Ausführung der Aufgabe zu einem bestimmten Zeitpunkt mithilfe des Tools "geplante Aufgaben" planen.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#examples).

## <a name="syntax"></a>Syntax

```
cleanmgr [/d <driveletter>] [/sageset:n]  [/sagerun:n] [/TUNEUP:n] [/LOWDISK] [/VERYLOWDISK]
```

## <a name="parameters"></a>Parameter

|      Parameter      |    Beschreibung     |
| ------------------- | ------------------ |
|  /d \<driveletter >          | Gibt das Laufwerk an, das Sie bereinigen möchten.<br>**Hinweis**: Die/d-Option wird nicht mit/sagerun: n verwendet. |
| /sageset: n | Zeigt das Dialogfeld Einstellungen für die Datenträger Bereinigung an und erstellt außerdem einen Registrierungsschlüssel zum Speichern der von Ihnen ausgewählten Einstellungen. Der `n`-Wert, der in der Registrierung gespeichert ist, ermöglicht es Ihnen, Aufgaben für die Datenträger Bereinigung anzugeben, die ausgeführt werden soll. Der `n`-Wert kann ein beliebiger ganzzahliger Wert zwischen 0 und 65535 sein. Wenn Sie alle Optionen bei Verwendung der Option/sageset verwenden möchten, geben Sie das Laufwerk an, auf dem Windows installiert ist.  |
|  /sagerun: n  |  Führt die angegebenen Aufgaben aus, die dem n-Wert zugewiesen sind, wenn Sie die Option \sageset verwenden. Alle Laufwerke auf dem Computer werden aufgezählt, und das ausgewählte Profil wird für jedes Laufwerk ausgeführt.           |
| /TuneUp: n    | Führen Sie/sageset und/sagerun für denselben `n` aus. |
| /LOWDISK     | Führen Sie mit den Standardeinstellungen aus. |
| /VERYLOWDISK | Führen Sie mit den Standardeinstellungen aus, keine Eingabe Aufforderungen. |
| /?           | Hilfe anzeigen. |

## <a name="options"></a>Optionen

Zu den Optionen für die Dateien, die Sie für die Datenträger Bereinigung mithilfe von/sageset und/sagerun angeben können, gehören:

- **Temporäre Setup Dateien** : Hierbei handelt es sich um Dateien, die von einem Setup Programm erstellt wurden, das nicht mehr ausgeführt wird.

- **Heruntergeladene Programmdateien** : heruntergeladene Programmdateien sind ActiveX-Steuerelemente und Java-Programme, die automatisch aus dem Internet heruntergeladen werden, wenn Sie bestimmte Seiten anzeigen. Diese Dateien werden temporär im Ordner "heruntergeladene Programmdateien" auf der Festplatte gespeichert. Diese Option umfasst die Schaltfläche Dateien anzeigen, sodass Sie die Dateien sehen können, bevor Sie von der Datenträger Bereinigung entfernt werden. Mit der Schaltfläche wird der Ordner "c:\winnt\herunter geladene Programmdateien" geöffnet.

- **Temporäre Internetdateien** : der Ordner "temporäre Internetdateien" enthält Webseiten, die für die schnelle Anzeige auf der Festplatte gespeichert sind. Mit der Datenträger Bereinigung werden diese Seiten entfernt, die personalisierten Einstellungen für Webseiten bleiben jedoch erhalten. Diese Option enthält auch die Schaltfläche Dateien anzeigen, die den Ordner "c:\Dokumente und Einstellungen\Benutzername\Lokale Einstellungen\Temporäre Internet Dateien \ Content.IE5" öffnet. 

- **Alte CHKDSK-Dateien** : Wenn Chkdsk einen Datenträger auf Fehler überprüft, speichert CHKDSK möglicherweise verlorene Dateifragmente als Dateien im Stamm Ordner auf dem Datenträger. Diese Dateien sind nicht erforderlich.

- **Papier** Korb: der Papierkorb enthält Dateien, die Sie vom Computer gelöscht haben. Diese Dateien werden erst dauerhaft entfernt, wenn Sie den Papierkorb leeren. Diese Option umfasst die Schaltfläche Dateien anzeigen, mit der der Papierkorb geöffnet wird. **Hinweis**: Ein Papierkorb kann in mehr als einem Laufwerk angezeigt werden, beispielsweise nicht nur in% SystemRoot%.

- **Temporäre Dateien** : Programme speichern manchmal temporäre Informationen in einem temporären Ordner. Vor dem Ausführen eines Programms löscht das Programm diese Informationen in der Regel. Sie können temporäre Dateien, die nicht innerhalb der letzten Woche geändert wurden, sicher löschen.

- **Temporäre Offlinedateien** temporäre Offline Dateien sind lokale Kopien der zuletzt verwendeten Netzwerkdateien. Diese Dateien werden automatisch zwischengespeichert, sodass Sie Sie nach dem Trennen der Verbindung mit dem Netzwerk verwenden können. Die Schaltfläche Dateien anzeigen Öffnet den Ordner Offlinedateien.

- **Offlinedateien** -Offline Dateien sind lokale Kopien von Netzwerkdateien, die Sie speziell offline zur Verfügung stellen möchten, sodass Sie Sie nach dem Trennen der Verbindung mit dem Netzwerk verwenden können. Die Schaltfläche Dateien anzeigen Öffnet den Ordner Offlinedateien.

- **Alte Dateien komprimieren** : Windows kann Dateien komprimieren, die Sie in jüngster Zeit nicht verwendet haben. Durch das Komprimieren von Dateien wird Speicherplatz gespart, aber Sie können die Dateien weiterhin verwenden. Es werden keine Dateien gelöscht. Da Dateien mit unterschiedlichen Raten komprimiert werden, ist die angezeigte Menge an Speicherplatz ungefähr annähernd. Mit der Schaltfläche "Optionen" können Sie angeben, wie viele Tage gewartet werden soll, bevor eine Datenträger Bereinigung eine nicht verwendete Datei komprimiert.

- **Katalogdateien für den inhaltsindexer** : der Indizierungs Dienst beschleunigt und verbessert die Dateisuche, indem ein Index der Dateien auf dem Datenträger verwaltet wird. Diese Katalogdateien bleiben von einem vorherigen Indizierungs Vorgang und können problemlos gelöscht werden. **Hinweis**: Die Katalog Datei wird möglicherweise in mehr als einem Laufwerk angezeigt, z. b. nicht nur in% SystemRoot%.

**Hinweis** Wenn Sie die Bereinigung des Laufwerks angeben, das die Windows-Installation enthält, sind alle diese Optionen auf der Registerkarte "Datenträger Bereinigung" verfügbar. Wenn Sie ein anderes Laufwerk angeben, sind nur die Optionen Papierkorb und Katalogdateien für Inhalts Index auf der Registerkarte Datenträger Bereinigung verfügbar. 

## <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um die Datenträger Bereinigungs-APP so auszuführen, dass Sie in Ihrem Dialogfeld Optionen für die spätere Verwendung angeben können, indem Sie die Einstellungen in Set **1**speichern:

```
cleanmgr /sageset:1
```

Zum Ausführen der Datenträger Bereinigung und einschließen der Optionen, die Sie mit dem Befehl cleanmgr/sageset: 1 angegeben haben, geben Sie Folgendes ein:

```
cleanmgr /sagerun:1
```

Um ```cleanmgr /sageset:1``` und ```cleanmgr /sagerun:1``` zu starten, geben Sie Folgendes ein:

```
cleanmgr /tuneup:1
```

## <a name="additional-references"></a>Weitere Verweise

[Freigeben von Laufwerk Speicher in Windows 10](https://support.microsoft.com/en-us/help/12425/windows-10-free-up-drive-space)
