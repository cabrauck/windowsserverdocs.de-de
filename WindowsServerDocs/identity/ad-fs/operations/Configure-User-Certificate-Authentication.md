---
ms.assetid: 1ea2e1be-874f-4df3-bc9a-eb215002da91
title: Konfigurieren AD FS Unterstützung für die Benutzerzertifikat Authentifizierung
description: ''
author: jenfieldmsft
ms.author: billmath
manager: samueld
ms.date: 01/18/2018
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 82d826d41e95be18fba689706025ce6f5195f726
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407667"
---
# <a name="configuring-ad-fs-for-user-certificate-authentication"></a>Konfigurieren von AD FS für die Benutzerzertifikat Authentifizierung

Die Benutzerzertifikat Authentifizierung wird hauptsächlich in zwei Anwendungsfällen verwendet.
* Benutzer verwenden Smartcards, um sich bei Ihrem AD FS System anzumelden.
* Benutzer verwenden Zertifikate, die für mobile Geräte bereitgestellt werden.


## <a name="prerequisites"></a>Erforderliche Komponenten
1) Bestimmen Sie den Modus der AD FS Benutzerzertifikat Authentifizierung, die Sie aktivieren möchten, mithilfe eines der Modi, die in [diesem Artikel](ad-fs-support-for-alternate-hostname-binding-for-certificate-authentication.md) beschrieben werden.
2) Stellen Sie sicher, dass die Vertrauenskette des Benutzer Zertifikats installiert ist & von allen AD FS-und WAP-Servern einschließlich aller zwischen Zertifizierungsstellen als vertrauenswürdig eingestuft. Dies erfolgt in der Regel über das Gruppenrichtlinien Objekt auf AD FS/WAP-Servern.
3)  Stellen Sie sicher, dass das Stamm Zertifikat der Vertrauenskette für ihre Benutzerzertifikate im NTAuth-Speicher in Active Directory
4) Wenn Sie AD FS im alternativen Zertifikat Authentifizierungsmodus verwenden, stellen Sie sicher, dass Ihre AD FS-und WAP-Server über SSL-Zertifikate verfügen, die den AD FS Hostnamen enthalten, dem das Präfix "certauth" vorangestellt ist, z. b. "certauth.fs.contoso.com" durch die Firewall
5) Wenn Sie die Zertifikat Authentifizierung über das Extranet verwenden, stellen Sie sicher, dass mindestens eine AIA und mindestens ein CDP-oder OCSP-Speicherort aus der Liste, die in ihren Zertifikaten angegeben ist, über das Internet zugänglich sind.
6) Außerdem muss für die Azure AD Zertifikat Authentifizierung für Exchange ActiveSync-Clients das Client Zertifikat über die Routing fähige e-Mail-Adresse des Benutzers in Exchange Online verfügen, entweder mit dem Prinzipal Namen oder dem Wert des RFC822-namens im Feld "alternativer Antragsteller Name". (Azure Active Directory ordnet den RFC822-Wert dem Proxy Adress Attribut im Verzeichnis zu.)


## <a name="configure-ad-fs-for-user-certificate-authentication"></a>Konfigurieren von AD FS für die Benutzerauthentifizierung Zertifikat  

Aktivieren Sie die Authentifizierung von Benutzer Zertifikaten als Intranet-oder Extranet-Authentifizierungsmethode in AD FS mithilfe der AD FS Management Console oder des PowerShell- `Set-AdfsGlobalAuthenticationPolicy`Cmdlets.

