---
title: Erstellen von OMA-DM-basierten VPNv2-Profilen für Windows 10-Geräte
description: 'Sie können eine von zwei Methoden zum Erstellen von OMA-DM-basierten VPNv2-Profilen verwenden. '
services: active-directory
ms.prod: windows-server
ms.technology: networking-ras
documentationcenter: ''
ms.assetid: ''
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2018
ms.author: pashort
author: shortpatti
ms.localizationpriority: medium
ms.reviewer: deverette
ms.openlocfilehash: 67d8a66552f77a66e1689989f412a844ef527880
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71404323"
---
# <a name="step-75-create-oma-dm-based-vpnv2-profiles-to-windows-10-devices"></a>Schritt 7.5. Erstellen von OMA-DM-basierten VPNv2-Profilen für Windows 10-Geräte

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows 10

- [**Vorher** Schritt 7.4. Bereitstellen von Stamm Zertifikaten für den bedingten Zugriff auf lokale Ad @ no__t-0
- [**Weiter** Erfahren Sie, wie der bedingte Zugriff für VPN funktioniert @ no__t-0

In diesem Schritt können Sie OMA-DM-basierte VPNv2-Profile mithilfe von InTune erstellen, um eine VPN-Geräte Konfigurationsrichtlinie bereitzustellen. Wenn Sie SCCM oder PowerShell-Skript zum Erstellen von VPNv2-Profilen verwenden möchten, finden Sie weitere Informationen unter [VPNv2 CSP Settings](https://docs.microsoft.com/windows/client-management/mdm/vpnv2-csp) . 

## <a name="managed-deployment-using-intune"></a>Verwaltete Bereitstellung mit InTune

Alles, was in diesem Abschnitt erläutert wird, ist die Mindestanforderung, um VPN mit bedingtem Zugriff zu arbeiten. Das Aufteilen von Tunneln, das Verwenden von WIP, das Erstellen von benutzerdefinierten InTune-Geräte Konfigurations Profilen zum Herstellen von autovpn oder das einmalige Anmelden (SSO) wird nicht behandelt. Integrieren Sie die folgenden Einstellungen in das VPN-Profil, das Sie zuvor unter [Schritt 5 erstellt haben. Konfigurieren von Windows 10-Client Always on VPN-Verbindungen @ no__t-0.  In diesem Beispiel integrieren wir Sie in das [Konfigurieren des VPN-Clients mithilfe der InTune](always-on-vpn/deploy/vpn-deploy-client-vpn-connections.md#configure-the-vpn-client-by-using-intune) -Richtlinie. 

**Setzung**

Der Windows 10-Client Computer wurde bereits mit einer VPN-Verbindung mithilfe von InTune konfiguriert.   


**Dringlichkeit**

1. Wählen Sie im Azure-Portal die Option **InTune**- > **Gerätekonfiguration** > -**Profilen** aus, und wählen Sie das VPN-Profil aus, das Sie zuvor unter [Konfigurieren des VPN-Clients mit InTune](always-on-vpn/deploy/vpn-deploy-client-vpn-connections.md#configure-the-vpn-client-by-using-intune)erstellt haben.
    
2. Wählen Sie im Richtlinien-Editor **Eigenschaften** > **Einstellungen** > **Basis-VPN**aus. Erweitern Sie den vorhandenen **EAP-XML** -Code so, dass er einen Filter enthält, der dem VPN-Client die Logik zum Abrufen des Aad-bedingten Zugriffs Zertifikats aus dem Zertifikat Speicher des Benutzers bietet, anstatt es zu erlauben, das erste Zertifikat zu verwenden. gefunden.

    >[!NOTE]
    >Ohne diesen Fehler könnte der VPN-Client das von der lokalen Zertifizierungsstelle ausgegebene Benutzerzertifikat abrufen, was zu einer fehlgeschlagenen VPN-Verbindung führt.

    ![InTune-Portal](../../media/Always-On-Vpn/intune-eap-xml.png)

3. Suchen Sie den Abschnitt, der mit **\</Akzeptanz Servername > \</eaptype >** endet, und fügen Sie die folgende Zeichenfolge zwischen diesen beiden Werten ein, um dem VPN-Client die Logik zur Auswahl des Aad-bedingten Zugriffs Zertifikats bereitzustellen:

    ```XML
    <TLSExtensions xmlns="http://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV2"><FilteringInfo xmlns="http://www.microsoft.com/provisioning/EapTlsConnectionPropertiesV3"><EKUMapping><EKUMap><EKUName>AAD Conditional Access</EKUName><EKUOID>1.3.6.1.4.1.311.87</EKUOID></EKUMap></EKUMapping><ClientAuthEKUList Enabled="true"><EKUMapInList><EKUName>AAD Conditional Access</EKUName></EKUMapInList></ClientAuthEKUList></FilteringInfo></TLSExtensions>
    ```

4. Wählen Sie das Blatt für den **bedingten Zugriff** aus, und schalten Sie den **bedingten Zugriff für diese VPN-Verbindung** auf **aktiviert**um.
   
   Wenn Sie diese Einstellung aktivieren, wird die Einstellung " **\<devicecompliance > \<aktivierte > true @ no__t-3/aktiviert >** " in der VPNv2-Profil-XML geändert.

    ![Bedingter Zugriff für Always on-VPN-Eigenschaften](../../media/Always-On-Vpn/vpn-conditional-access-azure-ad.png)

5. Wählen Sie **OK**.

6. Wählen Sie **Zuweisungen**unter einbeziehen aus, und wählen Sie **Gruppen auswählen, die**eingeschlossen werden sollen.

7. Wählen Sie die Gruppe **VPN-Benutzer** aus, die diese Richtlinie empfängt, und wählen Sie **Speichern**

    ![Obergrenze für automatische VPN-Benutzer-Zuweisungen](../../media/Always-On-Vpn/cap-for-auto-vpn-users-assignments.png)

## <a name="force-mdm-policy-sync-on-the-client"></a>Erzwingen der MDM-Richtlinien Synchronisierung auf dem Client

Wenn das VPN-Profil auf dem Client Gerät nicht angezeigt wird, können Sie unter Einstellungen @ no__t-0network & Internet @ no__t-1VPN erzwingen, dass die MDM-Richtlinie synchronisiert wird.

1. Melden Sie sich bei einem in die Domäne eingebundenen Client Computer als Mitglied der Gruppe " **VPN-Benutzer** " an.

2. Geben Sie im Startmenü **Account**ein, und drücken Sie die EINGABETASTE.

3. Klicken Sie im linken Navigationsbereich auf **Arbeits-oder Schul Konto zugreifen**.

4. Wählen Sie unter Arbeitsplatz oder Schule zugreifen **die Option verbunden mit < \domäne > MDM**aus, und wählen Sie dann **Info**aus.

5. Wählen Sie **Synchronisieren** aus, und vergewissern Sie sich, dass das VPN-Profil unter Settings @ no__t-1Network & Internet @ no__t-2vpn angezeigt wird.


## <a name="next-steps"></a>Nächste Schritte

Sie haben die Konfiguration des VPN-Profils für die Verwendung Azure AD bedingten Zugriffs abgeschlossen. 

|Wenn Sie möchten...  |Anzeige...  |
|---------|---------|
|Weitere Informationen zur Funktionsweise des bedingten Zugriffs mit VPNs  |[VPN und bedingter Zugriff](https://docs.microsoft.com/windows/access-protection/vpn/vpn-conditional-access): Auf dieser Seite finden Sie weitere Informationen zur Funktionsweise des bedingten Zugriffs mit VPNs.      |
|Weitere Informationen zu den erweiterten VPN-Features  |[Erweiterte VPN-Features](always-on-vpn/deploy/always-on-vpn-adv-options.md#advanced-vpn-features): Auf dieser Seite finden Sie Anleitungen zum Aktivieren von VPN-Datenverkehrs filtern, zum Konfigurieren automatischer VPN-Verbindungen mithilfe von App-Triggern und zum Konfigurieren von NPS für die ausschließliche Verwendung von VPN-Verbindungen von Clients mithilfe von Zertifikaten, die von Azure AD ausgestellt wurden.        |


## <a name="related-topics"></a>Verwandte Themen

- [VPNv2-CSP](https://msdn.microsoft.com/windows/hardware/commercialize/customize/mdm/vpnv2-csp):  Dieses Thema enthält eine Übersicht über VPNv2 CSP. Der VPNv2-Konfigurations Dienstanbieter ermöglicht dem MDM-Server, das VPN-Profil des Geräts zu konfigurieren.

- [Konfigurieren von Windows 10-Client Always on-VPN-Verbindungen](https://docs.microsoft.com/windows-server/remote/remote-access/vpn/always-on-vpn/deploy/vpn-deploy-client-vpn-connections): Dieses Thema enthält Informationen zu den profileXML-Optionen und-Schemas sowie zum Erstellen des profileXML-VPN. Nachdem Sie die Serverinfrastruktur eingerichtet haben, müssen Sie die Windows 10-Client Computer für die Kommunikation mit dieser Infrastruktur über eine VPN-Verbindung konfigurieren. 

- [Konfigurieren Sie den VPN-Client mithilfe von InTune](https://docs.microsoft.com/windows-server/remote/remote-access/vpn/always-on-vpn/deploy/vpn-deploy-client-vpn-connections#configure-the-vpn-client-by-using-intune): Dieses Thema enthält Informationen zum Bereitstellen von Windows 10-Remote Zugriff Always on VPN-Profilen. InTune verwendet nun Azure Ad Gruppen. Wenn Azure AD Connect die Gruppe "VPN-Benutzer" vom lokalen Standort zu "Azure AD" synchronisieren, ist es nicht erforderlich, den VPN-Client mit InTune zu konfigurieren.
