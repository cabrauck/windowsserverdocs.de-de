---
title: 'Schritt 1: Installieren der WSUS-Server Rolle'
description: 'Thema zu Windows Server Update Service (WSUS): Beschreibt die Installation der Server Rolle mit Server-Manager'
ms.prod: windows-server
ms.reviewer: na
ms.technology: manage-wsus
ms.topic: article
ms.assetid: fabc8619-350e-403b-96f8-116424931300
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 22554a9669c30cc827c509824f187fbaaedb1272
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71361702"
---
# <a name="step-1-install-the-wsus-server-role"></a>Schritt 1: Installieren der WSUS-Server Rolle

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Der nächste Schritt zur Bereitstellung des WSUS-Servers ist die Installation der WSUS-Serverrolle. Anhand des folgenden Verfahrens wird die Installation der WSUS-Serverrolle mithilfe von Server-Manager beschrieben.

> [!IMPORTANT]
> In diesem Installationsverfahren wird nur die Installation von WSUS mit der internen Windows-Datenbank (WID) behandelt. Die Verfahren zum Installieren von WSUS mithilfe von Microsoft SQL Server sind in [diesem Artikel](https://social.technet.microsoft.com/wiki/contents/articles/10020.installing-wsus-server-role-on-windows-server-2012-with-microsoft-sql-database.aspx)dokumentiert.

### <a name="to-install-the-wsus-server-role"></a>So installieren Sie die WSUS-Serverrolle

1.  Melden Sie sich an dem Server, auf dem Sie die WSUS-Serverrolle installieren möchten, mit einem Konto an, das Mitglied der Gruppe %%amp;quot;Lokale Administratoren%%amp;quot; ist.

2.  Klicken Sie in **Server-Manager**auf **Verwalten**, und klicken Sie dann auf **Rollen und Features hinzufügen**.

3.  Klicken Sie auf der Seite **Vorbereitung** auf **Weiter**.

4.  Vergewissern Sie sich, dass auf der Seite **Installationstyp auswählen** die Option **rollenbasierte oder featurebasierte Installation** ausgewählt ist, und klicken Sie auf **weiter**.

5.  Wählen Sie auf der Seite **Zielserver auswählen** aus, wo sich der Server befindet (in einem Server Pool oder auf einer virtuellen Festplatte). Wählen Sie nach der Auswahl des Orts den Server aus, auf dem Sie die WSUS-Serverrolle installieren möchten, und klicken Sie dann auf **Weiter**.

6.  Wählen Sie auf der Seite **Server Rollen auswählen** die Option **Windows Server Update Services**aus.  **Sollen für Windows Server Update Services erforderliche Features hinzugefügt werden?** wird geöffnet. Klicken Sie auf **Features hinzufügen**und dann auf **Weiter**.

7.  Auf der Seite **Features auswählen**. behalten Sie die Standardauswahl bei, und klicken Sie dann auf **weiter**.

    > [!IMPORTANT]
    > Für WSUS ist nur die Standardkonfiguration der Webserverrolle erforderlich. Wenn Sie beim Einrichten von WSUS aufgefordert werden, die Webserverrolle weiter zu konfigurieren, können Sie ohne Bedenken die Standardeinstellungen akzeptieren und die WSUS-Einrichtung fortsetzen.

8.  Klicken Sie auf der Seite **Windows Server Update Services** auf **Weiter**.

9. Behalten Sie auf der Seite **Rollendienste auswählen** die Standardauswahl bei, und klicken Sie auf **Weiter**.

    > [!TIP]
    > Sie müssen einen Datenbanktyp auswählen. Wenn die Datenbankoptionen alle deaktiviert (nicht ausgewählt) sind, treten bei Aufgaben im Anschluss an die Installation Fehler auf.

10. Geben Sie auf der Seite **Auswahl des Inhaltsspeicherorts** einen gültigen Speicherort zum Speichern der Updates ein. Sie können z. B. einen Ordner mit dem Namen "WSUS_database" im Stammverzeichnis von Laufwerks K: speziell für diesen Zweck erstellen und **k:\WSUS_database** als gültigen Speicherort eingeben.

11. Klicken Sie auf **Weiter**. Die Seite **Webserverrolle (IIS)** wird geöffnet. Überprüfen Sie die Informationen, und klicken Sie dann auf **Weiter**. Behalten **Sie in wählen Sie die Rollen Dienste aus, die für den Webserver (IIS) installiert werden müssen**die Standardeinstellungen bei, und klicken Sie dann auf **weiter**.

12. Überprüfen Sie die auf der Seite **Installationsauswahl bestätigen** ausgewählten Optionen, und klicken Sie dann auf **Installieren**. Der WSUS-Installations-Assistent ausgeführt wird. Dieser Vorgang kann einige Minuten dauern.

13. Klicken Sie nach Abschluss der WSUS-Installation im Fenster "Zusammenfassung" im Bereich **Installationsstatus** auf **Nachinstallationsaufgaben starten**. Der Text ändert sich und fordert Folgendes an: **Der Server wird konfiguriert. Bitte warten**. Wenn der Vorgang abgeschlossen ist, ändert sich der Text in: **Die Konfiguration wurde erfolgreich abgeschlossen**. Klicken Sie auf **Schließen**.

14. Überprüfen Sie, ob in **Server-Manager** eine Benachrichtigung erscheint, die Sie über einen erforderlichen Neustart informiert. Dies kann je nach installierter Serverrolle variieren. Falls ein Neustart erforderlich ist, starten Sie den Server neu, um die Installation abzuschließen.

> [!IMPORTANT]
> An diesem Punkt ist der Installationsvorgang abgeschlossen. damit WSUS jedoch funktionsfähig ist, müssen Sie mit [Schritt 2 fortfahren: Konfigurieren Sie WSUS @ no__t-0.

