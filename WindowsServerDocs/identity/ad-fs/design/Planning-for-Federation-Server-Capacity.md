---
ms.assetid: 7013fc21-9ced-4f9d-9588-cb04d6d60924
title: Planen der Verbundserverkapazität
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 418bc5d53a2bd11afa8563b07bbff76c89495715
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407977"
---
# <a name="planning-for-federation-server-capacity"></a>Planen der Verbundserverkapazität

Die Kapazitätsplanung für Verbund Server unterstützt Sie beim schätzen:  
  
-   Welche Faktoren die Größe der AD FS Konfigurations Datenbank vergrößern.  
  
-   Die erforderlichen Hardwareanforderungen für die einzelnen Verbund Server.  
  
-   Die Anzahl der Verbund Server, die in jeder Organisation platziert werden sollen.  
  
Verbund Server geben Sicherheits Token für Benutzer aus. Diese Token werden einer vertrauenden Seite für die Nutzung angezeigt. Verbund Server geben Sicherheits Token nach der Authentifizierung eines Benutzers oder nach dem Empfang eines Sicherheits Tokens aus, das zuvor von einem Partner Verbunddienst ausgestellt wurde. Ein-Sicherheits Token wird von einem Verbunddienst angefordert, wenn sich die Benutzer anfänglich bei Verbund Anwendungen anmelden oder wenn Ihre Sicherheits Token ablaufen, während Sie auf Verbund Anwendungen zugreifen.  
  
