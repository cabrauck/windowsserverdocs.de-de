---
title: tsdiscon
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 13139674-7dee-4965-8cac-32f4928e8b9a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 577ff8ee672583b85c907642bd21256124aa8034
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71369868"
---
# <a name="tsdiscon"></a>tsdiscon

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Trennt eine Sitzung von einem Remotedesktop-Sitzungshost Server (RD-Sitzungs Host).
Beispiele für die Verwendung dieses Befehls finden Sie unter [Beispiele](#BKMK_examples).

> [!NOTE]
> In Windows Server 2008 R2 heißen die Terminaldienste nun Remotedesktopdienste. Weitere Informationen zu den Neuerungen in der neuesten Version finden Sie unter [What es New in Remotedesktopdienste in Windows Server 2012](https://technet.microsoft.com/library/hh831527) in der TechNet-Bibliothek für Windows Server.

## <a name="syntax"></a>Syntax
```
tsdiscon [<SessionID> | <SessionName>] [/server:<ServerName>] [/v]
```

## <a name="parameters"></a>Parameter

|Parameter|Beschreibung|
|-------|--------|
|\<sessionid >|Gibt die ID der Sitzung an, die getrennt werden soll.|
|\<sessionname >|Gibt den Namen der Sitzung an, die getrennt werden soll.|
|/Server: \<servername >|Gibt den Terminal Server an, der die Sitzung enthält, die Sie trennen möchten. Andernfalls wird der aktuelle RD-Sitzungs Host Server verwendet.|
|/v|Zeigt Informationen zu den Aktionen an, die ausgeführt werden.|
|/?|Zeigt die Hilfe an der Eingabeaufforderung an.|

## <a name="remarks"></a>Hinweise
-   Sie müssen über die Berechtigung "Vollzugriff" verfügen oder eine spezielle Zugriffsberechtigung trennen, um einen anderen Benutzer von einer Sitzung zu trennen.
-   Wenn keine Sitzungs-ID oder kein Sitzungsname angegeben ist, wird die aktuelle Sitzung **von zdiscon** getrennt.
-   Alle Anwendungen, die ausgeführt wurden, als Sie die Sitzung getrennt haben, werden automatisch ausgeführt, wenn Sie die Verbindung zu dieser Sitzung ohne Datenverlust wiederherstellen. Verwenden Sie die **Reset-Sitzung** , um die ausgewendenden Anwendungen der getrennten Sitzung zu beenden, aber beachten Sie, dass dies zu einem Datenverlust in der Sitzung führen kann.
-   Der **/Server** -Parameter ist nur erforderlich, wenn Sie "out" von einem Remote **Server verwenden.**
-   Die Verbindung mit der Konsolen Sitzung kann nicht getrennt werden.

## <a name="BKMK_examples"></a>Beispiele
- Geben Sie zum Trennen der aktuellen Sitzung Folgendes ein:
  ```
  tsdiscon
  ```
- Zum Trennen der Sitzung 10 geben Sie Folgendes ein:
  ```
  tsdiscon 10
  ```
- Geben Sie Folgendes ein, um die Sitzung mit dem Namen TERM04 zu trennen
  ```
  tsdiscon TERM04
  ```
  #### <a name="additional-references"></a>Weitere Verweise
  [Befehlszeilen-Syntax Schlüssel](command-line-syntax-key.md)
  [Remotedesktopdienste &#40;Befehlsreferenz&#41; für Terminal Dienste](remote-desktop-services-terminal-services-command-reference.md)
