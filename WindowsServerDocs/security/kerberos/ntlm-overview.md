---
title: 'NTLM: Übersicht'
description: Windows Server-Sicherheit
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: security-kerberos
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 773909fd-c0bc-498a-95fc-bb452ec04d90
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: b8dec2877646fd2bfe00da9d5c9047e8edfd6f1d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71386261"
---
# <a name="ntlm-overview"></a>NTLM: Übersicht

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In diesem Thema für IT-Experten werden NTLM, alle Änderungen an der Funktionalität beschrieben und Links zu technischen Ressourcen für die Windows-Authentifizierung und NTLM für Windows Server 2012 und frühere Versionen bereitstellt.

## <a name="BKMK_OVER"></a>Funktionsbeschreibung
Die NTLM-Authentifizierung ist eine Familie von Authentifizierungs Protokollen, die in der Windows-Msv1\_0.dll enthalten sind. Zu den NTLM-Authentifizierungsprotokollen gehören LAN-Manager Version 1 und 2 sowie NTLM Version 1 und 2. Die NTLM-Authentifizierungsprotokolle authentifizieren Benutzer und Computer auf der Grundlage eines Challenge @ no__t-0response-Mechanismus, der einem Server oder einem Domänen Controller bestätigt, dass ein Benutzer das mit einem Konto verknüpfte Kennwort kennt. Bei Verwendung des NTLM-Protokolls muss ein Ressourcenserver eine der folgenden Aktionen ausführen, um die Identität eines Computers oder Benutzers zu überprüfen, wenn ein neues Zugriffstoken benötigt wird:

-   Kontaktieren eines Domänenauthentifizierungsdienstes auf dem Domänencontroller für die Kontodomäne des Computers oder Benutzers, wenn es sich um ein Domänenkonto handelt.

-   Nachschlagen des Computer- oder Benutzerkontos in der lokalen Kontendatenbank, wenn es sich um ein lokales Konto handelt.

## <a name="BKMK_APP"></a>Aktuelle Anwendungen
Die NTLM-Authentifizierung wird weiterhin unterstützt und muss für die Windows-Authentifizierung bei Systemen verwendet werden, die als Mitglied einer Arbeitsgruppe konfiguriert sind. Die NTLM-Authentifizierung wird auch für die lokale Anmelde Authentifizierung auf nicht-@ no__t-Domänen Controllern verwendet. Die Kerberos-Authentifizierung (Version 5) ist die bevorzugte Authentifizierungsmethode für Active Directory Umgebungen, aber eine nicht-@ no__t-0Microsoft-oder Microsoft-Anwendung verwendet möglicherweise weiterhin NTLM.

Die Verwendung des NTLM-Protokolls in einer IT-Umgebung zu reduzieren, setzt sowohl Kenntnisse der für NTLM geltenden Anwendungsanforderungen als auch der Strategien und Schritte voraus, die erforderlich sind, um Computerumgebungen für die Verwendung anderer Protokolle zu konfigurieren. Neue Tools und Einstellungen helfen Ihnen, zu entdecken, wie NTLM verwendet wird, um den NTLM-Verkehr selektiv einzuschränken. Informationen dazu, wie Sie die Verwendung von NTLM in Ihren Umgebungen analysieren und einschränken, finden Sie unter [Einführung der Einschränkung der NTLM-Authentifizierung](https://technet.microsoft.com/library/dd560653(v=ws.10).aspx) , wo Sie auf Anleitungen zum Überwachen und Einschränken der Verwendung von NTLM zugreifen können.

## <a name="BKMK_NEW"></a>Neue und geänderte Funktionalität
Es gibt keine Funktionsänderungen für NTLM für Windows Server 2012.

## <a name="BKMK_DEP"></a>Entfernte oder veraltete Funktionen
Für NTLM für Windows Server 2012 gibt es keine entfernten oder veralteten Funktionen.

## <a name="BKMK_INSTALL"></a>Server-Manager Informationen
NTLM kann nicht über den Server-Manager konfiguriert werden. Sie können Sicherheitsrichtlinieneinstellungen oder Gruppenrichtlinien verwenden, um die Verwendung der NTLM-Authentifizierung zwischen Computersystemen zu verwalten. In einer Domäne ist Kerberos das Standardauthentifizierungsprotokoll.

## <a name="BKMK_LINKS"></a>Siehe auch
In der folgenden Tabelle sind relevante Ressourcen für NTLM und andere Windows-Authentifizierungstechnologien aufgeführt.

|Inhaltstyp|Verweise|
|--------|-------|
|**Produktbewertung**|[Einführung der Einschränkung der NTLM-Authentifizierung](https://technet.microsoft.com/library/dd560653.aspx)<br /><br />[Änderungen bei der NTLM-Authentifizierung](https://technet.microsoft.com/library/dd566199.aspx)|
|**Planung**|[Leitfaden zur Bedrohungsmodellierung](https://technet.microsoft.com/library/dd941826.aspx)<br /><br />[bedrohungen und Gegenmaßnahmen: Sicherheitseinstellungen in Windows Server 2003 und Windows XP @ no__t-0<br /><br />[Handbuch zu Bedrohungen und Gegenmaßnahmen: Sicherheitseinstellungen in Windows Server 2008 und Windows Vista @ no__t-0<br /><br />[Handbuch zu Bedrohungen und Gegenmaßnahmen: Sicherheitseinstellungen in Windows Server 2008 R2 und Windows 7 @ no__t-0|
|**Bereitstellung**|[Erweiterter Schutz für die Authentifizierung](https://support.microsoft.com/kb/968389)<br /><br />[Leitfaden zur Überwachung und Einschränkung der NTLM-Verwendung](https://technet.microsoft.com/library/jj865674(v=ws.10).aspx)<br /><br />[fragen Sie das Verzeichnisdienst Team: NTLM Blocking and You: Methoden zum Analysieren und Überwachen von Anwendungen in Windows 7 @ no__t-0<br /><br />[Blog zur Windows-Authentifizierung](https://blogs.technet.com/authentication/)<br /><br />[Konfigurieren von "MaxConcurrentApi" für NTLM Pass @ no__t-1through-Authentifizierung](https://social.technet.microsoft.com/wiki/contents/articles/9759.configuring-maxconcurrentapi-for-ntlm-pass-through-authentication.aspx)|
|**Entwickelt**|[Microsoft NTLM \(Windows @ no__t-2](https://msdn.microsoft.com/library/aa378749(VS.85).aspx)<br /><br />[ @ NO__T-1MS @ NO__T-2NLMP @ NO__T-3: NT-LAN-Manager-\(ntlm @ no__t-1 Authentifizierungsprotokoll Spezifikation @ no__t-2<br /><br />[ @ NO__T-1MS @ NO__T-2NNTP @ NO__T-3: NT-LAN-Manager-\(ntlm @ no__t-1-Authentifizierung: Network News Transfer Protocol \(nntp @ no__t-1 Extension @ no__t-2<br /><br />[ @ NO__T-1MS @ NO__T-2NTHT @ NO__T-3: NTLM über HTTP-Protokollspezifikation @ no__t-0|
|**Problembehandlung**|Noch nicht verfügbar|
|**Communityressourcen**|[ist dieses Pferd noch tot: NTLM-Engpässe und RPC-Laufzeit @ no__t-0|



