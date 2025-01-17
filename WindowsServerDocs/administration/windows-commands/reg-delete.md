---
title: reg löschen
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cee05071-1607-4ab1-b8ab-65caebeb85c3
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 7156bf58b27da1602931f0dc1903de71d86764e7
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71384761"
---
# <a name="reg-delete"></a>reg löschen



Löscht einen Unterschlüssel oder Einträge aus der Registrierung.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
Reg delete <KeyName> [{/v ValueName | /ve | /va}] [/f]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|\<keyname >|Gibt den vollständigen Pfad des zu löschenden unter Schlüssels oder Eintrags an. Wenn Sie einen Remote Computer angeben möchten, fügen Sie den Computernamen (im Format \\ @ no__t-1computername @ no__t-2 als Teil des *keyName*-Steuerelement ein. Wenn \\ @ no__t-1computername \ weggelassen wird, wird der Vorgang standardmäßig auf dem lokalen Computer durchgesetzt. Der *keyName* muss einen gültigen Stamm Schlüssel enthalten. Gültige Stamm Schlüssel für den lokalen Computer sind: "HKLM", "HKCU", "HKCR", "HKU" und "HKCC" Wenn ein Remote Computer angegeben wird, sind gültige Stamm Schlüssel: HKLM und HKU.|
|/v \<valuename >|Löscht einen bestimmten Eintrag unter dem Unterschlüssel. Wenn kein Eintrag angegeben wird, werden alle Einträge und Unterschlüssel unter dem Unterschlüssel gelöscht.|
|/ve|Gibt an, dass nur Einträge, für die kein Wert vorhanden ist, gelöscht werden.|
|/va|Löscht alle Einträge unter dem angegebenen Unterschlüssel. Unterschlüssel unter dem angegebenen Unterschlüssel werden nicht gelöscht.|
|/f|Löscht den vorhandenen Registrierungs Unterschlüssel oder Eintrag, ohne zur Bestätigung aufzufordern.|
|/?|Zeigt die Hilfe zu **Reg Delete** an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

In der folgenden Tabelle sind die Rückgabewerte für den **reg-Lösch** Vorgang aufgeführt.

|Wert|Description|
|-----|-----------|
|0|Erfolgreich|
|1|Nicht möglich|

## <a name="BKMK_examples"></a>Beispiele

Geben Sie Folgendes ein, um den Registrierungsschlüssel Timeout und dessen alle Unterschlüssel und Werte zu löschen:
```
REG DELETE HKLM\Software\MyCo\MyApp\Timeout
```
Geben Sie Folgendes ein, um den Registrierungs Wert auf dem Computer mit dem Namen "Zodiac" unter HKLM\Software\MyCo zu löschen:
```
REG DELETE \\ZODIAC\HKLM\Software\MyCo /v MTU
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)