---
ms.assetid: 02580b2f-a339-4470-947c-d700b2d55f3f
title: Wann sollte eine Verbundserverfarm erstellt werden?
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: fcfc7d640d3688bf0e23557af9bd56082418ef37
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71358940"
---
# <a name="when-to-create-a-federation-server-farm"></a>Wann sollte eine Verbundserverfarm erstellt werden?

Sie sollten eine Verbund Serverfarm in Active Directory-Verbunddienste (AD FS) \(ad FS @ no__t-1 erstellen, wenn Sie über eine größere AD FS Bereitstellung verfügen und Fehlertoleranz, Load @ no__t-2balancing oder Skalierbarkeit für den Verbund Ihrer Organisation bereitstellen möchten. Leistungs. Das Erstellen von zwei oder mehr Verbund Servern im gleichen Netzwerk, das Konfigurieren der einzelnen Server für die Verwendung desselben Verbunddienst und das Hinzufügen des öffentlichen Schlüssels der Token @ no__t-0signing-Zertifikate des einzelnen Servers zum AD FS Management-Snap @ no__t-1In erstellt eine Verbund Serverfarm.  
  
Mithilfe des Konfigurations-Assistenten für AD FS-Verbund Server können Sie eine Verbund Serverfarm erstellen oder zusätzliche Verbund Server in einer vorhandenen Farm installieren. Weitere Informationen finden Sie unter [When to Create a Federation Server](When-to-Create-a-Federation-Server.md).  
  
> [!NOTE]  
> Wenn Sie die Option zum Erstellen einer **neuen Verbund Serverfarm** mithilfe des Konfigurations-Assistenten für AD FS-Verbund Server auswählen, versucht der Assistent, ein Container Objekt \(Für die Freigabe von Zertifikaten @ no__t-2 in Active Directory zu erstellen. Aus diesem Grund ist es wichtig, dass Sie sich zuerst bei dem Computer anmelden, auf dem Sie die Verbundserverrolle einrichten, und zwar mit einem Konto, das über ausreichende Berechtigungen zum Erstellen dieses Containerobjekts in Active Directory verfügt.  
  
Bevor Verbund Server als Farm gruppiert werden können, müssen Sie zuerst gruppiert werden, damit Anforderungen, die bei einem einzelnen voll qualifizierten Domänen Namen \(fqdn @ no__t-1 eintreffen, an die verschiedenen Verbund Server in der Serverfarm weitergeleitet werden. Sie können den Server Cluster erstellen, indem Sie den Netzwerk Lastenausgleich \(nlb @ no__t-1 innerhalb des Unternehmensnetzwerks bereitstellen. In dieser Anleitung wird davon ausgegangen, dass NLB entsprechend konfiguriert wurde, um jeden der Verbund Server in der Farm zu gruppieren.  
  
Weitere Informationen zum Konfigurieren eines Cluster-FQDN mit Microsoft NLB-Technologie finden Sie unter [angeben der Cluster Parameter](https://go.microsoft.com/fwlink/?LinkID=74651).  
  
## <a name="best-practices-for-deploying-a-federation-server-farm"></a>Bewährte Methoden zum Bereitstellen einer Verbundserverfarm  
Wir empfehlen die folgenden bewährten Methoden für die Bereitstellung eines Verbund Servers in einer Produktionsumgebung:  
  
-   Wenn Sie mehrere Verbund Server gleichzeitig bereitstellen oder wissen, dass Sie der Farm über einen Zeitraum weitere Server hinzufügen werden, sollten Sie in Erwägung gezogen werden, ein Server Abbild eines vorhandenen Verbund Servers in der Farm zu erstellen und dann bei Bedarf von diesem Abbild zu installieren. erhöhen Sie schnell zusätzliche Verbund Server.  
  
    > [!NOTE]  
    > Wenn Sie sich für die Bereitstellung zusätzlicher Verbund Server mit der Server Abbild Methode entscheiden, müssen Sie die Aufgaben in [checkliste nicht ausführen: Einrichten eines Verbund Servers @ no__t-0 jedes Mal, wenn Sie der Farm einen neuen Server hinzufügen möchten.  
  
-   Verwenden Sie NLB oder eine andere Form des Clustering, um eine einzelne IP-Adresse für viele Verbund Server Computer zuzuweisen.  
  
-   Reservieren Sie eine statische IP-Adresse für jeden Verbund Server in der Farm, und fügen Sie je nach Domain Name System \(dns @ no__t-1-Konfiguration einen Ausschluss für jede IP-Adresse in das Dynamic Host Configuration-Protokoll \(dhcp @ no__t-3 ein. Microsoft NLB-Technologie erfordert, dass jedem Server, der am NLB-Cluster teilnimmt, eine statische IP-Adresse zugewiesen wird.  
  
-   Wenn die AD FS Konfigurations Datenbank in einer SQL-Datenbank gespeichert wird, sollten Sie die SQL-Datenbank nicht gleichzeitig von mehreren Verbund Servern bearbeiten.  
  
## <a name="configuring-federation-servers-for-a-farm"></a>Konfigurieren von Verbundservern für eine Farm  
In der folgenden Tabelle werden die Aufgaben beschrieben, die durchgeführt werden müssen, damit jeder Verbund Server in eine Umgebung mit einem Server eingebunden werden kann.  
  
|Aufgabe|Beschreibung|  
|--------|---------------|  
|Wenn Sie SQL Server zum Speichern der AD FS-Konfigurationsdatenbank verwenden|Eine Verbund Serverfarm besteht aus zwei oder mehr Verbund Servern, die dieselbe AD FS Konfigurations Datenbank und Token @ no__t-0signing-Zertifikate gemeinsam verwenden. Die Konfigurationsdatenbank kann in jeder internen Windows-Datenbank oder in einer SQL Server-Datenbank gespeichert werden. Wenn Sie beabsichtigen, die Konfigurations Datenbank in einer SQL-Datenbank zu speichern, stellen Sie sicher, dass der Zugriff auf die Konfigurations Datenbank möglich ist, damit von allen neuen Verbund Servern, die an der Farm teilnehmen, auf Sie zugegriffen werden kann. **Hinweis**: Bei Farm Szenarios ist es wichtig, dass sich die Konfigurations Datenbank auf einem Computer befindet, der nicht auch als Verbund Server in der Farm verwendet wird. Microsoft NLB erlaubt den Computern, die an einer Farm teilnehmen, nicht, miteinander zu kommunizieren. **Hinweis**: Stellen Sie sicher, dass die Identität des AD FS AppPools in Internetinformationsdienste \(iis @ no__t-1 @ no__t-2 auf jedem Verbund Server, der an der Farm teilnimmt, über Lesezugriff auf die Konfigurations Datenbank verfügt.|  
|Abrufen und Freigeben von Zertifikaten|Sie können ein einzelnes Server Authentifizierungszertifikat von einer öffentlichen Zertifizierungsstelle abrufen \(ca @ no__t-1 – z. b. VeriSign. Anschließend können Sie das Zertifikat so konfigurieren, dass alle Verbund Server den gleichen privaten Schlüsselteil des Zertifikats gemeinsam verwenden. Weitere Informationen zum Freigeben desselben Zertifikats finden Sie unter [checkliste: Einrichten eines Verbund Servers @ no__t-0. **Hinweis**: Das AD FS-Verwaltungs-Snap @ no__t-0in bezieht sich auf Server Authentifizierungs Zertifikate für Verbund Server als Dienst Kommunikations Zertifikate.<br /><br />Weitere Informationen finden Sie unter [Certificate Requirements for Federation Servers](Certificate-Requirements-for-Federation-Servers.md).|  
|Zeigen auf die gleiche SQL Server-Instanz|Wenn die AD FS Konfigurations Datenbank in einer SQL-Datenbank gespeichert wird, muss der neue Verbund Server auf dieselbe SQL Server Instanz verweisen, die von anderen Verbund Servern in der Farm verwendet wird, damit der neue Server an der Farm teilnehmen kann.|  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
