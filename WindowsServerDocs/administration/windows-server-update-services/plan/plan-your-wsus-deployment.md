---
title: Planen der WSUS-Bereitstellung
description: 'Thema zu Windows Server Update Service (WSUS): eine Übersicht über den Bereitstellungs Planungsprozess mit Links zu den verwandten Themen.'
ms.prod: windows-server
ms.reviewer: na
ms.technology: manage-wsus
ms.topic: article
ms.assetid: 35865398-b011-447a-b781-1c52bc0c9e3a
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 05/24/2018
ms.openlocfilehash: 37e3a7788ccd409f4002f5fe2d7ea087e89b3419
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71369838"
---
# <a name="plan-your-wsus-deployment"></a>Planen der WSUS-Bereitstellung

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Der erste Schritt bei der Bereitstellung von Windows Server Update Services (WSUS) sind einige wichtige Entscheidungen, z. B. die Auswahl des WSUS-Bereitstellungsszenarios und der Netzwerktopologie sowie die Prüfung der Systemanforderungen. In der folgenden Prüfliste werden die Schritte zusammengefasst, die bei der Vorbereitung der Bereitstellung ausgeführt werden.

|Aufgabe|Beschreibung|
|----|--------|
|[1,1. Überprüfen der Überlegungen und Systemanforderungen @ no__t-0|Prüfen Sie die Liste der Bereitstellungshinweise und Systemanforderungen, um sicherzustellen, dass Sie über alle notwendige Hardware und Software für die Bereitstellung von WSUS verfügen.|
|[1,2. Auswählen eines WSUS-Bereitstellungs Szenarios @ no__t-0|Entscheiden Sie, welches WSUS-Bereitstellungsszenario verwendet werden soll.|
|[1,3. Auswählen einer WSUS-Speicherstrategie @ no__t-0|Entscheiden Sie, welche WSUS-Speicherstrategie am besten für Ihre Bereitstellung geeignet ist.|
|[1,4. Wählen Sie WSUS-Update Sprachen @ no__t-0 aus.|Entscheiden Sie, welche WSUS-Updatesprachen installiert werden sollen.|
|[1,5. Planen der WSUS-Computer Gruppen @ no__t-0|Planen Sie, wie WSUS-Computergruppen in Ihrer Bereitstellung verwendet werden sollen.|
|[1,6. Überlegungen zur Planung der WSUS-Leistung: Bits @ no__t-0|Erstellen Sie einen WSUS-Entwurf für optimierte Leistung.|
|[1,7. Plan automatische Updates Einstellungen @ no__t-0|Planen Sie, wie die Einstellungen für automatische Updates für Ihr Szenario konfiguriert werden sollen.|

## <a name="11-review-considerations-and-system-requirements"></a>1.1. Vorüberlegungen und Systemanforderungen

### <a name="system-requirements"></a>Systemanforderungen

Stellen Sie vor dem Aktivieren der WSUS-Serverrolle anhand der folgenden Richtlinien sicher, dass der Server die Systemanforderungen erfüllt und Sie die erforderlichen Berechtigungen zum Durchführen der Installation besitzen:

-   Serverhardwareanforderungen zum Aktivieren der WSUS-Rolle sind an die Hardware gebunden. Die Mindesthardwareanforderungen für WSUS sind:

    -   **Prozessor** 1,4 Gigahertz (GHz) x64-Prozessor (2 GHz oder schneller wird empfohlen)

    -   **Gedenkens** Für WSUS sind zusätzliche 2 GB RAM erforderlich, als für den Server und alle anderen Dienste oder Software erforderlich sind.

    -   **Verfügbarer Speicherplatz:** 10 GB (40 GB oder mehr wird empfohlen)

    -   **Netzwerkadapter:** 100 meits pro Sekunde (Mbit/s) oder höher

-   Software Anforderungen:

    -   Zum Anzeigen von Berichten benötigt WSUS [Microsoft Report Viewer Redistributable 2008](https://www.microsoft.com/download/details.aspx?id=6576). Unter Windows Server 2016 erfordert WSUS [Microsoft Report Viewer Runtime 2012](https://www.microsoft.com/download/details.aspx?id=35747)

-   Starten Sie den Server vor dem Aktivieren der WSUS-Serverrolle neu, falls Sie Rollen oder Softwareupdates installieren, bei denen der Server nach der Installation neu gestartet werden muss.

-   Microsoft .NET Framework 4.0 muss auf dem Server installiert sein, auf dem die WSUS-Serverrolle installiert wird.

-   Das Konto %%amp;quot;NT-Autorität\Netzwerkdienst%%amp;quot; muss über die Berechtigung %%amp;quot;Vollzugriff%%amp;quot; für die folgenden Ordner verfügen, damit das WSUS-Verwaltungs-Snap-In korrekt angezeigt wird:

    -   %windir%\Microsoft.NET\Framework\v4.0.30319\Temporary ASP.NET Files

        > [!NOTE]
        > Dieser Pfad ist vor der Installation der Webserverrolle, in der Internetinformationsdienste (IIS) enthalten ist, möglicherweise nicht vorhanden.

    -   %windir%\Temp

-   Stellen Sie sicher, dass das Konto, das Sie zum Installieren von WSUS verwenden, ein Mitglied der lokalen Administratorgruppe ist.

### <a name="installation-considerations"></a>Überlegungen zur Installation

Während des Installationsvorgangs installiert WSUS standardmäßig die folgenden Komponenten:

-   .NET-API und Windows PowerShell-Cmdlets

-   Interne Windows-Datenbank (Windows Internal Database, WID), wird von WSUS verwendet

-   Folgende von WSUS verwendete Dienste:

    -   Updatedienst

    -   Berichterstattungswebdienst

    -   Clientwebdienst

    -   Webdienst für die einfache Webauthentifizierung

    -   Serversynchronisierungsdienst

    -   DSS-Authentifizierungswebdienst

### <a name="features-on-demand-considerations"></a>Überlegungen zu Features bei Bedarf

Beachten Sie, dass das Konfigurieren von Clientcomputern (einschließlich Server) für die Aktualisierung über WSUS zu folgenden Einschränkungen führt:

1. Serverrollen, deren Nutzlasten mit Features bei Bedarf entfernt wurden, können nicht bei Bedarf von Microsoft Update installiert werden. Sie müssen entweder eine Installationsquelle bereitstellen, wenn Sie versuchen, solche Server Rollen zu installieren, oder eine Quelle für Features bei Bedarf in Gruppenrichtlinie konfigurieren.

2. Windows-Client-Editionen können .NET 3.5 nicht bei Bedarf über das Web installieren. Die gleichen Überlegungen wie Serverrollen gelten für .NET 3.5.

   > [!NOTE]
   > Das Konfigurieren einer Features bei Bedarf-Installationsquelle umfasst nicht WSUS. Informationen zum Konfigurieren von Features finden Sie unter [Configure Features on Demand in Windows Server](https://technet.microsoft.com/library/jj127275.aspx).

3. Bei Unternehmens Geräten, auf denen Windows 10, Version 1709 oder Version 1803 ausgeführt wird, können keine Features Bedarfs gesteuert direkt von WSUS installiert werden. Wenn Sie Features Bedarfs gesteuert installieren möchten, [Erstellen Sie eine Featuredatei (paralleler Speicher)](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj127275%28v=ws.11%29#create-a-feature-file-or-side-by-side-store) , oder rufen Sie das Feature on Demand-Paket aus einer der folgenden Quellen ab:
   - [Volume Licensing Service Center](https://www.microsoft.com/licensing/servicecenter) (VLSC): der VL-Zugriff ist erforderlich.
   - OEM-Portal: OEM-Zugriff ist erforderlich.
   - MSDN-Download: das MSDN-Abonnement ist erforderlich.

     Mithilfe der [Befehlszeilenoptionen des Befehlszeilen](https://docs.microsoft.com/windows-hardware/manufacture/desktop/dism-operating-system-package-servicing-command-line-options)Pakets können einzeln abgebenes Feature on Demand-Pakete installiert werden.

### <a name="wsus-database-requirements"></a>WSUS-Datenbankanforderungen
WSUS erfordert eine der folgenden Datenbanken:

-   Interne Windows-Datenbank (WID)

-   Microsoft SQL Server 2017

-   Microsoft SQL Server 2016

-   Microsoft SQL Server 2014

-   Microsoft SQL Server 2012

-   Microsoft SQL Server 2008 R2

Die folgenden Editionen von SQL Server werden von WSUS unterstützt:

-   Standard

-   Unternehmen

-   Express

> [!NOTE]
> Bei SQL Server Express 2008 R2 beträgt die maximale Datenbankgröße 10 GB. Die Größe dieser Datenbank ist für WSUS meist ausreichend, ihre Verwendung bietet gegenüber WID jedoch keinen spürbaren Vorteil. Die wid-Datenbank verfügt über eine minimale RAM-Arbeitsspeicher Anforderung von 2 GB über die standardmäßigen Windows Server-Systemanforderungen.

Sie können die WSUS-Rolle auf einem anderen Computer als dem Datenbankservercomputer installieren. In diesem Fall gelten folgende zusätzliche Kriterien:

1.  Der Datenbankserver kann nicht als Domänencontroller konfiguriert werden.

2.  Auf dem WSUS-Server können die Remotedesktopdienste nicht ausgeführt werden.

3.  Der Datenbankserver muss sich in derselben Active Directory-Domäne wie der WSUS-Server befinden, oder er muss über eine Vertrauensstellung mit der Active Directory-Domäne des WSUS-Servers verfügen.

4.  Der WSUS-Server und der Datenbankserver müssen sich in der gleichen Zeitzone befinden oder mit derselben koordinierte Weltzeit (Greenwich Mean Time)-Quelle synchronisiert werden.

## <a name="12-choose-a-wsus-deployment-scenario"></a>1.2. Auswählen des WSUS-Bereitstellungsszenarios
In diesem Abschnitt werden die grundlegenden Features aller WSUS-Bereitstellungen beschrieben. Sie finden hier Informationen zu einfachen Bereitstellungen mit nur einem WSUS-Server und komplexeren Szenarien, z. B. einer WSUS-Serverhierarchie oder einem WSUS-Server in einem isolierten Netzwerksegment.

### <a name="simple-wsus-deployment"></a>Einfache WSUS-Bereitstellung
Die einfachste WSUS-Bereitstellung besteht aus einem Server innerhalb der Unternehmens Firewall, der Client Computern in einem privaten Intranet bereitstellt. Der WSUS-Server stellt eine Verbindung mit Microsoft Update her, um Updates herunterzuladen. Dieser Vorgang wird als *Synchronisierung* bezeichnet. Während der Synchronisierung überprüft WSUS, ob seit der letzten Synchronisierung Updates verfügbar gemacht wurden. Bei der ersten Synchronisierung von WSUS werden alle Updates zum Download verfügbar gemacht.

> [!NOTE]
> Die Erstsynchronisierung kann mehr als eine Stunde in Anspruch nehmen. Alle anschließenden Synchronisierungen sollten deutlich schneller vonstatten gehen.

Der WSUS-Server verwendet standardmäßig Port 80 für das HTTP-Protokoll und Port 443 für das HTTPS-Protokoll, um Updates von Microsoft Update herunterzuladen. Falls eine Unternehmensfirewall zwischen dem Netzwerk und dem Internet vorhanden ist, müssen Sie diese Ports auf dem Server öffnen, der direkt mit Microsoft Update kommuniziert. Wenn Sie benutzerdefinierte Ports für diese Kommunikation verwenden möchten, müssen Sie diese Ports stattdessen öffnen. Sie können mehrere WSUS-Server zur Synchronisierung mit einem übergeordneten WSUS-Server konfigurieren. Der WSUS-Server verwendet standardmäßig Port 8530 für das HTTP-Protokoll und Port 8531 für das HTTPS-Protokoll, um Updates an Clientworkstations zu verteilen.

### <a name="multiple-wsus-servers"></a>Mehrere WSUS-Server
Administratoren können mehrere Server mit WSUS bereitstellen, die alle Inhalte innerhalb des Intranets der Organisation synchronisieren. Sie können nur einen Server für das Internet verfügbar machen. Dies wäre der einzige Server, der Updates von Microsoft Update herunterlädt. Dieser Server wird als Upstreamserver der Quelle eingerichtet, in der die Downstreamserver synchronisiert werden. Server können bei Bedarf in einem geografisch verteilten Netzwerk eingerichtet werden, um für alle Clientcomputer die bestmögliche Konnektivität bereitzustellen.

### <a name="disconnected-wsus-server"></a>Nicht verbundener WSUS-Server
Wenn der Zugriff auf das Internet aufgrund von Unternehmensrichtlinien oder aus anderen Gründen eingeschränkt ist, können Administratoren einen internen Server für WSUS einrichten. Ein Beispiel hierfür ist ein Server, der mit dem Intranet verbunden, aber vom Internet isoliert ist. Nachdem die Updates auf diesem Server heruntergeladen, getestet und genehmigt wurden, exportiert der Administrator Updatemetadaten und -inhalte auf eine DVD. Anschließend werden die Updatemetadaten und -inhalte von der DVD auf die WSUS-Server im Intranet importiert.

### <a name="wsus-server-hierarchies"></a>WSUS-Serverhierarchien
Sie können komplexe Hierarchien von WSUS-Servern erstellen. Da es möglich ist, einen WSUS-Server nicht mit Microsoft Update, sondern mit einem anderen WSUS-Server zu synchronisieren, benötigen Sie nur einen mit Microsoft Update verbundenen WSUS-Server. Wenn Sie WSUS-Server miteinander verbinden, haben Sie einen WSUS-Upstreamserver und einen WSUS-Downstreamserver. Die Bereitstellung einer WSUS-Serverhierarchie bietet die folgenden Vorteile:

-   Sie können Updates einmal aus dem Internet herunterladen und anschließend mithilfe von Downstreamservern an Clientcomputer verteilen. Durch diese Methode können Sie Bandbreite auf der Internetverbindung Ihres Unternehmens sparen.

-   Sie können Updates auf einen WSUS-Server herunterladen, der den Clientcomputern physisch näher ist, z. B. in Filialen.

-   Sie können separate WSUS-Server für Clientcomputer einrichten, auf denen Microsoft-Produkte in unterschiedlichen Sprachen verwendet werden.

-   Sie können WSUS für eine große Organisation skalieren, in der mehr Clientcomputer vorhanden sind als ein WSUS-Server effektiv verwalten kann.

> [!NOTE] 
> Es wird empfohlen, die WSUS-Serverhierarchie auf maximal drei Ebenen zu beschränken, da der Zeitaufwand für die Verteilung von Updates an die verbundenen Server durch jede Ebene zunimmt. Obwohl es für eine Hierarchie keine theoretische Beschränkung gibt, wurden nur bereit Stellungen mit einer Hierarchie von fünf Ebenen von Microsoft getestet.
>
> Außerdem müssen Downstreamserver die gleiche Version oder eine frühere Version von WSUS wie die Upstreamserver-Synchronisierungs Quelle aufweisen.

Sie können WSUS-Server im autonomen Modus (verteilte Verwaltung) oder im Replikatmodus (zentrale Verwaltung) verbinden und ggf. eine Serverhierarchie mit beiden Modi bereitstellen: Die WSUS-Lösung kann sowohl autonome WSUS-Server als auch WSUS-Replikatserver enthalten.

#### <a name="autonomous-mode"></a>Autonomer Modus
Der autonome Modus (auch als verteilte Verwaltung bezeichnet) ist die Standardinstallationsoption für WSUS. Im autonomen Modus gibt ein WSUS-Upstreamserver während der Synchronisierung Updates für Downstreamserver frei. WSUS-Downstreamserver werden separat verwaltet und müssen weder den Genehmigungsstatus von Updates noch Computergruppeninformationen vom Upstreamserver empfangen. Beim verteilten Verwaltungsmodell werden von jedem WSUS-Serveradministrator Updatesprachen ausgewählt, Computergruppen erstellt, Computer Gruppen zugewiesen sowie Updates getestet und genehmigt. Außerdem stellt der Administrator sicher, dass die richtigen Updates auf den entsprechenden Computergruppen installiert werden. Die folgende Abbildung zeigt, wie autonome WSUS-Server in einer Filialenumgebung bereitgestellt werden können.

#### <a name="replica-mode"></a>Replikatmodus
Beim Replikatmodus (auch als zentrale Verwaltung bezeichnet) wird ein WSUS-Upstreamserver eingesetzt, der Updates, Genehmigungsstatus und Computergruppen für Downstreamserver freigibt. Replikatserver erben Updategenehmigungen und werden nicht getrennt vom WSUS-Upstreamserver verwaltet. Die folgende Abbildung zeigt, wie WSUS-Replikatserver in einer Filialenumgebung bereitgestellt werden können.

> [!NOTE]
> Wenn Sie mehrere Replikatserver einrichten, die eine Verbindung mit einem einzigen WSUS-Upstreamserver herstellen, sollten Sie die Synchronisierung auf den einzelnen Replikatservern für unterschiedliche Zeitpunkte planen. So können Sie einen plötzlichen Anstieg der Bandbreitennutzung vermeiden.

### <a name="branch-offices"></a>Filialen
Sie können das Filialenfeature in Windows nutzen, um die WSUS-Bereitstellung zu optimieren. Dieser Bereitstellungstyp bietet die folgenden Vorteile:

1.  verringert die Verwendung von WAN-Verbindungen und verbessert die Reaktionsfähigkeit von Anwendungen. Sie können die Bereitstellung der vom WSUS-Server verarbeiteten Inhalte mithilfe von BranchCache beschleunigen, indem Sie BranchCache auf dem Server und den Clients installieren und sicherstellen, dass der BranchCache-Dienst gestartet wurde. Weitere Schritte sind nicht erforderlich.

2.  In Filialen, bei denen die Verbindungen mit der Zentrale eine niedrige Bandbreite haben, die Verbindungen mit dem Internet aber eine hohe Bandbreite, kann das Filialenfeature ebenfalls verwendet werden. In diesem Fall können Sie WSUS-Downstreamserver so konfigurieren, dass sie Informationen zu den zu installierenden Updates vom zentralen WSUS-Server abrufen, die Updates selbst aber von Microsoft Update herunterladen.

### <a name="network-load-balancing"></a>Netzwerklastenausgleich
Der Netzwerklastenausgleich (Network Load Balancing, NLB) verbessert die Zuverlässigkeit und Leistung Ihres WSUS-Netzwerks. Sie können mehrere WSUS-Server einrichten, die über einen einzelnen Failovercluster verfügen, auf SQL Server z. b. SQL Server 2008 R2 SP1 ausgeführt wird. In dieser Konfiguration müssen Sie eine vollständige SQL Server-Installation verwenden (nicht die von WSUS bereitgestellte interne Windows-Datenbank), und die Datenbankrolle muss auf allen WSUS-Front-End-Servern installiert werden. Sie können auch auch auf allen WSUS-Servern ein verteiltes Dateisystem (Distributed File System, DFS) zum Speichern der Inhalte verwenden.

**WSUS-Setup für NLB:** im Vergleich zum WSUS 3,2-Setup für NLB sind keine speziellen Setup-Aufrufe und Parameter mehr erforderlich, um WSUS für den NLB zu konfigurieren. Sie müssen lediglich jeden WSUS-Server einrichten, wobei Sie die folgenden Aspekte berücksichtigen sollten.

-   WSUS muss unter Verwendung der SQL-Datenbank-Option anstelle von WID eingerichtet werden.

-   Wenn Updates lokal gespeichert werden, muss der gleiche Inhaltsordner zwischen den WSUS-Servern freigegeben werden, die die gleiche SQL-Datenbank gemeinsam nutzen.

-   WSUS-Setup muss nacheinander durchgeführt werden. Postinstallationsaufgaben können nicht auf mehreren Servern gleichzeitig ausgeführt werden, wenn eine gemeinsame SQL-Datenbank genutzt wird.

### <a name="wsus-deployment-with-roaming-client-computers"></a>WSUS-Bereitstellung mit Roamingclientcomputern
Wenn sich mobile Benutzer an unterschiedlichen Orten beim Netzwerk anmelden, können Sie WSUS so konfigurieren, dass Roamingbenutzer ihre Clientcomputern mit dem geografisch am nächsten gelegenen WSUS-Server aktualisieren können. Beispielsweise können Sie einen WSUS-Server in jeder Region bereitstellen und für jede Region ein anderes DNS-Subnetz verwenden. Alle Client Computer könnten an denselben WSUS-Server weitergeleitet werden, der in jedem Subnetz zum nächsten physischen WSUS-Server aufgelöst wird.

## <a name="13-choose-a-wsus-storage-strategy"></a>1.3. Auswählen der WSUS-Speicherstrategie
Windows Server Update Services (WSUS) verwendet zwei Arten von Speichersystemen: eine Datenbank zum Speichern der WSUS-Konfiguration und Updatemetadaten und ein optionales lokales Dateisystem zum Speichern von Updatedateien. Bevor Sie WSUS installieren, sollten Sie entscheiden, wie Sie den Speicher implementieren möchten.

Updates bestehen aus zwei Teilen: Metadaten, die das Update beschreiben, und Dateien, die zum Installieren des Updates erforderlich sind. Updatemetadaten sind in der Regel sehr viel kleiner als das eigentliche Update und werden in der WSUS-Datenbank gespeichert. Updatedateien werden auf einem lokalen WSUS-Server oder einem Microsoft Update-Webserver gespeichert.

### <a name="wsus-database"></a>WSUS-Datenbank
WSUS erfordert eine Datenbank für jeden WSUS-Server. WSUS unterstützt – mit einigen Einschränkungen – die Verwendung einer Datenbank, die sich auf einem anderen Computer als dem WSUS-Server befindet. Eine Liste der unterstützten Datenbanken und Einschränkungen für Remote Datenbanken finden Sie im Abschnitt "1,1 Review (anfängliche Überlegungen und Systemanforderungen)" in diesem Handbuch.

In der WSUS-Datenbank werden die folgenden Informationen gespeichert:

-   Informationen zur WSUS-Serverkonfiguration

-   Metadaten, die die einzelnen Updates beschreiben

-   Informationen zu Clientcomputern, Updates und Interaktionen

Wenn Sie mehrere WSUS-Server installieren, ist eine separate Datenbank für jeden WSUS-Server erforderlich, unabhängig davon, ob es sich um einen autonomen Server oder einen Replikatserver handelt. Mit Ausnahme von NLB-Clustern mit SQL Server-Failover ist es nicht möglich, mehrere WSUS-Datenbanken auf einer einzigen SQL Server-Instanz zu speichern.

In einer Einzelserverkonfiguration, bei der sich die Datenbank und der WSUS-Dienst auf demselben Computer befinden, bieten SQL Server, SQL Server Express und die interne Windows-Datenbank die gleichen Leistungsmerkmale. Eine Einzelserverkonfiguration kann mehrere tausend WSUS-Clientcomputer unterstützen.

> [!NOTE]
> Versuchen Sie nicht, WSUS durch direkten Zugriff auf die Datenbank zu verwalten. eine direkte Bearbeitung der Datenbank kann zu einer Beschädigung der Datenbank führen. Die Beschädigung macht sich möglicherweise nicht sofort bemerkbar, kann aber dazu führen, dass Upgrades auf die nächste Version des Produkts nicht möglich sind. Sie können WSUS mithilfe der WSUS-Konsole oder mit WSUS-Anwendungsprogrammierschnittstellen (Application Programming Interface, API) verwalten.

#### <a name="wsus-with-windows-internal-database"></a>WSUS mit interner Windows-Datenbank
Standardmäßig erstellt und verwendet der Installations-Assistent eine interne Windows-Datenbank mit dem Namen %%amp;quot;SUSDB.mdf%%amp;quot;. Diese Datenbank befindet sich im Ordner %%amp;quot;%windir%\wid\data\%%amp;quot;, wobei %%amp;quot;%windir%%%amp;quot; das lokale Laufwerk ist, auf dem die WSUS-Serversoftware installiert ist.

> [!NOTE]
> Die interne Windows-Datenbank (WID) wurde in Windows Server 2008 eingeführt.

WSUS unterstützt für die Datenbank nur die Windows-Authentifizierung. Die SQL Server-Authentifizierung kann nicht mit WSUS verwendet werden. Wenn Sie die interne Windows-Datenbank für die WSUS-Datenbank verwenden, erstellt das WSUS-Setup eine SQL Server-Instanz mit dem Namen %%amp;quot;Server\Microsoft##WID%%amp;quot;, wobei %%amp;quot;Server%%amp;quot; der Name des Computers ist. Bei beiden Datenbankoptionen erstellt das WSUS-Setup eine Datenbank namens %%amp;quot;SUSDB%%amp;quot;. Der Name dieser Datenbank ist nicht konfigurierbar.

In den folgenden Fällen wird empfohlen, die interne Windows-Datenbank zu verwenden:

-   Die Organisation hat noch kein SQL Server-Produkt für eine andere Anwendung erworben und benötigt kein SQL Server-Produkt.

-   Die Organisation benötigt keine WSUS-Lösung mit Netzwerklastenausgleich (NLB).

-   Sie beabsichtigen, mehrere WSUS-Server bereitzustellen (z. B. in Filialen). In diesem Fall sollten Sie die Verwendung der internen Windows-Datenbank für die sekundären Server erwägen (auch wenn Sie SQL Server für den WSUS-Stammserver verwenden). Da für jeden WSUS-Server eine separate Instanz von SQL Server erforderlich ist, können schnell Probleme mit der Datenbankleistung auftreten, wenn nur eine Instanz von SQL Server für mehrere WSUS-Server eingesetzt wird.

Die interne Windows-Datenbank stellt keine Benutzeroberfläche oder Tools zur Datenbankverwaltung bereit. Wenn Sie diese Datenbank für WSUS verwenden, müssen Sie sie mit externen Tools verwalten. Weitere Informationen finden Sie in den folgenden Themen:

-   [Sichern und Wiederherstellen von WSUS-Daten und Sichern des Servers](https://technet.microsoft.com/library/dd939904(WS.10).aspx)

-   [Neuindizieren der WSUS-Datenbank](https://technet.microsoft.com/library/dd939795(WS.10).aspx)

#### <a name="wsus-with-sql-server"></a>WSUS mit SQL Server
In den folgenden Fällen wird empfohlen, SQL Server mit WSUS zu verwenden:

1.  Sie benötigen eine WSUS-Lösung mit Netzwerklastenausgleich (NLB).

2.  Sie haben bereits mindestens eine Instanz von SQL Server installiert.

3.  Sie können den SQL Server-Dienst nicht unter einem lokalen Konto, das kein Systemkonto ist, oder mit der SQL Server-Authentifizierung ausführen. WSUS unterstützt nur die Windows-Authentifizierung.

### <a name="wsus-update-storage"></a>WSUS-Updatespeicher
Beim Synchronisieren von Updates auf den WSUS-Server werden die Metadaten- und Updatedateien an zwei separaten Speicherorten gespeichert. Metadaten werden in der WSUS-Datenbank gespeichert. Updatedateien können auf dem WSUS-Server oder auf Microsoft Update-Servern gespeichert werden, je nachdem, wie Sie Ihre Optionen für die Synchronisierung konfiguriert haben. Falls Sie sich dafür entscheiden, Updatedateien auf dem WSUS-Server zu speichern, laden Clientcomputer genehmigte Updates vom lokalen WSUS-Server herunter. Andernfalls laden Clientcomputer genehmigte Updates direkt von Microsoft Update herunter. Welche Option für Ihre Organisation am sinnvollsten ist, hängt von der Netzwerkbandbreite zum Internet, der Netzwerkbandbreite im Intranet und der lokalen Speicherverfügbarkeit ab.

Sie können für jeden bereitgestellten WSUS-Server eine andere Updatespeicherlösung verwenden.

#### <a name="local-wsus-server-storage"></a>Lokaler WSUS-Serverspeicher
Die lokale Speicherung von Updatedateien ist bei der Installation und Konfiguration von WSUS die Standardoption. Mit dieser Option können Sie Bandbreite auf der Internetverbindung des Unternehmens sparen, da Clientcomputer Updates direkt vom lokalen WSUS-Server herunterladen.

Diese Option setzt voraus, dass auf dem Server ausreichend Speicherplatz für alle erforderlichen Updates verfügbar ist. WSUS erfordert mindestens 20 GB, um Updates lokal zu speichern. Es werden jedoch 30 GB basierend auf getesteten Variablen empfohlen.

#### <a name="remote-storage-on-microsoft-update-servers"></a>Remotespeicher auf Microsoft Update-Servern
Sie können Updates remote auf Microsoft Update-Servern speichern. Diese Option ist hilfreich, wenn die meisten Clientcomputer die Verbindung mit dem WSUS-Server über eine langsame WAN-Verbindung herstellen, für den Internetzugriff jedoch über eine Verbindung mit hoher Bandbreite verfügen.

In diesem Fall wird der WSUS-Stammserver mit Microsoft Update synchronisiert und empfängt die Updatemetadaten. Nachdem Sie die Updates genehmigt haben, laden die Clientcomputer die genehmigten Updates von Microsoft Update-Servern herunter.

## <a name="14-choose-wsus-update-languages"></a>1.4. Auswählen der WSUS-Updatesprachen
Wenn Sie eine WSUS-Serverhierarchie bereitstellen, sollten Sie bestimmen, für welche Sprachen Updates in der Organisation erforderlich sind. Konfigurieren Sie den WSUS-Stammserver zum Herunterladen von Updates in allen Sprachen, die in der Organisation verwendet werden.

Es kann z. B. vorkommen, dass die Hauptniederlassung Updates in Englisch und Französisch benötigt, für eine Filiale aber Updates in Englisch, Französisch und Deutsch und für eine weitere Filiale Updates in Englisch und Spanisch erforderlich sind. In dieser Situation konfigurieren Sie den WSUS-Stammserver zum Herunterladen von Updates in Englisch, Französisch, Deutsch und Spanisch. Anschließend konfigurieren Sie den WSUS-Server der ersten Filiale zum Herunterladen von Updates in Englisch, Französisch und Deutsch und den WSUS-Server der zweiten Filiale zum Herunterladen von Updates in Englisch und Spanisch.

Auf der Seite **Sprachen auswählen** des WSUS-Konfigurations-Assistenten können Sie auswählen, ob Sie Updates für alle Sprachen oder eine Teilmenge von Sprachen wünschen. Wenn Sie eine Teilmenge von Sprachen auswählen, sparen Sie Speicherplatz. es ist jedoch wichtig, alle Sprachen auszuwählen, die für alle Downstreamserver und Client Computer eines WSUS-Servers erforderlich sind.

Im folgenden finden Sie einige wichtige Hinweise zur Aktualisierungs Sprache, die Sie beachten sollten, bevor Sie diese Option konfigurieren:

-   Wählen Sie neben allen anderen Sprachen, die in der Organisation benötigt werden, immer Englisch aus. Alle Updates basieren auf englischen Sprachpaketen.

-   Downstreamserver und Clientcomputer empfangen nicht alle erforderlichen Updates, wenn Sie nicht alle benötigten Sprachen für den Upstreamserver auswählen. Achten Sie darauf, dass Sie alle erforderlichen Sprachen für alle zugeordneten Clientcomputer aller Downstreamserver auswählen.

-   Auf dem WSUS-Stammserver, der mit Microsoft Update synchronisiert wird, sollten Sie generell Updates in allen Sprachen herunterladen. Dadurch stellen Sie sicher, dass alle Downstreamserver und Clientcomputer Updates in den für sie erforderlichen Sprachen empfangen.

Wenn Sie Updates lokal speichern und einen WSUS-Server zum Herunterladen von Updates in einer begrenzten Anzahl von Sprachen eingerichtet haben, werden Sie möglicherweise feststellen, dass Updates in Sprachen vorhanden sind, die Sie nicht angegeben haben. Bei vielen Updatedateien handelt es sich um Bündel mehrerer Sprachen, von denen Sie mindestens eine auf dem Server angegeben haben.

**Upstreamserver**

> [!NOTE]
> Konfigurieren Sie Upstreamserver zum Synchronisieren von Updates in allen Sprachen, die für Downstreamserver im Replikatmodus erforderlich sind. Für nicht synchronisierte Sprachen erfolgt keine Benachrichtigung über erforderliche Updates.

Updates werden auf Clientcomputern, die diese Sprache erfordern, als **Nicht zutreffend** angezeigt. Um dies zu vermeiden, stellen Sie sicher, dass alle Betriebssystemsprachen in den Optionen für die Synchronisierung der WSUS-Server enthalten sind. Sie können alle Betriebssystemsprachen anzeigen, indem Sie die **Computer** Ansicht der WSUS-Verwaltungskonsole aufrufen und die Computer nach Betriebssystem Sprache sortieren. Möglicherweise möchten Sie jedoch weitere Sprachen einschließen, wenn Microsoft-Anwendungen in mehr als einer Sprache vorhanden sind (z. b. wenn die französische Version von Microsoft Word auf einigen Computern installiert ist, auf denen die englische Version von Windows 8 verwendet wird.

Das Auswählen von Sprachen für einen Upstreamserver ist nicht dasselbe wie das Auswählen von Sprachen für einen Downstreamserver. Das folgende Verfahren macht die Unterschiede deutlich.

#### <a name="to-choose-update-languages-for-a-server-synchronizing-from-microsoft-update"></a>Auswählen von Updatesprachen für einen Server, der über Microsoft Update synchronisiert wird

1.  Im WSUS-Konfigurationsassistenten:

    -   Um Updates in allen Sprachen zu erhalten, klicken Sie auf **Updates in allen Sprachen herunterladen, einschließlich neuer Sprachen**.

    -   Um Updates nur für bestimmte Sprachen zu erhalten, klicken Sie auf **Updates nur in folgenden Sprachen herunterladen**, und wählen Sie dann die gewünschten Sprachen aus.

#### <a name="to-choose-update-languages-for-a-downstream-server"></a>Auswählen von Updatesprachen für einen Downstreamserver

1.  Wenn der Upstreamserver zum Herunterladen von Updatedateien in einer Teilmenge von Sprachen konfiguriert wurde: Klicken Sie im WSUS-Konfigurationsassistenten auf **Updates nur in folgenden Sprachen herunterladen** (nur die Sprachen, die mit einem Sternchen gekennzeichnet sind, werden vom Upstreamserver unterstützt), und wählen Sie dann die gewünschten Sprachen aus.

> [!NOTE]
> Dies sollte geschehen, obwohl der Downstreamserver dieselben Sprachen wie der Upstreamserver herunterladen soll.

2. Wenn der Upstreamserver zum Herunterladen von Updatedateien in allen Sprachen konfiguriert wurde: Klicken Sie im WSUS-Konfigurationsassistenten auf **Updates in allen Sprachen herunterladen, die auf dem Upstreamserver unterstützt werden**.

> [!NOTE]
> Dies sollte geschehen, obwohl der Downstreamserver dieselben Sprachen wie der Upstreamserver herunterladen soll. Diese Einstellung bewirkt, dass der Upstreamserver Updates in allen Sprachen herunterlädt, einschließlich der Sprachen, die ursprünglich nicht für den Upstreamserver konfiguriert wurden. Wenn Sie dem Upstreamserver Sprachen hinzufügen, sollten Sie die neuen Updates auf dessen Replikatserver kopieren.
>
> Das Ändern der Sprachoptionen nur auf dem Upstreamserver könnte dazu führen, dass die Anzahl der Updates, die auf dem zentralen Server genehmigt sind, nicht mit der Anzahl der genehmigten Updates auf den Replikatservern übereinstimmt.

## <a name="15-plan-wsus-computer-groups"></a>1.5. Planen der WSUS-Computergruppen
WSUS bietet Ihnen die Möglichkeit, Updates gezielt auf Gruppen von Clientcomputern anzuwenden, sodass Sie sicherstellen können, dass bestimmte Computer immer zum geeigneten Zeitpunkt die richtigen Updates erhalten. Wenn z. B. für alle Computer in einer Abteilung (z. B. im Buchhaltungsteam) eine bestimmte Konfiguration verwendet wird, können Sie eine Gruppe für das Team erstellen, entscheiden, welche Updates für die Computer erforderlich sind und wann sie installiert werden sollen, und anschließend mithilfe von WSUS-Berichten die Updates für das Team auswerten.

> [!NOTE]
> Auf einem im Replikatmodus ausgeführten WSUS-Server können keine Computergruppen erstellt werden. Alle Computergruppen, die für Clientcomputer des Replikatservers erforderlich sind, müssen auf dem WSUS-Stammserver der WSUS-Serverhierarchie erstellt werden. Weitere Informationen zum Replikat Modus finden Sie unter Verwalten von WSUS-Replikat Servern [Verwalten von WSUS-Replikat Servern](https://technet.microsoft.com/library/dd939893(WS.10).aspx) im WSUS 3,0 SP2 Operations Guide.

Computer sind immer der Gruppe **alle Computer** zugewiesen und bleiben der Gruppe " **nicht zugewiesene Computer** " zugewiesen, bis Sie Sie einer anderen Gruppe zuweisen. Computer können mehreren Gruppen angehören.

Computergruppen können in Hierarchien eingerichtet werden (z. B. %%amp;quot;Gehaltsabrechnung%%amp;quot; und %%amp;quot;Kreditoren%%amp;quot; als untergeordnete Gruppen von %%amp;quot;Buchhaltung%%amp;quot;). Für eine übergeordnete Gruppe genehmigte Updates werden zusätzlich zur übergeordneten Gruppe automatisch für untergeordnete Gruppen bereitgestellt. Wenn Sie in diesem Beispiel Update1 für die Gruppe %%amp;quot;Buchhaltung%%amp;quot; genehmigen, wird das Update auf allen Computern in der Gruppe %%amp;quot;Buchhaltung%%amp;quot;, allen Computern in der Gruppe %%amp;quot;Gehaltsabrechnung%%amp;quot; und allen Computern in der Gruppe %%amp;quot;Kreditoren%%amp;quot; bereitgestellt.

Da Computer mehreren Gruppen zugewiesen werden können, kann es passieren, dass ein Update mehrmals für einen Computer genehmigt wird. Das Update wird jedoch nur einmal bereitgestellt, und alle Konflikte werden vom WSUS-Server aufgelöst. Um mit dem vorherigen Beispiel fortzufahren: Wenn ComputerA der Gehaltsgruppe und der Gruppe der Konten, die übertragen werden, zugewiesen ist und Update1 für beide Gruppen genehmigt wird, wird es nur einmal bereitgestellt.

Für die Zuweisung von Computern zu Computergruppen stehen zwei Methoden zur Verfügung: serverseitige Zielgruppenadressierung und clientseitige Zielgruppenadressierung. Die Vorgehensweise bei diesen beiden Methoden ist wie folgt:

-   **Serverseitige Zielgruppenadressierung**: Sie weisen manuell einen oder mehrere Clientcomputer gleichzeitig mehreren Gruppen zu.

-   **Clientseitige Zielgruppenadressierung**: Sie verwenden Gruppenrichtlinien oder bearbeiten die Registrierungseinstellungen auf Clientcomputern so, dass diese Computer sich den zuvor erstellten Computergruppen selbst hinzufügen.

### <a name="conflict-resolution"></a>Konfliktauflösung
Vom Server werden die folgenden Regeln zum Lösen von Konflikten und Ermitteln der sich ergebenden Aktion auf Clients angewendet:

1.  Priority

2.  Installieren/Deinstallieren

3.  Stichtag

#### <a name="priority"></a>Priority
Die der Gruppe mit der höchsten Priorität zugewiesenen Aktionen setzen die Aktionen der anderen Gruppen außer Kraft. Je tiefer sich eine Gruppe in der Hierarchie befindet, desto höher ist ihre Priorität. Die Priorität wird nur basierend auf der Tiefe zugewiesen. Alle Verzweigungen besitzen die gleiche Priorität. Beispielsweise hat eine Gruppe, die sich zwei Ebenen unterhalb des Desktops befindet, eine höhere Priorität als eine Gruppe eine Ebene unterhalb des Serverzweigs.

Im folgenden Textbeispiel für den Hierarchie Bereich der Update Services-Konsole wurden für einen WSUS-Server mit dem Namen WSUS-01 die Computer Gruppen "Desktop Computer" und "Server" der Standardgruppe **alle Computer** hinzugefügt. Die Desktop Computer und Server Gruppen befinden sich auf derselben hierarchischen Ebene.

-   **Aktualisieren von Diensten**

    -   **WSUS-01**

        -   **Updates**

        -   **Computer**

            -   **Alle Computer**

                -   **Nicht zugewiesene Computer**

                -   **Desktop Computer**

                    -   **Desktops-L1**

                        -   **Desktops-L2**

                -   **Leistungsverlauf für Server**

                    -   **Server-L1**

        -   **Downstreamserver**

        -   **Synchronisierungen**

        -   **Berichte**

        -   **Options**

In diesem Beispiel hat die Gruppe zwei Ebenen unterhalb des Zweigs "Desktop Computer" (Desktops L2) eine höhere Priorität als die Gruppe eine Ebene unterhalb der Server Verzweigung (Server L1). Dementsprechend haben bei einem Computer, der sowohl Mitglied der Gruppe %%amp;quot;Desktops-L2%%amp;quot; als auch der Gruppe %%amp;quot;Servers-L1%%amp;quot; ist, alle Aktionen für die Gruppe %%amp;quot;Desktops-L2%%amp;quot; Priorität gegenüber den für die Gruppe %%amp;quot;Servers-L1%%amp;quot; angegebenen Aktionen.

#### <a name="priority-of-install-and-uninstall"></a>Priorität der Installation und Deinstallation
Installationsaktionen setzen Deinstallationsaktionen außer Kraft. Erforderliche Installationen haben Vorrang vor optionalen Installationen. (Optionale Installationen sind nur über die API verfügbar, und durch das Ändern einer Genehmigung für ein Update mithilfe der WSUS-Verwaltungskonsole werden alle optionalen Genehmigungen gelöscht.)

#### <a name="priority-of-deadlines"></a>Priorität von Terminen
Aktionen, die über einen Stichtag (eine Frist) verfügen, setzen Aktionen ohne Stichtag außer Kraft.  Aktionen mit früheren Stichtagen setzen Aktionen mit späteren Stichtagen außer Kraft.

## <a name="16-plan-wsus-performance-considerations"></a>1.6. Planen der WSUS-Leistung
Es gibt einige Bereiche, die Sie vor der Bereitstellung von WSUS sorgfältig planen sollten, damit Sie eine optimierte Leistung erzielen können. Die wichtigsten Bereiche sind:

-   Netzwerkeinrichtung

-   Zurückgestellter Download

-   Filter

-   Installation

-   Große Updatebereitstellungen

-   BITS (Background Intelligent Transfer Service, Intelligenter Hintergrundübertragungsdienst)

### <a name="network-setup"></a>Netzwerkeinrichtung
Anhand der folgenden Methoden kann die Leistung in WSUS-Netzwerken optimiert werden:

1.  Richten Sie WSUS-Netzwerke nicht in einer hierarchischen Topologie, sondern in einer Hub-Spoke-Topologie ein.

2.  Verwenden Sie die DNS-Netzwerkmaskenanforderung für Roamingclientcomputer, und konfigurieren Sie Roamingclientcomputer zum Herunterladen von Updates vom lokalen WSUS-Server.

### <a name="deferred-download"></a>Zurückgestellter Download
Sie können Updates genehmigen und die Updatemetadaten herunterladen, bevor Sie die Updatedateien herunterladen. Diese Methode wird als *zurückgestellter Download*bezeichnet. Wenn Sie Downloads zurückstellen, wird ein Update erst nach seiner Genehmigung heruntergeladen. Da bei dieser Methode die Netzwerkbandbreiten- und Speicherplatznutzung optimiert wird, wird empfohlen, Downloads zurückzustellen.

In einer Hierarchie von WSUS-Servern wird für alle Downstreamserver automatisch die auf dem WSUS-Stammserver festgelegte Einstellung für zurückgestellten Download verwendet. Diese Standardeinstellung kann geändert werden. Sie können z. B. einen Upstreamserver für vollständige, sofortige Synchronisierungen und anschließend einen Downstreamserver zum Zurückstellen der Downloads konfigurieren.

Es wird empfohlen, in einer Hierarchie verbundener WSUS-Server möglichst wenig Serverebenen zu verwenden. Wenn Sie zurück gestellte Downloads aktivieren und ein Downstreamserver ein Update anfordert, das auf dem Upstreamserver nicht genehmigt ist, erzwingt die Anforderung des Downstreamservers einen Download auf dem Upstreamserver. Der Downstreamserver lädt das Update dann bei einer nachfolgenden Synchronisierung herunter. In einer WSUS-Serverhierarchie mit vielen Ebenen, kann es zu Verzögerungen kommen, wenn Updates angefordert, heruntergeladen und dann durch die Serverhierarchie übertragen werden. Wenn Updates lokal gespeichert werden, sind zurückgestellte Downloads standardmäßig aktiviert. Sie können diese Option manuell ändern.

### <a name="filters"></a>Filter
WSUS bietet Ihnen die Möglichkeit, Updatesynchronisierungen nach Sprache, Produkt und Klassifizierung zu filtern. In einer Hierarchie von WSUS-Servern werden für alle Downstreamserver automatisch die auf dem WSUS-Stammserver ausgewählten Updatefilteroptionen verwendet. Sie können Downloadserver neu konfigurieren, sodass sie nur eine Teilmenge von Sprachen empfangen.

Standardmäßig werden die Produkte Windows und Office aktualisiert, und die Standardklassifizierungen sind %%amp;quot;Wichtige Updates%%amp;quot;, %%amp;quot;Sicherheitsupdates%%amp;quot; und %%amp;quot;Definitionsupdates%%amp;quot;. Um die Bandbreiten- und Speicherplatznutzung zu reduzieren, sollten Sie nur die Sprachen auswählen, die Sie tatsächlich verwenden.

### <a name="installation"></a>Installation
Updates bestehen normalerweise aus neuen Versionen von Dateien, die bereits auf dem zu aktualisierenden Computer vorhanden sind. Auf binärer Ebene unterscheiden sich die vorhandenen Dateien möglicherweise nur wenig von den aktualisierten Versionen. Das Feature für Schnellinstallationsdateien ermittelt die genauen Byteunterschiede zwischen Versionen, erstellt und verteilt Updates nur für diese Unterschiede und führt die vorhandene Datei dann mit den aktualisierten Bytes zusammen.

Manchmal wird dieses Feature als "Delta-Übermittlung" bezeichnet, da es nur das Delta (die Differenz) zwischen zwei Versionen einer Datei herunterlädt. Schnellinstallationsdateien sind größer als die an Clientcomputer verteilten Updates, da sie alle möglichen Versionen jeder zu aktualisierenden Datei enthalten.

Schnellinstallationsdateien können zum Beschränken der Bandbreite im lokalen Netzwerk genutzt werden, da WSUS nur das Delta für eine bestimmte Version einer aktualisierten Komponente übermittelt. Allerdings erfordert dies zusätzliche Bandbreite zwischen dem WSUS-Server, eventuellen Upstream-WSUS-Server und Microsoft Update und zusätzlichen lokalen Speicherplatz. Standardmäßig verwendet WSUS keine Schnellinstallationsdateien.

Nicht alle Updates eignen sich für die Verteilung mittels Schnellinstallationsdateien. Wenn Sie diese Option aktivieren, erhalten Sie Schnellinstallationsdateien für alle Updates. Wenn Sie Updates nicht lokal speichern, entscheidet der Windows Update-Agent, ob die Dateien der Expressinstallation oder die Updatedistribution für das vollständige Update heruntergeladen werden.

### <a name="large-update-deployment"></a>Große Updatebereitstellung
Mithilfe der folgenden Methoden können Sie beim Bereitstellen großer Updates (z. B. Service Packs) eine Überlastung des Netzwerks verhindern:

1.  Verwenden Sie die Bandbreiteneinschränkung des intelligenten Hintergrundübertragungsdiensts (BITS). BITS-Bandbreiteneinschränkungen können nach Tageszeit gesteuert werden, sie gelten jedoch für alle Anwendungen, für die BITS verwendet wird. Weitere Informationen zur Steuerung der Bits-Drosselung finden Sie unter [Gruppenrichtlinien](https://msdn.microsoft.com/library/windows/desktop/aa362844(v=vs.85).aspx).

2.  Verwenden Sie die Bandbreiteneinschränkung der Internetinformationsdienste (Internet Information Services, IIS), um die Einschränkung auf einen oder mehrere Webdienste zu beschränken.

3.  Verwenden Sie Computergruppen, um das Rollout zu steuern. Ein Clientcomputer identifiziert sich selbst als Mitglied einer bestimmten Computergruppe, wenn er Informationen an den WSUS-Server sendet. Der WSUS-Server ermittelt anhand dieser Informationen, welche Updates auf dem Computer bereitgestellt werden müssen. Sie können mehrere Computergruppen einrichten und Downloads großer Service Packs nacheinander für eine Teilmenge dieser Gruppen genehmigen.

### <a name="background-intelligent-transfer-service"></a>Intelligenter Hintergrundübertragungsdienst (Background Intelligent Transfer Service, BITS)
WSUS verwendet das BITS-Protokoll für alle Dateiübertragungsaufgaben. Dies beinhaltet Downloads auf Clientcomputer und Serversynchronisierungen. Mithilfe von BITS können Programme Dateien mit wenig Bandbreite herunterladen. BITS verwaltet Dateiübertragungen durch Trennen von Netzwerkverbindungen und Computerneustarts. Weitere Informationen finden Sie in den folgenden Themen: [Bits](https://msdn.microsoft.com/library/bb968799.aspx).

## <a name="17-plan-automatic-updates-settings"></a>1.7. Planen der Einstellungen für automatische Updates
Sie können einen Stichtag für die Genehmigung von Updates auf dem WSUS-Server festlegen. Der Stichtag führt dazu, dass Clientcomputer das Update zu einem bestimmten Zeitpunkt installieren. Abhängig davon, ob der Stichtag abgelaufen ist, andere zu installierende Updates für den Computer in der Warteschlange vorhanden sind und das Update (oder ein anderes Update in der Warteschlange) einen Neustart erfordert, können jedoch unterschiedliche Situationen auftreten.

Standardmäßig ruft das Feature %%amp;quot;Automatische Updates%%amp;quot; alle 22 Stunden (minus einer zufälligen Verschiebung) Updates vom WSUS-Server ab. Wenn neue Updates installiert werden müssen, werden sie heruntergeladen. Die Zeit zwischen den einzelnen Ermittlungszyklen kann auf einen Wert zwischen 1 und 22 Stunden festgelegt werden.

Die Benachrichtigungsoptionen können wie folgt bearbeitet werden:

1.  Wenn %%amp;quot;Automatische Updates%%amp;quot; zur Benachrichtigung des Benutzers über Updates, die zur Installation bereit sind, konfiguriert ist, wird die Benachrichtigung an das Systemprotokoll und den Infobereich des Clientcomputers gesendet.

2.  Klickt ein Benutzer mit entsprechenden Anmeldeinformationen auf das Symbol im Infobereich, zeigt %%amp;quot;Automatische Updates%%amp;quot; die zur Installation verfügbaren Updates an. Der Benutzer muss auf **Installieren** klicken, um die Installation zu starten. Erfordert das Update einen Neustart des Computers, wird eine Meldung angezeigt. Wenn ein Neustart erforderlich ist, kann %%amp;quot;Automatische Updates%%amp;quot; erst nach dem Neustart des Computers weitere Updates ermitteln.

Wenn %%amp;quot;Automatische Updates%%amp;quot; zum Installieren von Updates nach einem festgelegten Zeitplan konfiguriert ist, werden die erforderlichen Updates heruntergeladen und als %%amp;quot;Bereit für die Installation%%amp;quot; markiert. %%amp;quot;Automatische Updates%%amp;quot; benachrichtigt Benutzer mit entsprechenden Anmeldeinformationen durch ein Symbol im Infobereich, und ein Ereignis wird im Systemprotokoll erfasst.

Zum geplanten Zeitpunkt installiert %%amp;quot;Automatische Updates%%amp;quot; das Update und startet den Computer neu (sofern erforderlich) – auch, wenn kein lokaler Administrator angemeldet ist. Falls ein lokaler Administrator angemeldet ist und der Computer neu gestartet werden muss, zeigt %%amp;quot;Automatische Updates%%amp;quot; eine Warnung und einen Countdown für den Neustart an. Andernfalls erfolgt die Installation im Hintergrund.

Wenn der Computer neu gestartet werden muss und ein Benutzer angemeldet ist, wird ein ähnliches Countdowndialogfeld angezeigt, um den Benutzer über den bevorstehenden Neustart zu informieren. Die Einstellungen für Computerneustarts können mit dem Feature %%amp;quot;Gruppenrichtlinie%%amp;quot; bearbeitet werden.

Nachdem die neuen Updates heruntergeladen wurden, ruft %%amp;quot; Automatische Updates%%amp;quot; die Liste genehmigter Pakete vom WSUS-Server ab, um zu überprüfen, ob die heruntergeladenen Pakete noch gültig und genehmigt sind. Entfernt ein WSUS-Administrator Updates aus der Liste genehmigter Updates, während Updates von %%amp;quot;Automatische Updates%%amp;quot; heruntergeladen werden, werden somit nur die Updates installiert, die noch immer genehmigt sind.