Wenn Sie AD FS für die Azure AD Zertifikat Authentifizierung konfigurieren, stellen Sie sicher, dass Sie die [Azure AD Einstellungen](https://docs.microsoft.com/azure/active-directory/active-directory-certificate-based-authentication-get-started#step-2-configure-the-certificate-authorities) und die [AD FS Anspruchs Regeln](https://docs.microsoft.com/azure/active-directory/active-directory-certificate-based-authentication-ios#requirements) konfiguriert haben, die für den Zertifikat Aussteller und die Seriennummer erforderlich sind.

Außerdem gibt es einige optionale Aspekte.
- Wenn Sie zusätzlich zu EKU (Anspruchstyp https://schemas.microsoft.com/2012/12/certificatecontext/extension/eku) ) Ansprüche basierend auf Zertifikat Feldern und Erweiterungen verwenden möchten, konfigurieren Sie zusätzliche Anspruchs Pass-Through-Regeln für die Active Directory Anspruchs Anbieter-Vertrauensstellung.  Im folgenden finden Sie eine umfassende Liste der verfügbaren Zertifikat Ansprüche.  
- Wenn Sie den Zugriff basierend auf dem Zertifikattyp einschränken müssen, können Sie die zusätzlichen Eigenschaften des Zertifikats in AD FS Ausstellungs Autorisierungs Regeln für die Anwendung verwenden. Häufige Szenarien sind "nur Zertifikate lassen, die von einem MDM-Anbieter bereitgestellt werden" oder "nur Smartcardzertifikate zulassen".
- Konfigurieren Sie zugelassene Zertifizierungsstellen für Client Zertifikate mithilfe der Anleitung unter "Verwaltung vertrauenswürdiger Aussteller für die Client Authentifizierung" in [diesem Artikel](https://technet.microsoft.com/library/dn786429(v=ws.11).aspx).
- Sie sollten die Anmelde Seiten ggf. so ändern, dass Sie den Anforderungen der Endbenutzer bei der Zertifikat Authentifizierung entsprechen. Häufige Fälle: (a) ändern Sie die Anmeldung mit Ihrem X509-Zertifikat, um Endbenutzer freundlicher zu werden.

## <a name="configure-seamless-certificate-authentication-for-chrome-browser-on-windows-desktops"></a>Konfigurieren der nahtlosen Zertifikat Authentifizierung für den Chrome-Browser auf Windows-Desktops
Wenn auf dem Computer mehrere Benutzerzertifikate (z. b. Wi-Fi-Zertifikate) vorhanden sind, die den Zweck der Client Authentifizierung erfüllen, fordert der Chrome-Browser auf dem Windows-Desktop den Benutzer auf, das richtige Zertifikat auszuwählen. Dies kann für den Endbenutzer verwirrend sein. Um diese Funktion zu optimieren, können Sie eine Richtlinie für Chrome festlegen, um das richtige Zertifikat automatisch auszuwählen, um die Benutzer Leistung zu verbessern. Diese Richtlinie kann manuell festgelegt werden, indem Sie eine Registrierungs Änderung vornehmen oder automatisch über das Gruppenrichtlinien Objekt konfiguriert wird (um die Registrierungsschlüssel festzulegen). Dies erfordert, dass Ihre Benutzer Client Zertifikate für die Authentifizierung bei AD FS über unterschiedliche Aussteller anderer Anwendungsfälle verfügen. 

Weitere Informationen zum Konfigurieren dieses für Chrome finden Sie unter diesem [Link](http://www.chromium.org/administrators/policy-list-3#AutoSelectCertificateForUrls).  


## <a name="troubleshoot-certificate-authentication"></a>Behandeln von Problemen mit der Zertifikat Authentifizierung
Dieses Dokument konzentriert sich auf Probleme, die häufig auftreten, wenn AD FS für die Zertifikat Authentifizierung für Benutzer konfiguriert ist. 

### <a name="check-if-certificate-trusted-issuers-is-configured-properly-in-all-the-ad-fswap-servers"></a>Überprüfen Sie, ob Zertifikat vertrauenswürdige Aussteller ordnungsgemäß für alle AD FS/WAP-Server konfiguriert sind.
*Häufiges Symptom: HTTP 204 "kein Inhalt von HTTPS\://certuath.ADFS.contoso.com"*

AD FS verwendet das zugrunde liegende Windows-Betriebssystem, um den Besitz des Benutzer Zertifikats zu belegen und sicherzustellen, dass es mit einem vertrauenswürdigen Aussteller durch Überprüfung der Zertifikats Vertrauenskette übereinstimmt. Um dem vertrauenswürdigen Aussteller zu entsprechen, müssen Sie sicherstellen, dass alle Stamm-und zwischen Zertifizierungsstellen im Speicher der lokalen Computer Zertifizierungsstellen als vertrauenswürdige Aussteller konfiguriert sind. Verwenden Sie das [AD FS Diagnostic Analyzer-Tool](https://adfshelp.microsoft.com/DiagnosticsAnalyzer/Analyze), um dies automatisch zu überprüfen. Das Tool fragt alle Server ab und stellt sicher, dass die richtigen Zertifikate ordnungsgemäß bereitgestellt werden. 
1)  Laden Sie das Tool gemäß den Anweisungen im obigen Link herunter, und führen Sie es aus.
2)  Hochladen der Ergebnisse und Überprüfen von Fehlern

### <a name="check-if-certificate-authentication-is-enabled-in-the-ad-fs-authentication-policy"></a>Überprüfen Sie, ob die Zertifikat Authentifizierung in der AD FS Authentifizierungs Richtlinie aktiviert ist.
AD FS aktiviert standardmäßig die Zertifikat Authentifizierung nicht. Informationen zum Aktivieren der Zertifikat Authentifizierung finden Sie am Anfang dieses Dokuments. 

### <a name="check-if-certificate-authentication-is-enabled-in-the-ad-fs-authentication-policy"></a>Überprüfen Sie, ob die Zertifikat Authentifizierung in der AD FS Authentifizierungs Richtlinie aktiviert ist.
AD FS führt die Benutzerzertifikat Authentifizierung standardmäßig an Port 49443 mit dem gleichen Hostnamen wie AD FS aus ( `adfs.contoso.com`z. b.). Sie können auch AD FS für die Verwendung von Port 443 (HTTPS-Standardport) mithilfe der alternativen SSL-Bindung konfigurieren. Die in dieser Konfiguration verwendete URL ist `certauth.<adfs-farm-name>` jedoch (z. b. `certauth.contoso.com`). Weitere Informationen finden Sie unter [diesem Link](ad-fs-support-for-alternate-hostname-binding-for-certificate-authentication.md) . Der häufigste Fall der Netzwerk Konnektivität besteht darin, dass eine Firewall falsch konfiguriert wurde und den Datenverkehr für die Authentifizierung von Benutzer Zertifikaten blockiert oder beeinträchtigt. Normalerweise wird ein leerer Bildschirm oder ein 500-Server Fehler angezeigt, wenn dieses Problem auftritt. 
1)  Beachten Sie den Hostnamen und den Port, die Sie in konfiguriert haben AD FS
2)  Stellen Sie sicher, dass jede Firewall vor AD FS oder webanwendungsproxy (WAP) so `hostname:port` konfiguriert ist, dass Sie die Kombination für Ihre AD FS Farm zulässt. Sie müssen sich an Ihren Netzwerktechniker wenden, um diesen Schritt auszuführen. 

### <a name="check-certificate-revocation-list-connectivity"></a>Überprüfen der Konnektivität der Zertifikat Sperr Liste
Zertifikat Sperr Listen (CRL) sind Endpunkte, die in das Benutzerzertifikat codiert werden, um Lauf Zeit Sperr Prüfungen auszuführen. Wenn beispielsweise ein Gerät gestohlen wird, das ein Zertifikat enthält, kann ein Administrator das Zertifikat der Liste der gesperrten Zertifikate hinzufügen. Bei jedem Endpunkt, der dieses Zertifikat zuvor akzeptiert hat, tritt nun die Authentifizierung ein.

Jeder AD FS-und WAP-Server muss den CRL-Endpunkt erreichen, um zu überprüfen, ob das Zertifikat, das ihm präsentiert wurde, weiterhin gültig ist und nicht widerrufen wurde. Die CRL-Überprüfung kann über HTTPS, http, LDAP oder über OCSP (Online Certificate Status-Protokoll) erfolgen. Wenn AD FS/WAP-Server den Endpunkt nicht erreichen können, tritt bei der Authentifizierung ein Fehler auf. Führen Sie die folgenden Schritte aus, um das Problem zu beheben. 
1) Informieren Sie sich bei Ihrem PKI-Techniker, welche CRL-Endpunkte zum Widerrufen von Benutzer Zertifikaten von Ihrem PKI-System verwendet werden. 
2)  Stellen Sie auf jedem AD FS/WAP-Server sicher, dass die CRL-Endpunkte über das verwendete Protokoll (in der Regel HTTPS oder http) erreichbar sind.
3)  Aktivieren Sie für die erweiterte Überprüfung die [CAPI2-Ereignisprotokollierung](https://blogs.msdn.microsoft.com/benjaminperkins/2013/09/30/enable-capi2-event-logging-to-troubleshoot-pki-and-ssl-certificate-issues/) auf jedem AD FS/WAP-Server
4) Überprüfen Sie die Ereignis-ID 41 (Sperrung überprüfen) in den CAPI2-Betriebs Protokollen.
5) Überprüfen auf`‘\<Result value="80092013"\>The revocation function was unable to check revocation because the revocation server was offline.\</Result\>'`

