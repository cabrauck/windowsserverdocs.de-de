---
title: Überwachen der Aktivitäten und des Status von verbundenen Remoteclients
description: Dieses Thema ist Teil des Leitfadens für die Remote Zugriffs Überwachung und-Kontoführung in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: beb94475-b21f-46a9-ac51-bf2bb28ca94e
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 03d87fb086a9f2797af8399be3d833b11bed79a5
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71367258"
---
# <a name="monitor-connected-remote-clients-for-activity-and-status"></a>Überwachen der Aktivitäten und des Status von verbundenen Remoteclients

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

**Hinweis**: Windows Server 2012 kombiniert DirectAccess und RAS-Dienst (RAS) zu einer einzigen Remote Zugriffs Rolle.  
  
Sie können die-Verwaltungskonsole auf dem Remote Zugriffs Server verwenden, um die Remote Client Aktivität und den Status zu überwachen.  
  
> [!NOTE]  
> Sie müssen auf jedem Computer als Mitglied der Gruppe "Domänen-Admins" oder "Administratoren" angemeldet sein, um die in diesem Thema beschriebenen Aufgaben ausführen zu können. Wenn Sie eine Aufgabe nicht ausführen können, während Sie mit einem Konto angemeldet sind, das Mitglied der Gruppe "Administratoren" ist, versuchen Sie, die Aufgabe auszuführen, während Sie mit einem Konto angemeldet sind, das Mitglied der Gruppe "Domänen-Admins" ist.  
  
#### <a name="to-monitor-remote-client-activity-and-status"></a>So überwachen Sie die Remote Client Aktivität und den Status  
  
1.  Klicken Sie im **Server Manager** auf **Tools** und dann auf **Remotezugriffsverwaltung**.  
  
2.  Klicken Sie auf **Berichterstattung** , um in der **Remote Zugriffs-Verwaltungskonsole**zur **Remote Zugriffs Berichterstattung** zu navigieren.  
  
3.  Klicken Sie auf **Remote Client Status** , um in der **Remote Zugriffs-Verwaltungskonsole**in der Remote Zugriffs-Verwaltungskonsole zur Remote Client Aktivität und zur Benutzeroberfläche  
  
4.  Es wird eine Liste der Benutzer angezeigt, die mit dem RAS-Server verbunden sind, sowie ausführliche Statistiken zu diesen. Klicken Sie auf die erste Zeile in der Liste, die einem Client entspricht. Wenn Sie eine Zeile auswählen, wird die Remote Benutzeraktivität im Vorschaubereich angezeigt.  
  
](../../../media/Monitor-connected-remote-clients-for-activity-and-status/PowerShellLogoSmall.gif)***<em>äquivalente Windows PowerShell-Befehle</em> mit @no__t 0shell***  
  
Die folgenden Windows PowerShell-Cmdlets erfüllen dieselbe Funktion wie das vorhergehende Verfahren. Geben Sie die einzelnen Cmdlets in einer einzelnen Zeile ein, auch wenn es den Anschein hat, dass aufgrund von Formatierungseinschränkungen Zeilenumbrüche vorhanden sind.  
  
```  
PS> Get-RemoteAccessConnectionStatistics  
```  
  
Die Benutzerstatistiken können mithilfe der Felder in der folgenden Tabelle gefiltert werden, basierend auf der Kriterienauswahl.  
  
|Feldname|Wert|  
|-------|-----|  
|Benutzername|Der Benutzername oder das Alias des Remotebenutzers. Platzhalter Zeichen können verwendet werden, um eine Gruppe von Benutzern auszuwählen, z. b. "no__t-0 *" oder "\* \ Administrator".|  
|Hostname|Der Name des Computerkontos des Remotebenutzers. Außerdem kann eine IPv4-oder IPv6-Adresse angegeben werden.|  
|Typ|DirectAccess oder VPN. Wenn DirectAccess ausgewählt ist, werden alle Remote Benutzer, die über DirectAccess verbunden sind, aufgeführt. Wenn VPN ausgewählt wird, werden alle Remote Benutzer aufgelistet, die über VPN verbunden sind.|  
|ISP-Adresse|Die IPv4- oder IPv6-Adresse des Remotebenutzers.|  
|IPv4-Adresse|Die innere IPv4-Adresse des Tunnels, der den Remote Benutzer mit dem Unternehmensnetzwerk verbindet.|  
|IPv6-Adresse|Die interne IPv6-Adresse des Tunnels, über den der Remotebenutzer mit dem Unternehmensnetzwerk verbunden ist.|  
|Protokoll//Tunnel|Die Übergangstechnologie, die vom Remote Client verwendet wird. Dies ist Teredo, 6de4 oder IP-HTTPS für DirectAccess-Benutzer, und es ist PPTP, L2TP, SSTP oder IKEv2 für VPN-Benutzer.|  
|Aufgerufene Ressource|Alle Benutzer, die auf eine bestimmte Unternehmensressource oder einen bestimmten Unternehmensendpunkt zugreifen. Der Wert, der diesem Feld entspricht, ist der Hostname/die IP-Adresse des Servers.|  
|Server|Der RAS-Server, mit dem Clients verbunden sind. Dies ist nur für Clusterbereitstellungen und Bereitstellungen für mehrere Standorte relevant.|  
  
  
  


