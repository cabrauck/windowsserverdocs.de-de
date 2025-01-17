---
title: Problembehandlung für Einstellungen für Einstiegspunkte und Domänencontroller
description: Dieses Thema ist Teil des Handbuchs Bereitstellen mehrerer Remote Zugriffs Server in einer Bereitstellung mit mehreren Standorten in Windows Server 2016.
manager: brianlic
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: networking-ras
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: b12dd0e8-1d80-4d4b-bb45-586f19d17ef0
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 10a0f7952fc27d0185d4383da21f0614885ddac3
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71367046"
---
# <a name="troubleshooting-setting-the-entry-point-domain-controller"></a>Problembehandlung für Einstellungen für Einstiegspunkte und Domänencontroller

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Dieses Thema enthält Informationen zum Beheben von Problemen mit dem Befehl `Set-DAEntryPointDC`. Überprüfen Sie, ob das Windows-Ereignisprotokoll ein Ereignis mit der ID 10065 enthält, um sicherzustellen, dass der Fehler mit den Einstellungen für Einstiegspunkte und Domänencontroller zusammenhängt.  
  
## <a name="SaveGPOSettings"></a>Server-GPO-Einstellungen werden gespeichert  
Der **Fehler wurde empfangen**. Fehler beim Speichern der Remote Zugriffs Einstellungen auf dem GPO-< GPO_name >.  
  
Informationen zum Beheben dieses Fehlers finden Sie unter Speichern von Server-GPO-Einstellungen.  
  
## <a name="remote-access-is-not-configured"></a>Nicht konfigurierter Remotezugriff  
Der **Fehler wurde empfangen**. Der Remote Zugriff ist auf < Servername-> nicht konfiguriert. Geben Sie den Namen eines Servers an, der zu einer Bereitstellung für mehrere Standorte gehört.  
  
oder  
  
Der Remote Zugriff ist auf dem Server < Servername-> nicht konfiguriert. Geben Sie einen Computer an, auf dem DirectAccess aktiviert ist.  
  
**Ursache**  
  
Remotezugriff ist auf dem mit dem *ComputerName*-Parameter angegebenen Computer nicht konfiguriert.  
  
Das Cmdlet `Set-DaEntryPointDC` ist nur auf Servern verfügbar, die zu einer konfigurierten Bereitstellung für mehrere Standorte gehören.  
  
**Lösung**  
  
Führen Sie den Befehl aus, und geben Sie im *ComputerName*-Parameter den Namen des Servers an, der bereits als Teil der Bereitstellung für mehrere Standorte konfiguriert ist.  
  
## <a name="multisite-is-not-enabled"></a>Bereitstellung für mehrere Standorte ist nicht aktiviert  
Der **Fehler wurde empfangen**. Sie müssen eine Bereitstellung für mehrere Standorte aktivieren, bevor Sie diesen Vorgang ausführen. Verwenden Sie hierzu das Cmdlet `Enable-DAMultiSite`.  
  
**Ursache**  
  
Die Funktionen für mehrere Standorte sind auf dem Server, der durch den Parameter *ComputerName* angegeben wird, nicht aktiviert.  
  
Das Cmdlet `Set-DaEntryPointDC` ist nur auf Servern verfügbar, die zu einer konfigurierten Bereitstellung für mehrere Standorte gehören.  
  
**Lösung**  
  
Führen Sie den Befehl aus, und geben Sie im *ComputerName*-Parameter den Namen des Servers an, der bereits als Teil der Bereitstellung für mehrere Standorte konfiguriert ist.  
  
