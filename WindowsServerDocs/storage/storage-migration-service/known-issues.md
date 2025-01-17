---
title: Bekannte Probleme bei Storage Migration Service
description: Bekannte Probleme und Problembehandlung für den Speicher Migrationsdienst, z. b. das Sammeln von Protokollen für Microsoft-Support.
author: nedpyle
ms.author: nedpyle
manager: siroy
ms.date: 10/09/2019
ms.topic: article
ms.prod: windows-server
ms.technology: storage
ms.openlocfilehash: e3ec7ee787fb6fd2e8e9f59249a6c4013a76b377
ms.sourcegitcommit: e2964a803cba1b8037e10d065a076819d61e8dbe
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/10/2019
ms.locfileid: "72252368"
---
# <a name="storage-migration-service-known-issues"></a>Bekannte Probleme bei Storage Migration Service

Dieses Thema enthält Antworten auf bekannte Probleme bei der Verwendung von [Storage Migration Service](overview.md) zum Migrieren von Servern.

Storage Migration Service wird in zwei Teilen veröffentlicht: der-Dienst in Windows Server und die Benutzeroberfläche im Windows Admin Center. Der Dienst ist in Windows Server, langfristig Wartungs Kanal sowie Windows Server, halbjährlicher Kanal, verfügbar. Obwohl Windows Admin Center als separater Download verfügbar ist. Wir schließen auch regelmäßig Änderungen an kumulativen Updates für Windows Server ein, die über Windows Update veröffentlicht werden. 

