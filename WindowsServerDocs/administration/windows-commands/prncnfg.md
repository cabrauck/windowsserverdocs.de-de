---
title: prncnfg
description: Erfahren Sie, wie Sie mit dem Befehl Prncfg einen Drucker konfigurieren.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 38a4e8fa-3122-495b-a125-35b926bc6415
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: 5cbbf82e832c50d168e0bef06b2b7c3022dd90e8
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71372139"
---
# <a name="prncnfg"></a>prncnfg

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Konfiguriert oder zeigt Konfigurationsinformationen zu einem Drucker an.

## <a name="syntax"></a>Syntax
```
cscript Prncnfg {-g | -t | -x | -?} [-S <ServerName>] [-P <printerName>] [-z <NewprinterName>] [-u <UserName>] [-w <Password>] [-r <PortName>] [-l <Location>] [-h <Sharename>] [-m <Comment>] [-f <SeparatorFileName>] [-y <Datatype>] [-st <starttime>] [-ut <Untiltime>] [-i <DefaultPriority>] [-o <Priority>] [<+|->shared] [<+|->direct] [<+|->hidden] [<+|->published] [<+|->rawonly] [<+|->queued] [<+|->enablebidi] [<+|->keepprintedjobs] [<+|->workoffline] [<+|->enabledevq] [<+|->docompletefirst]
```

