---
title: openfiles
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: c3be561d-a11f-4bf1-9835-8e4e96fe98ec
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 38b1d27b86551c6d4cd9e6b1ad87bfc0e8dd221d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71372501"
---
# <a name="openfiles"></a>openfiles



Ermöglicht es einem Administrator, Dateien und Verzeichnisse abzufragen, anzuzeigen oder zu trennen, die auf einem System geöffnet wurden. Aktiviert oder deaktiviert auch das globale Flag für die Liste der Objekte der Systemverwaltung.

Dieses Thema enthält Informationen zu den folgenden Befehlen:
-   [openfiles/disconnect](#BKMK_disconnect)
-   [openfiles/Query "aus](#BKMK_query)
-   [openfiles/local ein](#BKMK_local)

## <a name="BKMK_disconnect"></a>openfiles/disconnect

Ermöglicht einem Administrator das Trennen von Dateien und Ordnern, die per Remote Zugriff über einen freigegebenen Ordner geöffnet wurden.

### <a name="syntax"></a>Syntax

```
openfiles /disconnect [/s <System> [/u [<Domain>\]<UserName> [/p [<Password>]]]] {[/id <OpenFileID>] | [/a <AccessedBy>] | [/o {read | write | read/write}]} [/op <OpenFile>]
```

### <a name="parameters"></a>Parameter

|            Parameter             |                                                                                                                                 Beschreibung                                                                                                                                  |
|----------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|           /s \<system >           | Gibt das Remote System an, mit dem eine Verbindung hergestellt werden soll (nach Name oder IP-Adresse). Verwenden Sie keine umgekehrten Schrägstriche. Wenn Sie die Option **/s** nicht verwenden, wird der Befehl standardmäßig auf dem lokalen Computer ausgeführt. Dieser Parameter gilt für alle Dateien und Ordner, die im Befehl angegeben sind. |
|    /u [\<domäne > \] @ no__t-2     |                                                          Führt den Befehl mit den Berechtigungen des angegebenen Benutzerkontos aus. Wenn Sie die Option **/u** nicht verwenden, werden standardmäßig System Berechtigungen verwendet.                                                           |
|         /p [\<password >]         |                                               Gibt das Kennwort des Benutzerkontos an, das in der **/u** -Option angegeben ist. Wenn Sie die Option **/p** nicht verwenden, wird eine Kenn Wort Eingabeaufforderung angezeigt, wenn der Befehl ausgeführt wird.                                                |
|        /ID \<openfleid >         |                                       Trennt geöffnete Dateien mit der angegebenen Datei-ID. Das Platzhalter Zeichen **&#42;** () kann mit diesem Parameter verwendet werden.</br>Hinweis: Sie können den Befehl **openfiles/Query "aus** verwenden, um die Datei-ID zu suchen.                                       |
|         /a \<accessedby >         |                                                Trennt alle geöffneten Dateien, die mit dem im *Access sedby* -Parameter angegebenen Benutzernamen verknüpft sind. Das Platzhalter Zeichen **&#42;** () kann mit diesem Parameter verwendet werden.                                                 |
| /o {read \| Schreib \| Lese-/Schreibzugriff} |                                               Trennt alle geöffneten Dateien mit dem angegebenen Wert für den offenen Modus. Gültige Werte sind Lese-, Schreib-oder Lese-/Schreibzugriff. Das Platzhalter Zeichen **&#42;** () kann mit diesem Parameter verwendet werden.                                                |
|         /OP \<openfile >          |                                                           Trennt alle geöffneten Datei Verbindungen, die mit einem bestimmten geöffneten Dateinamen erstellt werden. Das Platzhalter Zeichen **&#42;** () kann mit diesem Parameter verwendet werden.                                                           |
|                /?                |                                                                                                                     Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                                     |

### <a name="examples"></a>Beispiele

Wenn Sie alle geöffneten Dateien mit der Datei-ID 26843578 trennen möchten, geben Sie Folgendes ein:
```
openfiles /disconnect /id 26843578
```
So trennen Sie alle geöffneten Dateien und Verzeichnisse, auf die der Benutzer "hiropln" zugreift,:
```
openfiles /disconnect /a hiropln
```
Geben Sie Folgendes ein, um alle geöffneten Dateien und Verzeichnisse mit dem Lese-/Schreibmodus zu trennen:
```
openfiles /disconnect /o read/write
```
Wenn Sie das Verzeichnis mit dem geöffneten Dateinamen "c:\testshare @ no__t-0" trennen möchten, geben Sie Folgendes ein, unabhängig davon, wer auf das Verzeichnis zugreift:
```
openfiles /disconnect /a * /op "c:\testshare\"
```
Wenn Sie alle geöffneten Dateien auf dem Remote Computer "srvmain" trennen möchten, auf den der Benutzer "hiropln" zugreift, unabhängig von ihrer ID, geben Sie Folgendes ein:
```
openfiles /disconnect /s srvmain /u maindom\hiropln /id *
```

## <a name="BKMK_query"></a>openfiles/Query "aus

Fragt alle geöffneten Dateien ab und zeigt diese an.

### <a name="syntax"></a>Syntax

```
openfiles /query [/s <System> [/u [<Domain>\]<UserName> [/p [<Password>]]]] [/fo {TABLE | LIST | CSV}] [/nh] [/v]
```

### <a name="parameters"></a>Parameter

|          Parameter           |                                                                                                                                 Beschreibung                                                                                                                                  |
|------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|         /s \<system >         | Gibt das Remote System an, mit dem eine Verbindung hergestellt werden soll (nach Name oder IP-Adresse). Verwenden Sie keine umgekehrten Schrägstriche. Wenn Sie die Option **/s** nicht verwenden, wird der Befehl standardmäßig auf dem lokalen Computer ausgeführt. Dieser Parameter gilt für alle Dateien und Ordner, die im Befehl angegeben sind. |
|  /u [\<domäne > \] @ no__t-2   |                                                          Führt den Befehl mit den Berechtigungen des angegebenen Benutzerkontos aus. Wenn Sie die Option **/u** nicht verwenden, werden standardmäßig System Berechtigungen verwendet.                                                           |
|       /p [\<password >]       |                                               Gibt das Kennwort des Benutzerkontos an, das in der **/u** -Option angegeben ist. Wenn Sie die Option **/p** nicht verwenden, wird eine Kenn Wort Eingabeaufforderung angezeigt, wenn der Befehl ausgeführt wird.                                                |
| [/FO {Table \| List \| CSV}] |                             Zeigt die Ausgabe im angegebenen Format an. Gültige Werte für das *Format* :</br>GLAUB  Zeigt die Ausgabe in einer Tabelle an.</br>LIST Zeigt die Ausgabe in einer Liste an.</br>CSV Zeigt die Ausgabe im Format mit Komma getrennten Werten an.                              |
|             /nh              |                                                                                Unterdrückt die Spaltenüberschrift in der Ausgabe. Nur gültig, wenn der **/FO** -Parameter auf **Table** oder **CSV**festgelegt ist.                                                                                 |
|              /v              |                                                                                                       Gibt an, dass ausführliche Informationen in der Ausgabe angezeigt werden.                                                                                                        |
|              /?              |                                                                                                                     Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                                     |

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um alle geöffneten Dateien abzufragen und anzuzeigen:
```
openfiles /query
```
Wenn Sie alle geöffneten Dateien im Tabellenformat ohne Header Abfragen und anzeigen möchten, geben Sie Folgendes ein:
```
openfiles /query /fo table /nh
```
Wenn Sie alle geöffneten Dateien im Listenformat mit detaillierten Informationen Abfragen und anzeigen möchten, geben Sie Folgendes ein:
```
openfiles /query /fo list /v
```
Wenn Sie alle geöffneten Dateien auf dem Remote System "srvmain" mithilfe der Anmelde Informationen für den Benutzer "hiropln" in der Domäne "Maindom" Abfragen und anzeigen möchten, geben Sie Folgendes ein:
```
openfiles /query /s srvmain /u maindom\hiropln /p p@ssW23
```

> [!NOTE]
> In diesem Beispiel wird das Kennwort in der Befehlszeile angegeben. Wenn Sie die Anzeige des Kennworts verhindern möchten, lassen Sie die Option **/p** aus. Sie werden zur Eingabe des Kennworts aufgefordert, das nicht auf dem Bildschirm angezeigt wird.

## <a name="BKMK_local"></a>openfiles/local ein

Aktiviert oder deaktiviert das globale Flag für die Liste der Objekte der Systemverwaltung. Bei Verwendung ohne Parameter zeigt **openfiles/local ein** den aktuellen Status der globalen Flag zum Auflisten von Objekten an.

### <a name="syntax"></a>Syntax

```
openfiles /local [on | off]
```

### <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|[on \| off]|Aktiviert oder deaktiviert das globale Flag für die Liste der System verwalteten Objekte, das lokale Datei Handles nachverfolgt.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

### <a name="remarks"></a>Hinweise

-   Wenn Sie das globale Flag zum Verwalten von Objekten aktivieren, kann das System verlangsamt werden.
-   Änderungen, die mithilfe der Option **on** oder **Off** vorgenommen wurden, werden erst wirksam, wenn Sie das System neu starten.

### <a name="examples"></a>Beispiele

Geben Sie Folgendes ein, um den aktuellen Status des globalen Flags für die Liste der verwalteten Objekte zu überprüfen:
```
openfiles /local
```
Standardmäßig ist das globale Flag zum Verwalten von Objekten deaktiviert, und die folgende Ausgabe wird angezeigt:
```
INFO: The system global flag 'maintain objects list' is currently disabled.
```
Geben Sie Folgendes ein, um das globale Flag "Objekte auflisten" zu aktivieren:
```
openfiles /local on
```
Wenn das globale Flag aktiviert ist, wird die folgende Meldung angezeigt:
```
SUCCESS: The system global flag 'maintain objects list' is enabled.
         This will take effect after the system is restarted.
```
Geben Sie Folgendes ein, um das globale Flag zum Verwalten von Objekten zu deaktivieren:
```
openfiles /local off
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)