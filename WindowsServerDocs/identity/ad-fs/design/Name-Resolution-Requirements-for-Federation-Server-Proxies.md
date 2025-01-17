---
ms.assetid: c28c60ff-693d-49ee-a75b-58f24866217b
title: Namensauflösungsanforderungen für Verbundserverproxys
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 51176101b471ec940e2b43a95e1a1a8d37b394f3
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71408061"
---
# <a name="name-resolution-requirements-for-federation-server-proxies"></a>Namensauflösungsanforderungen für Verbundserverproxys

Wenn Client Computer im Internet versuchen, auf eine Anwendung zuzugreifen, die durch Active Directory-Verbunddienste (AD FS) \(ad FS @ no__t-1 gesichert ist, müssen Sie sich zuerst beim Verbund Server authentifizieren. In den meisten Fällen ist der Verbund Server in der Regel nicht direkt über das Internet zugänglich. Daher müssen Internet Client Computer stattdessen an den Verbund Server Proxy umgeleitet werden. Sie können eine erfolgreiche Umleitung erreichen, indem Sie die entsprechenden Domain Name System \(dns @ no__t-1-Einträge zu Ihrer DNS-Zone oder ihren Zonen hinzufügen, die dem Internet überstehen.  
  
Die Methode, die Sie zum Umleiten von Internet Clients an den Verbund Server Proxy verwenden, hängt davon ab, wie Sie die DNS-Zone in Ihrem Umkreis Netzwerk konfigurieren, oder wie Sie eine DNS-Zone konfigurieren, die Sie im Internet steuern. Verbundserverproxys sind zur Verwendung in einem Umkreisnetzwerk vorgesehen. Sie leiten Internet Client Anforderungen nur dann erfolgreich an Verbund Server weiter, wenn DNS in allen von Ihnen kontrollierten Zonen mit Internet @ no__t-0 ordnungsgemäß konfiguriert wurde. Daher ist die Konfiguration Ihrer Zonen mit Internet @ no__t-0– unabhängig davon, ob Sie über eine DNS-Zone verfügen, die nur für das Umkreis Netzwerk oder eine DNS-Zone für das Umkreis Netzwerk und Internet Clients zuständig ist – wichtig.  
  
In diesem Thema werden die Schritte beschrieben, die Sie ausführen können, um die Namensauflösung zu konfigurieren, wenn Sie einen Verbund Server Proxy in Ihrem Umkreis Netzwerk platzieren. Um die erforderlichen Schritte zu bestimmen, ermitteln Sie zunächst, welches der folgenden DNS-Szenarien am ehesten der DNS-Infrastruktur im Umkreisnetzwerk Ihrer Organisation entspricht. Befolgen Sie dann die Schritte für das jeweilige Szenario.  
  
## <a name="dns-zone-serving-only-the-perimeter-network"></a>DNS-Zone nur für das Umkreisnetzwerk  
In diesem Szenario verfügt Ihre Organisation über ein oder zwei DNS-Zonen im Umkreisnetzwerk, ohne dass Ihre Organisation DNS-Zonen im Internet kontrolliert. Die erfolgreiche Namensauflösung für einen Verbund Server Proxy in der DNS-Zone, die nur dem Umkreis Netzwerkszenario dient, hängt von den folgenden Bedingungen ab:  
  
-   Der Verbund Server Proxy muss über eine Einstellung in der Hosts-Datei verfügen, um den voll qualifizierten Domänen Namen \(fqdn @ no__t-1 der Verbund Server-Endpunkt-URL in eine IP-Adresse eines Verbund Servers oder eines Verbund Server Clusters aufzulösen.  
  
-   Das DNS im Umkreis Netzwerk des Konto Partners muss so konfiguriert werden, dass der FQDN der Verbund Server-Endpunkt-URL in die IP-Adresse des Verbund Server Proxys aufgelöst wird.  
  
Die folgende Abbildung und die entsprechenden Schritte veranschaulichen, wie jede dieser Bedingungen für ein gegebenes Beispiel erfüllt wird. In dieser Abbildung bietet die Microsoft-Netzwerk Lastenausgleich-\(nlb @ no__t-1-Technologie einen einzelnen Cluster-voll qualifizierten Namen und eine einzelne Cluster-IP-Adresse für eine vorhandene Verbund Serverfarm.  
  
![namens Anforderungen](media/adfs2_deploy_single_fs.gif)  
  
Weitere Informationen zum Konfigurieren einer Cluster-IP-Adresse oder eines Cluster-voll qualifizierten Daten Controllers mithilfe von NLB finden Sie unter [angeben der Cluster Parameter](https://go.microsoft.com/fwlink/?LinkId=75282).  
  
### <a name="1-configure-the-hosts-file-on-the-federation-server-proxy"></a>1. Konfigurieren der "Hosts"-Datei für den Verbundserverproxy  
Da DNS im Umkreis Netzwerk so konfiguriert ist, dass alle Anforderungen von FS.fabrikam.com an den Konto Verbund Server Proxy aufgelöst werden, verfügt der Verbund Server Proxy des Konto Partners über einen Eintrag in der lokalen Hostdatei, um FS.fabrikam.com in die IP-Adresse des tatsächlicher Konto Verbund Server \(oder Cluster-DNS-Name für die Verbund Serverfarm @ no__t-1, die mit dem Unternehmensnetzwerk verbunden ist. Dies ermöglicht es dem Konto Verbund Server Proxy, den Hostnamen fs.fabrikam.com auf den Konto Verbund Server und nicht in sich selbst zu lösen – wie beim Versuch, FS.fabrikam.com mithilfe des Umkreis-DNS – zu suchen, sodass der Verbund der Server Proxy kann mit dem Verbund Server kommunizieren.  
  
### <a name="2-configure-perimeter-dns"></a>2. Konfigurieren des Umkreis-DNS  
Da es nur einen einzigen AD FS Hostnamen gibt, zu dem Client Computer geleitet werden – ob Sie sich in einem Intranet oder Internet befinden – müssen Client Computer im Internet, die den Umkreis-DNS-Server verwenden, den FQDN für den Konto Verbund Server @no__t -0FS. fabrikam. com @ no__t-1 in die IP-Adresse des Konto Verbund Server Proxys im Umkreis Netzwerk auflösen Damit Clients beim Auflösen von FS.fabrikam.com an den Konto Verbund Server Proxy weiterleiten können, enthält der Umkreis-DNS eine beschränkte Corp.fabrikam.com-DNS-Zone mit einem einzelnen Host \(A @ no__t-1-Ressourcen Daten Satz für FS @no__t -2fS. fabrikam. com @ no__t-3 und die IP-Adresse des Konto Verbund Server Proxys im Umkreis Netzwerk.  
  
Weitere Informationen zum Ändern der Hosts-Datei des Verbund Server Proxys und Konfigurieren von DNS im Umkreis Netzwerk finden Sie unter [Konfigurieren der Namensauflösung für einen Verbund Server Proxy in einer DNS-Zone, die nur dem Umkreis Netzwerk dient](../../ad-fs/deployment/Configure-Name-Resolution-for-a-Federation-Server-Proxy-in-a-DNS-Zone-That-Serves-Only-the-Perimeter-Network.md).  
  
## <a name="dns-zone-serving-both-the-perimeter-network-and-internet-clients"></a>DNS-Zone für das Umkreisnetzwerk und Internetclients  
In diesem Szenario kontrolliert Ihre Organisation die DNS-Zone im Umkreisnetzwerk und mindestens eine DNS-Zone im Internet. Die erfolgreiche Namensauflösung eines Verbund Server Proxys in diesem Szenario hängt von den folgenden Bedingungen ab:  
  
-   DNS in der Internet Zone des Konto Partners muss so konfiguriert werden, dass der FQDN des Verbund Server-Host namens in die IP-Adresse des Verbund Server Proxys im Umkreis Netzwerk aufgelöst wird.  
  
-   Das DNS im Umkreis Netzwerk des Konto Partners muss so konfiguriert werden, dass der FQDN des Verbund Server-Host namens in die IP-Adresse des Verbund Servers im Unternehmensnetzwerk aufgelöst wird.  
  
Die folgende Abbildung und die entsprechenden Schritte veranschaulichen, wie jede dieser Bedingungen für ein gegebenes Beispiel erfüllt wird.  
  
![namens Anforderungen](media/adfs2_deploy_fsp_3DNS.gif)  
  
### <a name="1-configure-perimeter-dns"></a>1. Konfigurieren des Umkreis-DNS  
In diesem Szenario wird davon ausgegangen, dass Sie die Internet-DNS-Zone, die Sie steuern, so konfigurieren, dass Anforderungen, die für eine bestimmte Endpunkt-URL \(, d. h. "FS. fabrikam. com @ no__t-1", an den Verbund Server Proxy im Umkreis Netzwerk aufgelöst werden. Außerdem müssen Sie die Zone im Umkreis-DNS so konfigurieren, dass diese Anforderungen an den Verbund Server im Unternehmensnetzwerk weiterleiten werden.  
  
Damit Clients beim Auflösen von FS.fabrikam.com an den Konto Verbund Server weitergeleitet werden können, wird der Umkreis-DNS mit einem einzelnen Host \(A @ no__t-1-Ressourcen Daten Satz für FS @no__t -2fS. fabrikam. com @ no__t-3 und der IP-Adresse des Konto Verbund Server im Unternehmensnetzwerk. Dies ermöglicht es dem Konto Verbund Server Proxy, den Hostnamen fs.fabrikam.com auf den Konto Verbund Server und nicht in sich selbst zu lösen – wie beim Versuch, FS.fabrikam.com mithilfe von Internet-DNS – zu suchen, sodass der Verbund Server der Proxy kann mit dem Verbund Server kommunizieren.  
  
### <a name="2-configure-internet-dns"></a>2. Konfigurieren von Internet-DNS  
Damit die Namensauflösung in diesem Szenario erfolgreich ist, müssen alle Anforderungen von Clientcomputern im Internet an "fs.fabrikam.com" von der von Ihnen kontrollierten Internet-DNS-Zone aufgelöst werden. Folglich müssen Sie die Internet-DNS-Zone so konfigurieren, dass Client Anforderungen für FS.fabrikam.com an die IP-Adresse des Konto-Verbund Server Proxys im Umkreis Netzwerk weiterleiten werden.  
  
Weitere Informationen zum Ändern des Umkreis Netzwerks und der Internet-DNS-Zonen finden Sie unter [Konfigurieren der Namensauflösung für einen Verbund Server Proxy in einer DNS-Zone, die sowohl das Umkreis Netzwerk als auch Internet Clients bedient](../../ad-fs/deployment/Configure-Name-Resolution-for-a-Federation-Server-Proxy-in-a-DNS-Zone-That-Serves-Both-the-Perimeter-Network-and-Internet-Clients.md).  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
