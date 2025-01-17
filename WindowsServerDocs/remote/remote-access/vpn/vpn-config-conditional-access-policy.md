---
title: Konfigurieren der Richtlinie für bedingten Zugriff
description: Nachdem ein Stamm Zertifikat erstellt wurde, löst die "VPN-Konnektivität" die Erstellung der cloudanwendung "VPN-Server" im Mandanten des Kunden aus.
services: active-directory
ms.prod: windows-server
ms.technology: networking-ras
documentationcenter: ''
ms.assetid: ''
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2018
ms.author: pashort
author: shortpatti
ms.localizationpriority: medium
ms.reviewer: deverette
ms.openlocfilehash: 22983c085f2b9d9e7e16810e25c6fa50111f9fa6
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71404347"
---
# <a name="step-73-configure-the-conditional-access-policy"></a>Schritt 7.3. Konfigurieren der Richtlinie für bedingten Zugriff

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows 10

- [**Vorher** Schritt 7.2. Erstellen von Stammzertifikaten für die VPN-Authentifizierung mit Azure AD](vpn-create-root-cert-for-vpn-auth-azure-ad.md)
- [**Weiter** Schritt 7.4. Bereitstellen von Stamm Zertifikaten für den bedingten Zugriff auf lokale Ad @ no__t-0

In diesem Schritt konfigurieren Sie die Richtlinie für bedingten Zugriff für VPN-Konnektivität. Wenn das erste Stamm Zertifikat auf dem Blatt "VPN-Konnektivität" erstellt wird, wird automatisch eine "VPN Server"-cloudanwendung im Mandanten erstellt.

Erstellen Sie eine Richtlinie für bedingten Zugriff, die der Gruppe "VPN-Benutzer" zugewiesen **ist, und legen Sie den**Bereich der **Cloud-App**

- **Benutzer**: VPN-Benutzer
- **Cloud-App**: VPN-Server
- **Grant (Zugriffs Steuerung)** : "Multi-Factor Authentication erforderlich". Andere Steuerelemente können bei Bedarf verwendet werden.

**Dringlichkeit** In diesem Schritt wird die Erstellung der grundlegendsten Richtlinie für den bedingten Zugriff behandelt.  Wenn gewünscht, können zusätzliche Bedingungen und Steuerelemente verwendet werden.


1. Wählen Sie auf der Seite **bedingter Zugriff** auf der Symbolleiste am oberen Rand die Option **Hinzufügen**aus.

    ![Wählen Sie auf der Seite zum bedingten Zugriff hinzufügen](../../media/Always-On-Vpn/07.png)

2. Geben Sie auf der Seite **neu** im Feld **Name** einen Namen für die Richtlinie ein. Geben Sie z. b. **VPN-Richtlinie**ein.

    ![Name der Richtlinie auf der Seite für bedingten Zugriff hinzufügen](../../media/Always-On-Vpn/08.png)

3. Wählen Sie im Abschnitt **Zuweisung** die Option **Benutzer und Gruppen**aus.

    ![Benutzer und Gruppen auswählen](../../media/Always-On-Vpn/09.png)

4. Führen Sie auf der Seite **Benutzer und Gruppen** die folgenden Schritte aus:

    ![Test Benutzer auswählen](../../media/Always-On-Vpn/10.png)

    a. Wählen Sie **Benutzer und Gruppen auswählen**aus.

    b. Wählen Sie **auswählen**aus.

    c. Wählen Sie auf der Seite **auswählen** die Gruppe **VPN-Benutzer** aus, und wählen Sie dann **auswählen**aus.

    d. Wählen Sie auf der Seite **Benutzer und Gruppen** die Option **abgeschlossen**aus.

5. Führen Sie auf der Seite **neu** die folgenden Schritte aus:

    ![Cloud-apps auswählen](../../media/Always-On-Vpn/11.png)

    a. Wählen Sie im Abschnitt **Zuweisungen** die Option **Cloud-apps**aus.

    b. Wählen Sie auf der Seite **Cloud-apps** die Option **apps auswählen**aus.

    d. Wählen Sie **VPN-Server**aus.

6.  Wählen Sie auf der Seite **neu** im Abschnitt Steuer **Elemente** die **Option erteilen aus**, um die Seite **erteilen** zu öffnen.

    !["Grant" auswählen](../../media/Always-On-Vpn/13.png)

7.  Führen Sie auf der Seite **Grant** die folgenden Schritte aus:

    ![Wählen Sie Multi-Factor Authentication erforderlich aus.](../../media/Always-On-Vpn/14.png)

    a. Wählen Sie **Multi-Factor Authentication erforderlich**aus.

    b. Wählen Sie **auswählen**aus.

8.  Wählen Sie auf der Seite **neu** unter **Richtlinie aktivieren**die Option **ein aus.**

    ![Richtlinie aktivieren](../../media/Always-On-Vpn/15.png)

9.  Wählen Sie auf der Seite **neu** die Option **Erstellen**aus.


## <a name="next-steps"></a>Nächste Schritte
[Schritt 7.4: Bereitstellen von Stamm Zertifikaten für den bedingten Zugriff für lokale Ad @ no__t-0: In diesem Schritt stellen Sie das Stamm Zertifikat für den bedingten Zugriff als vertrauenswürdiges Stamm Zertifikat für die VPN-Authentifizierung in Ihrem lokalen AD bereit.
