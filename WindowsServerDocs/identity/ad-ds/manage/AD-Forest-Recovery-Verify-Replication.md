---
title: Wiederherstellung der AD-Gesamtstruktur-Replikation
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server
ms.assetid: 302e522a-fb40-43bc-bc63-83dcc87ebde5
ms.technology: identity-adds
ms.openlocfilehash: f65508bf8973721a09c779a52f708d6a258e2cb5
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71390230"
---
# <a name="resources-to-verify-replication-is-working"></a>Ressourcen zum Überprüfen, ob die Replikation funktioniert 

>Gilt für: Windows Server 2016, Windows Server 2012 und 2012 R2, Windows Server 2008 und 2008 R2

Nachdem Sie alle Domänen Controller wieder hergestellt oder neu installiert haben, können Sie überprüfen, ob AD DS und SYSVOL mithilfe von **repadmin/replsum**, das unter jeder beliebigen Version von Windows Server ausgeführt wird, ordnungsgemäß wieder hergestellt und replizieren.  
  
> [!TIP]
> Sie können auch das [Active Directory-Replikationsstatusmonitor Tool](https://www.microsoft.com/download/details.aspx?id=30005) (adreplstatus) herunterladen und ausführen, ein kostenloses Tool zum Überwachen des Replikations Status von DCS und zum Melden von Fehlern. Adreplstatus erfordert .NET Framework 4, das installiert wird, wenn es nicht bereits vorhanden ist.  

Überprüfen Sie die DFS-Replikation Ereignisanzeige für Ereignis-ID 4602 (oder Datei Replikations Dienst Ereignis-ID 13516), die anzeigt, dass SYSVOL initialisiert wurde.  

Wenn der erste wiederhergestellte Domänen Controller die Ereignis-ID 4614 ("der Domänen Controller wartet auf die anfängliche Replikation) protokolliert. Der replizierte Ordner verbleibt im Status der erst Synchronisierung, bis er mit seinem DFS-Replikation Partner repliziert wurde, und die Ereignis-ID 4602 wird nicht angezeigt, und Sie müssen die folgenden manuellen Schritte ausführen, um SYSVOL wiederherzustellen, wenn es von DFSR  

1. Wenn das DFSR-Ereignis 4612 auf dem ersten wiederhergestellten DC angezeigt wird, führen Sie eine manuelle autorisierende Wiederherstellung durch, wie in [2218556: Erzwingen einer autoritativen und nicht autoritativen Synchronisierung für DFSR-repliziertes SYSVOL (wie "D4/D2" für FRS) ](https://support.microsoft.com/kb/2218556) (https://support.microsoft.com/kb/2218556).  
2. Legen Sie das **sysvolready-Flag** manuell auf 1 fest, wie unter [947022 die Netlogon-Freigabe ist nach der Installation von Active Directory Domain Services auf einem neuen vollständigen oder schreibgeschützten Windows Server 2008-basierten Domänen Controller nicht vorhanden](https://support.microsoft.com/kb/947022).  

Sie können auch einen DFS-Replikation für diagnostische Berichte erstellen. Weitere Informationen finden Sie unter [Erstellen eines Diagnose Berichts für DFS-Replikation](https://technet.microsoft.com/library/cc754227.aspx) und [DFS-Schritt-für-Schritt-Anleitung für Windows Server 2008](https://technet.microsoft.com/library/cc732863\(WS.10\).aspx). Wenn auf dem Server Windows Server 2008 R2 ausgeführt wird, können Sie den [Befehls Zeilenschalter Dfsrdiag. exe replicationstate](http://blogs.technet.com/b/filecab/archive/2009/05/28/dfsrdiag-exe-replicationstate-what-s-dfsr-up-to.aspx)verwenden.  

Sie können den Replikations Test auch mit Dcdiag. exe ausführen, um nach Replikations Fehlern zu suchen. Weitere Informationen finden Sie im Knowledge Base- [Artikel 249256](https://support.microsoft.com/kb/249256).

## <a name="next-steps"></a>Nächste Schritte

- [Wiederherstellung der AD-Gesamtstruktur: Leitfaden](AD-Forest-Recovery-Guide.md)
- [Wiederherstellung der AD-Gesamtstruktur: Verfahren](AD-Forest-Recovery-Procedures.md)
