---
title: ntfrsutl
description: 'Windows-Befehle Thema ****- '
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-windows-commands
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d7721a19-5a87-4ab6-b816-65d2da2c811f
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: f1301b6876698e9eb552ae0ef9e70ed278319a7c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71372623"
---
# <a name="ntfrsutl"></a>ntfrsutl

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Sichert die internen Tabellen-, Thread-und Speicherinformationen für den NT-Datei Replikations Dienst \(ntfrs @ no__t-1. Sie wird auf lokalen und Remote Servern ausgeführt. Die Wiederherstellungs Einstellung für NTFRS im Dienststeuerungs-Manager \(scm @ no__t-1 kann für die Suche und Aufbewahrung wichtiger Protokollereignisse auf dem Computer von entscheidender Bedeutung sein. Dieses Tool bietet eine bequeme Methode zum Überprüfen dieser Einstellungen.   
  
## <a name="syntax"></a>Syntax  
  
```  
ntfrsutl[idtable|configtable|inlog|outlog][<computer>]  
ntfrsutl[memory|threads|stage][<computer>]  
ntfrsutl ds[<computer>]  
ntfrsutl [sets][<computer>]  
ntfrsutl [version][<computer>]  
ntfrsutl poll[/quickly[=[<N>]]][/slowly[=[<N>]]][/now][<computer>]  
```  
  
### <a name="parameters"></a>Parameter  
  
|  Parameter  |                                                                                                                                                                                                                                                                                                                                        Beschreibung                                                                                                                                                                                                                                                                                                                                         |
|-------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   IDtable   |                                                                                                                                                                                                                                                                                                                                          ID-Tabelle                                                                                                                                                                                                                                                                                                                                          |
| ConfigTable |                                                                                                                                                                                                                                                                                                                                  FRS-Konfigurations Tabelle                                                                                                                                                                                                                                                                                                                                   |
|    inlog    |                                                                                                                                                                                                                                                                                                                                        Eingehendes Protokoll                                                                                                                                                                                                                                                                                                                                         |
|   OUTLOG    |                                                                                                                                                                                                                                                                                                                                        Ausgeh Endes Protokoll                                                                                                                                                                                                                                                                                                                                        |
| <computer>  |                                                                                                                                                                                                                                                                                                                                  Gibt den Computer an.                                                                                                                                                                                                                                                                                                                                   |
|   memory    |                                                                                                                                                                                                                                                                                                                                        Speicherauslastung                                                                                                                                                                                                                                                                                                                                        |
|   Threads   |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
|    Stufe    |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
|     DS      |                                                                                                                                                                                                                                                                                                                         Listet die Ansicht der DS des NTFRS-dienstanders auf.                                                                                                                                                                                                                                                                                                                          |
|    Sationen     |                                                                                                                                                                                                                                                                                                                             Gibt die aktiven Replikat Gruppen an                                                                                                                                                                                                                                                                                                                              |
|   version   |                                                                                                                                                                                                                                                                                                                       Gibt die API-und NtFrs-Dienst Versionen an.                                                                                                                                                                                                                                                                                                                        |
|    Umfrage     | Gibt die aktuellen Abruf Intervalle an.<br /><br />Parameter:<br /><br /><ul><li>**\/schnell**\[ **\=** \[ <N> @ no__t-7 @ no__t-8 @ no__t-9umfragen schnell @ no__t-10<br /><br /><ul><li>**schnell** \- schnell Abrufe, bis die stabile Konfiguration wiederholt wird.</li><li>**schnell no__t-1** , \- alle Standard Minuten schnell abruft.</li><li>**schnelles @ no__t-1**<N> \-, schnell alle *N* Minuten</li></ul></li><li>**\/langsam**\[ **\=** \[ <N> @ no__t-7 @ no__t-8 \(umfragen langsam @ no__t-10<br /><br /><ul><li>**langsam** \--Umfrage langsam, bis eine stabile Konfiguration abgerufen wird.</li><li>**langsam @ no__t-1** \--Abfragen alle Standard Minuten langsam</li><li>**langsam @ no__t-1**<N> \-, schnell alle *N* Minuten</li></ul></li><li>**\/now** \(umfragen jetzt @ no__t-3</li></ul> |
|     \/?     |                                                                                                                                                                                                                                                                                                                            Zeigt die Hilfe an der Eingabeaufforderung an.                                                                                                                                                                                                                                                                                                                            |
  
## <a name="BKMK_Examples"></a>Beispiele  
So bestimmen Sie das Abruf Intervall für die Datei Replikation:  
  
```  
C:\Program Files\SupportTools>ntfrsutl poll wrkstn-1  
```  
  
So bestimmen Sie die aktuelle NTFRS-Anwendungsprogramm Schnittstelle \(api @ no__t-1-Version:  
  
```  
C:\Program Files\SupportTools>ntfrsutl version  
```  
  
## <a name="additional-references"></a>Weitere Verweise  
  
-   [Erläuterung zur Befehlszeilensyntax](command-line-syntax-key.md)  
  
  
  