## <a name="entry-point-and-domain-controller-not-provided-in-cmdlet"></a>Einstiegspunkt und Domänencontroller wurden nicht im Cmdlet angegeben  
Das Cmdlet `Set-DaEntryPointDC` bietet Ihnen die Möglichkeit, den zugeordneten Domänencontroller für verschiedene Einstiegspunkte zu ändern, z. B. wenn ein bestimmter Domänencontroller nicht mehr verfügbar ist. Sie können einen spezifischen Einstiegspunkt zur Verwendung eines anderen Domänencontrollers aktualisieren oder alle Einstiegspunkte mit einem bestimmten Domänencontroller zur Verwendung eines neuen Domänencontrollers aktualisieren. In ersten Fall sollten Sie den zu aktualisierenden Einstiegspunkt mit dem *EntryPointName*-Parameter angeben. In zweiten Fall sollten Sie den zu ersetzenden Domänencontroller mit dem *ExistingDC*-Parameter angeben. Sie können nur einen dieser Parameter angeben.  
  
Der **Fehler wurde empfangen**. Es wurden keine erforderlichen Parameter angegeben. Geben Sie einen Einstiegspunktnamen oder den Namen eines vorhandenen Domänencontrollers an.  
  
oder  
  
Für das Cmdlet `Set-DaEntryPointDC` fehlen alle erforderlichen Parameter.  
  
**Ursache**  
  
Die Parameter *EntryPointName* oder *ExistingDC* wurden nicht angegeben oder es wurden beide Parameter für das Cmdlet `Set-DaEntryPointDC` angegeben.  
  
**Lösung**  
  
Führen Sie den Befehl aus, und geben Sie dabei entweder den *EntryPointName*-Parameter oder den *ExistingDC*-Parameter an.  
  
## <a name="could-not-locate-domain-controller"></a>Domänencontroller wurde nicht gefunden  
Der **Fehler wurde empfangen**. Ein neuer Domänen Controller kann nicht automatisch gefunden werden. Versuchen Sie es später noch einmal, oder überprüfen Sie die Einstellungen des Domänencontrollers.  
  
**Ursache**  
  
Der mit dem *ComputerName*-Parameter angegebene Computer ist nicht über RPC erreichbar, oder die Domäne enthält keine verfügbaren beschreibbaren Domänencontroller.  
  
**Lösung**  
  
Stellen Sie sicher, dass der Remotecomputer über RPC erreichbar und ein beschreibbarer Domänencontroller für die Domäne verfügbar ist. Falls ein beschreibbarer Domänencontroller für die Domäne verfügbar ist, können Sie seinen Namen auch explizit mit dem *NewDC*-Parameter angeben.  
  
## <a name="could-not-connect-to-domain-controller"></a>Es konnte keine Verbindung mit dem Domänencontroller hergestellt werden  
  
-   **Problem 1**  
  
    Der **Fehler wurde empfangen**. Der Domänen Controller < Domänencontroller > kann nicht erreicht werden. Überprüfen Sie die Netzwerkkonnektivität und die Serververfügbarkeit.  
  
    **Ursache**  
  
    Der Domänencontroller ist nicht erreichbar. Dieses Problem tritt nur auf, wenn der Administrator mit den Parametern *NewDC* oder *ExistingDC* einen Domänencontroller angibt.  
  
    **Lösung**  
  
    Stellen Sie sicher, dass der Name des Domänencontrollers richtig geschrieben ist. Falls Sie einen Kurznamen als Namen angegeben haben, verwenden Sie den vollqualifizierten Domänennamen (FQDN), und versuchen Sie es noch einmal.  
  
-   **Problem 2**  
  
    Der **Fehler wurde empfangen**. Der Domänen Controller < Domänencontroller > kann nicht kontaktiert werden.  
  
    **Ursache**  
  
    Möglicherweise liegt ein Netzwerkproblem vor, aufgrund dessen der mit dem *NewDC*-Parameter angegebene Domänencontroller oder ein anderer vorhandener Domänencontroller in der Konfiguration nicht erreicht werden kann.  
  
    **Lösung**  
  
    Stellen Sie sicher, dass der Name des Domänencontrollers richtig geschrieben ist, dass er aktiv und beschreibbar ist und eine Vertrauensstellung zwischen dem Domänencontroller und der Domäne besteht.  
  
