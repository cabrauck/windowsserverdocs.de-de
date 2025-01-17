---
title: Erweiterte Features von Always On VPN
description: Neben dem Bereitstellungs Szenario in dieser Bereitstellung können Sie weitere erweiterte VPN-Features hinzufügen, um die Sicherheit und Verfügbarkeit Ihrer VPN-Verbindung zu verbessern.
ms.assetid: 51a1ee61-3ffe-4f65-b8de-ff21903e1e74
ms.prod: windows-server
ms.technology: networking-ras
ms.topic: article
ms.date: 07/24/19
ms.author: pashort, v-tea
author: shortpatti
ms.localizationpriority: medium
ms.reviewer: deverette
ms.openlocfilehash: aee2f14d0d99fd453fa6fb1f3147a515ca57abb1
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71366911"
---
# <a name="advanced-features-of-always-on-vpn"></a>Erweiterte Features von Always on-VPN

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows 10

- [**Vorher** Erfahren Sie mehr über die Always on VPN-Technologie](../always-on-vpn-technology-overview.md)
- [**Weiter** Beginnen der Planung der Always on-VPN-Bereitstellung](always-on-vpn-deploy-planning.md)

Neben den bereitgestellten Bereitstellungs Szenarien können Sie weitere erweiterte VPN-Features hinzufügen, um die Sicherheit und Verfügbarkeit Ihrer VPN-Verbindung zu verbessern. Beispielsweise kann der VPN-Server diese Features verwenden, um sicherzustellen, dass der Verbindungs Client fehlerfrei ist, bevor er eine Verbindung zulässt.

## <a name="high-availability"></a>Hohe Verfügbarkeit

Im folgenden finden Sie zusätzliche Optionen für hohe Verfügbarkeit.