***Tipp***: Sie können eine einzelne AD FS oder einen WAP-Server für eine einfachere Problembehandlung konfigurieren, indem Sie die DNS-Auflösung (Hostdatei unter Windows) so konfigurieren, dass Sie auf einen bestimmten Server verweist Dies ermöglicht es Ihnen, die Ablauf Verfolgung für einen Server zu aktivieren. 

### <a name="check-if-this-is-a-server-name-indication-sni-issue"></a>Überprüfen, ob es sich um ein Servernamensanzeige-Problem (SNI) handelt
AD FS erfordert, dass das Client Gerät (oder die Browser) und die Load Balancer SNI unterstützen. Einige Client Geräte (in der Regel ältere Android-Versionen) unterstützen SNI möglicherweise nicht. Darüber hinaus unterstützen Lasten Ausgleichs Module ggf. keine SNI oder wurden nicht für SNI konfiguriert. In diesen Fällen werden Benutzer Zertifizierungs Fehler wahrscheinlich angezeigt. 
1)  Arbeiten Sie mit Ihrem Netzwerktechniker zusammen, um sicherzustellen, dass die Load Balancer für AD FS/WAP SNI unterstützt.
2)  Falls SNI nicht unterstützt werden kann AD FS eine Problem Umgehung, indem Sie die folgenden Schritte ausführen:
    *   Öffnen eines Eingabe Aufforderungs Fensters mit erhöhten Rechten auf dem primären AD FS Server
    *   Eingeben```Netsh http show sslcert```
    *   Kopieren Sie die Anwendungs-GUID und den Zertifikat Hash des Verbund Dienstanbieter.
    *   Eingeben`netsh http add sslcert ipport=0.0.0.0:{your_certauth_port} certhash={your_certhash} appid={your_applicaitonGUID}`

