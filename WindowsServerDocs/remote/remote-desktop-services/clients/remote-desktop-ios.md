---
title: Erste Schritte mit dem iOS-Client
description: Informationen zum Einrichten des Remotedesktopclients für iOS
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 03ec5a3d-d3f2-4afd-9405-ae58b6ecc91c
author: lizap
manager: dongill
ms.author: elizapo
date: 08/27/2019
ms.localizationpriority: medium
ms.openlocfilehash: 700d419d06c0b007ed05be4f82137828f52143e1
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71404142"
---
# <a name="get-started-with-the-ios-client"></a>Erste Schritte mit dem iOS-Client

>Gilt für: Windows 10, Windows 8.1, Windows Server 2019, Windows Server 2016, Windows Server 2012 R2

Sie können den Remotedesktopclient für iOS verwenden, um mit Windows-Apps, -Ressourcen und -Desktops auf Ihrem iOS-Gerät (auf iPhones und iPads) zu arbeiten.

Verwenden Sie die folgenden Informationen für die ersten Schritte. Lesen Sie unbedingt die [häufig gestellten Fragen](remote-desktop-client-faq.md), wenn Sie Fragen haben.

> [!NOTE]
> - Möchten Sie mehr über die neuen Versionen für den iOS-Client erfahren? Lesen Sie [Neuerungen bei Remotedesktop unter iOS](ios-whatsnew.md).
> - Der iOS-Client unterstützt Geräte unter iOS 6.x oder höher.

## <a name="get-the-remote-desktop-beta-client-and-start-using-it"></a>Abrufen des Remotedesktop-Beta-Clients und Ausführen der ersten Schritte
Der heute über Apple TestFlight verfügbare iOS-Beta-Client unterstützt Verbindungen mit Windows Virtual Desktop-Ressourcen.

### <a name="download-the-remote-desktop-ios-beta-client-from-apple-testflight"></a>Herunterladen des Remotedesktop-Beta-Clients für iOS von Apple TestFlight
So richten Sie den Remotedesktop Beta-Client auf Ihrem IOS-Gerät ein:

