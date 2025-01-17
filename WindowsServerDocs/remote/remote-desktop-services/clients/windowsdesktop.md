---
title: Erste Schritte mit dem Windows-Desktopclient
description: Grundlegende Informationen zum Windows-Desktopclient.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: remote-desktop-services
ms.tgt_pltfrm: na
ms.topic: article
author: heidilohr
manager: daveba
ms.author: helohr
ms.date: 09/24/2019
ms.localizationpriority: medium
ms.openlocfilehash: 961d636fb59b33d0c562ec25d13174abbe766606
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71404081"
---
# <a name="get-started-with-the-windows-desktop-client"></a>Erste Schritte mit dem Windows-Desktopclient

>Gilt für: Windows 10 und Windows 7

Du kannst den Remotedesktopclient für Windows-Desktop verwenden, um Windows-Apps und -Desktops über ein anderes Windows-Gerät per Remotezugriff zu nutzen.

> [!NOTE]
> - Diese Dokumentation bezieht sich nicht auf den Remotedesktopverbindungs-Client (MSTSC), der mit Windows geliefert wird. Sie bezieht sich auf den neuen Remotedesktopclient (MSRDC).
> - Dieser Client unterstützt derzeit nur den Zugriff auf Remote-Apps und -Desktops aus dem [virtuellen Windows-Desktop](https://aka.ms/wvd).
> - Möchtest du mehr über die neuen Versionen für den Windows-Desktopclient erfahren? [Neuigkeiten im Windows-Desktopclient](windowsdesktop-whatsnew.md) ansehen

## <a name="install-the-client"></a>Installieren des Clients

Derzeit kannst du den Client für Windows 64-Bit herunterladen. Wir aktualisieren diese Liste, sobald der Client für weitere Versionen von Windows verfügbar wird.

- [Windows 64-Bit-Client](https://go.microsoft.com/fwlink/?linkid=2068602)

Du kannst den Client für den aktuellen Benutzer installieren – dafür sind keine Administratorrechte erforderlich –, oder dein Administrator kann den Client installieren und ihn so konfigurieren, dass alle Benutzer des Geräts darauf zugreifen können.

Nachdem Du den Client installiert hast, kannst du ihn aus dem Startmenü starten, indem du nach **Remotedesktop** suchst.

## <a name="update-the-client"></a>Update des Clients

Du wirst benachrichtigt, wenn eine neue Version des Clients verfügbar ist, sofern Benachrichtigungen nicht durch deinen Administrator deaktiviert wurden. Die Benachrichtigung wird entweder im Connection Center oder im Windows Info-Center angezeigt. Um deinen Client zu aktualisieren, wähle die Benachrichtigung einfach aus.

Du kannst außerdem manuell nach neuen Updates für den Client suchen:

1. Tippe im Connection Center auf das Überlaufmenü ( **...** ) in der Befehlsleiste am oberen Rand des Clients.
2. Wähle im Dropdownmenü **Info** aus.
3. Tippe auf **Nach Updates suchen**.
4. Wenn ein Update verfügbar ist, tippe auf **Update installieren**, um ein Update des Clients auszuführen.

## <a name="feeds"></a>Feeds

Rufe die Liste der verwalteten Ressourcen ab, auf die du Zugriff hast, wie etwa Apps und Desktops, indem du den Feed abonnierst, den dir dein Administrator bereitgestellt hat. Wenn du abonnierst, werden die Ressourcen auf deinem lokalen PC verfügbar. Der Windows-Desktopclient unterstützt aktuell Ressourcen, die vom virtuellen Windows-Desktop veröffentlicht wurden.

### <a name="subscribe-to-a-feed"></a>Abonnieren eines Feeds

1. Tippe auf der Hauptseite des Clients, die auch als Connection Center bezeichnet wird, auf **Abonnieren**.
2. Melde dich bei entsprechender Aufforderung mit deinem Benutzerkonto an.
3. Die Ressourcen werden im Connection Center nach Arbeitsbereich gruppiert angezeigt.

Du kannst Ressourcen mit einer der folgenden Methoden starten:

- Wechsle zum Connection Center, und doppelklicke auf eine Ressource, um sie zu starten.
- Alternativ kannst du zum Startmenü navigieren und nach einem Ordner mit dem Namen des Arbeitsbereichs suchen oder den Namen der Ressource in die Suchleiste eingeben.

### <a name="workspace-details"></a>Arbeitsbereichsdetails

Nach dem Abonnieren kannst du weitere Informationen zu einem Arbeitsbereich im Bereich „Details“ anzeigen:

- Den Namen des Arbeitsbereichs
- Die zum Abonnieren verwendete URL und den Benutzernamen
- Die Anzahl der Apps und Desktops
- Datum/Uhrzeit der letzten Aktualisierung
- Den Status der letzten Aktualisierung

Zugriff auf den Bereich „Details“:

1. Tippe im Connection Center auf das Überlaufmenü ( **...** ) neben dem Arbeitsbereich.
2. Wähle im Dropdownmenü **Details** aus.
3. Der Bereich „Details“ wird auf der rechten Seite des Clients angezeigt.

Nachdem du abonniert hast, wird der Arbeitsbereich automatisch regelmäßig aktualisiert. Da bei können Ressourcen hinzugefügt, geändert oder entfernt werden, basierend auf Änderungen, die von deinem Administrator vorgenommen werden.

Du kannst bei Bedarf auch manuell nach Aktualisierungen suchen, indem du im Detailbereich **Jetzt aktualisieren** auswählst.

### <a name="unsubscribe-from-a-feed"></a>Kündigen des Abonnements eines Feeds

In diesem Abschnitt erfährst du, wie du das Abonnement eines Feeds beendest. Du kannst das Abonnement beenden, um entweder erneut mit einem anderen Konto zu abonnieren oder um deine Ressourcen vom System zu entfernen.

1. Tippe im Connection Center auf das Überlaufmenü ( **...** ) neben dem Arbeitsbereich.
2. Wähle im Dropdownmenü **Abonnement kündigen** aus.
3. Überprüfe das Dialogfeld, und wähle **Fortfahren** aus.

## <a name="managed-desktops"></a>Verwaltete Desktops

Arbeitsbereiche können mehrere verwaltete Ressourcen enthalten, einschließlich Desktops. Wenn du auf einen verwalteten Desktop zugreifst, hast du Zugriff auf alle Apps, die von deinem Administrator installiert wurden.

### <a name="desktop-settings"></a>Desktopeinstellungen

Du kannst einige der Einstellungen für Desktopressourcen konfigurieren, um sicherzustellen, dass die Oberfläche deinen Anforderungen entspricht. So greifst du auf die Liste der verfügbaren Einstellungen zu:

1. Klicke im Connection Center mit der rechten Maustaste auf eine Desktopressource.
2. Wähle im Dropdownmenü **Einstellungen** aus.
3. Der Bereich „Einstellungen“ wird auf der rechten Seite des Clients mit dem Namen des Desktops angezeigt.

Der Client verwendet die von deinem Administrator konfigurierten Einstellungen, es sei denn, du deaktivierst die Option **Standardeinstellungen verwenden**. Auf diese Weise kannst du die folgenden Optionen konfigurieren:

- **Alle Monitore verwenden** schaltet die Desktopsitzung zwischen der Nutzung aller lokalen Monitore und nur einem Monitor um.
- **Im Vollbildmodus starten** legt fest, ob die Sitzung im Vollbild- oder im Fenstermodus gestartet wird. Diese Einstellung ist bei Verwendung aller Monitore automatisch aktiviert.
- **Auflösung beim Ändern der Größe aktualisieren** ändert das Verhalten beim Ändern der Größe im Fenstermodus. Wenn die Option aktiviert ist, wird die Auflösung des Remotedesktops aktualisiert, damit sie mit der Größe des lokalen Fensters übereinstimmt. Bei deaktivierter Option behält die Sitzung die in **Auflösung** angegebene Auflösung für ihre gesamte Dauer bei. Diese Einstellung ist bei Verwendung aller Monitore automatisch aktiviert.
- In **Auflösung** kannst du die Auflösung des Remotedesktops festlegen. Die Sitzung behält diese Auflösung für ihre gesamte Dauer bei. Diese Einstellung wird automatisch deaktiviert, wenn für die Auflösung Aktualisierung beim Ändern der Größe festgelegt wird.
- **Größe von Text und Apps ändern** gibt die Größe der Inhalte der Sitzung an. Diese Einstellung gilt nur für Verbindungen mit Windows 8.1 und höher oder Windows Server 2012 R2 und höher. Diese Einstellung wird automatisch deaktiviert, wenn für die Auflösung Aktualisierung beim Ändern der Größe festgelegt wird.
- **Sitzung an Fenster anpassen** bestimmt, wie die Sitzung angezeigt wird, wenn die Auflösung des Remotedesktops von der Größe des lokalen Fensters abweicht. Wenn die Option aktiviert ist, wird die Größe der Sitzungsinhalte innerhalb des Fensters passend geändert, wobei das Seitenverhältnis der Sitzung beibehalten wird. Ist sie deaktiviert, werden Scrollleisten oder schwarze Bereiche angezeigt, wenn Auflösung und Fenstergröße nicht übereinstimmen.

## <a name="provide-feedback"></a>Feedback bereitstellen

Hast du einen Vorschlag für eine Funktion, oder möchtest du ein Problem melden? Teile uns den Vorschlag über den [Feedback-Hub](feedback-hub://?tabid=2&contextid=883) mit. Du kannst über deinen Client auch auf den Feedback-Hub zugreifen:

1. Tippe im Connection Center auf das Überlaufmenü ( **...** ) in der Befehlsleiste am oberen Rand des Clients.
2. Wähle im Dropdownmenü **Feedback** aus, um den Feedback-Hub zu öffnen.