Verbund Server sind so konzipiert, dass Sie High @ no__t-Serverfarm Konfigurationen unterstützen, die den Microsoft-Netzwerk Lastenausgleich \(nlb @ no__t-2-Technologie verwenden. Verbund Server in einer Farm Konfiguration können Anforderungen unabhängig voneinander bedienen, ohne für jede Anforderung auf allgemeine Farm Komponenten zugreifen zu müssen. Daher ist der Aufwand für das horizontale hochskalieren einer Verbund Server Bereitstellung geringfügig.  
  
**Empfehlungen**  
  
-   Für die Bereitstellung von Unternehmens @ no__t-0critical oder High @ no__t-1 Availability empfiehlt es sich, in jeder Partnerorganisation eine kleine Verbund Serverfarm mit mindestens zwei Verbund Servern pro Farm zu erstellen, um Fehlertoleranz bereitzustellen.  
  
-   Mit dem Bedarf an Hochverfügbarkeit und der Erleichterung der horizontalen Skalierung von Verbund Servern ist das horizontale hochskalieren die empfohlene Methode für die Verarbeitung einer hohen Anzahl von Anforderungen pro Sekunde für eine bestimmte Verbunddienst. Das horizontale hochskalieren über die Basiskonfiguration in diesem Handbuch hinaus führt wahrscheinlich nicht zu erheblichen Leistungssteigerungen.  
  
## <a name="ad-fs-configuration-database-size-and-growth"></a>Größe und Wachstum der AD FS-Konfigurations Datenbank  
Die Größe der AD FS Konfigurations Datenbank wird in der Regel als klein betrachtet, und die Datenbankgröße ist in AD FS Bereitstellungen tendenziell kein wichtiger Faktor.  Die genaue Größe der AD FS Konfigurations Datenbank kann größtenteils von der Anzahl der Vertrauens Stellungen und den zugeordneten –-bezogenen no__t-Metadaten wie z. b. Ansprüchen, Anspruchs Regeln und Überwachungs Einstellungen abhängen, die für jede Vertrauensstellung konfiguriert sind. Wenn die Anzahl von Vertrauens Einträgen in der Konfigurations Datenbank zunimmt, ist es daher erforderlich, mehr Speicherplatz zu benötigen.  
  
Weitere Informationen zur Bereitstellung der AD FS Konfigurations Datenbank finden Sie unter [Überlegungen zur AD FS Bereitstellungs Topologie](AD-FS-Deployment-Topology-Considerations.md).  
  
## <a name="memory-cpu-and-disk-space-requirements"></a>Speicher-, CPU-und Speicherplatzanforderungen  
Glücklicherweise sind Arbeitsspeicher-, CPU-und Speicherplatzanforderungen für Verbund Server gering, und Sie sind wahrscheinlich kein Fahr Faktor bei den Hardware Entscheidungen. Weitere Informationen zu Hardwareanforderungen finden Sie unter [anhang A: Überprüfen der AD FS Anforderungen @ no__t-0.  
  
> [!NOTE]  
> In Tests, die vom AD FS-Produktteam mithilfe einer Verbund Serverfarm ausgeführt wurden, die mit einem dedizierten SQL Server zum Speichern der AD FS Konfigurations Datenbank konfiguriert wurde, war die Gesamtlast auf dem SQL Server tendenziell gering. In einem Test, der eine vier @ no__t-0federation @ no__t-1 Server-Farm verwendet, die für die Verwendung eines einzelnen SQL Server konfiguriert war, hat die CPU-Auslastung trotz der Tests, bei denen die Verbund Server zur Ziel Auslastung geführt haben, 10% nicht überschritten.  
  
## <a name="bk_estimatefs"></a>Schätzen Sie die Anzahl der Verbund Server für Ihre Organisation.  
Um den Hardware Planungsprozess für Verbund Server zu optimieren, hat das AD FS-Produktteam das Arbeitsblatt für die Größenanpassung AD FS Kapazitätsplanung entwickelt. Dieses Excel-Arbeitsblatt enthält die Funktion "Calculator @ no__t-0like", die erwartete Verwendungs Daten verwendet, die Sie für Benutzer in Ihrer Organisation bereitstellen, und eine empfohlene optimale Anzahl von Verbund Servern für Ihre AD FS Produktionsumgebung zurückgeben.  
  
> [!NOTE]  
> Die Anzahl der Verbund Server, die von diesem Arbeitsblatt empfohlen werden, basiert auf den Hardware-und Netzwerk Spezifikationen, die das AD FS Produktteam während des Tests verwendet hat. Daher muss die Anzahl der Verbund Server, die für die Kalkulations Tabelle empfohlen werden, innerhalb dieses Kontexts verstanden werden.  Weitere Informationen zu den während des Tests verwendeten Spezifikationen finden Sie im Thema [Planning for AD FS Server Capacity](Planning-for-AD-FS-Server-Capacity.md).  
  
### <a name="using-the-ad-fs-capacity-planning-sizing-spreadsheet"></a>Verwenden des Arbeitsblatts zur Größenanpassung von AD FS Capacity Planning  
Wenn Sie dieses Arbeitsblatt verwenden, müssen Sie einen Wert \(entweder **40%** , **60%** oder **80%** \) auswählen, der den Prozentsatz der Gesamtzahl der Benutzer angibt, die von Ihnen erwartet werden, dass Authentifizierungsanforderungen an Ihre Verbund Server gesendet werden. Spitzen Nutzungs Zeiträume.  
  
Anschließend müssen Sie einen Wert \(entweder **1 Minute**, **15 Minuten**oder **1 Stunde**\) auswählen, der die Zeitspanne angibt, für die Sie den Zeitraum der Spitzen Auslastung erwarten. Beispielsweise können Sie 40% als Wert für die Gesamtzahl der Benutzer schätzen, die sich innerhalb eines Zeitraums von 15 Minuten anmelden werden, oder dass sich 60% der Benutzer innerhalb eines Zeitraums von 1 Stunde anmelden. Mit diesen Werten wird das Spitzenlast Profil definiert, mit dem ihre Größen Änderungs Empfehlung berechnet wird.  
  
Als nächstes müssen Sie die Gesamtzahl der Benutzer angeben, die für den Zugriff auf die Zielanwendung @ no__t-1aware-Anwendung das einmalige Zeichen @ no__t-0benötigen, je nachdem, ob die Benutzer folgende Aktionen ausführen:  
  
-   Anmelden bei Active Directory von einem lokalen Computer, der physisch mit dem Unternehmensnetzwerk verbunden ist \(über die integrierte Windows-Authentifizierung @ no__t-1  
  
-   Remote Anmeldung bei Active Directory von einem Computer, der nicht physisch mit dem Unternehmensnetzwerk verbunden ist \(über die integrierte Windows-Authentifizierung oder Benutzername und Kennwort @ no__t-1  
  
-   Aus einer anderen Organisation und versuchen, von einem vertrauenswürdigen Partner auf die Ziel Ansprüche @ no__t 0aware-Anwendung zuzugreifen.  
  
-   Von einem SAML 2,0-Identitäts Anbieter und versuchen, auf die Ziel Ansprüche @ no__t-abhängige Anwendung zuzugreifen  
  
#### <a name="how-to-use-this-spreadsheet"></a>Verwenden dieses Arbeitsblatts  
Sie können die folgenden Schritte für jede Instanz der Verbund Serverfarm verwenden, die Sie bereitstellen möchten, um die empfohlene Anzahl von Verbund Servern zu ermitteln.  
  
1.  Laden Sie das Arbeitsblatt zur [Größenanpassung von AD FS Kapazitätsplanung für Windows Server 2012 R2](https://adfsdocs.blob.core.windows.net/adfs/ADFSCapacityPlanning.xlsx) oder das Arbeitsblatt [für die Größenanpassung AD FS Kapazitätsplanung für Windows Server 2016](https://adfsdocs.blob.core.windows.net/adfs/ADFSCapacity2016.xlsx)herunter.
  
2.  In der Zelle auf der rechten Seite des **Zeitraums während des Spitzen Zeitraums für die System Auslastung erwarte ich, dass der Prozentsatz der Benutzer die Zelle authentifiziert** , auf die Zelle und dann auf die Pfeile mit dem Drop @ no__t-1-Down-Wert, um die geschätzte System Auslastung auszuwählen, entweder **40%** , **60%** oder **80%** für die Bereitstellung.  
  
3.  Klicken Sie in der Zelle rechts neben der Zelle in **der folgenden** Zelle auf die Zelle, und verwenden Sie dann die Pfeile Drop @ no__t-1down, um entweder **eine Minute**, **15 Minuten**oder **eine Stunde** auszuwählen, um die Dauer der Spitzenlast auszuwählen.  
  
4.  Geben Sie in der Zelle rechts neben der Zelle " **geschätzte Anzahl interner Anwendungen \(, z. b. SharePoint \(2007 oder 2010 @ no__t-3 oder Ansprüche unterstützende Webanwendungen @ no__t-4** " die Anzahl der internen Anwendungen ein, die Sie in Ihrem Ordnung.  
  
5.  Geben Sie in der Zelle rechts neben der Zelle **geschätzte Anzahl von Online-Anwendungen \(, z. b. Office 365 Exchange Online, SharePoint Online oder lync Online @ no__t-2** die Anzahl von Online Anwendungen oder-Diensten ein, die Sie in Ihrer Organisation verwenden.  
  
6.  Geben Sie in der Zelle mit der Bezeichnung **Anzahl von Benutzern**eine Zahl für jede Zeile ein, die für ein Beispiel Anwendungsszenario gilt, das für Ihre Benutzer das einmalige Anmelden (Single Sign, no__t-1On Access) benötigt wird. Diese Spalte sollte die Anzahl der definierten Benutzer, nicht die Spitzen Benutzer pro Sekunde enthalten. Wenn die Anwendung auf die Anwendung zugreifen muss, müssen Sie zunächst die Seite "Startbereichs Ermittlung **" eingeben.** Wenn Sie sich nicht sicher sind, geben Sie **Y**ein.  
  
7.  Überprüfen Sie die folgenden empfohlenen Werte:  
  
    1.  Die Gesamtanzahl der empfohlenen Verbund Server finden Sie in der unteren rechten Zelle, die grau hervorgehoben ist.  
  
    2.  Die Anzahl der für die einzelnen Beispiel Anwendungsszenarien empfohlenen Server finden Sie in der Zelle in der Zeile, die in grau hervorgehoben ist.  
  
> [!NOTE]  
> Der Wert, der automatisch in der Zelle rechts von der Zelle mit dem Titel **Gesamtzahl der Verbund Server** , die unten in der Kalkulations Tabelle empfohlen wird, berechnet wird, enthält eine Formel, mit der der Gesamtsumme aller Werte in den einzelnen vorangehenden Zeilen. Die Formel, die der **Gesamtzahl der empfohlenen Verbund Server** hinzugefügt wird, wird in diesem Puffer auf die insgesamt empfohlene Anzahl bereitgestellter Verbund Server hochskaliert, um es sehr unwahrscheinlich zu machen, dass die Gesamtlast für die Farm jemals den Sättigungspunkt erreichen wird.  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
