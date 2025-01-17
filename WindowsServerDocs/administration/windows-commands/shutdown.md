---
title: Herunterfahren
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c432f5cf-c5aa-4665-83af-0ec52c87112e
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: e8a5170fa214d4ed639ff3b817cf949a9f44ebd6
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71383887"
---
# <a name="shutdown"></a>Herunterfahren



Ermöglicht das Herunterfahren oder Neustarten von jeweils einem lokalen Computer oder Remotecomputer.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
shutdown [/i | /l | /s | /r | /a | /p | /h | /e] [/f] [/m \\<ComputerName>] [/t <XXX>] [/d [p|u:]<XX>:<YY> [/c "comment"]] 
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/i|Zeigt das **Dialog Feld Remote herunter** fahren an. Die **/i** -Option muss der erste Parameter sein, der dem Befehl folgt. Wenn **/i** angegeben wird, werden alle anderen Optionen ignoriert.|
|/l|Meldet den aktuellen Benutzer sofort und ohne Timeout Zeitraum ab. **/L** kann nicht mit **/m** oder **/t**verwendet werden.|
|/s|Fährt den Computer herunter.|
|/r|Startet den Computer nach dem Herunterfahren neu.|
|/a|Bricht das Herunterfahren eines Systems ab. Nur während des Timeout Zeitraums gültig. Um **/a**zu verwenden, müssen Sie auch die **/m** -Option verwenden.|
|/p|Schaltet nur den lokalen Computer (nicht einen Remote Computer) ein – ohne Timeout Zeitraum oder Warnung. Sie können **/p** nur mit **/d** oder **/f**verwenden. Wenn der Computer keine ausschalten-Funktionalität unterstützt, wird er bei Verwendung von **/p**heruntergefahren, aber die Stromversorgung des Computers bleibt eingeschaltet.|
|/h|Versetzt den lokalen Computer in den Ruhezustand, wenn der Ruhezustand aktiviert ist. Sie können **/h** nur mit **/f**verwenden.|
|/e|Hiermit können Sie den Grund für das unerwartete Herunterfahren auf dem Bereitstellungs Zielcomputer dokumentieren.|
|/f|Erzwingt das Schließen der Ausführung von Anwendungen ohne Warn Benutzer.</br>Vorsicht: Die Verwendung der **/f** -Option kann zu einem Verlust nicht gespeicherter Daten führen.|
|/m \\ @ no__t-1 @ no__t-2computername >|Gibt den Zielcomputer an. Kann nicht mit der **/l** -Option verwendet werden.|
|/t \<xxx >|Legt den Timeout Zeitraum oder die Verzögerung auf *xxx* Sekunden vor einem Neustart oder Herunterfahren fest. Dies bewirkt, dass eine Warnung in der lokalen Konsole angezeigt wird. Sie können 0-600 Sekunden angeben. Wenn Sie **/t**nicht verwenden, beträgt der Timeout Zeitraum standardmäßig 30 Sekunden.|
|/d [p @ no__t-0U:] \<xx >: \<YY >|Listet den Grund für den Neustart oder das Herunterfahren des Systems auf. Im folgenden werden die Parameterwerte aufgeführt:</br>**p** gibt an, dass der Neustart oder das Herunterfahren geplant ist.</br>**u** gibt an, dass der Grund Benutzer definiert ist.</br>Hinweis: Wenn **p** oder **u** nicht angegeben wird, ist der Neustart oder das Herunterfahren nicht geplant.</br>*Xx* gibt die Hauptgrund Zahl an (positive ganze Zahl kleiner als 256).</br>*J* Gibt die neben Grund Nummer an (positive Ganzzahl kleiner als 65536).|
|/c "\<comment >"|Hier können Sie detaillierte Kommentare zum Grund für das Herunterfahren eingeben. Sie müssen zuerst einen Grund angeben, indem Sie die Option **/d** verwenden. Sie müssen Kommentare in Anführungszeichen einschließen. Sie können maximal 511 Zeichen verwenden.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an, einschließlich einer Liste der Haupt-und neben Gründe, die auf dem lokalen Computer definiert sind.|

## <a name="remarks"></a>Hinweise

-   Benutzern muss das **System** Benutzerrecht Herunterfahren zugewiesen werden, um einen lokalen oder remote verwalteten Computer zu beenden, der den Befehl **Shutdown** verwendet.
-   Benutzer müssen Mitglied der Gruppe "Administratoren" sein, um ein unerwartetes Herunterfahren eines lokalen oder remote verwalteten Computers zu kommentieren. Wenn der Zielcomputer einer Domäne angehört, können Mitglieder der Gruppe "Domänen-Admins" dieses Verfahren möglicherweise ausführen. Weitere Informationen finden Sie in den folgenden Themen:  
    -   [Lokale Standard Gruppen](https://technet.microsoft.com/library/cc785098(v=ws.10).aspx)
    -   [Standard Gruppen](https://technet.microsoft.com/library/cc756898(v=ws.10).aspx)
-   Wenn Sie mehrere Computer gleichzeitig Herunterfahren möchten, können Sie das **herunter** fahren für jeden Computer mithilfe eines Skripts aufrufen, oder Sie können **Shutdown** **/i** verwenden, um das Dialog Feld Remote Herunterfahren anzuzeigen.
-   Wenn Sie Haupt-und Nebengrund Codes angeben, müssen Sie diese Ursachen Codes zunächst auf jedem Computer definieren, auf dem Sie die Gründe verwenden möchten. Wenn die Ursachen Codes nicht auf dem Zielcomputer definiert sind, kann die Shutdown-Ereignisprotokollierung den richtigen Grund Text nicht protokollieren.
-   Denken Sie daran, dass ein Herunterfahren mithilfe des Parameters " **p:** " geplant ist. **P:** gibt an, dass ein Herunterfahren nicht geplant ist. Wenn Sie **p:** gefolgt von dem Ursachen Code für ein ungeplantes Herunterfahren eingeben, führt der Befehl das Herunterfahren nicht aus. Wenn Sie hingegen **p:** weglassen und den Grund Code für ein geplantes Herunterfahren eingeben, führt der Befehl das Herunterfahren nicht aus.

## <a name="BKMK_examples"></a>Beispiele

So erzwingen Sie das Schließen und Neustarten des lokalen Computers nach einer Verzögerung von einer Minute mit dem Grund "Anwendung: Wartung (geplant) "und der Kommentar" Neukonfiguration von MyApp. exe ":
```
shutdown /r /t 60 /c "Reconfiguring myapp.exe" /f /d p:4:1
```
Um den Remote Computer \\ @ no__t-1servername mit denselben Parametern neu zu starten, geben Sie Folgendes ein:
```
shutdown /r /m \\servername /t 60 /c "Reconfiguring myapp.exe" /f /d p:4:1
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