|Option  |Beschreibung  |
|---------|---------|
|Server Resilienz und Lastenausgleich     |In Umgebungen, die Hochverfügbarkeit erfordern oder eine große Anzahl von Anforderungen unterstützen, können Sie die Leistung und Resilienz des Remote Zugriffs steigern, indem Sie den Lastenausgleich zwischen mehreren Servern verwenden, auf denen der Netzwerk Richtlinien Server (Network Policy Server, NPS) ausgeführt wird. Remote Zugriffs Server-Clustering.<p>Verwandte Dokumente:<ul><li>[NPS-Proxy Server-Lastenausgleich](../../../../../networking/technologies/nps/nps-manage-proxy-lb.md)</li><li>[Bereitstellen des Remotezugriffs in einem Cluster](https://docs.microsoft.com/windows-server/remote/remote-access/ras/cluster/deploy-remote-access-in-cluster)</li></ul>        |
|Stabilität des geografischen Standorts     |Für die IP-basierte geolozierung können Sie globale Traffic Manager mit DNS in Windows Server 2016 verwenden. Um einen stabileren geografischen Lastenausgleich zu erreichen, können Sie Lösungen für den Lastenausgleich auf globaler Server wie Microsoft Azure Traffic Manager verwenden.<p>Verwandte Dokumente:<ul><li>[Übersicht über Traffic Manager](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview)</li><li>[Microsoft Azure Traffic Manager](https://azure.microsoft.com/services/traffic-manager)</li></ul>         |

## <a name="advanced-authentication"></a>Erweiterte Authentifizierung

Im folgenden finden Sie zusätzliche Authentifizierungs Optionen.

|Option  |Beschreibung  |
|---------|---------|
|Windows Hello for Business     |In Windows 10 ersetzt Windows Hello for Business Kenn Wörter durch eine starke zweistufige Authentifizierung auf PCs und mobilen Geräten. Diese Authentifizierung besteht aus einem neuen Typ von Benutzer Anmelde Informationen, der an ein Gerät gebunden ist und eine biometrische oder persönliche Identifikationsnummer (PIN) verwendet.<p>Der Windows 10-VPN-Client ist kompatibel mit Windows Hello for Business. Nachdem sich der Benutzer mit einer Geste anmeldet, verwendet die VPN-Verbindung das Windows Hello for Business-Zertifikat für die Zertifikat basierte Authentifizierung.<p>Verwandte Dokumente:<ul><li>[Windows Hello for Business](https://docs.microsoft.com/windows/access-protection/hello-for-business/hello-identity-verification)</li><li>Technische Fallstudie: [Aktivieren des Remote Zugriffs mit Windows Hello for Business in Windows 10](https://msdn.microsoft.com/library/mt728163.aspx)</li></ul>         |
|Azure Multi-Factor Authentication (MFA)     |Azure MFA verfügt über Cloud-und lokale Versionen, die Sie in den Windows-VPN-Authentifizierungsmechanismus integrieren können.<p>Weitere Informationen zur Funktionsweise dieses Mechanismus finden Sie unter [integrieren der RADIUS-Authentifizierung mit dem Azure Multi-Factor Authentication-Server](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-server-radius).         |

## <a name="advanced-vpn-features"></a>Erweiterte VPN-Features

Im folgenden finden Sie zusätzliche Optionen für erweiterte Funktionen.

|Option  |Beschreibung  |
|---------|---------|
|Filtern von Datenverkehr     |Wenn Sie die Auswahl der Anwendungen erzwingen müssen, auf die VPN-Clients zugreifen können, können Sie VPN-Datenverkehrs Filter aktivieren.<p>Weitere Informationen finden Sie unter [VPN-Sicherheitsfeatures](https://docs.microsoft.com/windows/access-protection/vpn/vpn-security-features).         |
|Durch Apps ausgelöstes VPN     |Sie können VPN-Profile so konfigurieren, dass Sie automatisch eine Verbindung herstellen, wenn bestimmte Anwendungen oder Anwendungs Typen gestartet werden.<p>Weitere Informationen zu dieser und anderen auslösenden Optionen finden Sie unter von [automatisch ausgelöste VPN-Profil Optionen](https://docs.microsoft.com/windows/access-protection/vpn/vpn-auto-trigger-profile).         |
|Bedingter VPN-Zugriff   |Bedingter Zugriff und Geräte Konformität können von verwalteten Geräten verlangt werden, dass Sie die Standards erfüllen, bevor Sie eine Verbindung mit dem VPN herstellen können. Eine der erweiterten Features für den bedingten VPN-Zugriff ermöglicht es Ihnen, die VPN-Verbindungen auf solche einzuschränken, auf denen das Client Authentifizierungszertifikat die OID "Aad Conditional Access" von **1.3.6.1.4.1.311.87**enthält.<p>Um die VPN-Verbindungen einzuschränken, müssen Sie die folgenden Schritte ausführen:<ol><li>Öffnen Sie auf dem NPS-Server das Snap-in " **Netzwerk Richtlinien Server** ".</li><li>Erweitern Sie **Richtlinien** > **Netzwerk Richtlinien**.</li><li>Klicken Sie mit der rechten Maustaste auf die Netzwerk Richtlinie **VPN-Verbindungen (virtuelles privates Netzwerk)** , und wählen Sie **Eigenschaften**.</li><li>Wählen Sie die Registerkarte **Einstellungen** aus.</li><li>Wählen Sie **Hersteller spezifisch**aus, und klicken Sie dann auf **Hinzufügen**.</li><li>Wählen Sie die Option **Allowed-Certificate-OID** aus, und klicken Sie dann auf **Hinzufügen**.</li><li>Fügen Sie die Aad Conditional Access OID of **1.3.6.1.4.1.311.87** als Attribut Wert ein, und wählen Sie dann zweimal **OK** aus.</li><li>Wählen Sie **Schließen**aus, und klicken Sie dann auf **anwenden**.<p>Nachdem Sie diese Schritte ausgeführt haben, schlägt die Verbindung fehl, wenn VPN-Clients versuchen, eine Verbindung mit einem anderen Zertifikat als dem kurzlebigen cloudzertifikat herzustellen.</li></ol>Weitere Informationen zum bedingten Zugriff finden Sie unter [VPN und bedingter Zugriff](https://docs.microsoft.com/windows/access-protection/vpn/vpn-conditional-access).   |


---
## <a name="blocking-vpn-clients-that-use-revoked-certificates"></a>Blockieren von VPN-Clients, die widerrufene Zertifikate verwenden
  
Nachdem Sie Updates installiert haben, kann der RRAS-Server die Zertifikat Sperrung für VPNs erzwingen, die IKEv2-und Computer Zertifikate für die Authentifizierung verwenden, z. b. Geräte Tunnel-Always-on-VPNs. Dies bedeutet, dass der RRAS-Server für solche VPNs VPN-Verbindungen zu Clients verweigern kann, die versuchen, ein gesperrtes Zertifikat zu verwenden.

**Verfügbarkeit**

In der folgenden Tabelle sind die Versionen aufgeführt, die die Fixes für jede Windows-Version enthalten.

|Version des Betriebssystems |Version  |
|---------|---------|
|Windows Server, Version 1903  |[KB4501375](https://support.microsoft.com/help/4501375/windows-10-update-kb4501375) |
|Windows Server 2019<br />Windows Server, Version 1809  |[KB4505658](https://support.microsoft.com/help/4505658/windows-10-update-kb4505658)  |
|Windows Server, Version 1803  |[KB4507466](https://support.microsoft.com/help/4507466/windows-10-update-kb4507466)  |
|Windows Server, Version 1709  |[KB4507465](https://support.microsoft.com/help/4507465/windows-10-update-kb4507465)  |
|Windows Server 2016, Version 1607  |[KB4503294](https://support.microsoft.com/help/4503294/windows-10-update-kb4503294) |

**Vorgehensweise beim Konfigurieren der Voraussetzungen** 

1. Installieren Sie die Windows-Updates, sobald Sie verfügbar werden.
1. Stellen Sie sicher, dass alle VPN-Client-und RRAS-Server Zertifikate, die Sie verwenden, über CDP-Einträge verfügen und dass der RRAS-Server die entsprechenden CRLs erreichen kann.
1. Verwenden Sie auf dem RRAS-Server das PowerShell-Cmdlet **Set-vpnauthprotocol** , um den Parameter **rootcertificatenametoaccept** zu konfigurieren.<br /><br />
   Im folgenden Beispiel werden die zu diesem Zweck aufgeführten Befehle aufgelistet. Im Beispiel stellt CN = die Stamm Zertifizierungsstelle von " **CN =** " den Distinguished Name der Stamm Zertifizierungsstelle dar. 
   ``` powershell
   $cert1 = ( Get-ChildItem -Path cert:LocalMachine\root | Where-Object -FilterScript { $_.Subject -Like "*CN=Contoso Root Certification Authority*" } )
   Set-VpnAuthProtocol -RootCertificateNameToAccept $cert1 -PassThru
   ```
**Konfigurieren des RRAS-Servers, um die Zertifikat Sperrung für VPN-Verbindungen zu erzwingen, die auf IKEv2-Computer Zertifikaten basieren**

1. Führen Sie in einem Eingabe Aufforderungs Fenster den folgenden Befehl aus: 
   ```
   reg add HKLM\SYSTEM\CurrentControlSet\Services\RemoteAccess\Parameters\Ikev2 /f /v CertAuthFlags /t REG_DWORD /d "4"
   ```

1. Starten Sie den **Routing-und RAS-** Dienst neu.
  
Um die Zertifikat Sperrung für diese VPN-Verbindungen zu deaktivieren, legen Sie **certauthflags = 2** fest, oder entfernen Sie den Wert **certauthflags** , und starten Sie dann den **Routing-und** RAS-Dienst neu. 

**Widerrufen eines VPN-Client Zertifikats für eine VPN-Verbindung, die auf einem IKEv2-Computer Zertifikat basiert**
1. Widerrufen Sie das VPN-Client Zertifikat von der Zertifizierungsstelle.
1. Veröffentlichen Sie eine neue CRL von der Zertifizierungsstelle.
1. Öffnen Sie auf dem RRAS-Server ein Administrator Eingabe Aufforderungs Fenster, und führen Sie dann die folgenden Befehle aus:
   ```
   certutil -urlcache * delete
   certutil -setreg chain\ChainCacheResyncFiletime @now
   ```

**Überprüfen, ob die Zertifikat Sperrung für Zertifikat basierte VPN-Verbindungen auf IKEv2-Computern funktioniert**  
>[!Note]  
> Bevor Sie dieses Verfahren verwenden, stellen Sie sicher, dass Sie das Betriebs Ereignisprotokoll CAPI2 aktivieren.
1. Führen Sie die vorherigen Schritte aus, um ein VPN-Client Zertifikat aufzuheben.
1. Versuchen Sie, mithilfe eines Clients, der über das gesperrte Zertifikat verfügt, eine Verbindung mit dem VPN herzustellen. Der RRAS-Server sollte die Verbindung ablehnen und eine Meldung wie "die Anmelde Informationen für die IKE-Authentifizierung sind nicht zulässig" anzeigen.
1. Öffnen Sie auf dem RRAS-Server Ereignisanzeige, und navigieren Sie zu **Anwendungs-und Dienst Protokolle/Microsoft/Windows/CAPI2**. 
1. Suchen Sie nach einem Ereignis, das die folgenden Informationen enthält:
   * Protokoll Name: **Microsoft-Windows-CAPI2/Operational Microsoft-Windows-CAPI2/Operational**
   * Ereignis-ID: **41** 
   * Das Ereignis enthält den folgenden Text: **Subject = "*Client FQDN*"** (*Client-FQDN* steht für den voll qualifizierten Domänen Namen des Clients, der über das gesperrte Zertifikat verfügt). 

   Das-Feld der Ereignisdaten sollte einschließen, dass **das Zertifikat gesperrt ist.** **<Result>** Sehen Sie sich beispielsweise die folgenden Ausschnitte eines Ereignisses an:
   ```xml
   Log Name:      Microsoft-Windows-CAPI2/Operational Microsoft-Windows-CAPI2/Operational  
   Source:        Microsoft-Windows-CAPI2  
   Date:          5/20/2019 1:33:24 PM  
   Event ID:      41  
   ...  
   Event Xml:
   <Event xmlns="http://schemas.microsoft.com/win/2004/08/events/event">
    <UserData>  
     <CertVerifyRevocation>  
      <Certificate fileRef="C97AE73E9823E8179903E81107E089497C77A720.cer" subjectName="client01.corp.contoso.com" />  
      <IssuerCertificate fileRef="34B1AE2BD868FE4F8BFDCA96E47C87C12BC01E3A.cer" subjectName="Contoso Root Certification Authority" />
      ...
      <Result value="80092010">The certificate is revoked.</Result>
     </CertVerifyRevocation>
    </UserData>
   </Event>
   ```

---
## <a name="additional-protection"></a>Zusätzlicher Schutz

### <a name="trusted-platform-module-tpm-key-attestation"></a>TPM-Schlüssel Nachweis (Trusted Platform Module)

Ein Benutzerzertifikat, das über einen TPM-geprüften Schlüssel verfügt, bietet eine höhere Sicherheitsgarantie, die durch nicht Exportierbarkeit, Anti-hammerung und Isolation der von TPM bereitgestellten Schlüssel gesichert wird.

Weitere Informationen zum TPM-Schlüssel Nachweis in Windows 10 finden Sie unter [TPM Key Nachweis](https://docs.microsoft.com/windows-server/identity/ad-ds/manage/component-updates/tpm-key-attestation).

## <a name="next-step"></a>Nächster Schritt

[Beginnen Sie mit der Planung der Always on VPN-Bereitstellung](always-on-vpn-deploy-planning.md): Bevor Sie die Remote Zugriffs-Server Rolle auf dem Computer installieren, den Sie als VPN-Server verwenden möchten, führen Sie die folgenden Aufgaben aus. Nach der entsprechenden Planung können Sie Always on VPN bereitstellen und optional den bedingten Zugriff für VPN-Konnektivität mithilfe Azure AD konfigurieren.  

## <a name="related-topics"></a>Verwandte Themen
- [NPS-Proxy Server-Lastenausgleich](../../../../../networking/technologies/nps/nps-manage-proxy-lb.md): RADIUS-Clients (Remote Authentication Dial-in User Service), die Netzwerk Zugriffs Server wie VPN-Server (virtuelles privates Netzwerk) und drahtlos Zugriffspunkte sind, erstellen Verbindungsanforderungen und senden Sie an RADIUS-Server wie z. b. NPS. In einigen Fällen kann ein NPS-Server zu viele Verbindungsanforderungen gleichzeitig empfangen, was zu einer Beeinträchtigung der Leistung oder einer Überlastung führt.

- [Übersicht über Traffic Manager](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview): Dieses Thema bietet einen Überblick über Azure Traffic Manager, mit dem Sie die Verteilung von Benutzer Datenverkehr für Dienst Endpunkte steuern können. Traffic Manager verwendet die Domain Name System (DNS), um Client Anforderungen auf der Grundlage einer Datenverkehrs Routing-Methode und der Integrität der Endpunkte an den am besten geeigneten Endpunkt weiterzuleiten. 

- [Windows Hello for Business](https://docs.microsoft.com/windows/access-protection/hello-for-business/hello-identity-verification): Dieses Thema enthält die Voraussetzungen, z. b. reine Cloud-bereit Stellungen und Hybrid Bereitstellungen.  Außerdem werden in diesem Thema häufig gestellte Fragen zu Windows Hello for Business aufgeführt.

- [Technische Fallstudie: Aktivieren des Remote Zugriffs mit Windows Hello for Business in Windows](https://msdn.microsoft.com/library/mt728163.aspx)10: In dieser technischen Fallstudie erfahren Sie, wie Microsoft den Remote Zugriff mit Windows Hello for Business implementiert.  Bei Windows Hello for Business handelt es sich um einen privaten/öffentlichen oder Zertifikat basierten Authentifizierungs Ansatz für Unternehmen und Consumer, die über die Kenn Wörter hinausgehen. Diese Form der Authentifizierung basiert auf Schlüsselpaar-Anmelde Informationen, die Kenn Wörter ersetzen können und gegen Verstöße, Dieb zierungen und Phishing verstoßen. 

- [Integrieren der RADIUS-Authentifizierung mit dem Azure Multi-Factor Authentication-Server](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication-get-started-server-radius): Dieses Thema führt Sie durch das Hinzufügen und Konfigurieren einer RADIUS-Client Authentifizierung mit dem Azure Multi-Factor Authentication-Server. RADIUS ist ein Standardprotokoll zum Annehmen und Verarbeiten von Authentifizierungsanforderungen. Der Azure Multi-Factor Authentication-Server kann als RADIUS-Server fungieren. 

- [VPN-Sicherheitsfeatures](https://docs.microsoft.com/windows/access-protection/vpn/vpn-security-features): Dieses Thema enthält Richtlinien für VPN-Sicherheit für das Sperren von VPN, Windows Information Protection-Integration (WIP) mit VPN und Datenverkehrs Filter. 

- [Automatisch ausgelöste VPN-Profil Optionen](https://docs.microsoft.com/windows/access-protection/vpn/vpn-auto-trigger-profile): Dieses Thema enthält die automatisch ausgelösten VPN-Profil Optionen, z. b. app-Trigger, namensbasierte Trigger und Always on.

- [VPN und bedingter Zugriff](https://docs.microsoft.com/windows/access-protection/vpn/vpn-conditional-access): Dieses Thema bietet einen Überblick über die cloudbasierte Plattform für den bedingten Zugriff, mit der Sie eine Geräte Kompatibilitäts Option für Remote Clients bereitstellen können. Beim bedingten Zugriff handelt es sich um ein richtlinienbasiertes Auswertungsmodul, mit dem Sie Zugriffsregeln für alle mit Azure Active Directory (Azure AD) verknüpften Anwendungen erstellen können. 

- [TPM-Schlüssel](https://docs.microsoft.com/windows-server/identity/ad-ds/manage/component-updates/tpm-key-attestation)Nachweis: In diesem Thema erhalten Sie einen Überblick über Trusted Platform Module (TPM) und die Schritte zum Bereitstellen von TPM-Schlüssel Nachweis. Außerdem finden Sie Informationen zur Problembehandlung und zu den Schritten, um Probleme zu beheben.