-   **Problem 3**  
  
    Der **Fehler wurde empfangen**. Der Domänen Controller < Domänencontroller-> kann für% 2! s! nicht erreicht werden.  
  
    **Ursache**  
  
    Um die Einheitlichkeit der Konfiguration in einer Bereitstellung für mehrere Standorte zu wahren, müssen Sie sicherstellen, dass jedes GPO von einem einzigen Domänencontroller verwaltet wird. Wenn der Domänen Controller, der das Server-Gruppenrichtlinien Objekt eines Einstiegs Punkts verwaltet, nicht verfügbar ist, können die RAS-Konfigurationseinstellungen nicht gelesen oder geändert werden.  
  
    **Lösung**  
  
    Befolgen Sie das Verfahren "so ändern Sie den Domänen Controller, der Server-Gruppenrichtlinien Objekte verwaltet" in [2,4. Konfigurieren von GPOs @ no__t-0.  
  
-   **Problem 4**  
  
    Der **Fehler wurde empfangen**. Der primäre Domänen Controller in Domänen < domain_name > kann nicht erreicht werden.  
  
    **Ursache**  
  
    Um die Einheitlichkeit der Konfiguration in einer Bereitstellung für mehrere Standorte zu wahren, müssen Sie sicherstellen, dass jedes GPO von einem einzigen Domänencontroller verwaltet wird. Client-GPOs werden auf dem primären Domänencontroller verwaltet. Wenn der primäre Domänencontroller nicht verfügbar ist, können die RAS-Konfigurationseinstellungen nicht gelesen oder geändert werden.  
  
    **Lösung**  
  
    Befolgen Sie das Verfahren "So übertragen Sie die PDC-Emulatorrolle", wie in [2,4 beschrieben. Konfigurieren von GPOs @ no__t-0.  
  
## <a name="read-only-domain-controller"></a>Schreibgeschützter Domänencontroller  
Der **Fehler wurde empfangen**. Der Domänen Controller < Domänencontroller > ist schreibgeschützt. Geben Sie einen Domänencontroller an, der nicht schreibgeschützt ist.  
  
**Ursache**  
  
Der mit dem *NewDC*-Parameter angegebene Domänencontroller ist schreibgeschützt.  
  
**Lösung**  
  
Bei der Verwendung von `Set-DAEntryPointDC` wird der *NewDC*-Parameter zum Aktualisieren des zugeordneten Domänencontrollers eines bestimmten Einstiegspunkts oder zum Aktualisieren aller zugeordneten Einstiegspunkte eines Domänencontrollers verwendet. Der neue Domänencontroller muss daher beschreibbar sein. Geben Sie einen beschreibbaren Domänencontroller im *NewDC*-Parameter an, und versuchen Sie es noch einmal.  
  
## <a name="cannot-retrieve-gpo"></a>GPO kann nicht abgerufen werden  
  
-   **Problem 1**  
  
    Der **Fehler wurde empfangen**. Die GPO-< GPO_name > auf dem Domänen Controller < previous_domain_controller-> können nicht vom Domänen Controller < replacement_domain_controller > abgerufen werden, da Sie sich nicht in derselben Domäne befinden.  
  
    **Ursache**  
  
    Der RAS-Server und der Domänencontroller befinden sich nicht in derselben Domäne. Daher kann das GPO nicht abgerufen werden.  
  
    **Lösung**  
  
    Falls Sie versucht haben, einen bestimmten Einstiegspunkt zu aktualisieren, vergewissern Sie sich, dass sich der neue Domänencontroller in derselben Domäne befindet wie der Einstiegspunktserver. Falls Sie versucht haben, einen bestimmten Domänencontroller zu aktualisieren, vergewissern Sie sich, dass sich der neue Domänencontroller in derselben Domäne befindet wie der, den Sie ersetzen möchten.  
  
-   **Problem 2**  
  
    Der **Fehler wurde empfangen**. Die GPO-< GPO_name > auf dem Domänen Controller < previous_domain_controller-> können nicht vom Domänen Controller < replacement_domain_controller > abgerufen werden. Warten Sie, bis die Domänenreplikation abgeschlossen ist, und wiederholen Sie den Vorgang.  
  
    **Ursache**  
  
    Wenn Sie den Domänencontroller für einen Einstiegspunkt aktualisieren, versucht das Cmdlet, das Server-GPO vom neuen Domänencontroller zu lesen. Das GPO wird jedoch nicht auf dem neuen Domänencontroller gefunden, weil es noch nicht repliziert wurde.  
  
    **Lösung**  
  
    Das Server-GPO ist nicht auf dem neuen Domänencontroller vorhanden. Stellen Sie sicher, dass die GPOs erfolgreich zum neuen Domänencontroller repliziert wurden, und versuchen Sie es noch einmal.  
  
-   **Problem 3**  
  
    Der **Fehler wurde empfangen**. Sie verfügen nicht über die erforderlichen Berechtigungen für den Zugriff auf GPO < GPO_name >.  
  
    **Ursache**  
  
    Wenn Sie den Domänencontroller für einen Einstiegspunkt aktualisieren, versucht das Cmdlet, das Server-GPO vom neuen Domänencontroller zu lesen. Das GPO kann jedoch nicht vom neuen Domänencontroller gelesen werden, weil Sie nicht über die entsprechenden Berechtigungen verfügen.  
  
    **Lösung**  
  
    Das GPO ist auf dem Domänencontroller vorhanden, kann aber nicht gelesen werden. Stellen Sie sicher, dass Sie über die erforderlichen Berechtigungen verfügen, und versuchen Sie es noch einmal.  
  
## <a name="entry-point-not-part-of-multisite-deployment"></a>Einstiegspunkt ist nicht Teil der Bereitstellung für mehrere Standorte  
Der **Fehler wurde empfangen**. Der Einstiegspunkt < Einstiegspunktname > ist nicht Teil der Bereitstellung für mehrere Standorte. Geben Sie einen anderen Wert an.  
  
**Ursache**  
  
Der angegebene Einstiegspunktname wurde nicht gefunden.  
  
**Lösung**  
  
Stellen Sie sicher, dass der Name des Einstiegspunkts richtig geschrieben ist und GPOs zu den erforderlichen Domänencontrollern repliziert wurden, und versuchen Sie es noch einmal. Verwenden Sie `Get-DAEntryPointDC`, um den zugewiesenen Domänencontroller für jeden Einstiegspunkt anzuzeigen.  
  
## <a name="remote-access-server-settings"></a>Einstellungen des RAS-Servers  
  
-   **Problem 1**  
  
    Der **Fehler wurde empfangen**. Auf die Server < Servername-> im Einstiegspunkt < > Einstiegspunktname kann nicht zugegriffen werden.  
  
    **Ursache**  
  
    Wenn Sie den Domänencontroller für einen Einstiegspunkt aktualisieren, versucht das Cmdlet, den Domänencontroller für den Einstiegspunkt von allen relevanten RAS-Servern zu lesen und zu schreiben. Das Cmdlet konnte die Daten von mindestens einem RAS-Server nicht lesen.  
  
    **Lösung**  
  
    Stellen Sie sicher, dass alle relevanten RAS-Server aktiv sind und Sie auf allen Servern über lokale Administratorberechtigungen verfügen, und versuchen Sie es noch einmal.  
  
-   **Problem 2**  
  
    Der **Fehler wurde empfangen**. Die Einstellungen können nicht in der Registrierung auf dem Server < Servername > im Einstiegspunkt < Einstiegspunktname-> gespeichert werden.  
  
    **Ursache**  
  
    Wenn Sie den Domänencontroller für einen Einstiegspunkt aktualisieren, versucht das Cmdlet, den Domänencontroller für den Einstiegspunkt von allen relevanten RAS-Servern zu lesen und zu schreiben. Das Cmdlet konnte die Daten auf mindestens einen RAS-Server nicht schreiben.  
  
    **Lösung**  
  
    Stellen Sie sicher, dass alle relevanten RAS-Server aktiv sind und Sie auf allen Servern über lokale Administratorberechtigungen verfügen, und versuchen Sie es noch einmal.  
  
-   **Problem 3**  
  
    Der **Fehler wurde empfangen**. GPO-Aktualisierungen können nicht auf < Servername-> angewendet werden. Die Änderungen werden erst nach der nächsten Richtlinienaktualisierung wirksam.  
  
    **Ursache**  
  
    Bei der Verwendung des Cmdlets `Set-DAEntryPointDC` ist der angegebene *ComputerName*-Parameter ein RAS-Server an einem anderen Einstiegspunkt als dem, der der Bereitstellung für mehrere Standorte zuletzt hinzugefügt wurde.  
  
    **Lösung**  
  
    Alle Server, die nicht aktualisiert wurden, können mithilfe des **Konfigurationsstatus** im **DASHBOARD** der Remotezugriffs-Verwaltungskonsole angezeigt werden. Dieser Fehler verursacht keine Funktionsprobleme. Sie können jedoch auf allen nicht aktualisierten Servern `gpupdate /force` ausführen, damit der Konfigurationsstatus sofort aktualisiert wird.  
  
## <a name="problem-resolving-fqdn"></a>Problem bei der Auflösung des vollqualifizierten Domänennamens (FQDN)  
Der **Fehler wurde empfangen**. Auf die Server < Servername-> im Einstiegspunkt < > Einstiegspunktname kann nicht zugegriffen werden.  
  
**Ursache**  
  
Beim Abrufen der Liste zu ändernder DirectAccess-Server konnte das Cmdlet den vollqualifizierten Domänennamen (FQDN) eines der Server nicht aus der Computer-SID auflösen.  
  
**Lösung**  
  
Der in der Fehlermeldung angegebene Einstiegspunkt ist einem Domänencontroller zugeordnet. Stellen Sie sicher, dass der Domänencontroller für den Einstiegspunkt verfügbar ist. Falls der Computer, zu dem die angegebene SID gehört, aus der Domäne entfernt wurde, ignorieren Sie die Meldung, und entfernen Sie den Server aus der Bereitstellung für mehrere Standorte.  
  
## <a name="no-entry-points-to-update"></a>Keine zu aktualisierenden Einstiegspunkte vorhanden  
Die **Warnung wurde empfangen**. Die Domänen Controller Einstellungen wurden nicht geändert. Wenn Ihrer Meinung nach Änderungen erforderlich sind, stellen Sie sicher, dass die Cmdlet-Parameter richtig konfiguriert sind und GPOs auf den erforderlichen Domänencontrollern repliziert werden.  
  
**Ursache**  
  
Wenn das Cmdlet `Set-DaEntryPointDC` mit dem *ExistingDC*-Parameter aufgerufen wird, überprüft DirectAccess alle Einstiegspunkte und aktualisiert die Einstiegspunkte, die dem angegebenen Domänencontroller zugeordnet sind. Es ist jedoch kein Einstiegspunkt mit dem angegebenen *ExistingDC* vorhanden.  
  
**Lösung**  
  
Verwenden Sie das Cmdlet `Get-DAEntryPointDC`, um eine Liste der Einstiegspunkte und der zugeordneten Domänencontroller anzuzeigen. Falls Änderungen vorgenommen wurden, stellen Sie sicher, dass die Cmdlet-Parameter richtig geschrieben sind und die GPOs zu den erforderlichen Domänencontrollern repliziert wurden, und versuchen Sie es noch einmal.  
  


