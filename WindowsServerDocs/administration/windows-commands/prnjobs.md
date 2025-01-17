---
title: prnjobs
description: Erfahren Sie, wie Druckaufträge über die Befehlszeile verwaltet werden.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 5ad34199-7a5a-40c1-8053-bccd5929df43
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 07/11/2018
ms.openlocfilehash: c4fb9be9545274bbbf33926042f7a4deec5ceb05
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71372097"
---
# <a name="prnjobs"></a>prnjobs

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

hält Druckaufträge an, setzt Sie fort, bricht Sie ab und listet Sie auf.

## <a name="syntax"></a>Syntax
```
cscript Prnjobs {-z | -m | -x | -l | -?} [-s <ServerName>] 
[-p <printerName>] [-j <JobID>] [-u <UserName>] [-w <Password>]
```

## <a name="parameters"></a>Parameter

|          Parameter           |                                                                                                                                                                                        Beschreibung                                                                                                                                                                                        |
|------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|              -z              |                                                                                                                                                                 hält den Druckauftrag an, der mit dem **-j-** Parameter angegeben wird.                                                                                                                                                                 |
|              -m              |                                                                                                                                                                Setzt den mit dem **-j-** Parameter angegebenen Druckauftrag fort.                                                                                                                                                                 |
|              -x              |                                                                                                                                                                Bricht den mit dem **-j-** Parameter angegebenen Druckauftrag ab.                                                                                                                                                                 |
|              -l              |                                                                                                                                                                        Listet alle Druckaufträge in einer Druck Warteschlange auf.                                                                                                                                                                         |
|       -s \<servername >       |                                                                                                                  Gibt den Namen des Remote Computers an, der den Drucker hostet, den Sie verwalten möchten. Wenn Sie keinen Computer angeben, wird der lokale Computer verwendet.                                                                                                                  |
|      -p \<printername >       |                                                                                                                                                           Gibt den Namen des Druckers an, den Sie verwalten möchten. Erforderlich.                                                                                                                                                            |
|         -j \<jobid >          |                                                                                                                                                                Gibt (nach ID-Nummer) den Druckauftrag an, den Sie abbrechen möchten.                                                                                                                                                                 |
| -u \<username >-w <Password> | Gibt ein Konto mit Berechtigungen zum Herstellen einer Verbindung mit dem Computer an, der den zu verwaltenden Drucker hostet. Alle Mitglieder der lokalen Administratoren Gruppe des Ziel Computers verfügen über diese Berechtigungen, die Berechtigungen können jedoch auch anderen Benutzern erteilt werden. Wenn Sie kein Konto angeben, müssen Sie unter einem Konto mit diesen Berechtigungen angemeldet sein, damit der Befehl funktioniert. |
|              /?              |                                                                                                                                                                           Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                                                                                            |

## <a name="remarks"></a>Hinweise
-   Der **prnjobs** -Befehl ist ein Visual Basic Skript, das sich im Verzeichnis%WINdir%\System32\printing_Admin_Scripts @ no__t-1 @ no__t-2 befindet. Wenn Sie diesen Befehl verwenden möchten, geben Sie an einer Eingabeaufforderung **cscript** gefolgt vom vollständigen Pfad zur Datei prnjobs ein, oder ändern Sie die Verzeichnisse in den entsprechenden Ordner. Zum Beispiel:
    ```
    cscript %WINdir%\System32\printing_Admin_Scripts\en-US\prnjobs.vbs
    ```
-   Wenn die Informationen, die Sie angeben, Leerzeichen enthalten, verwenden Sie den Text in Anführungszeichen (z. b. `"computer Name"`).

## <a name="BKMK_examples"></a>Beispiele
Geben Sie Folgendes ein, um einen Druckauftrag mit der Auftrags-ID 27 anzuhalten, die auf dem Remote Computer mit dem Namen HRServer zum Drucken auf dem Drucker mit dem Namen COLORPRINTER gesendet wurde:
```
cscript prnjobs.vbs -z -s HRServer -p colorprinter -j 27
```
Um alle aktuellen Druckaufträge in der Warteschlange für den lokalen Drucker mit dem Namen colorprinter_2 aufzulisten, geben Sie Folgendes ein:
```
cscript prnjobs.vbs -l -p colorprinter_2
```

#### <a name="additional-references"></a>Weitere Verweise

-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)
-   [Druckbefehlsreferenz](print-command-reference.md)