### <a name="check-if-the-client-device-has-been-provisioned-with-the-certificate-correctly"></a>Überprüfen Sie, ob das Client Gerät ordnungsgemäß mit dem Zertifikat bereitgestellt wurde.
Möglicherweise stellen Sie fest, dass einige Geräte ordnungsgemäß funktionieren, aber andere Geräte nicht. In diesem Fall ist dies normalerweise darauf zurückzuführen, dass das Benutzerzertifikat auf dem Client Gerät nicht ordnungsgemäß bereitgestellt wurde. Führen Sie die folgenden Schritte aus. 
1)  Wenn das Problem für ein Android-Gerät spezifisch ist, besteht das häufigste Problem darin, dass die Zertifikatskette auf dem Android-Gerät nicht vollständig vertrauenswürdig ist.  Wenden Sie sich an Ihren MDM-Anbieter, um sicherzustellen, dass das Zertifikat ordnungsgemäß bereitgestellt wurde und die gesamte Kette auf dem Android-Gerät vollständig vertrauenswürdig ist. 
2)  Wenn das Problem für ein Windows-Gerät spezifisch ist, überprüfen Sie, ob das Zertifikat ordnungsgemäß bereitgestellt wurde, indem Sie den Windows-Zertifikat Speicher für den angemeldeten Benutzer (nicht System/Computer) überprüfen.
3)  Exportieren Sie das Client Benutzerzertifikat in die CER-Datei, und führen Sie den Befehl "Certutil-f-urlfetch-Verify certificatefilename. cer" aus.


### <a name="check-if-the-tls-version-is-compatible-between-ad-fswap-servers-and-the-client-device"></a>Überprüfen Sie, ob die TLS-Version zwischen AD FS/WAP-Servern und dem Client Gerät kompatibel ist.
In seltenen Fällen wird ein Client Gerät (in der Regel Mobile Geräte) aktualisiert, um nur eine höhere TLS-Version zu unterstützen (z. 1,3;), oder es liegt ein umgekehrtes Problem vor, bei dem AD FS/WAP-Server aktualisiert wurden, um nur eine höhere TLS-Version zu verwenden, und das Client Gerät diese Mit den Online-SSL-Tools können Sie Ihre AD FS/WAP-Server überprüfen und festzustellen, ob diese mit dem Gerät kompatibel sind. Weitere Informationen zum Steuern der TLS-Versionen finden Sie unter [diesem Link](manage-ssl-protocols-in-ad-fs.md).

