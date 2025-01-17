---
title: Vorbereiten der Migration einer AD FS 2,0 wid-Farm
description: Enthält Informationen zum Vorbereiten der Migration einer AD FS 2,0-Server-wid-Farm zu Windows Server 2012.
author: billmath
ms.author: billmath
manager: femila
ms.date: 06/28/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: e6612856a2e00c47e9cc87c75c802ff86697b781
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71359259"
---
# <a name="prepare-to-migrate-an-ad-fs-20-wid-farm"></a>Vorbereiten der Migration einer AD FS 2,0 wid-Farm  
 Zum Vorbereiten der Migration von AD FS 2,0-Verbund Servern, die zu einer internen Windows-Daten Bank Farm (WID) zu Windows Server 2012 gehören, müssen Sie die AD FS Konfigurationsdaten von diesen Servern exportieren und sichern.  
  
 Führen Sie zum Exportieren der AD FS-Konfigurationsdaten die folgenden Schritte aus:  
  
-   [Schritt 1: Exportieren der Dienst Einstellungen](#step-1-export-service-settings)  
  
-   [Schritt 2: Sichern der benutzerdefinierten Attribut Speicher @ no__t-0  
  
-   [Schritt 3: Sichern von Webseiten Anpassungen @ no__t-0  
  
## <a name="step-1-export-service-settings"></a>Schritt 1: Exportieren der Diensteinstellungen  
 Gehen Sie wie folgt vor, um die Diensteinstellungen zu exportieren:  
  
### <a name="to-export-service-settings"></a>So exportieren Sie Diensteinstellungen  
  
1.  Notieren Sie den Antragstellernamen des Zertifikats sowie den Fingerabdruckwert des SSL-Zertifikats, die vom Verbunddienst verwendet werden. Um das SSL-Zertifikat zu finden, öffnen Sie die Internetinformationsdienste (IIS)-Verwaltungskonsole, wählen Sie im linken Bereich **Standard Website** aus, und klicken Sie auf **Bindungen...** Suchen Sie im **Aktions** Bereich die HTTPS-Bindung, wählen Sie Sie aus, klicken Sie auf **Bearbeiten**, und klicken Sie dann auf **anzeigen**.  
  
> [!NOTE]
>  Optional können Sie auch SSL-Zertifikat und seinen privaten Schlüssel in eine PFX-Datei exportieren. Weitere Informationen finden Sie unter [Exportieren des Bereichs mit dem privaten Schlüssel eines Serverauthentifizierungszertifikats](Export-the-Private-Key-Portion-of-a-Server-Authentication-Certificate.md).  
>   
>  Dieser Schritt ist optional, da dieses Zertifikat auf dem lokalen Computer im privaten Zertifikatspeicher gespeichert wird und beim Upgrade des Betriebssystems erhalten bleibt.  
  
2. Exportieren Sie zusätzlich zu den selbstsignierten Zertifikaten alle Zertifikate und Schlüssel für die Tokensignatur, Tokenverschlüsselung oder Dienstkommunikation, die nicht intern generiert werden.  
  
Sie können alle auf Ihrem Server verwendeten Zertifikate mithilfe von Windows PowerShell anzeigen. Öffnen Sie Windows PowerShell, und führen Sie den folgenden Befehl zum Hinzufügen der AD FS-Cmdlets zur Windows PowerShell-Sitzung aus: `PSH:>add-pssnapin “Microsoft.adfs.powershell”`. Führen Sie dann den folgenden Befehl aus, um alle Zertifikate anzuzeigen, die auf dem Server verwendet werden `PSH:>Get-ADFSCertificate`. Die Ausgabe dieses Befehls umfasst StoreLocation- und StoreName-Werte, die den Speicherort für die einzelnen Zertifikate angeben.  Sie können dann die Anleitung in [Exportieren des Bereichs mit dem privaten Schlüssel eines Serverauthentifizierungszertifikats](Export-the-Private-Key-Portion-of-a-Server-Authentication-Certificate.md) verwenden, um die einzelnen Zertifikate und den entsprechenden privaten Schlüssel in eine PFX-Datei zu exportieren.  
  
> [!NOTE]
>  Dieser Schritt ist optional, da alle externen Zertifikate während des Betriebssystemupgrades erhalten bleiben.  
  
3. Notieren Sie die Identität des AD FS 2,0-Verbund Dienst Kontos und das Kennwort für dieses Konto.  
  
Um den Identitäts Wert zu ermitteln, überprüfen Sie die Spalte **Anmelden** unter **AD FS 2,0-Windows-Dienst** in der Konsole **Dienste** , und notieren Sie den Wert manuell.  
  
## <a name="step-2-back-up-custom-attribute-stores"></a>Schritt 2: Sichern der benutzerdefinierten Attributspeicher  
 Informationen zu von AD FS verwendeten benutzerdefinierten Attributspeichern erhalten Sie mithilfe von Windows PowerShell. Öffnen Sie Windows PowerShell, und führen Sie den folgenden Befehl zum Hinzufügen der AD FS-Cmdlets zur Windows PowerShell-Sitzung aus: `PSH:>add-pssnapin “Microsoft.adfs.powershell”`. Führen Sie dann den folgenden Befehl aus, um Informationen zu den benutzerdefinierten Attribut speichern zu suchen: `PSH:>Get-ADFSAttributeStore`. Die Schritte zum Aktualisieren oder Migrieren von Attributspeichern variieren.  
  
## <a name="step-3-back-up-webpage-customizations"></a>Schritt 3: Sichern der Webseitenanpassungen  
 Um Webseiten Anpassungen zu sichern, kopieren Sie die AD FS Webseiten und die Datei **Web. config** aus dem Verzeichnis, das dem virtuellen Pfad **"/ADFS/ls"** in IIS zugeordnet ist. Standardmäßig befindet sie sich im Verzeichnis **%systemdrive%\inetpub\adfs\ls**.  

## <a name="next-steps"></a>Nächste Schritte
 [Vorbereiten der Migration des AD FS 2,0](prepare-to-migrate-ad-fs-fed-server.md)-Verbund Servers    
 [Vorbereiten der Migration des AD FS 2,0-Verbund Server Proxys](prepare-to-migrate-ad-fs-fed-proxy.md)   
 [Migrieren Sie den AD FS 2,0](migrate-the-ad-fs-fed-server.md)-Verbund Server  .  
 [Migrieren Sie den AD FS 2,0-Verbund Server Proxy](migrate-the-ad-fs-2-fed-server-proxy.md) .  
 [Migrieren der AD FS 1.1-Web-Agents](migrate-the-ad-fs-web-agent.md)