## <a name="parameters"></a>Parameter
|Parameter|Beschreibung|
|-------|--------|
|-g|Zeigt Konfigurationsinformationen zu einem Drucker an.|
|-t|Konfiguriert einen Drucker.|
|-x|benennt einen Drucker um.|
|-S \<Server Name @ no__t-1|Gibt den Namen des Remote Computers an, der den Drucker hostet, den Sie verwalten möchten. Wenn Sie keinen Computer angeben, wird der lokale Computer verwendet.|
|-P \<printername @ no__t-1|Gibt den Namen des Druckers an, den Sie verwalten möchten. Erforderlich.|
|-z \<newprintername @ no__t-1|Gibt den neuen Drucker Namen an. Erfordert die Parameter **-x** und **-P** .|
|-u \<username @ no__t-1-w \<password @ no__t-3|Gibt ein Konto mit Berechtigungen zum Herstellen einer Verbindung mit dem Computer an, der den zu verwaltenden Drucker hostet. Alle Mitglieder der lokalen Administratoren Gruppe des Ziel Computers verfügen über diese Berechtigungen, die Berechtigungen können jedoch auch anderen Benutzern erteilt werden. Wenn Sie kein Konto angeben, müssen Sie unter einem Konto mit diesen Berechtigungen angemeldet sein, damit der Befehl funktioniert.|
|-r \<portname @ no__t-1|Gibt den Port an, mit dem der Drucker verbunden ist. Wenn es sich um einen parallelen oder seriellen Anschluss handelt, verwenden Sie die ID des Ports (z. b. LPT1 oder COM1). Wenn dies ein TCP/IP-Port ist, verwenden Sie den Portnamen, der beim Hinzufügen des Ports angegeben wurde.|
|-l \<location @ no__t-1|Gibt den Drucker Speicherort an, z. b. "Raum kopieren".|
|-h \<sharename @ no__t-1|Gibt den Freigabe Namen des Druckers an.|
|-m \<comment @ no__t-1|Gibt die Kommentar Zeichenfolge des Druckers an.|
|-f \<separatorfilename @ no__t-1|Gibt eine Datei an, die den Text enthält, der auf der Trenn Seite angezeigt wird.|
|-y \<datatype @ no__t-1|Gibt die Datentypen an, die der Drucker annehmen kann.|
|-St \<starttime @ no__t-1|Konfiguriert den Drucker für eingeschränkte Verfügbarkeit. Gibt die Uhrzeit an, zu der der Drucker verfügbar ist. Wenn Sie ein Dokument an einen Drucker senden, wenn es nicht verfügbar ist, wird das Dokument gespeichert (Spoolvorgang), bis der Drucker verfügbar ist. Sie müssen die Uhrzeit als 24-Stunden-Format angeben. Wenn Sie z. b. 11:00 Uhr angeben möchten, geben Sie **2300**ein.|
|-UT \<endtime @ no__t-1|Konfiguriert den Drucker für eingeschränkte Verfügbarkeit. Gibt die Uhrzeit an, zu der der Drucker nicht mehr verfügbar ist. Wenn Sie ein Dokument an einen Drucker senden, wenn es nicht verfügbar ist, wird das Dokument gespeichert (Spoolvorgang), bis der Drucker verfügbar ist. Sie müssen die Uhrzeit als 24-Stunden-Format angeben. Wenn Sie z. b. 11:00 Uhr angeben möchten, geben Sie **2300**ein.|
|-o \<priority @ no__t-1|Gibt eine Priorität an, die der Spooler zum Weiterleiten von Druckaufträgen in der Druck Warteschlange verwendet. Eine Druck Warteschlange mit höherer Priorität empfängt alle zugehörigen Aufträge vor jeder Warteschlange mit niedrigerer Priorität.|
|-i \<defaultpriority @ no__t-1|Gibt die Standardpriorität an, die jedem Druckauftrag zugewiesen ist.|
|{+&#124;-} freigegeben|Gibt an, ob dieser Drucker im Netzwerk freigegeben ist.|
|{+&#124;-} direkt|Gibt an, ob das Dokument direkt an den Drucker gesendet werden soll, ohne dass es gespoolte ist.|
|{+&#124;-} veröffentlicht|Gibt an, ob dieser Drucker in Active Directory veröffentlicht werden soll. Wenn Sie den Drucker veröffentlichen, können andere Benutzer basierend auf dem Speicherort und den Funktionen (z. b. Farb Druck und Heftung) danach suchen.|
|{+&#124;-} ausgeblendet|Reservierte Funktion.|
|{+&#124;-} raweinzierl|Gibt an, ob in dieser Warteschlange nur unformatierte Datendruck Aufträge gespoziert werden können.|
|{+ &#124; -} in Warteschlange eingereiht|Gibt an, dass der Drucker erst nach dem Spoolvorgang der letzten Seite des Dokuments gedruckt werden soll. Das Druckprogramm ist nicht verfügbar, bis das Drucken des Dokuments abgeschlossen ist. Durch die Verwendung dieses Parameters wird jedoch sichergestellt, dass das gesamte Dokument für den Drucker verfügbar ist.|
|{+ &#124; -} KeepPrintedJobs|Gibt an, ob der Spooler Dokumente nach dem Drucken aufbewahren soll. Wenn Sie diese Option aktivieren, kann ein Benutzer ein Dokument aus der Druck Warteschlange und nicht aus dem Druckprogramm erneut an den Drucker übermitteln.|
|{+ &#124; -} WorkOffline|Gibt an, ob ein Benutzer Druckaufträge an die Druck Warteschlange senden kann, wenn der Computer nicht mit dem Netzwerk verbunden ist.|
|{+ &#124; -} EnableDevq|Gibt an, ob Druckaufträge, die nicht der Drucker Einrichtung entsprechen (z. b. bei nicht-PostScript-Druckern gespoolten Dateien), in der Warteschlange gespeichert werden sollen, anstatt gedruckt zu werden.|
|{+ &#124; -} docompletefirst|Gibt an, ob der Spooler Druckaufträge mit niedrigerer Priorität senden soll, bei denen die Spoolvorgänge abgeschlossen wurden, bevor Druckaufträge mit einer höheren Priorität gesendet werden, für die das Spoolvorgang noch nicht abgeschlossen wurde. Wenn diese Option aktiviert ist und keine Dokumente das Spoolvorgang abgeschlossen haben, sendet der Spooler größere Dokumente vor kleineren. Sie sollten diese Option aktivieren, wenn Sie die Drucker Effizienz auf Kosten der Auftrags Priorität maximieren möchten. Wenn diese Option deaktiviert ist, sendet der Spooler zunächst immer Aufträge mit höherer Priorität an die entsprechenden Warteschlangen.|
|{+ &#124; -} EnableBIDI|Gibt an, ob der Druckerstatus Informationen an den Spooler sendet.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise
-   Der **prncnfg** -Befehl ist ein Visual Basic Skript, das sich im Verzeichnis%WINdir%\System32\printing_Admin_Scripts @ no__t-1 @ no__t-2 befindet. Wenn Sie diesen Befehl verwenden möchten, geben Sie an einer Eingabeaufforderung **cscript** ein, gefolgt vom vollständigen Pfad zur Datei prncnfg, oder ändern Sie die Verzeichnisse in den entsprechenden Ordner. Zum Beispiel:
    ```
    cscript %WINdir%\System32\printing_Admin_Scripts\en-US\prncnfg
    ```
-   Wenn die Informationen, die Sie angeben, Leerzeichen enthalten, verwenden Sie den Text in Anführungszeichen (z. b. `"computer Name"`).

## <a name="BKMK_examples"></a>Beispiele
Wenn Sie Konfigurationsinformationen für den Drucker namens colorprinter_2 mit einer Druck Warteschlange anzeigen möchten, die vom Remote Computer namens HRServer gehostet wird, geben Sie Folgendes ein:
```
cscript prncnfg -g -S HRServer -P colorprinter_2 
```

Geben Sie Folgendes ein, um einen Drucker mit dem Namen colorprinter_2 zu konfigurieren, damit der Spooler auf dem Remote Computer mit dem Namen HRServer Druckaufträge nach dem Drucken beibehält:
```
cscript prncnfg -t -S HRServer -P colorprinter_2 +keepprintedjobs 
```

Wenn Sie den Namen eines Druckers auf dem Remote Computer mit dem Namen HRServer von colorprinter_2 auf COLORPRINTER 3 ändern möchten, geben Sie Folgendes ein:
```
cscript prncnfg -x -S HRServer -P colorprinter_2 -z "colorprinter 3" 
```

#### <a name="additional-references"></a>Weitere Verweise
[Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
[Druck Befehlsreferenz](print-command-reference.md)