1. Installieren Sie die [Apple Testflight](https://apps.apple.com/us/app/testflight/id899247664)-App auf Ihrem IOS-Gerät.
2. Öffnen Sie auf Ihrem iOS-Gerät einen Browser, und navigieren Sie zu [aka.ms/rdiosbeta](https://aka.ms/rdiosbeta).
3. Wählen Sie unter der Beschriftung **Schritt 2 – Betaversion** die Option **Mit Testen beginnen** aus.
4. Wenn Sie zur Testflight-App umgeleitet werden, wählen Sie **Akzeptieren** aus , und **installieren** Sie dann den Client.

### <a name="add-a-connection-to-a-pc"></a>Hinzufügen einer Verbindung zu einem PC
So erstellen Sie eine Remoteverbindung mit einem PC:

1. Tippen Sie im Connection Center auf **+** , und tippen Sie dann auf **PC hinzufügen**.
2. Geben Sie den Namen des Remotecomputers in **PC-Name** ein. Dies kann der Name eines Windows-Computers, ein Internetdomänenname oder eine IP-Adresse sein. Sie können auch Portinformationen an den PC-Namen anfügen (z. B. **MyDesktop:3389** oder **10.0.0.1:3389**).
3. Wählen Sie das **Benutzerkonto** aus, das Sie für den Zugriff auf den Remotecomputer verwenden möchten.
   - Wählen Sie **Immer nachfragen** aus, wenn der Client bei jeder Anmeldung am Remotecomputer Ihre Anmeldeinformationen abfragen soll.
   - Wählen Sie **Benutzerkonto hinzufügen** aus, um ein Konto zu speichern, das Sie häufig verwenden, damit Sie nicht bei jeder Anmeldung Ihre Anmeldeinformationen eingeben müssen. Befolgen Sie [diese Anweisungen](#manage-your-user-accounts) zum Verwalten Ihrer Benutzerkonten.
4. Sie können außerdem die folgenden optionalen Parameter festlegen:
   - In **Anzeigename** können Sie einen leicht zu merkenden Namen für den PC eingeben, mit dem Sie die Verbindung herstellen möchten.
   - Mit **Administratormodus** können Sie eine Verbindung mit einer Administratorsitzung auf dem Remotecomputer herstellen.
   - **Maustasten tauschen** vertauscht die Befehle, die von der linken und der rechten Maustaste gesendet werden. Ideal für linkshändige Benutzer.
   - **Gateway** ist das Remotedesktopgateway, das Sie verwenden, um von einem externen Netzwerk aus eine Verbindung mit einem Computer herzustellen. Weitere Informationen erhalten Sie von Ihrem Systemadministrator.
   - **Sound** wählt das Gerät aus, das von der Remote Sitzung für die Audiowiedergabe verwendet wird. Sie können sich entscheiden, Audiosignale auf Ihrem lokalen Gerät, dem Remotegerät oder gar nicht wiederzugeben.
   - **Mikrofon** aktiviert die Mikrofonumleitung. Diese Einstellung ist standardmäßig deaktiviert.
   - **Kamera** aktiviert die Kameraumleitung. Diese Einstellung ist standardmäßig deaktiviert.
   - **Zwischenablage** aktiviert die Umleitung der Zwischenablage. Die Einstellung ist standardmäßig aktiviert.
   - **Speicher** aktiviert die Umleitung des lokalen Speichers. Diese Einstellung ist standardmäßig deaktiviert.
5. Wählen Sie **Speichern** aus, um die Remote-PC-Verbindung hinzuzufügen.

### <a name="add-remote-resources"></a>Hinzufügen von Remoteressourcen
Bei Remoteressourcen handelt es sich um RemoteApp-Programme, sitzungsbasierte Desktops und virtuelle Desktops, die von Ihrem Administrator veröffentlicht werden. Der iOS-Client unterstützt Ressourcen, die von Bereitstellungen von **Remotedesktopdienste** und **Windows Virtual Desktop** veröffentlicht werden. So fügen Sie Remoteressourcen hinzu:

1. Tippen Sie im Connection Center auf **+** , und tippen Sie dann auf **Arbeitsbereich hinzufügen**.
2. Geben Sie die **Feed-URL** ein. Dies kann eine URL oder eine E-Mail-Adresse sein:
   - Die **URL** ist die URL des RD-Webzugriffsservers, die Ihnen von Ihrem Administrator zur Verfügung gestellt wird. Wenn Sie auf Ressourcen von Windows Virtual Desktop zugreifen, können Sie `https://rdweb.wvd.microsoft.com` verwenden.
   - Wenn Sie **E-Mail** verwenden möchten, geben Sie in diesem Feld Ihre E-Mail-Adresse ein. Dies weist den Client an, nach einem RD-Webzugriffsserver zu suchen, der Ihrer E-Mail-Adresse zugeordnet ist, wenn dies von Ihrem Administrator konfiguriert wurde.
3. Tippen Sie auf **Weiter**.
4. Geben Sie auf Aufforderung Ihre Anmeldeinformationen ein. Diese können sich je nach Bereitstellung unterscheiden und können Folgendes beinhalten:
   - **Benutzername**, der Name des Benutzers, der über die Zugriffsberechtigung auf die Ressourcen verfügt.
   - **Kennwort**, das dem Benutzernamen zugeordnete Kennwort.
   - **Zusätzlicher Faktor**, zu dessen Eingabe Sie ggf. aufgefordert werden, wenn die Authentifizierung von Ihrem Administrator in dieser Weise konfiguriert wurde.
5. Tippen Sie auf **Speichern**.

Die Remoteressourcen werden im Connection Center angezeigt.

## <a name="get-the-remote-desktop-client-and-start-using-it"></a>Abrufen des Remotedesktopclients und Ausführen der ersten Schritte

### <a name="download-the-remote-desktop-client-from-the-ios-store"></a>Herunterladen des Remotedesktopclients aus dem App Store für iOS-Geräte

Führen Sie die folgenden Schritte für den Einstieg in Remotedesktop auf Ihrem iOS-Gerät aus:

1. Laden Sie den Microsoft-Remotedesktopclient von [iTunes](https://itunes.apple.com/app/microsoft-remote-desktop/id714464092?mt=8) herunter.
2. [Richten Sie Ihren PC so ein, dass Remoteverbindungen zulässig sind](remote-desktop-client-faq.md#how-do-i-set-up-a-pc-for-remote-desktop).
3. Fügen Sie eine [Remotedesktopverbindung](#add-a-remote-desktop-connection) oder eine [Remoteressource](#add-a-remote-resource) hinzu. Mit einer Verbindung können Sie eine direkte Verbindung mit einem Windows-PC herstellen, und mit einer Remoteressource können Sie ein RemoteApp-Programm, einen sitzungsbasierten Desktop oder einen virtuellen Desktop verwenden, das/der mithilfe von RemoteApp- und Desktopverbindungen veröffentlicht wird. Dieses Feature ist in der Regel in Unternehmensumgebungen verfügbar.

### <a name="add-a-remote-desktop-connection"></a>Hinzufügen einer Remotedesktopverbindung

Gehen Sie wie folgt vor, um eine Remotedesktopverbindung zu erstellen:

1. Tippen Sie im Connection Center auf das Pluszeichen ( **+** ), und tippen Sie dann auf **PC oder Server hinzufügen**.
2. Geben Sie die folgenden Informationen für die Remotedesktopverbindung ein:
   - **PC-Name**: Der Name des Computers. Dies kann der Name eines Windows-Computers, ein Internetdomänenname oder eine IP-Adresse sein. Sie können auch Portinformationen an den PC-Namen anfügen (z. B. **MyDesktop:3389** oder **10.0.0.1:3389**).
   - **Benutzername**: Der Benutzername, der für den Zugriff auf den Remotecomputer verwendet werden soll. Sie können die folgenden Formate verwenden: *Benutzername*, *Domäne\Benutzername* oder `user_name@domain.com`. Sie können auch angeben, ob der Benutzer zur Eingabe eines Benutzernamens und Kennworts aufgefordert werden soll.
3. Sie können auch die folgenden zusätzlichen Optionen festlegen:
   - **Anzeigename (optional)** : Ein leicht zu merkender Name für den PC, mit dem Sie eine Verbindung herstellen. Sie können eine beliebige Zeichenfolge verwenden, aber wenn Sie keinen Anzeigenamen angeben, wird der PC-Name angezeigt.
   - **Gateway (optional)** : Das Remotedesktopgateway, das Sie zum Herstellen einer Verbindung mit virtuellen Desktops, RemoteApp-Programmen und sitzungsbasierten Desktops in einem internen Unternehmensnetzwerk verwenden möchten. Sie erhalten die Informationen über das Gateway von Ihrem Systemadministrator.
   - **Sound**: Wählen Sie das während der Remotesitzung für Audio zu verwendende Gerät aus. Sie können auswählen, ob Sound auf den lokalen Geräten, auf dem Remotegerät oder überhaupt nicht wiedergegeben werden soll.
   - **Maustasten tauschen**: Wenn eine Mausbewegung einen Befehl mit der linken Maustaste senden würde, wird derselbe Befehl stattdessen mit der rechten Maustaste gesendet. Dies ist erforderlich, wenn der Remote-PC für den Linkshänder-Mausmodus konfiguriert ist.
   - **Administratormodus**: Stellen Sie eine Verbindung mit einer Verwaltungssitzung auf einem Server unter Windows Server 2003 oder höher her.
4. Tippen Sie auf **Speichern**.

Müssen Sie diese Einstellungen bearbeiten? Drücken und halten Sie den Desktop, den Sie bearbeiten möchten, und tippen Sie dann auf das Symbol „Einstellungen“.

### <a name="add-a-remote-resource"></a>Hinzufügen einer Remoteressource

Bei Remoteressourcen handelt es sich um RemoteApp-Programme, sitzungsbasierte Desktops und virtuelle Desktops, die mithilfe von RemoteApp- und Desktopverbindungen veröffentlicht werden.

- Die URL zeigt den Link zum Server mit Web Access für Remotedesktop an, der Ihnen Zugriff auf RemoteApp- und Desktopverbindungen bietet.
- Die konfigurierten RemoteApp- und Desktopverbindungen werden aufgeführt.

Gehen Sie wie folgt vor, um eine Remoteressource hinzuzufügen:

1. Tippen Sie auf dem Bildschirm „Connection Center“ auf das Pluszeichen ( **+** ), und tippen Sie dann auf **Remoteressourcen hinzufügen**.
2. Geben Sie Informationen für die Remoteressource ein:
   - **Feed-URL**: Die URL des Servers mit Web Access für Remotedesktop. In dieses Feld können Sie auch Ihr geschäftliches E-Mail-Konto eingeben. Dies weist den Client an, nach dem Ihrer E-Mail-Adresse zugeordneten Server mit Web Access für Remotedesktop zu suchen.
   - **Benutzername**: Der Benutzername, der für den Server mit Web Access für Remotedesktop verwendet werden soll, mit dem Sie eine Verbindung herstellen.
   - **Kennwort**: Das Kennwort, das für den Server mit Web Access für Remotedesktop verwendet werden soll, mit dem Sie eine Verbindung herstellen.
3. Tippen Sie auf **Speichern**.

Die Remoteressourcen werden im Connection Center angezeigt.

## <a name="manage-your-user-accounts"></a>Verwalten Ihrer Benutzerkonten

Wenn Sie eine Verbindung mit einem Desktop oder Remoteressourcen herstellen, können Sie die Benutzerkonten speichern, um sie erneut auswählen zu können.

Gehen Sie wie folgt vor, um ein neues Benutzerkonto zu erstellen:

1. Tippen Sie im Connection Center auf **Einstellungen**, und tippen Sie dann auf **Benutzerkonten**.
2. Tippen Sie auf **Benutzerkonto hinzufügen**.
3. Geben Sie die folgenden Informationen ein:
   - **Benutzername**: Der Name des Benutzers, der zur Verwendung für eine Remoteverbindung gespeichert werden soll. Sie können den Benutzernamen in einem der folgenden Formate eingeben: Benutzername, Domäne\Benutzername oder user_name@domain.com.
   - **Kennwort**: Das Kennwort für den angegebenen Benutzer. Jedem Benutzerkonto, das Sie zur Verwendung für Remoteverbindungen speichern möchten, muss ein Kennwort zugeordnet sein.
4. Tippen Sie auf **Speichern**.

Gehen Sie wie folgt vor, um ein Benutzerkonto zu löschen:

1. Tippen Sie im Connection Center auf **Einstellungen**, und tippen Sie dann auf **Benutzerkonten**.
2. Wählen Sie das Konto aus, das Sie löschen möchten.
3. Tippen Sie auf **Löschen**.   

## <a name="connect-to-an-rd-gateway-to-access-internal-assets"></a>Herstellen einer Verbindung mit einem Remotedesktopgateway zum Zugreifen auf interne Ressourcen

Mit einem Remotedesktopgateway (RD-Gateway) können Sie eine Verbindung mit einem Remotecomputer in einem Unternehmensnetzwerk über das Internet herstellen. Sie können Ihre Gateways mit dem Remotedesktopclient erstellen und verwalten.

Gehen Sie wie folgt vor, um ein neues Gateway einzurichten:

1. Tippen Sie im Connection Center auf **Einstellungen** > **Gateways**.
2. Tippen Sie auf **Remotedesktopgateway hinzufügen**.
3. Geben Sie die folgenden Informationen ein:
   - **Servername**: Der Name des Computers, den Sie als Gateway verwenden möchten. Dies kann der Name eines Windows-Computers, ein Internetdomänenname oder eine IP-Adresse sein. Sie können dem Servernamen auch Portinformationen hinzufügen (z. B.: **RDGateway:443** oder **10.0.0.1:443**).
   - **Benutzername**: Der Benutzername und das Kennwort für das Remotedesktopgateway, mit dem Sie eine Verbindung herstellen. Sie können auch **Anmeldeinformationen für die Verbindung verwenden** auswählen, damit derselbe Benutzername und dasselbe Kennwort wie für die Remotedesktopverbindung verwendet werden.

## <a name="navigate-the-remote-desktop-session"></a>Navigieren in der Remotedesktopsitzung
Wenn Sie eine Remotedesktopsitzung starten, stehen Tools zur Verfügung, die Sie für die Navigation in der Sitzung verwenden können.

### <a name="start-a-remote-desktop-connection"></a>Starten einer Remotedesktopverbindung

1. Tippen Sie auf die Remotedesktopverbindung, um die Remotedesktopsitzung zu starten.
2. Wenn Sie zur Überprüfung des Zertifikats für den Remotedesktop aufgefordert werden, tippen Sie auf **Annehmen**. Sie können auch auswählen, dass das Zertifikat immer akzeptiert werden soll, indem Sie den Umschalter **Nicht erneut nach Verbindungen mit diesem Computer fragen** auf **EIN** schieben.

### <a name="connection-bar"></a>Verbindungsleiste

Die Verbindungsleiste ermöglicht den Zugriff auf zusätzliche Navigationssteuerelemente.

- **Schwenken-Steuerelement**: Mit dem Schwenken-Steuerelement kann der Bildschirm vergrößert und verschoben werden. Beachten Sie, dass das Schwenken-Steuerelement nur mithilfe direkter Touchbewegung verfügbar ist.
   - Aktivieren/Deaktivieren des Schwenken-Steuerelements: Tippen Sie auf der Verbindungsleiste auf das Schwenksymbol, um das Schwenken-Steuerelement anzuzeigen und den Bildschirm zu vergrößern. Tippen Sie auf der Verbindungsleiste erneut auf das Schwenksymbol, um das Steuerelement auszublenden und die ursprüngliche Auflösung des Bildschirms wiederherzustellen.
   - Verwenden des Schwenken-Steuerelements: Tippen Sie auf das Schwenken-Steuerelement, halten Sie es gedrückt, und ziehen Sie es dann in die Richtung, in der Sie den Bildschirm verschieben möchten.
   - Verschieben des Schwenken-Steuerelements: Doppeltippen Sie auf das Schwenken-Steuerelement, und halten Sie das Steuerelement gedrückt, um es auf dem Bildschirm zu verschieben.
- **Verbindungsname**: Der aktuelle Verbindungsname wird angezeigt. Tippen Sie auf den Verbindungsnamen, um die Sitzungsauswahlleiste anzuzeigen.
- **Tastatur**: Tippen Sie auf das Tastatursymbol, um die Tastatur ein- oder auszublenden. Das Schwenken-Steuerelement wird automatisch angezeigt, wenn die Tastatur eingeblendet ist.
- **Verschieben der Verbindungsleiste**: Tippen Sie auf die Verbindungsleiste, halten Sie die Leiste gedrückt, und ziehen Sie sie dann per Drag & Drop an eine neue Position am oberen Rand des Bildschirms.

### <a name="session-selection"></a>Sitzungsauswahl
Es können mehrere Verbindungen mit verschiedenen PCs gleichzeitig geöffnet sein. Tippen Sie auf die Verbindungsleiste, um die Sitzungsauswahlleiste auf der linken Seite des Bildschirms anzuzeigen. Mit der Sitzungsauswahlleiste können Sie Ihre geöffneten Verbindungen anzeigen und zwischen diesen wechseln.

- Wechseln Sie zwischen Apps in einer geöffneten Remoteressourcensitzung.

    Wenn Sie mit Remoteressourcen verbunden sind, können Sie zwischen geöffneten Anwendungen innerhalb dieser Sitzung wechseln, indem Sie auf das Erweiterungsmenü tippen und eine Anwendung aus der Liste der verfügbaren Elemente auswählen.
- Starten einer neuen Sitzung

  Sie können neue Anwendungen oder Desktopsitzungen innerhalb Ihrer aktuellen Verbindung starten: Tippen Sie auf **Neu starten**, und wählen Sie dann eine Anwendung oder Sitzung aus der Liste der verfügbaren Elemente aus.

- Trennen einer Sitzung

  Um eine Sitzung zu trennen, tippen Sie auf der linken Seite der Kachel für die Sitzung auf das „X“.

### <a name="command-bar"></a>Befehlsleiste

Ab Version 8.0.1 wird die Utility-Leiste durch die Befehlsleiste ersetzt. Über die Befehlsleiste können Sie zwischen den Mausmodi wechseln und zum Connection Center zurückkehren.

## <a name="use-touch-gestures-and-mouse-modes-in-a-remote-session"></a>Verwenden von Touchgesten und Mausmodi in einer Remotesitzung

Der Client verwendet Standardtouchgesten. Sie können auch Touchgesten verwenden, um Mausaktionen auf dem Remotedesktop zu replizieren. Die verfügbaren Mausmodi sind in der folgenden Tabelle aufgeführt.

> [!NOTE]
> Bei der Interaktion mit Windows 8 oder höher werden die nativen Touchgesten im Modus für die direkte Touchbewegung unterstützt. Weitere Informationen zu Windows 8-Gesten findest du unter [Touchbewegung: Wischen, Tippen und vieles mehr](https://windows.microsoft.com/en-US/windows-8/touch-swipe-tap-beyond).

| Mausmodus    | Mausvorgang      | Geste                                                    |
|---------------|----------------------|------------------------------------------------------------|
| Direkte Touchbewegung  | Linksklick           | Mit einem Finger tippen                                               |
| Direkte Touchbewegung  | Rechtsklick          | Mit einem Finger tippen und halten                                      |
| Mauszeiger | Linksklick           | Mit einem Finger tippen                                               |
| Mauszeiger | Linksklick und ziehen  | Mit einem Finger doppeltippen und halten, dann ziehen                    |
| Mauszeiger | Rechtsklick          | Mit zwei Fingern tippen                                               |
| Mauszeiger | Rechtsklick und ziehen | Mit zwei Fingern doppeltippen und halten, dann ziehen                    |
| Mauszeiger | Mausrad          | Mit zwei Fingern tippen und halten, dann nach oben oder unten ziehen                |
| Mauszeiger | Zoom                 | Zwei Finger zusammenführen, um die Ansicht zu vergrößern, oder zwei Finger auseinander spreizen, um die Ansicht zu verkleinern |

## <a name="supported-input-devices"></a>Unterstützte Eingabegeräte

Der [Remotedesktop-Beta Client für iOS](https://aka.ms/rdiosbeta) unterstützt die physischen Mäuse Swiftpoint GT und ProPoint. Swiftpoint bietet Benutzern des iOS-Beta-Clients einen [exklusiven Rabatt](https://www.swiftpoint.com/microsoft/) für die GT-Maus.

Der iOS-Client unterstützt derzeit nur Swiftpoint-Mäuse. Informationen zur Unterstützung von anderen Geräten in der Zukunft finden Sie auf der Seite [Neuerungen beim iOS-Client](ios-whatsnew.md) und im [App Store für iOS-Geräte](https://aka.ms/rdios).

## <a name="use-a-keyboard-in-a-remote-session"></a>Verwenden einer Tastatur in einer Remotesitzung

Sie können in Ihrer Remotesitzung entweder eine Bildschirmtastatur oder eine physische Tastatur verwenden.

Verwenden Sie bei Bildschirmtastaturen die Schaltfläche am rechten Rand der Leiste über der Tastatur, um zwischen der Standardtastatur und der zusätzlichen Tastatur zu wechseln.

Wenn für Ihr iOS-Gerät Bluetooth aktiviert ist, wird die Bluetooth-Tastatur vom Client automatisch erkannt.

Bedenken Sie, dass Sondertasten wie STRG, die OPTIONSTASTE und Funktionstasten aufgrund von Beschränkungen des Betriebssystems bei Verwendung einer Bluetooth-Tastatur nicht wie erwartet funktionieren. Die folgenden Tasten funktionieren:

- Alphanumerische Tasten
- Pfeiltasten
- TAB: TAB funktioniert, aber die Tastenkombination UMSCHALT+TAB funktioniert nicht.
- Home-Taste/POS1: ALT+NACH-LINKS-TASTE = POS1
- ENDE: ALT+NACH-RECHTS-TASTE = ENDE
- BILD-AUF: ALT+NACH-OBEN-TASTE = BILD-AUF
- BILD-AB: ALT+NACH-UNTEN-TASTE = BILD-AB
- Alle auswählen: BEFEHLSTASTE+A = STRG+A („Alle auswählen“ in den meisten Programmen)
- Ausschneiden: BEFEHLSTASTE+X = STRG+X („Ausschneiden“ in den meisten Programmen)
- Kopieren: BEFEHLSTASTE+C = STRG+C („Kopieren“ in den meisten Programmen)
- Einfügen: BEFEHLSTASTE+V = STRG+V („Einfügen“ in den meisten Programmen)
- Sonderzeichen: Mit der ALT-TASTE + alphanumerischen Tasten werden je nach konfigurierter Sprache andere Sonderzeichen erzeugt.

> [!TIP]
> Fragen und Kommentare sind immer willkommen. Verwenden Sie jedoch NICHT die Kommentarfunktion am Ende dieses Artikels, um Hilfe bei der Problembehandlung anzufordern. Verwenden Sie stattdessen das [Remotedesktopclient-Forum](https://social.technet.microsoft.com/forums/windowsserver/en-us/home?forum=winrdc), und erstellen Sie einen neuen Thread. Haben Sie einen Vorschlag für ein Feature? Teilen Sie uns dies im [UserVoice-Forum für den Client](https://remotedesktop.uservoice.com/forums/272085-remote-desktop-for-android) mit.
