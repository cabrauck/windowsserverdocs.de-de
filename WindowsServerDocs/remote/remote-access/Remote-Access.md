---
title: Remotezugriff
description: Dieses Thema enthält eine Übersicht über die Remote Zugriffs-Server Rolle in Windows Server 2016.
manager: dougkim
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.assetid: eeca4cf7-90f0-485d-843c-76c5885c54b0
ms.author: pashort
author: shortpatti
ms.date: 05/18/2018
ms.openlocfilehash: d2fa9c82c4cab05b2a60916fee3f09c1ea48a472
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71388906"
---
# <a name="remote-access"></a>Remotezugriff

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows 10

Im Handbuch für den Remote Zugriff erhalten Sie eine Übersicht über die RAS-Server Rolle in Windows Server 2016 und die folgenden Themen:

- [Always on VPN-Bereitstellungs Handbuch](vpn/always-on-vpn/deploy/always-on-vpn-deploy.md)
- [Border Gateway Protocol &#40;BGP&#41;](bgp/Border-Gateway-Protocol-BGP.md)
- [RAS-Gateway](ras-gateway/RAS-Gateway.md) 
- [RAS-Serverrolle: Dokumentation](ras/Remote-Access-Server-Role-Documentation.md)
- [RAS-Gateway für SDN](../../networking/sdn/technologies/network-function-virtualization/RAS-Gateway-for-SDN.md)
- [Virtual Private Networking (VPN)](vpn/vpn-top.md)
 
Weitere Informationen zu anderen Netzwerktechnologien finden Sie unter [Netzwerk in Windows Server 2016](https://docs.microsoft.com/windows-server/networking/networking).

Die Remote Zugriffs-Server Rolle ist eine logische Gruppierung dieser verwandten Netzwerk Zugriffs Technologien: [RAS-Dienst (RAS)](#bkmk_da), [Routing](#bkmk_rras)und [webanwendungsproxy](#bkmk_proxy). Diese Technologien sind die *Rollendienste* der Serverrolle "Remotezugriff". Wenn Sie die Remote Zugriffs-Server Rolle mit dem **Assistenten zum Hinzufügen von Rollen und Features** oder mit Windows PowerShell installieren, können Sie einen oder mehrere dieser drei Rollen Dienste installieren.

>[!IMPORTANT]
>Versuchen Sie nicht, den Remote Zugriff auf einem virtuellen Computer \(vm @ no__t-1 in Microsoft Azure bereitzustellen. Die Verwendung des Remote Zugriffs in Microsoft Azure wird nicht unterstützt. Sie können den Remote Zugriff auf einem virtuellen Azure-Computer nicht verwenden, um VPN, DirectAccess oder andere Remote Zugriffs Funktionen in Windows Server 2016 oder früheren Versionen von Windows Server bereitzustellen. Weitere Informationen finden Sie [unter Microsoft Server Software Support for Microsoft Azure Virtual Machines](https://support.microsoft.com/help/2721672/microsoft-server-software-support-for-microsoft-azure-virtual-machines).

## <a name="bkmk_da"></a>RAS-Dienst \(ras @ no__t-2-RAS-Gateway

Wenn Sie den **DirectAccess-und VPN-Rollen Dienst (RAS)** installieren, stellen Sie das RAS-Gateway für den Remote Zugriff \(**RAS-Gateway**\) bereit. Sie können das RAS-Gateway als virtuelles privates Netzwerk für das RAS-Gateway \(vpn @ no__t-1 Server, einen mehr Instanzen fähigen RAS-Gateway-VPN-Server und als DirectAccess-Server bereitstellen.

- **RAS-Gateway: einzelner**Mandant. Mithilfe des RAS-Gateways können Sie VPN-Verbindungen bereitstellen, um Endbenutzern Remote Zugriff auf das Netzwerk und die Ressourcen Ihrer Organisation zu bieten. Wenn auf Ihren Clients Windows 10 ausgeführt wird, können Sie Always on VPN bereitstellen, das immer dann eine permanente Verbindung zwischen Clients und Ihrem Organisations Netzwerk unterhält, wenn Remote Computer mit dem Internet verbunden sind. Mit dem RAS-Gateway können Sie auch eine Site-to-Site-VPN-Verbindung zwischen zwei Servern an unterschiedlichen Standorten erstellen, z. b. zwischen Ihrer primären Niederlassung und einer Zweigstelle, und die Netzwerk Adressübersetzung \(nat @ no__t-1 verwenden, damit Benutzer im Netzwerk Zugreifen auf externe Ressourcen, z. b. das Internet. Außerdem unterstützt das RAS-Gateway Border Gateway Protocol (BGP), das dynamische Routing Dienste bereitstellt, wenn Ihre Remote Niederlassungen auch Edge-Gateways aufweisen, die BGP unterstützen.

- **RAS-Gateway: mehr**Instanzen fähig. Wenn Sie die Hyper @ no__t-0V-Netzwerkvirtualisierung verwenden oder VM-Netzwerke mit virtuellen lokalen Netzwerken \(vlans @ no__t-2 bereitgestellt werden, können Sie das RAS-Gateway als mehrinstanzfähiges, softwarebasiertes Edge-Gateway und Router bereitstellen. Mit dem RAS-Gateway können clouddienstanbieter \(csps @ no__t-1 und Unternehmen das Routing von Daten Center-und cloudnetzwerkdatenverkehr zwischen virtuellen und physischen Netzwerken (einschließlich Internet) aktivieren. Mit dem RAS-Gateway können Ihre Mandanten Punkt-Standort-Standort-VPN-Verbindungen verwenden, um von überall aus auf Ihre VM-Netzwerkressourcen im Rechenzentrum zuzugreifen. Sie können Mandanten auch Standort-zu-Standort-VPN-Verbindungen zwischen ihren Remote Standorten und Ihrem CSP-Rechenzentrum bereitstellen. Darüber hinaus können Sie das RAS-Gateway mit BGP für dynamisches Routing konfigurieren, und Sie können die Netzwerk Adressübersetzung \(nat @ no__t-1 aktivieren, um den Internet Zugriff für virtuelle Computer in VM-Netzwerken bereitzustellen.

>[!IMPORTANT]
> Das RAS-Gateway mit mehr Instanzen fähigen Funktionen ist auch in Windows Server 2012 R2 verfügbar.

- **Always on-VPN**. Always on-VPN ermöglicht Remote Benutzern den sicheren Zugriff auf freigegebene Ressourcen, Intranetwebsites und Anwendungen in einem internen Netzwerk, ohne eine Verbindung mit einem VPN herzustellen. 

Weitere Informationen finden Sie unter [RAS-Gateway](ras-gateway/RAS-Gateway.md) und [Border Gateway Protocol (BGP)](bgp/Border-Gateway-Protocol-BGP.md).

## <a name="bkmk_rras"></a>Routing

Sie können den Remote Zugriff verwenden, um Netzwerk Datenverkehr zwischen Subnetzen in Ihrem lokalen Netzwerk weiterzuleiten. Das Routing bietet Unterstützung für NAT-Router (Netzwerk Adressübersetzung), LAN-Router mit BGP, Routing Information Protocol (RIP) und Multicast fähige Router unter Verwendung von IGMP (Internet Group Management Protocol). Als Router mit vollem Funktionsumfang können Sie RAS entweder auf einem Server Computer oder als virtueller Computer (VM) auf einem Computer bereitstellen, auf dem Hyper-V ausgeführt wird.

Verwenden Sie zum Installieren des Remote Zugriffs als LAN-Router entweder den Assistenten zum Hinzufügen von Rollen und Features in Server-Manager, und wählen Sie die **Remote Zugriffs** -Server Rolle und den **Routing** Rollen Dienst aus. oder geben Sie den folgenden Befehl an einer Windows PowerShell-Eingabeaufforderung ein, und drücken Sie dann die EINGABETASTE.

```  
Install-RemoteAccess -VpnType RoutingOnly
```  

## <a name="bkmk_proxy"></a>Webanwendungs Proxy

Der webanwendungsproxy ist ein Remote Zugriffs-Rollen Dienst in Windows Server 2016. Der Webanwendungsproxy bietet Reverseproxyfunktionen für Webanwendungen in Ihrem Unternehmensnetzwerk, damit Benutzer außerhalb des Unternehmensnetzwerks von allen Geräten auf die Anwendungen zugreifen können. Der webanwendungsproxy authentifiziert den Zugriff auf Webanwendungen mit Active Directory-Verbunddienste (AD FS) (AD FS) und fungiert auch als AD FS Proxy.

Verwenden Sie zum Installieren des Remote Zugriffs als webanwendungsproxy den Assistenten zum Hinzufügen von Rollen und Features in Server-Manager, und wählen Sie **die Server Rolle** RAS und den **webanwendungsproxy** -Rollen Dienst aus. oder geben Sie den folgenden Befehl an einer Windows PowerShell-Eingabeaufforderung ein, und drücken Sie dann die EINGABETASTE.  

```  
Install-RemoteAccess -VpnType SstpProxy  
```  

Weitere Informationen finden Sie unter [webanwendungsproxy](https://technet.microsoft.com/windows-server-docs/identity/web-application-proxy/web-application-proxy-windows-server).


---