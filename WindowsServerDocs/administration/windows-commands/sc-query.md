---
title: SC-Abfrage
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ac365f89-4b20-4de6-a582-b204c5e7d0eb
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 4d2f3f603ad173b5ab90bc56a9a4e589c0fe9d8a
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71384343"
---
# <a name="sc-query"></a>SC-Abfrage



Ruft Informationen zum angegebenen Dienst, Treiber, Diensttyp oder Typ des Treibers ab und zeigt diese an.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
sc [<ServerName>] query [<ServiceName>] [type= {driver | service | all}] [type= {own | share | interact | kernel | filesys | rec | adapt}] [state= {active | inactive | all}] [bufsize= <BufferSize>] [ri= <ResumeIndex>] [group= <GroupName>]
```

## <a name="parameters"></a>Parameter

|       Parameter        |                                                                                                                          Beschreibung                                                                                                                          |
|------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     \<servername >      |                       Gibt den Namen des Remote Servers an, auf dem sich der Dienst befindet. Der Name muss das Universal Naming Convention Format (UNC) verwenden (z. b. \\ @ no__t-1myserver). Wenn Sie "SC. exe" lokal ausführen möchten, lassen Sie diesen Parameter Weg.                        |
|     \<servicename >     |                                      Gibt den Dienstnamen an, der vom **getkeyname** -Vorgang zurückgegeben wird. Dieser **Abfrage** Parameter wird nicht in Verbindung mit anderen **Abfrage** Parametern (mit Ausnahme von *Servername*) verwendet.                                      |
|     Type = {Driver      |                                                                                                                            Dienst                                                                                                                            |
|       Type = {Own       |                                                                                                                             Freigeben                                                                                                                             |
|     State = {Active     |                                                                                                                           VSTE                                                                                                                            |
| buf size = \<buffersize > |                     Gibt die Größe (in Bytes) des enumerationspuffers an. Die Standardpuffergröße beträgt 1.024 Bytes. Sie sollten die Größe des enumerationspuffers erhöhen, wenn die aus einer Abfrage resultierende Anzeige 1.024 Bytes überschreitet.                      |
|   RI = \<resumeindex >   | Gibt die Indexnummer an, bei der die Enumeration gestartet oder fortgesetzt werden soll. Der Standardwert ist **0** (null). Verwenden Sie diesen Parameter in Verbindung mit dem Parameter " **bussize =** ", wenn mehr Informationen von einer Abfrage zurückgegeben werden, als der Standard Puffer anzeigen kann. |
|  Group = \<groupname >   |                                                                             Gibt die aufzuzählende Dienstgruppe an. Standardmäßig werden alle Gruppen aufgelistet (**Group = ""** ).                                                                              |
|           /?           |                                                                                                             Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                              |

## <a name="remarks"></a>Hinweise

- Ohne Leerzeichen zwischen einem Parameter und dessen Wert (d. h. **Type = own**, nicht **Type = own**) schlägt der Vorgang fehl.
- Der **Abfrage** Vorgang zeigt die folgenden Informationen zu einem Dienst an: SERVICE_NAME (Name des Registrierungs unter Schlüssels des dienstanders), Typ, Status (sowie nicht verfügbare Zustände), WIN32_EXIT_B, SERVICE_EXIT_B, Checkpoint und WAIT_HINT.
- Der **Type =** -Parameter kann in einigen Fällen zweimal verwendet werden. Die erste Darstellung des **Type =** -Parameters gibt an, ob Dienste, Treiber oder beides (**alle**) abgefragt werden sollen. Die zweite Darstellung des **Type =** -Parameters gibt einen Typ aus dem **Create** -Vorgang an, um den Bereich einer Abfrage weiter einzugrenzen.
- Wenn die von einem **Abfrage** Befehl resultierende Anzeige die Größe des enumerationspuffers überschreitet, wird eine Meldung ähnlich der folgenden angezeigt:  
  ```
  Enum: more data, need 1822 bytes start resume at index 79
  ```  
  Um die restlichen **Abfrage** Informationen anzuzeigen, führen Sie die **Abfrage**erneut aus, und legen Sie für " **bufsize =** " die Anzahl von Bytes und für " **RI =** " den angegebenen Index fest. Beispielsweise würde die verbleibende Ausgabe angezeigt werden, indem Sie an der Eingabeaufforderung Folgendes eingeben:  
  ```
  sc query bufsize= 1822 ri= 79
  ```

## <a name="BKMK_examples"></a>Beispiele

Wenn Sie nur Informationen für aktive Dienste anzeigen möchten, geben Sie einen der folgenden Befehle ein:
```
sc query
sc query type= service
```
Um Informationen für aktive Dienste anzuzeigen und eine Puffergröße von 2.000 Bytes anzugeben, geben Sie Folgendes ein:
```
sc query type= all bufsize= 2000
```
Geben Sie Folgendes ein, um Informationen für den wuauserv-Dienst anzuzeigen:
```
sc query wuauserv
```
Geben Sie Folgendes ein, um Informationen für alle Dienste anzuzeigen (aktiv und inaktiv):
```
sc query state= all
```
Zum Anzeigen von Informationen für alle Dienste (aktiv und inaktiv) geben Sie ab Zeile 56 Folgendes ein:
```
sc query state= all ri= 56
```
Geben Sie Folgendes ein, um Informationen für interaktive Dienste anzuzeigen:
```
sc query type= service type= interact
```
Geben Sie Folgendes ein, um nur Informationen für Treiber anzuzeigen:
```
sc query type= driver
```
Geben Sie Folgendes ein, um Informationen für Treiber in der Network Driver Interface Specification (NDIS)-Gruppe anzuzeigen:
```
sc query type= driver group= ndis
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)