---
title: Group Managed Service Accounts Overview
description: Windows Server-Sicherheit
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: security-gmsa
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: cef0693c-f861-48a7-a1c0-8d1bc06143ce
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 4e7f46739dd8def6ffc34c6cc50210c0e6999c79
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71403744"
---
# <a name="group-managed-service-accounts-overview"></a>Group Managed Service Accounts Overview

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

In diesem Thema für IT-Experten wird das Gruppen verwaltete Dienst Konto eingeführt. hierzu werden praktische Anwendungen, Änderungen in der Implementierung von Microsoft sowie Hardware-und Softwareanforderungen beschrieben.


## <a name="BKMK_OVER"></a>Funktionsbeschreibung
Ein eigenständiges verwaltetes Dienst Konto (Managed Service Account, SMSA) ist ein verwaltetes Domänen Konto, das die automatische Kenn Wort Verwaltung, vereinfachte Dienst Prinzipal Namen-Verwaltung (Service Principal Name, SPN) und die Möglichkeit zum Delegieren der Verwaltung Diese Art von verwaltetem Dienst Konto (MSA) wurde in Windows Server 2008 R2 und Windows 7 eingeführt.

Das Gruppen verwaltete Dienst Konto (Group Managed Service Account, GMSA) bietet die gleiche Funktionalität innerhalb der Domäne, erweitert diese Funktionalität aber auch auf mehrere Server. Beim Herstellen einer Verbindung mit einem auf einer Serverfarm gehosteten Dienst, wie z. b. der Lösung für Netzwerk Lastenausgleich, erfordern die Authentifizierungsprotokolle, die gegenseitige Authentifizierung unterstützen, dass alle Instanzen der Dienste denselben Prinzipal Wenn ein GMSA als Dienst Prinzipale verwendet wird, verwaltet das Windows-Betriebssystem das Kennwort für das Konto, anstatt sich auf den Administrator zu verlassen, um das Kennwort zu verwalten.

Der Microsoft-Schlüssel Verteilungsdienst @no__t -0kdssvc. dll @ no__t-1 bietet den Mechanismus zum sicheren Abrufen des aktuellen Schlüssels oder eines bestimmten Schlüssels mit einer Schlüssel Kennung für ein Active Directory Konto. Vom Schlüsselverteilungsdienst werden geheime Informationen zur Erstellung von Schlüsseln für das Konto bereitgestellt. Diese Schlüssel werden regelmäßig geändert. Bei einem GMSA berechnet der Domänen Controller das Kennwort für den Schlüssel, der von den Schlüssel Verteilungs Diensten bereitgestellt wird, zusätzlich zu anderen Attributen des GMSA.  Mitglieder Hosts können die aktuellen und vorangehenden Kenn Wort Werte abrufen, indem Sie einen Domänen Controller kontaktieren.

## <a name="BKMK_APP"></a>Praktische Anwendungen
gmsas bieten eine einzelne Identitäts Lösung für Dienste, die in einer Serverfarm oder auf Systemen hinter Netzwerk Load Balancer ausgeführt werden. Durch die Bereitstellung einer GMSA-Lösung können Dienste für den neuen GMSA-Prinzipal konfiguriert werden, und die Kenn Wort Verwaltung wird von Windows verarbeitet.

Durch die Verwendung eines GMSA müssen Dienste oder Dienst Administratoren die Kenn Wort Synchronisierung zwischen Dienst Instanzen nicht verwalten. Das GMSA unterstützt Hosts, die über einen längeren Zeitraum offline gehalten werden, sowie die Verwaltung von Mitglieds Hosts für alle Instanzen eines Diensts. Sie können also eine Serverfarm bereitstellen, die eine einzelne Identität unterstützt, gegenüber der sich vorhandene Clientcomputer authentifizieren können, ohne zu wissen, mit welcher Instanz des Diensts eine Verbindung hergestellt wird.

