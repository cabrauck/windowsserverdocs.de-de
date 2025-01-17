---
title: Häufig gestellte Fragen (FAQ) zu Storage Migration Service
description: Häufig gestellte Fragen zum Speicher Migrationsdienst, z. b. welche Dateien bei der Migration von einem Server zu einem anderen von Übertragungen ausgeschlossen werden.
author: nedpyle
ms.author: nedpyle
manager: siroy
ms.date: 08/19/2019
ms.topic: article
ms.prod: windows-server
ms.technology: storage
ms.openlocfilehash: 6895c4b5f74beb237378060f82135d6f578986b7
ms.sourcegitcommit: e92a78f8d307200e64617431a701b9112a9b4e48
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/05/2019
ms.locfileid: "71973865"
---
# <a name="storage-migration-service-frequently-asked-questions-faq"></a>Häufig gestellte Fragen (FAQ) zu Storage Migration Service

Dieses Thema enthält Antworten auf häufig gestellte Fragen (FAQs) zur Verwendung von [Storage Migration Service](overview.md) zum Migrieren von Servern.

## <a name="what-files-and-folders-are-excluded-from-transfers"></a>Welche Dateien und Ordner sind von Übertragungen ausgeschlossen?

Der Speicher Migrationsdienst überträgt keine Dateien oder Ordner, die mit dem Windows-Vorgang beeinträchtigt werden könnten. Im folgenden finden Sie Informationen, die wir nicht übertragen oder in den Ordner "preexistingdata" des Ziels verschieben:

- Windows, Programme, Programmdateien (x86), Programm Daten, Benutzer
- $Recycle. bin, Recycler, recycelt, systemvolumeinformationen, $UpgDrv $, $SysReset, $Windows. ~ BT, $Windows. ~ ls, Windows. Old, Boot, Recovery, Documents und Settings
- Pagefile. sys, hiberfil. sys, swap file. sys, winpepge. sys, config. sys, Bootsect. bak, Bootmgr, bootnxt
- Alle Dateien oder Ordner auf dem Quell Server, die mit den ausgeschlossenen Ordnern auf dem Ziel in Konflikt stehen. <br>Wenn z. b. ein Ordner "n:\Windows" in der Quelle vorhanden ist und der "C:\" zugeordnet wird. das Volume auf dem Ziel, das nicht übertragen wird – unabhängig davon, was darin enthalten ist –, weil es den Ordner "c:\Windows" auf dem Ziel beeinträchtigt.

## <a name="are-domain-migrations-supported"></a>Werden Domänen Migrationen unterstützt?

Der Speicher Migrationsdienst lässt keine Migration zwischen Active Directory Domänen zu. Bei Migrationen zwischen Servern wird der Zielserver immer derselben Domäne hinzugefügt. Sie können die Anmelde Informationen für die Migration von verschiedenen Domänen in der Active Directory Gesamtstruktur verwenden. Der Speicher Migrationsdienst unterstützt die Migration zwischen Arbeitsgruppen.  

## <a name="are-clusters-supported-as-sources-or-destinations"></a>Werden Cluster als Quellen oder Ziele unterstützt?