Beispielsweise enthält Windows Server, Version 1903, neue Features und Korrekturen für den Speicher Migrationsdienst, die auch für Windows Server 2019 und Windows Server, Version 1809, verfügbar sind, indem Sie [KB4512534](https://support.microsoft.com/help/4512534/windows-10-update-kb4512534)installieren.

## <a name="collecting-logs"></a>Sammeln von Protokolldateien beim Arbeiten mit Microsoft-Support

Der Speicher Migrationsdienst enthält Ereignisprotokolle für den Orchestrator-Dienst und den Proxy Dienst. Der urchestrator-Server enthält immer Ereignisprotokolle, und Zielserver, auf denen der Proxy Dienst installiert ist, enthalten die Proxy Protokolle. Diese Protokolle befinden sich unter:

- Anwendungs-und Dienst Protokolle \ Microsoft \ Windows \ storagemigrationservice
- Anwendungs-und Dienst Protokolle \ Microsoft \ Windows \ storagemigrationservice-Proxy

Wenn Sie diese Protokolle für die Offline Anzeige oder zum Senden an Microsoft-Support erfassen müssen, ist auf GitHub ein Open-Source-PowerShell-Skript verfügbar:

 [Hilfsprogramm für den Speicher Migrationsdienst](https://aka.ms/smslogs) 

Lesen Sie die Informationen zur Verwendung.

## <a name="storage-migration-service-doesnt-show-up-in-windows-admin-center-unless-managing-windows-server-2019"></a>Der Speicher Migrationsdienst wird nicht im Windows Admin Center angezeigt, es sei denn, Windows Server 2019 wird verwaltet.

Wenn Sie die Version 1809 von Windows Admin Center zum Verwalten eines Windows Server 2019 Orchestrator verwenden, wird die Option Tool für Storage Migration Service nicht angezeigt. 

Die Windows Admin Center Storage Migration Service-Erweiterung ist nur für die Verwaltung der Betriebssysteme Windows Server 2019, Version 1809 oder höher, Versions gebunden. Wenn Sie damit ältere Windows Server-Betriebssysteme oder Insider-Vorschau Versionen verwalten, wird das Tool nicht angezeigt. Dieses Verhalten ist entwurfsbedingt. 

Verwenden Sie zum Auflösen von Windows Server 2019 Build 1809 oder höher, oder führen Sie ein Upgrade durch.

## <a name="storage-migration-service-doesnt-let-you-choose-static-ip-on-cutover"></a>Der Speicher Migrationsdienst ermöglicht Ihnen nicht, statische IP-Adressen auf dem Umstellung auszuwählen.

Wenn Sie die Version 0,57 der Storage Migration Service-Erweiterung im Windows Admin Center verwenden und die Umschalter Phase erreichen, können Sie keine statische IP-Adresse für eine Adresse auswählen. Sie sind gezwungen, DHCP zu verwenden.

Um dieses Problem zu beheben, suchen Sie im Windows Admin Center unter **Einstellungen** > **Erweiterungen** eine Warnung, die besagt, dass die aktualisierte Version Storage Migration Service 0.57.2 zur Installation zur Verfügung steht. Möglicherweise müssen Sie die Browser Registerkarte für Windows Admin Center neu starten.

## <a name="storage-migration-service-cutover-validation-fails-with-error-access-is-denied-for-the-token-filter-policy-on-destination-computer"></a>Die Überprüfung des Speicher Migrationsdienst-cutovers schlägt mit dem Fehler "Zugriff wird für die tokenfilterrichtlinie auf dem Zielcomputer verweigert" fehl

Beim Ausführen der Überprüfung des cutovers erhalten Sie den Fehler "Fehler: Der Zugriff auf die tokenfilterrichtlinie auf dem Zielcomputer wird verweigert. " Dies geschieht auch, wenn Sie sowohl für den Quell-als auch für den Zielcomputer die richtigen lokalen Administrator Anmelde Informationen angegeben haben

Dieses Problem wird durch einen Code Fehler in Windows Server 2019 verursacht. Das Problem tritt auf, wenn Sie den Zielcomputer als Orchestrator für den Speicher Migrationsdienst verwenden.

Um dieses Problem zu umgehen, installieren Sie den Speicher Migrationsdienst auf einem Windows Server 2019-Computer, der nicht das Ziel für die Migration ist. Stellen Sie dann eine Verbindung mit diesem Server über das Windows Admin Center her, und führen Sie die Migration aus.

Dies wurde in einer späteren Version von Windows Server korrigiert. Öffnen Sie eine Supportanfrage über [Microsoft-Support](https://support.microsoft.com) , um einen Backport für diesen Fehler zu erstellen.

## <a name="storage-migration-service-isnt-included-in-windows-server-2019-evaluation-or-windows-server-2019-essentials-edition"></a>Storage Migration Service ist nicht in Windows Server 2019 Evaluation oder Windows Server 2019 Essentials Edition enthalten.

Wenn Sie Windows Admin Center verwenden, um eine Verbindung mit einer [Windows Server 2019-Evaluierungsversion](https://www.microsoft.com/evalcenter/evaluate-windows-server-2019) oder Windows Server 2019 Essentials Edition herzustellen, gibt es keine Option zum Verwalten des Speicher Migrations Dienstanbieter. Storage Migration Service ist auch nicht in Rollen und Features enthalten.

Dieses Problem wird durch ein Wartungsproblem in den Evaluierungs Medien von Windows Server 2019 und Windows Server 2019 Essentials verursacht. 

Um dieses Problem für die Evaluierung zu umgehen, installieren Sie eine Einzelhandels-, MSDN-, OEM-oder Volumenlizenz Version von Windows Server 2019, und aktivieren Sie Sie nicht. Ohne Aktivierung werden alle Editionen von Windows Server 180 Tage lang im Evaluierungs Modus ausgeführt. 

Dieses Problem wurde in einem späteren Release von Windows Server behoben.  

## <a name="storage-migration-service-times-out-downloading-the-transfer-error-csv"></a>Timeout des Speicher Migrations Dienstanbieter beim Herunterladen des Übertragungsfehler-CSV

Wenn Sie das Windows Admin Center oder PowerShell verwenden, um das CSV-Protokoll mit ausführlichen Fehlern bei der Übertragungs Operation herunterzuladen, erhalten Sie folgende Fehlermeldung:

 >   Übertragungsprotokoll: Überprüfen Sie, ob die Dateifreigabe in der Firewall zulässig ist. : Dieser Anforderungs Vorgang, der an net. TCP://localhost: 28940/SMS/Service/1/Transfer gesendet wurde, hat innerhalb des konfigurierten Timeouts (00:01:00) keine Antwort empfangen. Der für diesen Vorgang zugewiesene Zeitraum war möglicherweise ein Teil eines längeren Timeouts. Dies liegt möglicherweise daran, dass der Dienst den Vorgang noch verarbeitet oder der Dienst keine Antwortnachricht senden konnte. Erhöhen Sie das Timeout für den Vorgang (indem Sie den Kanal/Proxy in IContextChannel umwandeln und die Eigenschaft OperationTimeout festlegen), und stellen Sie sicher, dass der Dienst eine Verbindung mit dem Client herstellen kann.

Dieses Problem wird durch eine extrem große Anzahl übertragener Dateien verursacht, die nicht in dem vom Speicher Migrationsdienst zulässigen Standard Timeout von einer Minute gefiltert werden können. 

So umgehen Sie dieses Problem:

1. Bearbeiten Sie auf dem Orchestrator-Computer die Datei *%systemroot%\SMS\Microsoft.StorageMigration.Service.exe.config* mithilfe von "Notepad. exe", um "SendTimeout" von der 1-minütigen Standardeinstellung in 10 Minuten zu ändern.

   ```
     <bindings>
      <netTcpBinding>
        <binding name="NetTcpBindingSms"
                 sendTimeout="00:01:00"
   ```

2. Starten Sie den Dienst "Storage Migration Service" auf dem Orchestrator-Computer neu. 
3. Starten Sie auf dem Orchestrator-Computer "regedit. exe".
4. Suchen Sie den folgenden Registrierungsunterschlüssel, und klicken Sie darauf: 

   `HKEY_LOCAL_MACHINE\Software\Microsoft\SMSPowershell`

5. Zeigen Sie im Menü „Bearbeiten“ auf „Neu“, und klicken Sie dann auf „DWORD-Wert“. 
6. Geben Sie "wcfoperationtimeoutinminutes" als Namen für das DWORD ein, und drücken Sie dann die EINGABETASTE.
7. Klicken Sie mit der rechten Maustaste auf "wcfoperationtimeoutinminutes", und klicken Sie dann auf ändern. 
8. Klicken Sie im Feld Base Data auf "Decimal".
9. Geben Sie im Feld Wertdaten den Wert "10" ein, und klicken Sie dann auf OK.
10. Beenden Sie den Registrierungs-Editor.
11. Es wird erneut versucht, die CSV-Datei mit Fehlern herunterzuladen. 

Wir beabsichtigen, dieses Verhalten in einer späteren Version von Windows Server 2019 zu ändern.  

## <a name="cutover-fails-when-migrating-between-networks"></a>Fehler bei der Migration zwischen Netzwerken

Beim Migrieren zu einem Zielcomputer, der in einem anderen Netzwerk als der Quelle ausgeführt wird, z. b. eine Azure-IaaS-Instanz, kann Umstellung nicht fertiggestellt werden, wenn die Quelle eine statische IP-Adresse verwendet hat. 

Dieses Verhalten ist beabsichtigt, um Konnektivitätsprobleme nach der Migration von Benutzern, Anwendungen und Skripts zu verhindern, die über die IP-Adresse verbunden werden Wenn die IP-Adresse vom alten Quellcomputer zum neuen Zielziel verschoben wird, entspricht Sie nicht den neuen netzwerksubnetzinformationen und vielleicht DNS und WINS.

Um dieses Problem zu umgehen, führen Sie eine Migration zu einem Computer im gleichen Netzwerk durch. Verschieben Sie diesen Computer dann in ein neues Netzwerk, und weisen Sie seine IP-Informationen erneut zu. Wenn Sie beispielsweise eine Migration zu Azure IaaS durchführen, führen Sie zuerst eine Migration zu einer lokalen VM durch, und verwenden Sie dann Azure migrate, um den virtuellen Computer in Azure  

Dieses Problem wurde in einem späteren Release von Windows Admin Center behoben. Wir ermöglichen es Ihnen jetzt, Migrationen anzugeben, die die Netzwerkeinstellungen des Zielservers nicht ändern. Die aktualisierte Erweiterung wird hier aufgelistet, wenn Sie veröffentlicht wird. 

## <a name="validation-warnings-for-destination-proxy-and-credential-administrative-privileges"></a>Validierungs Warnungen für den Ziel Proxy und Administratorrechte für Anmelde Informationen

Beim Validieren eines Übertragungs Auftrags werden folgende Warnungen angezeigt:

 > **Die Anmelde Informationen verfügen über Administratorrechte.**
 > Warnung: Die Aktion ist nicht Remote verfügbar.
 > **Der Ziel Proxy ist registriert.**
 > Warnung: Der Ziel Proxy wurde nicht gefunden.

Wenn Sie den Speicher Migrationsdienst-Proxy Dienst auf dem Windows Server 2019-Zielcomputer nicht installiert haben, oder wenn der Zielcomputer Windows Server 2016 oder Windows Server 2012 R2 ist, ist dieses Verhalten Entwurfs bedingt. Es wird empfohlen, zu einem Windows Server 2019-Computer zu migrieren, auf dem der Proxy installiert ist  

## <a name="certain-files-do-not-inventory-or-transfer-error-5-access-is-denied"></a>Bestimmte Dateien werden nicht inventarisiert oder übertragen, Fehler 5: "Zugriff verweigert"

Bei der Inventarisierung oder Übertragung von Dateien von einer Quell-auf einen Zielcomputer können Dateien, von denen ein Benutzer die Administrator Gruppenberechtigungen entfernt hat, nicht migriert werden. Überprüfen des Speicher Migrations Dienstanbieter: Proxy Debug zeigt Folgendes an:

  Protokoll Name:      Microsoft-Windows-storagemigrationservice-Proxy/debugquelle:        Microsoft-Windows-storagemigrationservice-Proxy Datum:          2/26/2019 9:00:04 Uhr Ereignis-ID:      10000 Aufgaben Kategorie: Keine Ebene:         Fehler Schlüsselwörter:      
  Benutzer:          Netzwerkdienst Computer: SRV1.contoso.com Beschreibung:

  02/26/2019-09:00:04.860 [Fehler] Übertragungsfehler für \\srv1. c. ". com\public\indy.png": (5) der Zugriff wurde verweigert.
Stapel Überwachung: bei Microsoft. storagemigration. Proxy. Service. Transfer. filedirutils. OpenFile (Zeichenfolge Dateiname, desiredAccess desiredAccess, share Mode Share Mode, kreationdisposition erationdisposition, flagsandattribute flagsandattribute) unter Microsoft. storagemigration. Proxy. Service. Transfer. filedirutils. gettargetfile (Zeichen folgen Pfad) bei Microsoft. storagemigration. Proxy. Service. Transfer. filedirutils. gettargetfile (FileInfo-Datei) unter Microsoft. storagemigration. Proxy. Service. Transfer. Filetransfer. initializesourcefileingefo () bei Microsoft. storagemigration. Proxy. Service. Transfer. Filetransfer. Transfer () at Microsoft. storagemigration. Proxy. Service. Transfer. Filetransfer. trytransfer () [d:\os\src\base\dms\proxy\transfer\transferproxy\filetransfer.cs:: trytransfer:: 55]


Dieses Problem wird durch einen Code Fehler im Speicher Migrationsdienst verursacht, bei dem die Sicherungs Berechtigung nicht aufgerufen wurde. 

Um dieses Problem zu beheben, installieren Sie [Windows Update 2. April 2019 – KB4490481 (OS Build 17763,404)](https://support.microsoft.com/help/4490481/windows-10-update-kb4490481) auf dem Orchestrator-Computer und dem Zielcomputer, wenn der Proxy Dienst dort installiert ist. Stellen Sie sicher, dass das Benutzerkonto der Quell Migration ein lokaler Administrator auf dem Quellcomputer und der Orchestrator für den Speicher Migrationsdienst ist. Stellen Sie sicher, dass das Benutzerkonto für die Ziel Migration ein lokaler Administrator auf dem Zielcomputer und der Orchestrator für den Speicher Migrationsdienst ist. 

## <a name="dfsr-hashes-mismatch-when-using-storage-migration-service-to-preseed-data"></a>Nicht übereinstimmende DFSR-Hashes bei der Verwendung von Storage Migration Service zum vorab Seed von Daten

Wenn Sie den Speicher Migrationsdienst zum Übertragen von Dateien an ein neues Ziel verwenden, können Sie die DFS-Replikation (DFSR) zum Replizieren dieser Daten mit einem vorhandenen DFSR-Server über die vorab bereitgestellte Replikation oder das Klonen von DFSR-Datenbanken konfigurieren. nicht übereinstimmende und werden erneut repliziert. Die Datenströme, Sicherheitsdaten Ströme, Größen und Attribute werden nach der Verwendung von SMS für die Übertragung der Datenströme angezeigt. Wenn Sie die Dateien mit icacls oder dem Klon Debugprotokoll der DFSR-Datenbank untersuchen, werden folgende

Quelldatei:

  icacls d:\test\quelle:

  icacls d:\test\thatcher.png/Save out. txt/t Thatcher. png d:Ai (A;; FA;;; BA) (A;; 0 x1200a9;;;D D) (A;; 0 x1301bf;;;D U) (A; ID; FA;;; BA) (A; ID; FA;;; SY) (A; ID; 0x1200a9;;; ECM

Zieldatei:

  icacls d:\test\thatcher.png/Save out. txt/t Thatcher. png d:Ai (A;; FA;;; BA) (A;; 0 x1301bf;;;D U) (A;; 0 x1200a9;;;D D) (A; ID; FA;;; BA) (A; ID; FA;;; SY) (A; ID; 0x1200a9;;; BU)**S:PAINO_ACCESS_CONTROL**

DFSR-Debugprotokoll:

  20190308 10:18:53.116 3948 dbcl 4045 [warn] dbclone:: idtableimportupdate-Konflikt Daten Satz gefunden. 

  Lokaler ACL-Hash: 1bcdfe03-A18BCE01-D1AE9859-23a0a5f 6 LastWrite-Time: 20190308 18:09:44.876 filesizelow: 1131654 filesizehigh: 0 Attribute: 32 

  Klon-ACL-Hash:**DDC4FCE4-DDF329C4-977ced6d-F4D72A5B** LastWrite-Time: 20190308 18:09:44.876 filesizelow: 1131654 filesizehigh: 0 Attribute: 32 

Dieses Problem wird durch einen Code Fehler in einer Bibliothek verursacht, die vom Speicher Migrationsdienst zum Festlegen von Sicherheits Überwachungs-Zugriffs Steuerungs Listen (Security Audit ACLs, SACL) verwendet wird. Eine SACL, die keine NULL-Werte ist, wird versehentlich festgelegt, wenn die SACL leer war, was dazu führte, dass DFSR den Hash nicht übereinstimmt. 

Um dieses Problem zu umgehen, verwenden Sie weiterhin Robocopy für [DFSR-Pre-Seeding-und DFSR-Daten Bank Klon Vorgänge](../dfs-replication/preseed-dfsr-with-robocopy.md) anstelle des Storage Migration Service. Wir untersuchen dieses Problem und beabsichtigen, dieses Problem in einer neueren Version von Windows Server und möglicherweise einer backportiert-Windows Update zu beheben. 

## <a name="error-404-when-downloading-csv-logs"></a>Fehler 404 beim Herunterladen von CSV-Protokollen

Wenn Sie versuchen, die Übertragungs-oder Fehlerprotokolle am Ende eines Übertragungs Vorgangs herunterzuladen, erhalten Sie folgende Fehlermeldung:

  $Jobname: Übertragungsprotokoll: AJAX-Fehler 404

Dieser Fehler wird erwartet, wenn Sie die Firewallregel "Datei-und Druckerfreigabe (SMB-in)" auf dem Orchestrator-Server nicht aktiviert haben. Zum Herunterladen von Windows Admin Center-Dateien ist Port TCP/445 (SMB) auf verbundenen Computern erforderlich.  

## <a name="error-couldnt-transfer-storage-on-any-of-the-endpoints-when-transferring-from-windows-server-2008-r2"></a>Fehler "der Speicher konnte bei der Übertragung von Windows Server 2008 R2 nicht an einen der Endpunkte übertragen werden.

Beim Versuch, Daten von einem Windows Server 2008 R2-Quellcomputer zu übertragen, erhalten Sie keine Datenübertragungen, und Sie erhalten eine Fehlermeldung:  

  Der Speicher konnte auf keinem der Endpunkte übertragen werden.
0x9044

Dieser Fehler wird erwartet, wenn Ihr Windows Server 2008 R2-Computer nicht vollständig mit allen kritischen und wichtigen Updates von Windows Update gepatcht ist. Unabhängig vom Speicher Migrationsdienst empfehlen wir immer, einen Windows Server 2008 R2-Computer zu Sicherheitszwecken zu patchen, da dieses Betriebssystem nicht die Sicherheitsverbesserungen von neueren Versionen von Windows Server enthält.

## <a name="error-couldnt-transfer-storage-on-any-of-the-endpoints-and-check-if-the-source-device-is-online---we-couldnt-access-it"></a>Fehler "der Speicher konnte nicht an einen der Endpunkte übertragen werden", und "Überprüfen Sie, ob das Quellgerät Online ist-wir konnten nicht darauf zugreifen."

Beim Versuch, Daten von einem Quellcomputer zu übertragen, werden einige oder alle Freigaben nicht übertragen, zusammenfassende Fehler:

   Der Speicher konnte auf keinem der Endpunkte übertragen werden.
0x9044

Die Überprüfung der Details zur SMB-Übertragung zeigt Folgendes

   Überprüfen Sie, ob das Quellgerät Online ist-wir konnten nicht darauf zugreifen.

Die Untersuchung des storagemigrationservice/Admin-Ereignis Protokolls zeigt Folgendes:

   Speicher konnte nicht übertragen werden.

   Auftrag Den job1-ID:  
   Land Fehler: 36931-Fehlermeldung: 

   Leitfaden: Überprüfen Sie den detaillierten Fehler, und stellen Sie sicher, dass die Übertragungsanforderungen erfüllt sind. Der Übertragungs Auftrag konnte keine Quell-und Zielcomputer übertragen. Dies kann darauf zurückzuführen sein, dass der Orchestrator-Computer keinen Quell-oder Zielcomputer erreichen konnte, möglicherweise aufgrund einer Firewallregel oder fehlender Berechtigungen.

Die Untersuchung des storagemigrationservice-Proxy/Debug-Protokolls zeigt Folgendes:

   07/02/2019-13:35:57.231 [Fehler] Fehler bei der Überprüfung der Übertragung. ErrorCode 40961, der Quell Endpunkt ist nicht erreichbar oder nicht vorhanden, oder die Quell Anmelde Informationen sind ungültig, oder der authentifizierte Benutzer verfügt nicht über ausreichende Zugriffsberechtigungen.
bei Microsoft. storagemigration. Proxy. Service. Transfer. transferoperation. Validate () bei Microsoft. storagemigration. Proxy. Service. Transfer. transferrequesthandler. ProcessRequest (filetransferrequest filetransferrequest, GUID operationId)    [d:\os\src\base\dms\proxy\transfer\transferproxy\transferrequesthandler.cs::

Dieser Fehler wird erwartet, wenn Ihr Migrations Konto nicht mindestens über Lese Zugriffsberechtigungen für die SMB-Freigaben verfügt. Um diesen Fehler zu umgehen, fügen Sie eine Sicherheitsgruppe mit dem Quell Migrations Konto zu den SMB-Freigaben auf dem Quellcomputer hinzu, und erteilen Sie Lese-, Änderungs-oder Vollzugriff. Nachdem die Migration abgeschlossen ist, können Sie diese Gruppe entfernen.

## <a name="error-0x80005000-when-running-inventory"></a>Fehler 0x80005000 beim Ausführen des Inventars.

Nach der Installation von [KB4512534](https://support.microsoft.com/en-us/help/4512534/windows-10-update-kb4512534) und dem Versuch, das Inventar auszuführen, schlägt die Inventur mit Fehlern fehl

  AUSNAHME VON HRESULT: 0x80005000
  
  Protokoll Name:      Microsoft-Windows-storagemigrationservice/Administrator Quelle:        Microsoft-Windows-storagemigrationservice-Datum:          9/9/2019 5:21:42 Uhr Ereignis-ID:      2503 Aufgaben Kategorie: Keine Ebene:         Fehler Schlüsselwörter:      
  Benutzer:          Netzwerkdienst Computer:      FS02. TailwindTraders.net Beschreibung: Computer konnten nicht inventarisiert werden.
Job: foo2-ID: 20ac3f75-4945-41d1-9a79-d11dbb57798b-Status: Fehler: 36934-Fehlermeldung: Fehler bei der Inventur für alle Geräte Leit Faden: Prüfen Sie den detaillierten Fehler, und stellen Sie sicher, dass die Inventur Anforderungen erfüllt sind. Der Auftrag konnte keinen der angegebenen Quellcomputer inventarisieren. Dies kann darauf zurückzuführen sein, dass der Orchestrator-Computer ihn nicht über das Netzwerk erreichen konnte, möglicherweise aufgrund einer Firewallregel oder fehlender Berechtigungen.
  
  Protokoll Name:      Microsoft-Windows-storagemigrationservice/Administrator Quelle:        Microsoft-Windows-storagemigrationservice-Datum:          9/9/2019 5:21:42 Uhr Ereignis-ID:      2509 Aufgaben Kategorie: Keine Ebene:         Fehler Schlüsselwörter:      
  Benutzer:          Netzwerkdienst Computer:      FS02. TailwindTraders.net Beschreibung: Konnte keinen Computer inventarisieren.
Auftrag: foo2 Computer: FS01. TailwindTraders.net-Status: Fehler:-2147463168 Fehlermeldung: Leitfaden: Prüfen Sie den detaillierten Fehler, und stellen Sie sicher, dass die Inventur Anforderungen erfüllt sind. Das Inventar konnte keine Aspekte des angegebenen Quell Computers ermitteln. Dies kann daran liegen, dass fehlende Berechtigungen oder Berechtigungen für die Quelle oder einen gesperrten Firewallport vorhanden sind.
  
Dieser Fehler wird durch einen Code Fehler im Speicher Migrationsdienst verursacht, wenn Sie Migrations Anmelde Informationen in Form eines Benutzer Prinzipal namens (User Principal Name, UPN) bereitstellen, z. b. "meghan@contoso.com". Der Orchestrator-Dienst des Speicher Migrations Dienstanbieter kann dieses Format nicht ordnungsgemäß analysieren, was zu einem Fehler bei einer Domänen Suche führt, die zur Unterstützung der Cluster Migration in KB4512534 und 19h1 hinzugefügt wurde.

Um dieses Problem zu umgehen, geben Sie Anmelde Informationen im Format "Domäne \ Benutzer" an, z. b. "contoso\meghan".

## <a name="error-serviceerror0x9006-or-the-proxy-isnt-currently-available-when-migrating-to-a-windows-server-failover-cluster"></a>Fehler "ServiceError0x9006" oder "der Proxy ist zurzeit nicht verfügbar." beim Migrieren zu einem Windows Server-Failovercluster

Wenn Sie versuchen, Daten auf einen Cluster Datei Server zu übertragen, erhalten Sie folgende Fehlermeldung: 

   Stellen Sie sicher, dass der Proxy Dienst installiert ist und ausgeführt wird, und wiederholen Sie dann den Vorgang. Der Proxy ist zurzeit nicht verfügbar.
0x9006 ServiceError0x9006, Microsoft. storagemigration. Commands. unregistersmsproxycommand

Dieser Fehler wird erwartet, wenn die Datei Server Ressource vom ursprünglichen Windows Server 2019-Cluster Besitzer Knoten auf einen neuen Knoten verschoben wurde und die Proxy Funktion für den Speicher Migrationsdienst nicht auf diesem Knoten installiert wurde.

Um dieses Problem zu umgehen, verschieben Sie die Ressource des Ziel Dateiservers zurück auf den ursprünglichen Besitzer Cluster Knoten, der bei der ersten Konfiguration der Übertragungs Paare verwendet wurde.

Als Alternative Problem Umgehung:

1. Installieren Sie das Feature "Speicher Migrationsdienst-Proxy" auf allen Knoten in einem Cluster.
2. Führen Sie den folgenden PowerShell-Befehl für den Speicher Migrationsdienst auf dem Orchestrator-Computer aus: 

   ```PowerShell
   Register-SMSProxy -ComputerName *destination server* -Force
   ```
## <a name="error-dll-was-not-found-when-running-inventory-from-a-cluster-node"></a>Fehler "dll wurde nicht gefunden" beim Ausführen des Inventars von einem Cluster Knoten

Wenn Sie versuchen, eine Inventur mit dem auf einem Windows Server 2019-Failoverclusterknoten installierten Orchestrator auf einem Windows Server-Failoverclusterknoten auszuführen und als Ziel eines Windows Server-Failoverclusters die allgemeine Verwendung von Datei Server Quelle

    DLL not found
    [Error] Failed device discovery stage VolumeInfo with error: (0x80131524) Unable to load DLL 'Microsoft.FailoverClusters.FrameworkSupport.dll': The specified module could not be found. (Exception from HRESULT: 0x8007007E)   

Um dieses Problem zu umgehen, installieren Sie die Failovercluster-Verwaltungs Tools (RSAT-Clustering-Mgmt) auf dem Server, auf dem der Orchestrator für den Speicher Migrationsdienst ausgeführt wird. 

## <a name="error-there-are-no-more-endpoints-available-from-the-endpoint-mapper-when-running-inventory-against-a-windows-server-2003-source-computer"></a>Fehler "Es sind keine weiteren Endpunkte von der Endpunkt Zuordnung verfügbar", wenn die Inventur auf einem Windows Server 2003-Quellcomputer ausgeführt wird.

Wenn Sie versuchen, die Inventur mit dem für den Speicher Migrationsdienst Orchestrator-Server mit dem kumulativen Update für [KB4512534](https://support.microsoft.com/help/4512534/windows-10-update-kb4512534) oder später auszuführen, erhalten Sie die folgende Fehlermeldung:

    There are no more endpoints available from the endpoint mapper  

Um dieses Problem zu umgehen, deinstallieren Sie das kumulative Update KB4512534 (und ggf. das kumulative Update) vorübergehend über den Orchestrator-Computer des Speicher Migrations Dienstanbieter. Installieren Sie nach Abschluss der Migration das aktuellste kumulative Update neu.  

Beachten Sie, dass es unter bestimmten Umständen dazu führen kann, dass der Speicher Migrationsdienst nicht mehr gestartet wird, wenn Sie KB4512534 oder seine ersetzenden Updates deinstallieren Um dieses Problem zu beheben, können Sie die Speicher Migrationsdienst-Datenbank sichern und löschen:

1.  Öffnen Sie eine Eingabeaufforderung mit erhöhten Rechten, bei der Sie ein Mitglied der Administratoren auf dem Orchestrator-Server für den Speicher Migrationsdienst sind, und führen Sie Folgendes aus:

     ```
     MD c:\ProgramData\Microsoft\StorageMigrationService\backup

     ICACLS c:\ProgramData\Microsoft\StorageMigrationService\* /grant Administrators:(GA)

     XCOPY c:\ProgramData\Microsoft\StorageMigrationService\* .\backup\*

     DEL c:\ProgramData\Microsoft\StorageMigrationService\* /q

     ICACLS c:\ProgramData\Microsoft\StorageMigrationService  /GRANT networkservice:F /T /C

     ICACLS c:\ProgramData\Microsoft\StorageMigrationService /GRANT networkservice:(GA)F /T /C
     ```
   
2.  Starten Sie den Dienst "Storage Migration Service", mit dem eine neue Datenbank erstellt wird.



## <a name="see-also"></a>Siehe auch

- [Übersicht über den Speicher Migrationsdienst](overview.md)