### <a name="check-if-azure-ad-promptloginbehavior-is-configured-correctly-on-your-federated-domain-settings"></a>Überprüfen Sie, ob Azure AD promptloginbehavior in den Einstellungen der Verbund Domäne ordnungsgemäß konfiguriert ist.
Viele Office 365-Anwendungen senden prompt = Login an Azure AD. Azure AD konvertiert diese standardmäßig in eine neue Kenn Wort Anmeldung in AD FS. Dies hat zur Folge, dass die Endbenutzer auch dann, wenn Sie die Zertifikat Authentifizierung in AD FS konfiguriert haben, nur eine Kenn Wort Anmeldung sehen. 
1)  Die Verbund Domänen Einstellungen können mithilfe des Befehls Lets "Get-msoldomainfederationsettings" angezeigt werden.
2)  Stellen Sie sicher, dass der promptloginbehavior-Parameter auf den Wert "deaktiviert" oder "nativesupport" festgelegt ist.

Weitere Informationen finden Sie unter [diesem Link](ad-fs-prompt-login.md). 

### <a name="additional-troubleshooting"></a>Weitere Problembehandlung
Dies sind seltene vorkommen.
1)  Wenn die CRL-Liste sehr lang ist, kann es beim herunterladen zu einem Timeout kommen. In diesem Fall müssen Sie die Werte für "MaxFieldLength" und "maxrequestbyte" entsprechend aktualisieren. https://support.microsoft.com/en-us/help/820129/http-sys-registry-settings-for-windows




## <a name="reference-complete-list-of-user-certificate-claim-types-and-example-values"></a>Referenz: Umfassende Liste der Anspruchs Typen und Beispiel Werte für Benutzerzertifikate

|                                         Anspruchstyp                                         |                              Beispiel Wert                               |
|--------------------------------------------------------------------------------------------|--------------------------------------------------------------------------|
|         https://schemas.microsoft.com/2012/12/certificatecontext/field/x509version         |                                    3                                     |
|     https://schemas.microsoft.com/2012/12/certificatecontext/field/signaturealgorithm      |                                sha256RSA                                 |
|           https://schemas.microsoft.com/2012/12/certificatecontext/field/issuer            |                 CN = entca, DC = Domain, DC = ca. DC = com                  |
|         https://schemas.microsoft.com/2012/12/certificatecontext/field/issuername          |                 CN = entca, DC = Domain, DC = ca. DC = com                  |
|          https://schemas.microsoft.com/2012/12/certificatecontext/field/notbefore          |                           12/05/2016 20:50:18                            |
|          https://schemas.microsoft.com/2012/12/certificatecontext/field/notafter           |                           12/05/2017 20:50:18                            |
|           https://schemas.microsoft.com/2012/12/certificatecontext/field/subject           |   E =user@contoso.com, CN = User, CN = Users, DC = Domain, DC =, DC = com   |
|         https://schemas.microsoft.com/2012/12/certificatecontext/field/subjectname         |   E =user@contoso.com, CN = User, CN = Users, DC = Domain, DC =, DC = com   |
|           https://schemas.microsoft.com/2012/12/certificatecontext/field/rawdata           |                {Base64-codierte digitale Zertifikat Daten}                 |
|        https://schemas.microsoft.com/2012/12/certificatecontext/extension/keyusage         |                             DigitalSignature                             |
|        https://schemas.microsoft.com/2012/12/certificatecontext/extension/keyusage         |                             KeyEncipherment                              |
|  https://schemas.microsoft.com/2012/12/certificatecontext/extension/subjectkeyidentifier   |                 9D11941EC06FAKCCCB1B116B56AA97O3987D620A                 |
| https://schemas.microsoft.com/2012/12/certificatecontext/extension/authoritykeyidentifier  |    Keyid = D6 13 E3 6B BC E5 D8 15 52 0A FD 36 6a D5 0B 51 F3 0B 25 7F     |
| https://schemas.microsoft.com/2012/12/certificatecontext/extension/certificatetemplatename |                                   Benutzer                                   |
|           https://schemas.microsoft.com/2012/12/certificatecontext/extension/san           | Anderer Name: Prinzipal Nameuser@contoso.com=, RFC822 Name =user@contoso.com |
|           https://schemas.microsoft.com/2012/12/certificatecontext/extension/eku           |                          1.3.6.1.4.1.311.10.3.4                          |

## <a name="related-links"></a>Verwandte Links
* [Konfigurieren alternativer Hostname-Bindungen für AD FS Zertifikat Authentifizierung](ad-fs-support-for-alternate-hostname-binding-for-certificate-authentication.md)
* [Konfigurieren von Zertifizierungsstellen in Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-certificate-based-authentication-get-started#step-2-configure-the-certificate-authorities)
