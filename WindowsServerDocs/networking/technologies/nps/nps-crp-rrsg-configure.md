---
title: Konfigurieren von RADIUS-Remoteservergruppen
description: Dieses Thema enthält Informationen zum Konfigurieren von RADIUS-Remote Server Gruppen auf dem Netzwerk Richtlinien Server unter Windows Server 2016.
manager: brianlic
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: ca125e57-249c-4d97-85d1-2929cbf871f1
ms.author: pashort
author: shortpatti
ms.openlocfilehash: fe34d25d2b54b02bb56fcad99c433054a309f60b
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405459"
---
# <a name="configure-remote-radius-server-groups"></a>Konfigurieren von RADIUS-Remoteservergruppen

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Sie können dieses Thema verwenden, um RADIUS-Remote Server Gruppen zu konfigurieren, wenn Sie NPS so konfigurieren möchten, dass Sie als Proxy Server fungieren und Verbindungsanforderungen zur Verarbeitung an andere NPSS weiterleiten.

## <a name="add-a-remote-radius-server-group"></a>Hinzufügen einer Remote-RADIUS-Server Gruppe

Mit diesem Verfahren können Sie eine neue Remote-RADIUS-Server Gruppe im Netzwerk Richtlinien Server-Snap-in hinzufügen.

Wenn Sie NPS als RADIUS-Proxy konfigurieren, erstellen Sie eine neue Verbindungs Anforderungs Richtlinie, die von NPS verwendet wird, um zu bestimmen, welche Verbindungsanforderungen an andere RADIUS-Server weiterzuleiten sind. Außerdem wird die Verbindungs Anforderungs Richtlinie konfiguriert, indem eine Remote-RADIUS-Server Gruppe angegeben wird, die einen oder mehrere RADIUS-Server enthält, die NPS anweist, wohin die Verbindungsanforderungen gesendet werden sollen, die der Verbindungs Anforderungs Richtlinie entsprechen.

>[!NOTE]
>Sie können auch eine neue Remote-RADIUS-Server Gruppe beim Erstellen einer neuen Verbindungs Anforderungs Richtlinie konfigurieren.

Grundvoraussetzung für die Ausführung dieses Vorgangs ist die Mitgliedschaft in **Domänen-Admins** oder einer gleichwertigen Gruppe.

### <a name="to-add-a-remote-radius-server-group"></a>So fügen Sie eine Remote-RADIUS-Server Gruppe hinzu 

1. Klicken Sie in Server-Manager auf **Extras, und**klicken Sie dann auf **Netzwerk Richtlinien Server** , um die NPS-Konsole zu öffnen.
2. Doppelklicken Sie in der Konsolen Struktur auf **RADIUS-Clients und-Server**, klicken Sie mit der rechten Maustaste auf RADIUS- **Remote Server Gruppen**, und klicken Sie dann auf **neu**.
3. Das Dialogfeld **neue Remote-RADIUS-Server Gruppe** wird geöffnet. Geben Sie unter **Gruppenname**einen Namen für die Remote-RADIUS-Server Gruppe ein.
4. Klicken Sie **in RADIUS-Server**auf **Hinzufügen**. Das Dialogfeld **RADIUS-Server hinzufügen** wird geöffnet. Geben Sie die IP-Adresse des RADIUS-Servers ein, den Sie der Gruppe hinzufügen möchten, oder geben Sie den voll qualifizierten Domänen Namen \(fqdn @ no__t-1 des RADIUS-Servers ein, und klicken Sie dann auf **überprüfen**.
5. Klicken Sie im Dialogfeld **RADIUS-Server hinzufügen** auf die Registerkarte **Authentifizierung/Kontoführung**. Geben Sie unter **gemeinsames Geheimnis** und **gemeinsames Geheimnis bestätigen**den gemeinsamen geheimen Schlüssel ein. Sie müssen den gleichen gemeinsamen geheimen Schlüssel verwenden, wenn Sie den lokalen Computer als RADIUS-Client auf dem RADIUS-Remote Server konfigurieren.
6. Wenn Sie das Extensible Authentication Protocol (EAP) nicht für die Authentifizierung verwenden, **muss die Click-Anforderung das Message Authenticator-Attribut enthalten**. EAP verwendet standardmäßig das Message-Authenticator-Attribut.
7. Vergewissern Sie sich, dass die Portnummern für Authentifizierung und Buchhaltung für Ihre Bereitstellung korrekt sind.
8. Wenn Sie für die Kontoführung einen anderen gemeinsamen geheimen Schlüssel verwenden, deaktivieren Sie das Kontrollkästchen **dasselbe gemeinsame Geheimnis für Authentifizierung und Kontoführung verwenden** , und geben Sie dann den gemeinsamen geheimen Schlüssel der **Buchhaltung in** **gemeinsames Geheimnis** ein, und **bestätigen Sie Shared. geheimer**Schlüssel.
9. Wenn Sie keine Nachrichten zum Starten und Beenden des Netzwerk Zugriffs Servers an den Remote-RADIUS-Server weiterleiten möchten, deaktivieren Sie das Kontrollkästchen **Netzwerk Zugriffs Server-Benachrichtigungen an diesen Server starten und beenden** .

Weitere Informationen zum Verwalten von NPS finden Sie unter [Verwalten des Netzwerk Richtlinien Servers](nps-manage-top.md).

Weitere Informationen zu NPS finden Sie unter [Netzwerk Richtlinien Server (Network Policy Server, NPS)](nps-top.md).