Failovercluster unterstützen keine gruppenverwalteten Dienstkonten. Dienste, die oben im Clusterdienst ausgeführt werden, können jedoch ein gMSA oder sMSA verwenden, wenn sie ein Windows-Dienst, ein App-Pool, eine geplante Aufgabe oder gMSA oder sMSA systemeigen unterstützen.

## <a name="BKMK_SOFT"></a>Software Anforderungen

Zum Ausführen der Windows PowerShell-Befehle, die zur Verwaltung von gmsas verwendet werden, ist eine 64 @ no__t-0bit-Architektur erforderlich.

Ein verwaltetes Dienstkonto ist abhängig von Verschlüsselungstypen mit Kerberos-Unterstützung. Wenn sich ein Clientcomputer gegenüber einem Server per Kerberos authentifiziert, wird vom Domänencontroller ein Kerberos-Dienstticket erstellt, das mit einer Verschlüsselung geschützt ist, die sowohl vom Domänencontroller als auch vom Server unterstützt wird. Der Domänen Controller verwendet das msDS @ no__t-0supportedencryptiontypes-Attribut des Kontos, um zu bestimmen, welche Verschlüsselung der Server unterstützt. Wenn kein Attribut vorhanden ist, wird davon ausgegangen, dass der Client Computer keine stärkeren Verschlüsselungstypen unterstützt. Wenn der Host so konfiguriert ist, dass RC4 nicht unterstützt wird, tritt bei der Authentifizierung immer ein Fehler auf. Aus diesem Grund muss AES für verwaltete Dienstkonten immer explizit konfiguriert sein.

> [!NOTE]
> Ab Windows Server 2008 R2 ist DES standardmäßig deaktiviert. Weitere Informationen zu den unterstützten Verschlüsselungsarten finden Sie unter [Changes in Kerberos Authentication](https://technet.microsoft.com/library/dd560670(WS.10).aspx).

gmsas gelten nicht für Windows-Betriebssysteme vor Windows Server 2012.

## <a name="server-manager-information"></a>Informationen zum Server-Manager
Es sind keine Konfigurationsschritte erforderlich, um MSA und GMSA mithilfe von Server-Manager oder mit dem Cmdlet Install @ no__t-0windows Feature zu implementieren.

## <a name="BKMK_LINKS"></a>Siehe auch
In der folgenden Tabelle sind Links zu weiterführenden Ressourcen im Zusammenhang mit verwalteten Dienstkonten und gruppenverwalteten Dienstkonten aufgeführt.

|Inhaltstyp|Verweise|
|--------|-------|
|**Produktbewertung**|[Neuerungen bei verwalteten Dienst Konten](what-s-new-for-managed-service-accounts.md)<br /><br />[Dokumentation zu verwalteten Dienst Konten für Windows 7 und Windows Server 2008 R2](https://technet.microsoft.com/library/ff641731(v=ws.10).aspx)<br /><br />[Dienst Konten Schritt @ no__t-1BY @ no__t-2 Step Guide](https://technet.microsoft.com/library/dd548356(v=ws.10).aspx)|
|**Planung**|Noch nicht verfügbar|
|**Bereitstellung**|Noch nicht verfügbar|
|**Betrieb**|[Verwaltete Dienst Konten in Active Directory](https://technet.microsoft.com/library/dd378925(v=ws.10).aspx)|
|**Problembehandlung**|Noch nicht verfügbar|
|**Evaluation**|[Erste Schritte mit gruppenverwalteten Dienstkonten](getting-started-with-group-managed-service-accounts.md)|
|**Tools und Einstellungen**|[Verwaltete Dienst Konten in Active Directory Domain Services](https://technet.microsoft.com/library/dd378925(v=WS.10).aspx)|
|**Communityressourcen**|[verwaltete Dienst Konten: Grundlegendes, Implementierung, bewährte Methoden und Problembehandlung bei @ no__t-0|
|**Verwandte Technologien**|[Übersicht über die Active Directory Domain Services](active-directory-domain-services-overview.md)|


