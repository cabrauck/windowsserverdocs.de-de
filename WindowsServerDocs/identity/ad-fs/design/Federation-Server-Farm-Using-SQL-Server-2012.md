---
ms.assetid: 6618b3ce-0e94-4009-b887-d8e05453358b
title: Verbundserverfarm mit SQL Server
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 358199fd37cdbb320bc8f3e3e5b2900d261986f0
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71359150"
---
# <a name="federation-server-farm-using-sql-server"></a>Verbundserverfarm mit SQL Server

Diese Topologie für Active Directory-Verbunddienste (AD FS) \(AD FS\) unterscheidet sich von der Verbund Serverfarm mithilfe der \(internen\) Windows-Datenbank-wid-Bereitstellungs Topologie darin, dass die Daten nicht in repliziert werden. Alle Verbund Server in der Farm. Stattdessen können alle Verbund Server in der Farm Daten in eine gemeinsame Datenbank lesen und schreiben, die auf einem Server mit Microsoft SQL Server gespeichert ist, der sich im Unternehmensnetzwerk befindet.  
  
## <a name="deployment-considerations"></a>Überlegungen zur Bereitstellung  
In diesem Abschnitt werden verschiedene Überlegungen zu den beabsichtigten Zielgruppen, Vorteilen und Einschränkungen beschrieben, die mit dieser Bereitstellungs Topologie verknüpft sind.  
  
### <a name="who-should-use-this-topology"></a>Wer sollte diese Topologie verwenden?  
  
-   Große Unternehmen mit mehr als 100 Vertrauens Stellungen, die sowohl internen als auch externen Benutzern\- \(SSO\) -Zugriff auf Verbund Anwendungen oder-Dienste bereitstellen müssen  
  
-   Organisationen, die bereits SQL Server verwenden und Ihre vorhandenen Tools und Fachkenntnisse nutzen möchten  
  
### <a name="what-are-the-benefits-of-using-this-topology"></a>Welche Vorteile bietet die Verwendung dieser Topologie?  
  
-   Unterstützung für \(eine größere Anzahl von Vertrauens Stellungen mehr als 100\)  
  
-   Unterstützung für die Erkennung \(von tokenwiedergabe, eine \(Sicherheitsfunktion\) und einen \(artefaktauflösungs Teil des Security Assertion Markup Language SAML\) 2,0-Protokolls\)  
  
-   Unterstützung für die vollständigen Vorteile von SQL Server, z. b. Daten Bank Spiegelung, Failoverclustering, Berichterstellung und Verwaltungs Tools  
  
### <a name="what-are-the-limitations-of-using-this-topology"></a>Welche Einschränkungen gelten für die Verwendung dieser Topologie?  
  
-   Diese Topologie bietet standardmäßig keine Daten Bank Redundanz. Obwohl eine Verbund Serverfarm mit wid-Topologie die wid-Datenbank automatisch auf jedem Verbund Server in der Farm repliziert, enthält die Verbund Serverfarm mit SQL Server Topologie nur eine Kopie der Datenbank.  
  
> [!NOTE]  
> SQL Server unterstützt viele verschiedene Daten-und Anwendungs Redundanz Optionen, einschließlich Failoverclustering, Daten Bank Spiegelung und verschiedene Typen von SQL Server Replikation.  
  
Die \(IT\- \-\) \(-Abteilung der Microsoft Information Technology verwendet SQL Server Daten Bank Spiegelung im synchronen Modus mit hoher Sicherheit und Failoverclustering für hohe\) Verfügbarkeits Unterstützung für die SQL Server-Instanz. SQL Server transaktionaler \(Peer\--\-to\) -Peer-und Mergereplikation wurde nicht vom AD FS-Produktteam bei Microsoft getestet. Weitere Informationen zu SQL Server finden Sie unter [Übersicht über Lösungen mit hoher Verfügbarkeit](https://go.microsoft.com/fwlink/?LinkId=179853) oder [auswählen des geeigneten Replikations Typs](https://go.microsoft.com/fwlink/?LinkId=214648).  
  
### <a name="supported-sql-server-versions"></a>Unterstützte SQL Server Versionen  
Die folgenden SQL Server-Versionen werden mit AD FS unterstützt, die mit Windows Server 2012 installiert werden:  
  
-   SQL Server 2008 \/ R2  
  
-   SQL Server 2012  
  
## <a name="server-placement-and-network-layout-recommendations"></a>Empfehlungen zur Server Platzierung und zum Netzwerk Layout  
Ähnlich der Verbund Serverfarm mit der wid-Topologie sind alle Verbund Server in der Farm so konfiguriert, dass Sie einen Cluster Domain Name System \(DNS\) - \(Namen verwenden, der den Verbunddienst Namen\)darstellt.und eine Cluster-IP-Adresse als Teil der NLB \(\) -Cluster Konfiguration für den Netzwerk Lastenausgleich. Dadurch kann der NLB-Host Client Anforderungen den einzelnen Verbund Servern zuordnen. Verbund Server Proxys können zum Proxy von Client Anforderungen an die Verbund Serverfarm verwendet werden.  
  
In der folgenden Abbildung wird gezeigt, wie das fiktive Unternehmen von Unternehmen in der Verbund Serverfarm mit SQL Server Topologie im Unternehmensnetzwerk bereitgestellt hat. Außerdem wird gezeigt, wie das Unternehmen das Umkreis Netzwerk mit Zugriff auf einen DNS-Server konfiguriert hat, einem zusätzlichen NLB-Host, der denselben DNS-Cluster Namen verwendet @no__t -0FS. "FS... com @ no__t-1", der im NLB-Cluster des Unternehmensnetzwerks verwendet wird, und mit zwei Verbund Servern. Proxys \(sp1 und fsp2 @ no__t-3.  
  
![Serverfarm mit SQL](media/FarmSQLProxies.gif)  
  
Weitere Informationen zum Konfigurieren der Netzwerkumgebung für die Verwendung mit Verbund Servern oder Verbund Server Proxys finden Sie unter Anforderungen für die [Namensauflösung für Verbund Server](Name-Resolution-Requirements-for-Federation-Servers.md) oder [Anforderungen für die Namensauflösung für den Verbund. Server](Name-Resolution-Requirements-for-Federation-Server-Proxies.md)Proxys.  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
