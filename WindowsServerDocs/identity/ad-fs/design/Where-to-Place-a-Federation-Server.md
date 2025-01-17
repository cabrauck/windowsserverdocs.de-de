---
ms.assetid: 935ea7c2-4678-4033-b50f-2036a0359c5d
title: Platzieren eines Verbundservers
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: c64b28f0e62839ff771cd50c0f09b534861cf9e2
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71358778"
---
# <a name="where-to-place-a-federation-server"></a>Platzieren eines Verbundservers

Stellen Sie als bewährte Sicherheitsmaßnahme Active Directory-Verbunddienste (AD FS) \(ad FS @ no__t-1federation-Server vor einer Firewall her, und verbinden Sie Sie mit Ihrem Unternehmensnetzwerk, um eine Gefährdung im Internet zu verhindern. Dies ist wichtig, da Verbund Server über eine vollständige Autorisierung zum Erteilen von Sicherheits Token verfügen. Daher sollten sie den gleichen Schutz wie Domänencontroller haben. Wenn ein Verbund Server kompromittiert ist, kann ein böswilliger Benutzer voll Zugriffs Token für alle Webanwendungen und Verbund Server ausstellen, die durch Active Directory-Verbunddienste (AD FS) \(ad FS @ no__t-1 in allen Ressourcen Partnern geschützt sind. Umstrukturierungen.  
  
> [!NOTE]  
> Aus Sicherheitsgründen sollten Sie vermeiden, dass auf Ihre Verbund Server direkt über das Internet zugegriffen werden kann. Es empfiehlt sich, den Verbund Servern nur dann direkten Internet Zugriff zu gewähren, wenn Sie eine Testumgebung einrichten oder wenn Ihre Organisation über kein Umkreis Netzwerk verfügt.  
  
Bei typischen Unternehmensnetzwerken wird eine Intranetschnittstelle mit der no__t-Verbindung zwischen dem Unternehmensnetzwerk und dem Umkreis Netzwerk eingerichtet, und eine Firewall mit Internet @ no__t-1 wird häufig zwischen dem Umkreis Netzwerk und dem Internet eingerichtet. In diesem Fall befindet sich der Verbund Server innerhalb des Unternehmensnetzwerks und ist nicht direkt für Internet Clients zugänglich.  
  
> [!NOTE]  
> Client Computer, die mit dem Unternehmensnetzwerk verbunden sind, können über die integrierte Windows-Authentifizierung direkt mit dem Verbund Server kommunizieren.  
  
Ein Verbund Server Proxy sollte im Umkreis Netzwerk platziert werden, bevor Sie die Firewallserver für die Verwendung mit AD FS konfigurieren. Weitere Informationen finden Sie unter [Where to Place a Federation Server Proxy](Where-to-Place-a-Federation-Server-Proxy.md).  
  
## <a name="configuring-your-firewall-servers-for-a-federation-server"></a>Konfigurieren der Firewallserver für einen Verbundserver  
Damit die Verbund Server direkt mit Verbund Server Proxys kommunizieren können, muss der Intranetfirewallserver so konfiguriert werden, dass er Secure Hypertext Transfer Protocol \(https @ no__t-1-Datenverkehr vom Verbund Server Proxy zum Verbund Server. Dies ist eine Anforderung, da der Intranetfirewallserver den Verbund Server mithilfe von Port 443 veröffentlichen muss, damit der Verbund Server Proxy im Umkreis Netzwerk auf den Verbund Server zugreifen kann.  
  
Darüber hinaus verwendet der Firewallserver mit Intranetzugriff mit der no__t-Verbindung, z. b. ein Server, auf dem Internet Security und Acceleration \(ISA @ no__t-2 Server ausgeführt wird, einen als Server Veröffentlichung bezeichneten Prozess, um Internet Client Anforderungen an das entsprechende Unternehmen zu verteilen. Verbund Server. Dies bedeutet, dass Sie manuell eine Server Veröffentlichungs Regel auf dem Intranetserver mit ISA Server erstellen müssen, der die gruppierte Verbund Server-URL veröffentlicht, z. b. http: @no__t -0\/FS.fabrikam.com.  
  
Weitere Informationen zum Konfigurieren der Serververöffentlichung in einem Umkreisnetzwerk finden Sie unter [Where to Place a Federation Server Proxy](Where-to-Place-a-Federation-Server-Proxy.md). Informationen zum Konfigurieren von ISA Server zum Veröffentlichen eines Servers finden Sie unter [Erstellen einer sicheren Webpublishing Regel](https://go.microsoft.com/fwlink/?LinkId=75182).  
  
## <a name="see-also"></a>Siehe auch
[AD FS-Entwurfshandbuch in Windows Server 2012](AD-FS-Design-Guide-in-Windows-Server-2012.md)
