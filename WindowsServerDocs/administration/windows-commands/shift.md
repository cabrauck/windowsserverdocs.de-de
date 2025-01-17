---
title: shift
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b56574e8-570a-4cc9-bbac-1b94fbf6a47a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f74e0f1f9041a4a7b95d83772ea79376c82876de
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71371247"
---
# <a name="shift"></a>shift



Ändert die Position von Batch Parametern in einer Batchdatei.

Beispiele für das Verwenden dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

## <a name="syntax"></a>Syntax

```
shift [/n <N>]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|---------|-----------|
|/n \<n >|Gibt an, dass die Verschiebung beim *n*-ten Argument gestartet werden soll, wobei *N* ein beliebiger Wert zwischen 0 und 8 ist. Erfordert Befehls Erweiterungen, die standardmäßig aktiviert sind.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise

- Der **Shift** -Befehl ändert die Werte der Batch Parameter **% 0** bis **% 9** durch Kopieren jedes Parameters in den vorherigen – der Wert von **% 1** wird in **% 0**kopiert, der Wert von **% 2** wird in **% 1**kopiert usw. Dies ist hilfreich beim Schreiben einer Batchdatei, die denselben Vorgang für eine beliebige Anzahl von Parametern ausführt.
- Wenn Befehls Erweiterungen aktiviert sind, unterstützt der Befehl **Shift** die Befehlszeilenoption **/n** . Die **/n** -Option gibt an, dass die Verschiebung beim n-ten Argument gestartet werden soll, wobei **n** ein beliebiger Wert zwischen 0 und 8 ist. Beispielsweise würde **Shift/2** " **% 3** " in **"% 2**", " **% 4** " in " **% 3**" usw. verschieben und " **% 0** " und " **% 1** " nicht beeinträchtigt. Befehls Erweiterungen werden standardmäßig aktiviert.
- Mit dem Befehl **Shift** können Sie eine Batchdatei erstellen, die mehr als 10 Batch Parameter annehmen kann. Wenn Sie mehr als 10 Parameter in der Befehlszeile angeben, werden diejenigen, die nach dem zehnten ( **% 9**) angezeigt werden, nacheinander in **% 9**verschoben.
- Der **Shift** -Befehl hat keine Auswirkung auf den Parameter **% @ no__t-3*** Batch.
- Es ist kein rückwärts **Verschiebungs** Befehl vorhanden. Nachdem Sie den Befehl **Shift** implementiert haben, können Sie den Batch Parameter ( **% 0**), der vor der Verschiebung vorhanden war, nicht wiederherstellen.

## <a name="BKMK_examples"></a>Beispiele

Die folgenden Zeilen aus einer Beispiel Batchdatei namens mycopy. bat veranschaulichen, wie Sie **Shift** mit einer beliebigen Anzahl von Batch-Parametern verwenden. In diesem Beispiel kopiert mycopy. bat eine Liste von Dateien in ein bestimmtes Verzeichnis. Die Batch Parameter werden durch das Verzeichnis und die Dateinamen Argumente dargestellt.
```
@echo off 
rem MYCOPY.BAT copies any number of files
rem to a directory.
rem The command uses the following syntax:
rem mycopy dir file1 file2 ... 
set todir=%1
:getfile
shift
if "%1"=="" goto end
copy %1 %todir%
goto getfile
:end
set todir=
echo All done
```

#### <a name="additional-references"></a>Weitere Verweise

[Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)