Der Storage Migration Service unterstützt die Migration von und zu Clustern nach der Installation des kumulativen Updates [KB4513534](https://support.microsoft.com/help/4512534/windows-10-update-kb4512534) oder nachfolgende Updates. Dies umfasst auch das Migrieren von einem Quell Cluster zu einem Ziel Cluster sowie das Migrieren von einem eigenständigen Quell Server zu einem Ziel Cluster für die Geräte Konsolidierung. 

## <a name="do-local-groups-and-local-users-migrate"></a>Werden lokale Gruppen und lokale Benutzer migriert?

Der Storage Migration Service unterstützt die Migration lokaler Benutzer und Gruppen nach der Installation des kumulativen Updates [KB4513534](https://support.microsoft.com/help/4512534/windows-10-update-kb4512534) oder nachfolgende Updates. 

## <a name="is-domain-controller-migration-supported"></a>Wird die Migration des Domänen Controllers unterstützt?

Der Speicher Migrationsdienst migriert zurzeit keine Domänen Controller in Windows Server 2019. Wenn Sie mehr als einen Domänen Controller in der Active Directory Domäne haben, sollten Sie den Domänen Controller vor der Migration herabstufen und dann das Ziel herauf Stufen, nachdem der Vorgang abgeschlossen wurde.

## <a name="what-attributes-are-migrated-by-the-storage-migration-service"></a>Welche Attribute werden vom Speicher Migrationsdienst migriert?

Der Speicher Migrationsdienst migriert alle Flags, Einstellungen und die Sicherheit von SMB-Freigaben. Die Liste der Flags, die von Storage Migration Service migriert werden, umfasst Folgendes:

    - Freigabe Status
    - Verfügbarkeitsart
    - Freigabetyp
    - Ordner *enumerationsmodus (auch als Zugriffs basierte Enumeration oder Abe bezeichnet)*
    - Cache Modus
    - Leasing Modus
    - SMB-Instanz
    - ZS-Timeout
    - Limit für gleichzeitige Benutzer
    - Fortlaufend verfügbar
    - Beschreibung           
    - Verschlüsseln von Daten
    - Identitäts-Remoting
    - Infrastruktur
    - Name
    - Pfad
    - Bereich
    - Bereichsname
    - Sicherheitsbeschreibung
    - Schatten Kopie
    - Spezielle
    - Zeitwei

## <a name="can-i-consolidate-multiple-servers-into-one-server"></a>Kann ich mehrere Server auf einem Server konsolidieren?

Die in Windows Server 2019 enthaltene Version des Speicher Migrations Dienstanbieter unterstützt nicht das Konsolidieren mehrerer Server zu einem Server. Ein Beispiel für eine Konsolidierung wäre die Migration von drei separaten Quell Servern, die die gleichen Freigabe Namen und lokalen Dateipfade aufweisen können, auf einem einzelnen neuen Server, der diese Pfade und Freigaben virtualisiert, um Überschneidungen oder Kollisionen zu vermeiden und dann alle drei vorherige Servernamen und IP-Adresse. Es ist jedoch möglich, eigenständige Server auf mehrere Dateiserver Ressourcen in einem einzelnen Cluster zu migrieren. 

## <a name="can-i-migrate-from-sources-other-than-windows-server"></a>Kann ich aus anderen Quellen als Windows Server migrieren?

Der Storage Migration Service unterstützt die Migration von Samba-Linux-Servern nach der Installation des kumulativen Updates [KB4513534](https://support.microsoft.com/help/4512534/windows-10-update-kb4512534) oder nachfolgende Updates. Eine Liste der unterstützten Samba-Versionen und Linux-Distributionen finden Sie in den Anforderungen.

## <a name="can-i-migrate-previous-file-versions"></a>Können frühere Dateiversionen migriert werden?

Die in Windows Server 2019 enthaltene Version des Storage Migration Service unterstützt nicht die Migration vorheriger Versionen (die mit dem Volumeschattenkopie-Dienst erstellt wurden) von Dateien. Nur die aktuelle Version wird migriert. 

## <a name="optimizing-inventory-and-transfer-performance"></a>Optimieren der Inventur-und Übertragungsleistung

Der Speicher Migrationsdienst enthält eine Multithread-Lese-und-Kopier-Engine, die als Storage Migration Service-Proxy Dienst bezeichnet wird, der sowohl schnell als auch eine perfekte Daten Treue mit vielen Tools zum Kopieren von Dateien enthält. Obwohl die Standardkonfiguration für viele Kunden optimal ist, gibt es Möglichkeiten, die SMS-Leistung während des Inventars und der Übertragung zu verbessern.

- **Verwenden Sie Windows Server 2019 für das Ziel Betriebssystem.** Windows Server 2019 enthält den Proxy Dienst für den Speicher Migrationsdienst. Wenn Sie dieses Feature installieren und zu Windows Server 2019-Zielen migrieren, werden alle Übertragungen als direkte Linie zwischen Quelle und Ziel ausgeführt. Dieser Dienst wird während der Übertragung auf dem Orchestrator ausgeführt, wenn es sich bei den Ziel Computern um Windows Server 2012 R2 oder Windows Server 2016 handelt, was bedeutet, dass der Double-Hop übertragen wird und viel langsamer ist. Wenn mehrere Aufträge mit Windows Server 2012 R2-oder Windows Server 2016-Zielen ausgeführt werden, wird der Orchestrator zu einem Engpass. 

- **Standard Übertragungs Threads ändern.** Der Speicher Migrationsdienst-Proxy Dienst kopiert 8 Dateien gleichzeitig in einem bestimmten Auftrag. Sie können die Anzahl der gleichzeitigen kopierthreads erhöhen, indem Sie den folgenden Registrierungs REG_DWORD Wert für jeden Knoten, auf dem der Storage Migration Service-Proxy ausgeführt wird, in Dezimalform anpassen:

    HKEY_Local_Machine\Software\Microsoft\SMSProxy
    
    Filetransferthreadcount

   Der gültige Bereich liegt zwischen 1 und 128 in Windows Server 2019. Nachdem Sie geändert haben, müssen Sie den Speicher Migrationsdienst-Proxy Dienst auf allen Computern, die Teil einer Migration sind, neu starten. Verwenden Sie diese Einstellung mit Bedacht. Wenn Sie einen höheren Wert festlegen, benötigen Sie möglicherweise zusätzliche Kerne, Speicherleistung und Netzwerkbandbreite. Wenn die Einstellung zu hoch ist, kann dies im Vergleich zu den Standardeinstellungen zu Leistungseinbußen führen.

- **Fügen Sie Kerne und Arbeitsspeicher hinzu.**  Es wird dringend empfohlen, dass auf den Quell-, Orchestrator-und Ziel Computern mindestens zwei Prozessorkerne oder zwei vCPUs vorhanden sind und mehr Inventur-und Übertragungsleistung erheblich unterstützen, insbesondere in Kombination mit filetransferthreadcount (oben). Beim Übertragen von Dateien, die größer sind als die üblichen Office-Formate (Gigabyte oder höher), profitiert die Übertragungsleistung von mehr Arbeitsspeicher als der Standardwert von 2 GB.

- **Erstellen Sie mehrere Aufträge.** Wenn Sie einen Auftrag mit mehreren Server Quellen erstellen, werden die einzelnen Server seriell für Inventur-, Übertragungs-und umerstellungsart kontaktiert. Dies bedeutet, dass jeder Server seine Phase beenden muss, bevor ein anderer Server gestartet wird. Um gleichzeitig weitere Server auszuführen, erstellen Sie einfach mehrere Aufträge, wobei jeder Auftrag nur einen Server enthält. SMS unterstützt bis zu 100 gleichzeitig laufende Aufträge. Dies bedeutet, dass ein einzelner Orchestrator viele Windows Server 2019-Zielcomputer parallelisieren kann. Es wird nicht empfohlen, mehrere parallele Aufträge auszuführen, wenn es sich bei den Ziel Computern um Windows Server 2016 oder Windows Server 2012 R2 handelt, ohne dass der SMS-Proxy Dienst auf dem Ziel ausgeführt wird. der Orchestrator muss alle Übertragungen selbst ausführen und kann zu einem eng. Die Möglichkeit, Server parallel innerhalb eines einzelnen Auftrags auszuführen, ist eine Funktion, die in einer späteren Version von SMS hinzugefügt werden soll.

- **Verwenden Sie SMB 3 mit RDMA-Netzwerken.** Bei der Übertragung von einem Quellcomputer mit Windows Server 2012 oder höher unterstützt SMB 3. x den SMB Direct-Modus und RDMA-Netzwerk. RDMA verschiebt die meisten CPU-Kosten für die Übertragung von den CPUs CPUs zu den NIC-Prozessoren, wodurch die Latenz und die CPU-Auslastung des Servers reduziert Außerdem haben RDMA-Netzwerke wie ROCE und IWarp in der Regel eine wesentlich höhere Bandbreite als typische TCP/Ethernet-Verbindungen, einschließlich der Geschwindigkeit von 25, 50 und 100 GB pro Schnittstelle. Durch die Verwendung von SMB Direct wird die Übertragungsgeschwindigkeit in der Regel vom Netzwerk in den Speicher selbst verlagert.   

- **Verwenden Sie SMB 3 Multichannel.** Bei der Übertragung von einem Quellcomputer mit Windows Server 2012 oder höher unterstützt SMB 3. x Multichannel-Kopien, die die Datei Kopier Leistung erheblich verbessern können. Diese Funktion funktioniert automatisch so lange, wie Quelle und Ziel beide:

   - Mehrere Netzwerkadapter
   - Ein oder mehrere Netzwerkadapter, die die Empfangs seitige Skalierung unterstützen (RSS)
   - Einer von mehreren Netzwerkadaptern, die mithilfe des NIC-Team Vorgangs konfiguriert werden
   - Ein oder mehrere Netzwerkadapter, die RDMA unterstützen

- **Aktualisieren von Treibern.** Installieren Sie ggf. den aktuellen Hersteller Speicher und die Gehäuse Firmware und-Treiber, die neuesten Hersteller-HBA-Treiber, den neuesten Hersteller-BIOS/UEFI-Firmware, die neuesten Netzwerktreiber des Anbieters und die aktuellen Haupt Hersteller-Chipsatz Treiber für Quelle, Ziel und Orchestrator Webserver. Starten Sie die Knoten gegebenenfalls neu. Konfigurieren Sie die Hardware für freigegebenen Speicher und Netzwerk gemäß der Dokumentation des jeweiligen Herstellers.

- **Aktivieren Sie die Verarbeitung mit hoher Leistung.** Stellen Sie sicher, dass die BIOS/UEFI-Einstellungen für Server eine hohe Leistung ermöglichen (z. B. Deaktivieren des C-Status, Festlegen der QPI-Geschwindigkeit, Aktivieren von NUMA und Festlegen der höchsten Speicherfrequenz). Stellen Sie sicher, dass die Energie Verwaltung in Windows Server auf hohe Leistung festgelegt ist. Führen Sie gegebenenfalls einen Neustart aus. Vergessen Sie nicht, diese nach Abschluss der Migration an die entsprechenden Zustände zurückzugeben. 

- **Optimieren der Hardware** Lesen Sie die [Richtlinien zur Leistungsoptimierung für Windows Server 2016](https://docs.microsoft.com/windows-server/administration/performance-tuning/) zur Optimierung von Orchestrator und Ziel Computern unter Windows Server 2019 und Windows Server 2016. Der Abschnitt zur Optimierung der [Leistung des Netzwerk Subsystems](https://docs.microsoft.com/windows-server/networking/technologies/network-subsystem/net-sub-performance-tuning-nics) enthält besonders wertvolle Informationen.

- **Verwenden Sie schnellere Speicherung.** Obwohl es möglicherweise schwierig ist, die Speichergeschwindigkeit des Quell Computers zu aktualisieren, sollten Sie sicherstellen, dass der Zielspeicher bei der e/a-Leistung mindestens so schnell ist, dass die e/a-Leistung der Quelle erreicht ist, um sicherzustellen, dass bei Übertragungen kein unnötiger Engpass vorliegt. Wenn es sich bei dem Ziel um einen virtuellen Computer handelt, stellen Sie sicher, dass es zumindest für die Migration in der schnellsten Speicher Ebene ihrer Hypervisor-Hosts ausgeführt wird, z. b. auf der Flash-Ebene oder mit direkte Speicherplätze HCI-Clustern, die gespiegelte alle Flash-oder Hybrid Bereiche verwenden. Wenn die SMS-Migration fertiggestellt ist, kann der virtuelle Computer auf eine langsamere Ebene oder einen langsameren Host migriert werden.

- **Aktualisieren Sie Antivirus.** Stellen Sie sicher, dass Ihre Quelle und Ihr Ziel die neueste gepatchte Version der Antivirussoftware ausführen, um einen minimalen Leistungs Aufwand Als Test können Sie die Überprüfung von Ordnern, die inventarisiert oder migriert werden, *vorübergehend* auf den Quell-und Ziel Servern ausschließen. Wenn die Übertragungsleistung verbessert wurde, wenden Sie sich an den Hersteller der Antivirussoftware, um Anweisungen oder eine aktualisierte Version der Antivirussoftware oder eine Erläuterung der erwarteten Leistungsminderung zu erhalten

## <a name="can-i-migrate-from-ntfs-to-refs"></a>Kann ich von NTFS zu Refs migrieren?

Die in Windows Server 2019 enthaltene Version des Speicher Migrations Dienstanbieter unterstützt nicht die Migration von NTFS zu Refs-Dateisystemen. Sie können von NTFS zu NTFS und Refs zu Refs migrieren. Dies ist Entwurfs bedingt, da viele Unterschiede in der Funktionalität, den Metadaten und anderen Aspekten bestehen, die refs nicht von NTFS dupliziert. Refs ist als Anwendungs-Arbeits Auslastungs Dateisystem gedacht, nicht als allgemeines Dateisystem. Weitere Informationen finden Sie unter [Übersicht über robuste Dateisysteme (Refs)](../refs/refs-overview.md) . 

## <a name="can-i-move-the-storage-migration-service-database"></a>Kann ich die Datenbank für den Speicher Migrationsdienst verschieben?

Der Speicher Migrationsdienst verwendet eine ESE (Extensible Storage Engine)-Datenbank, die standardmäßig im Ordner "Hidden c:\programdata\microsoft\storagemigrationservice" installiert wird. Diese Datenbank wächst, wenn Aufträge hinzugefügt und Übertragungen abgeschlossen werden, und kann nach der Migration von Millionen von Dateien einen erheblichen Speicherplatz beanspruchen, wenn Sie keine Aufträge löschen. Wenn die Datenbank verschoben werden muss, führen Sie die folgenden Schritte aus:

1. Beendet den Dienst "Storage Migration Service" auf dem Orchestrator-Computer.
2. Besitz des Ordners "`%programdata%/Microsoft/StorageMigrationService`" übernehmen
3. Fügen Sie Ihr Benutzerkonto hinzu, um die vollständige Kontrolle über diese Freigabe und alle Dateien und Unterordner zu haben.
4. Verschieben Sie den Ordner auf ein anderes Laufwerk auf dem Orchestrator-Computer.
5. Legen Sie den folgenden Registrierungs REG_SZ Wert fest:

    HKEY_Local_Machine\Software\Microsoft\SMS DatabasePath = *Pfad zum neuen Daten Bank Ordner auf einem anderen Volume* . 
6. Stellen Sie sicher, dass das System über Vollzugriff auf alle Dateien und Unterordner des Ordners verfügt.
7. Entfernen Sie Ihre eigenen Konten Berechtigungen.
8. Starten Sie den Dienst "Storage Migration Service".

## <a name="give-feedback"></a>Welche Optionen gibt es, um Feedback zu geben, Fehler zu melden oder Support zu erhalten?

So geben Sie Feedback zum Speicher Migrationsdienst an:

- Verwenden Sie das in Windows 10 enthaltene Feedback-Hub-Tool, klicken Sie auf "Feature vorschlagen", und geben Sie die Kategorie "Windows Server" und die Unterkategorie "Speicher Migration" an.
- Verwenden der [Windows Server UserVoice](https://windowsserver.uservoice.com) -Website
- E-Mail-smsfeed@microsoft.com

So melden Sie Fehler:

- Verwenden Sie das in Windows 10 enthaltene Feedback-Hub-Tool, klicken Sie auf "Problem melden", und geben Sie die Kategorie "Windows Server" und die Unterkategorie "Speicher Migration" an.
- Öffnen Sie eine Supportanfrage über [Microsoft-Support](https://support.microsoft.com)

So erhalten Sie Support:

 - Veröffentlichen einer Frage in der [Windows Server Tech Community](https://techcommunity.microsoft.com/t5/Windows-Server/ct-p/Windows-Server)
 - Beitrag im [TechNet-Forum zu Windows Server 2019](https://social.technet.microsoft.com/Forums/en-US/home?forum=ws2019&filter=alltypes&sort=lastpostdesc) 
 - Öffnen Sie eine Supportanfrage über [Microsoft-Support](https://support.microsoft.com)

## <a name="see-also"></a>Siehe auch

- [Übersicht über den Speicher Migrationsdienst](overview.md)
