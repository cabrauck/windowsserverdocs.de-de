---
title: Migrieren des AD FS 2,0-Verbund Servers
description: Bietet Informationen zum Migrieren eines AD FS Servers zu Windows Server 2012 R2.
author: billmath
ms.author: billmath
manager: femila
ms.date: 07/10/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 9e947f1894516de232a0db50bcbb56c7452098cd
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71359420"
---
# <a name="migrate-the-ad-fs-20-federation-server-to-ad-fs-on-windows-server-2012-r2"></a>Migrieren des AD FS 2,0-Verbund Servers zu AD FS unter Windows Server 2012 R2

Zum Migrieren eines AD FS Verbund Servers, der zu einer AD FS Farm mit einem einzelnen Knoten, einer WIF-Farm oder einer SQL Server-Farm gehört, zu Windows Server 2012 R2 müssen Sie die folgenden Aufgaben ausführen:  
  
1.  [Exportieren und Sichern der AD FS Konfigurationsdaten](migrate-ad-fs-fed-server-r2.md#export-and-backup-the-ad-fs-configuration-data)  
  
2.  [Erstellen einer Windows Server 2012 R2-Verbund Server Farm](migrate-ad-fs-fed-server-r2.md#create-a-windows-server-2012-r2-federation-server-farm)  
  
3.  [Importieren der ursprünglichen Konfigurationsdaten in die Windows Server 2012 R2-AD FS Farm](migrate-ad-fs-fed-server-r2.md#import-the-original-configuration-data-into-the-windows-server-2012-r2-ad-fs-farm)  
  
##  <a name="export-and-backup-the-ad-fs-configuration-data"></a>Exportieren und Sichern der AD FS-Konfigurationsdaten  
 Führen Sie zum Exportieren der AD FS-Konfigurationseinstellungen die folgenden Schritte aus:  
  
###  <a name="to-export-service-settings"></a>So exportieren Sie Diensteinstellungen  
  
1.  Stellen Sie sicher, dass Sie über Zugriff auf die folgenden Zertifikate und ihre privaten Schlüssel in einer PFX-Datei verfügen:  
  
    -   Das SSL-Zertifikat, das von der zu migrierenden Verbundserverfarm verwendet wird  
  
    -   Das Dienstkommunikationszertifikat (falls es sich vom SSL-Zertifikat unterscheidet), das von der zu migrierenden Verbundserverfarm verwendet wird  
  
    -   Alle Tokensignaturzertifikate oder Tokenverschlüsselungs-/Tokenentschlüsselungszertifikate von Drittanbietern, die von der zu migrierenden Verbundserverfarm verwendet werden  
  
Öffnen Sie zum Aufrufen des SSL-Zertifikats die IIS (Internetinformationsdienste)-Verwaltungskonsole, wählen Sie im linken Bereich **Standardwebsite** aus, und klicken Sie im Bereich **Aktion** auf **Bindungen…** . Navigieren Sie zur HTTPS-Bindung, wählen Sie sie aus, und klicken Sie auf **Bearbeiten**und anschließend auf **Anzeigen**.  
  
Sie müssen das vom Verbunddienst verwendete SSL-Zertifikat und seinen privaten Schlüssel in eine PFX-Datei exportieren. Weitere Informationen finden Sie unter [Exportieren des Bereichs mit dem privaten Schlüssel eines Serverauthentifizierungszertifikats](export-the-private-key-portion-of-a-server-authentication-certificate.md).  
  
> [!NOTE]
>  Wenn Sie den Geräte Registrierungsdienst im Rahmen der Ausführung Ihrer AD FS in Windows Server 2012 R2 bereitstellen möchten, müssen Sie ein neues SSL-Zertifikat abrufen. Weitere Informationen finden Sie unter [Registrieren eines SSL-Zertifikats für AD FS](enroll-an-ssl-certificate-for-ad-fs.md) und [Konfigurieren eines Verbundservers mit Device Registration Service](configure-a-federation-server-with-device-registration-service.md).  
  
Führen Sie zum Anzeigen der verwendeten Tokensignatur-, Tokenentschlüsselungs- und Dienstkommunikationszertifikate den folgenden Windows PowerShell-Befehl aus, um eine Liste aller verwendeten Zertifikate in einer Datei zu erstellen:  
  
``` powershell
Get-ADFSCertificate | Out-File “.\certificates.txt”  
 ```  
  
2. Exportieren Sie AD FS-Verbunddiensteigenschaften wie etwa den Verbunddienstnamen, den Anzeigenamen des Verbunddiensts und den Bezeichner des Verbunddiensts in eine Datei.  
  
Öffnen Sie zum Exportieren der Verbunddiensteigenschaften Windows PowerShell und führen Sie den folgenden Befehl aus: 

``` powershell
Get-ADFSProperties | Out-File “.\properties.txt”`.  
``` 

Die Ausgabedatei enthält die folgenden wichtigen Konfigurationswerte:  
 
|**Verbunddienst Eigenschaftsnamen wie von Get-ADF sproperties gemeldet**|**Eigenschaften Name Verbunddienst in AD FS Verwaltungskonsole**|
|-----|-----|  
|HostName|Verbunddienstname|  
|Bezeichner|Bezeichner des Verbunddiensts|  
|DisplayName|Anzeigename des Verbunddiensts|  
  
3. Sichern Sie die Anwendungskonfigurationsdatei. Neben anderen Einstellungen enthält diese Datei die Verbindungszeichenfolge der Richtliniendatenbank.  
  
Zum Sichern der Anwendungskonfigurationsdatei muss die Datei `%programfiles%\Active Directory Federation Services 2.0\Microsoft.IdentityServer.Servicehost.exe.config` manuell an einen sicheren Speicherort auf einem Sicherungsserver kopiert werden.  
  
> [!NOTE]
>  Notieren Sie sich die Datenbankverbindungszeichenfolge in dieser Datei. Sie befindet sich direkt hinter "policystore connectionstring=". Gibt die Verbindungszeichenfolge eine SQL Server-Datenbank an, ist der Wert beim Wiederherstellen der ursprünglichen AD FS-Konfiguration auf dem Verbundserver erforderlich.  
>   
>  Im Folgenden sehen Sie ein Beispiel für eine WID-Verbindungszeichenfolge: `“Data Source=\\.\pipe\mssql$microsoft##ssee\sql\query;Initial Catalog=AdfsConfiguration;Integrated Security=True"`. Im Folgenden sehen Sie ein Beispiel für eine SQL Server-Verbindungszeichenfolge: `"Data Source=databasehostname;Integrated Security=True"`.  
  
4. Notieren Sie die Identität des AD FS-Verbunddienstkontos und das Kennwort für dieses Konto.  
  
Der Identitätswert befindet sich in der Konsole **Dienste** in der Spalte **Anmelden als** unter **AD FS 2.0-Windows-Dienst** . Zeichnen Sie diesen Wert manuell auf.  
  
> [!NOTE]
>  Für einen eigenständigen Verbunddienst wird das integrierte Konto NETZWERKDIENST verwendet.  In diesem Fall benötigen Sie kein Kennwort.  
  
5. Exportieren Sie die Liste aktivierter AD FS-Endpunkte in eine Datei.  
  
Öffnen Sie dazu Windows PowerShell, und führen Sie den folgenden Befehl aus: 

``` powershell
Get-ADFSEndpoint | Out-File “.\endpoints.txt”`.  
``` 

6. Exportieren Sie alle benutzerdefinierten Anspruchbeschreibungen in eine Datei.  
  
Öffnen Sie dazu Windows PowerShell, und führen Sie den folgenden Befehl aus: 

``` powershell
Get-ADFSClaimDescription | Out-File “.\claimtypes.txt”`.  
 ```

7. Falls in der Datei %%amp;quot;web.config%%amp;quot; benutzerdefinierte Einstellungen wie etwa %%amp;quot;useRelayStateForIdpInitiatedSignOn%%amp;quot; konfiguriert sind, muss die Datei %%amp;quot;web.config%%amp;quot; zu Referenzzwecken gesichert werden. Sie können die Datei aus dem Verzeichnis kopieren, das dem virtuellen Pfad **%%amp;quot;/adfs/ls%%amp;quot;** in IIS zuwiesen ist. Standardmäßig befindet sie sich im Verzeichnis **%systemdrive%\inetpub\adfs\ls**.  
  
###  <a name="to-export-claims-provider-trusts-and-relying-party-trusts"></a>So exportieren Sie Anspruchsanbieter-Vertrauensstellungen und Vertrauensstellungen der vertrauenden Seite  
  
1.  Wenn Sie AD FS Anspruchs Anbieter-Vertrauens Stellungen und Vertrauens Stellungen der vertrauenden Seite exportieren möchten, müssen Sie sich als Administrator (jedoch nicht als Domänen Administrator) auf dem Verbund Server anmelden und das folgende Windows PowerShell-Skript ausführen, das sich im **Medium "Media/server_support" befindet.** Ordner "/ADFS" der Windows Server 2012 R2-Installations-CD: `export-federationconfiguration.ps1`.  
  
> [!IMPORTANT]
>  Das Exportskript enthält die folgenden Parameter:  
> 
> - Export-FederationConfiguration. ps1-Path < String @ no__t-0 [-Computername < String @ no__t-1] [-Credential < PSCredential @ no__t-2] [-Force] [-Certifi-epassword < SecureString @ no__t-3]  
>   -   Export-FederationConfiguration. ps1-Path < String @ no__t-0 [-Computername < String @ no__t-1] [-Credential < PSCredential @ no__t-2] [-Force] [-Certifi-epassword < SecureString @ no__t-3] [-relyingpartytrustidentifier < String [] >] [-claimsprovidertrustidentifier < String [] >]  
>   -   Export-FederationConfiguration. ps1-Path < String @ no__t-0 [-Computername < String @ no__t-1] [-Credential < PSCredential @ no__t-2] [-Force] [-Certifi-epassword < SecureString @ no__t-3] [-relyingpartytrustname < String [] >] [- Claimsprovidertrustname < Zeichenfolge [] >]  
> 
>   **-Relyingpartytrustidentifier < String [] >** : das Cmdlet exportiert nur Vertrauens Stellungen der vertrauenden Seite, deren Bezeichner im Zeichen folgen Array angegeben sind. Standardmäßig werden KEINE Vertrauensstellungen der vertrauenden Seite exportiert. Wenn weder %%amp;quot;RelyingPartyTrustIdentifier%%amp;quot;, %%amp;quot;ClaimsProviderTrustIdentifier%%amp;quot;, %%amp;quot;RelyingPartyTrustName%%amp;quot; noch %%amp;quot;ClaimsProviderTrustName%%amp;quot; angegeben ist, werden vom Skript alle Vertrauensstellungen der vertrauenden Seite und Anspruchsanbieter-Vertrauensstellungen exportiert.  
> 
>   **-Claimsprovidertrustidentifier < String [] >** -das Cmdlet exportiert nur Anspruchs Anbieter-Vertrauens Stellungen, deren Bezeichner im Zeichen folgen Array angegeben sind. Standardmäßig werden KEINE Anspruchsanbieter-Vertrauensstellungen exportiert.  
> 
>   **-Relyingpartytrustname < String [] >** : das Cmdlet exportiert nur Vertrauens Stellungen der vertrauenden Seite, deren Namen im Zeichen folgen Array angegeben sind. Standardmäßig werden KEINE Vertrauensstellungen der vertrauenden Seite exportiert.  
> 
>   **-Claimsprovidertrustname < String [] >** -das Cmdlet exportiert nur Anspruchs Anbieter-Vertrauens Stellungen, deren Namen im Zeichen folgen Array angegeben sind. Standardmäßig werden KEINE Anspruchsanbieter-Vertrauensstellungen exportiert.  
> 
>   **-Path < Zeichen\> Folge** : der Pfad zu einem Ordner, der die exportierten Dateien enthält.  
> 
>   **-Computername < Zeichen\> Folge** : gibt den STS-Server Hostnamen an. Der Standardwert ist der lokale Computer. Bei der Migration von AD FS 2.0 oder AD FS unter Windows Server 2012 zu AD FS unter Windows Server 2012 R2 ist dies der Hostname des AD FS-Legacyservers.  
> 
>   **-Credential < PSCredential\>**  : gibt ein Benutzerkonto an, das über die Berechtigung zum Ausführen dieser Aktion verfügt. Der Standardwert ist der aktuelle Benutzer.  
> 
>   **-Force** – Gibt an, dass keine Benutzerbestätigung angefordert wird.  
> 
>   **-Certifi-epassword < SecureString\>**  : gibt ein Kennwort zum Exportieren der privaten Schlüssel AD FS Zertifikate an. Wird dieser Parameter nicht angegeben, wird vom Skript ein Kennwort angefordert, wenn ein AD FS-Zertifikat mit privatem Schlüssel exportiert werden muss.  
> 
>   **Eingaben**: Keine  
> 
>   Zeichenfolge **Outputs**: – Dieses Cmdlet gibt den Ordnerpfad für den Export an. Sie können das zurückgegebene Objekt über die Pipeline an %%amp;quot;Import-FederationConfiguration%%amp;quot; übergeben.  
  
###  <a name="to-back-up-custom-attribute-stores"></a>So sichern Sie benutzerdefinierte Attributspeicher  
  
1.  Sie müssen alle benutzerdefinierten Attribut Speicher, die Sie in ihrer neuen AD FS Farm in Windows Server 2012 R2 aufbewahren möchten, manuell exportieren.  
  
> [!NOTE]
>  In Windows Server 2012 R2 sind für AD FS benutzerdefinierte Attribut Speicher erforderlich, die auf .NET Framework 4,0 oder höher basieren. Folgen Sie zum Installieren und Einrichten von .Net Framework 4.5 den Anweisungen unter [Microsoft .NET Framework 4.5](https://www.microsoft.com/download/details.aspx?id=30653) .  
  
Informationen zu von AD FS verwendeten benutzerdefinierten Attributspeichern erhalten Sie durch Ausführen des folgenden Windows PowerShell-Befehls: 

``` powershell
Get-ADFSAttributeStore
```  

Die Schritte zum Aktualisieren oder Migrieren von Attributspeichern variieren.  
  
2. Außerdem müssen Sie alle dll-Dateien der benutzerdefinierten Attribut Speicher, die Sie in ihrer neuen AD FS Farm in Windows Server 2012 R2 aufbewahren möchten, manuell exportieren. Die Schritte zum Aktualisieren oder Migrieren von DLL-Dateien benutzerdefinierter Attributspeicher variieren.  
  
##  <a name="create-a-windows-server-2012-r2-federation-server-farm"></a>Erstellen einer Windows Server 2012 R2-Verbundserverfarm  
  
1.  Installieren Sie das Windows Server 2012 R2-Betriebssystem auf einem Computer, der als Verbund Server fungieren soll, und fügen Sie dann die AD FS Server-Rolle hinzu. Weitere Informationen finden Sie unter [Install the AD FS Role Service](install-the-ad-fs-role-service.md). Konfigurieren Sie anschließend den neuen Verbunddienst entweder mithilfe des Konfigurations-Assistenten für Active Directory-Verbunddienste oder der Windows PowerShell. Weitere Informationen finden Sie unter [Konfigurieren eines Verbundservers](configure-a-federation-server.md) im Thema %%amp;quot;Konfigurieren des ersten Verbundservers in einer neuen Verbundserverfarm%%amp;quot;.  

Beachten Sie beim Ausführen dieses Schritts die folgenden Anweisungen:  
  
-   Zum Konfigurieren des Verbunddiensts sind Domänenadministratorberechtigungen erforderlich.  
  
-   Sie müssen denselben Verbunddienstnamen (Farmnamen) angeben wie in AD FS 2.0 oder AD FS unter Windows Server 2012. Wenn Sie nicht denselben Verbund Dienstnamen verwenden, funktionieren die gesicherten Zertifikate nicht im Windows Server 2012 R2-Verbund Dienst, den Sie konfigurieren möchten.  
  
-   Geben Sie an, ob es sich um eine WID- oder SQL Server-Verbundserverfarm handelt. Geben Sie im Falle einer SQL-Farm den Speicherort und den Instanznamen der SQL Server-Datenbank an.  
  
-   Sie müssen eine PFX-Datei mit dem SSL-Serverauthentifizierungszertifikat angeben, das Sie bei der Vorbereitung für die AD FS-Migration gesichert haben.  
  
-   Geben Sie dieselbe Dienstkontoidentität wie in der AD FS 2.0-Farm oder der Farm mit AD FS unter Windows Server 2012 an.  
  
2. Wenn der erste Knoten konfiguriert ist, können Sie der neuen Farm weitere Knoten hinzufügen. Weitere Informationen finden Sie unter [Konfigurieren eines Verbundservers](configure-a-federation-server.md) im Thema %%amp;quot;Hinzufügen eines Verbundservers zu einer vorhandenen Verbundserverfarm%%amp;quot;.  
  
##  <a name="import-the-original-configuration-data-into-the-windows-server-2012-r2-ad-fs-farm"></a>Importieren der ursprünglichen Konfigurationsdaten in die AD FS-Farm mit Windows Server 2012 R2  
 Nachdem Sie nun über eine AD FS-Verbund Serverfarm verfügen, die unter Windows Server 2012 R2 ausgeführt wird, können Sie die ursprünglichen AD FS Konfigurationsdaten in die Datei importieren.  
  
1.  Importieren und konfigurieren Sie weitere benutzerdefinierte AD FS-Zertifikate, u. a. extern registrierte Tokensignaturzertifikate und Tokenverschlüsselungs-/Tokenentschlüsselungszertifikate, und das Dienstkommunikationszertifikat, falls es vom SSL-Zertifikat abweicht.  
  
Wählen Sie in der AD FS-Verwaltungskonsole **Zertifikate** aus. Überprüfen Sie die Dienstkommunikations-, Tokenverschlüsselungs-/Tokenentschlüsselungs- und Tokensignaturzertifikate. Vergleichen Sie dazu die einzelnen Zertifikate mit den Werten, die Sie bei der Vorbereitung der Migration in die Datei %%amp;quot;certificates.txt%%amp;quot; exportiert haben.  
  
Wenn Sie die Tokenverschlüsselungs- oder Tokensignaturzertifikate von den standardmäßigen selbstsignierten Zertifikaten in externe Zertifikate ändern möchten, müssen Sie zuerst das standardmäßig aktivierte Feature für das automatische Zertifikatrollover deaktivieren. Hierzu können Sie den folgenden Windows PowerShell-Befehl verwenden:  
  
``` powershell 
Set-ADFSProperties –AutoCertificateRollover $false  
```  
  
2. Konfigurieren Sie mithilfe des Cmdlets %%amp;quot;Set-AdfsProperties%%amp;quot; beliebige benutzerdefinierte AD FS-Diensteinstellungen, z. B. %%amp;quot;AutoCertificateRollover%%amp;quot; oder SSO-Lebensdauer.  
  
3. Wenn Sie AD FS Vertrauens Stellungen der vertrauenden Seite und Anspruchs Anbieter-Vertrauens Stellungen importieren möchten, müssen Sie als Administrator (jedoch nicht als Domänen Administrator) auf dem Verbund Server angemeldet sein und das folgende Windows PowerShell-Skript ausführen, das sich im Ordner "\support\adfs" befindet. der Windows Server 2012 R2-Installations-CD:  
  
``` powershell 
import-federationconfiguration.ps1  
```  
  
> [!IMPORTANT]
>  Das Importskript enthält die folgenden Parameter:  
> 
> - Import-FederationConfiguration. ps1-Path < String @ no__t-0 [-Computername < String @ no__t-1] [-Credential < PSCredential @ no__t-2] [-Force] [-logPath < String @ no__t-3] [-Certifi-epassword < SecureString @ no__t-4]  
>   -   Import-FederationConfiguration. ps1-Path < String @ no__t-0 [-Computername < String @ no__t-1] [-Credential < PSCredential @ no__t-2] [-Force] [-logPath < String @ no__t-3] [-Certifi-epassword < SecureString @ no__t-4] [- Relyingpartytrustidentifier < String [] >] [-claimsprovidertrustidentifier < String [] >  
>   -   Import-FederationConfiguration. ps1-Path < String @ no__t-0 [-Computername < String @ no__t-1] [-Credential < PSCredential @ no__t-2] [-Force] [-logPath < String @ no__t-3] [-Certifi-epassword < SecureString @ no__t-4] [- Relyingpartytrustname < String [] >] [-claimsprovidertrustname < String [] >]  
> 
>   **-Relyingpartytrustidentifier < String [] >** : das Cmdlet importiert nur Vertrauens Stellungen der vertrauenden Seite, deren Bezeichner im Zeichen folgen Array angegeben sind. Standardmäßig werden KEINE Vertrauensstellungen der vertrauenden Seite importiert. Wenn weder %%amp;quot;RelyingPartyTrustIdentifier%%amp;quot;, %%amp;quot;ClaimsProviderTrustIdentifier%%amp;quot;, %%amp;quot;RelyingPartyTrustName%%amp;quot; noch %%amp;quot;ClaimsProviderTrustName%%amp;quot; angegeben ist, werden vom Skript alle Vertrauensstellungen der vertrauenden Seite und Anspruchsanbieter-Vertrauensstellungen importiert.  
> 
>   **-Claimsprovidertrustidentifier < String [] >** -das Cmdlet importiert nur Anspruchs Anbieter-Vertrauens Stellungen, deren Bezeichner im Zeichen folgen Array angegeben sind. Standardmäßig werden KEINE Anspruchsanbieter-Vertrauensstellungen importiert.  
> 
>   **-Relyingpartytrustname < String [] >** : das Cmdlet importiert nur Vertrauens Stellungen der vertrauenden Seite, deren Namen im Zeichen folgen Array angegeben sind. Standardmäßig werden KEINE Vertrauensstellungen der vertrauenden Seite importiert.  
> 
>   **-Claimsprovidertrustname < String [] >** -das Cmdlet importiert nur Anspruchs Anbieter-Vertrauens Stellungen, deren Namen im Zeichen folgen Array angegeben sind. Standardmäßig werden KEINE Anspruchsanbieter-Vertrauensstellungen importiert.  
> 
>   **-Path < Zeichen\> Folge** : der Pfad zu einem Ordner, der die zu importierenden Konfigurationsdateien enthält.  
> 
>   **-LogPath < Zeichen\> Folge** : der Pfad zu einem Ordner, der die Import Protokolldatei enthält. In diesem Ordner wird eine Protokolldatei mit dem Namen %%amp;quot;import.log%%amp;quot; erstellt.  
> 
>   **-Computername < Zeichen\> Folge** : gibt den Hostnamen des STS-Servers an. Der Standardwert ist der lokale Computer. Bei der Migration von AD FS 2.0 oder AD FS unter Windows Server 2012 zu AD FS unter Windows Server 2012 R2 muss für diesen Parameter der Hostname des AD FS-Legacyservers angegeben werden.  
> 
>   **-Credential < PSCredential\>** : gibt ein Benutzerkonto an, das über die Berechtigung zum Ausführen dieser Aktion verfügt. Der Standardwert ist der aktuelle Benutzer.  
> 
>   **-Force** – Gibt an, dass keine Benutzerbestätigung angefordert wird.  
> 
>   **-Certifi-epassword < SecureString\>**  : gibt ein Kennwort zum Importieren der privaten Schlüssel der AD FS Zertifikate an. Wird dieser Parameter nicht angegeben, wird vom Skript ein Kennwort angefordert, wenn ein AD FS-Zertifikat mit privatem Schlüssel importiert werden muss.  
> 
>   Zeichenfolge **Inputs:** – Dieser Befehl verwendet den Importordnerpfad als Eingabe. Sie können %%amp;quot;Export-FederationConfiguration%%amp;quot; über die Pipeline an diesen Befehl übergeben.  
> 
>   **Ausgaben** Keine  
  
Nachgestellte Leerzeichen in der WSFedEndpoint-Eigenschaft einer Vertrauensstellung der vertrauenden Seite können Fehler im Importskript verursachen. Entfernen Sie in diesem Fall vor dem Import die Leerzeichen manuell aus der Datei. Die folgenden Einträge können beispielsweise Fehler verursachen:  
  
    ```  
    <URI N="WSFedEndpoint">https://127.0.0.1:444 /</URI>  
    ```  
  
    ```  
    <URI N="WSFedEndpoint">https://myapp.cloudapp.net:83 /</URI>  
    ```  
  
     They must be edited to:  
  
    ```  
    <URI N="WSFedEndpoint">https://127.0.0.1:444/</URI>  
    ```  
  
    ```  
    <URI N="WSFedEndpoint">https://myapp.cloudapp.net:83/</URI>  
    ```  
> [!IMPORTANT]
>  Falls die Active Directory-Anspruchsanbieter-Vertrauensstellung im Quellsystem benutzerdefinierte Anspruchsregeln (also nicht die AD FS-Standardregeln) enthält, werden diese von den Skripts nicht migriert. Dies liegt daran, dass Windows Server 2012 R2 über neue Standardwerte verfügt. Alle benutzerdefinierten Regeln müssen zusammengeführt werden, indem Sie manuell der Active Directory Anspruchs Anbieter-Vertrauensstellung in der neuen Windows Server 2012 R2-Farm hinzugefügt werden.  
  
4. Konfigurieren Sie alle benutzerdefinierten AD FS-Endpunkteinstellungen. Wählen Sie in der AD FS-Verwaltungskonsole **Endpunkte** aus. Vergleichen Sie die aktivierten AD FS-Endpunkte mit der Liste der aktivierten AD FS-Endpunkte, die Sie beim Vorbereiten der AD FS-Migration in eine Datei exportiert haben.  
  
    \-Immer  
  
    Konfigurieren Sie alle benutzerdefinierten Anspruchbeschreibungen. Wählen Sie in der AD FS-Verwaltungskonsole **Anspruchbeschreibungen**aus. Vergleichen Sie die Liste der AD FS-Anspruchsbeschreibungen mit der Liste der Anspruchsbeschreibungen, die Sie beim Vorbereiten der AD FS-Migration in eine Datei exportiert haben. Fügen Sie alle benutzerdefinierten Anspruchbeschreibungen hinzu, die in der Datei, aber nicht in der Standardliste in AD FS enthalten sind. Der Claim-Bezeichner in der Verwaltungskonsole ist %%amp;quot;ClaimType%%amp;quot; in der Datei zugeordnet.  
  
5. Installieren und konfigurieren Sie alle gesicherten benutzerdefinierten Attributspeicher. Stellen Sie als Administrator sicher, dass alle Binärdateien für benutzerdefinierte Attributspeicher auf .NET Framework 4.0 oder höher aktualisiert werden, bevor die AD FS-Konfiguration für den Verweis auf die Speicher aktualisiert wird.  
  
6. Konfigurieren Sie Diensteigenschaften, die den Parametern der Legacydatei %%amp;quot;web.config%%amp;quot; zugeordnet sind.  
  
   -   Wenn **userelaystateforidpinitiatedsignon** der Datei " **Web. config** " in Ihrer AD FS 2,0 oder AD FS in der Windows Server 2012-Farm hinzugefügt wurde, müssen Sie die folgenden Dienst Eigenschaften in Ihrem AD FS in der Windows Server 2012 R2-Farm konfigurieren:  
  
       -   AD FS in Windows Server 2012 R2 enthält eine **%systemroot%\ADFS\Microsoft.IdentityServer.ServiceHost.exe.config** -Datei. Erstellen Sie ein Element mit derselben Syntax wie das **Web. config** -Datei Element `<useRelayStateForIdpInitiatedSignOn enabled="true" />`:. Fügen Sie dieses Element als Teil **< Microsoft. identityserver. Web >** -Abschnitts der Datei **Microsoft. identityserver. ServiceHost. exe. config** ein.  
  
   -   Wenn **< persistidentityproviderinformation aktiviert = "true&#124;false" lifetimeindays = "90" enablewhrpersistenz = "&#124;true false"\> /** wurde der Datei "Web. config" in der Datei " **Web. config** " in Ihrem AD FS 2,0 oder AD FS in Windows Server hinzugefügt. 2012-Farm, dann müssen Sie die folgenden Dienst Eigenschaften in Ihrem AD FS in der Windows Server 2012 R2-Farm konfigurieren:  
  
       1.  Führen Sie in AD FS in Windows Server 2012 R2 den folgenden Windows PowerShell-Befehl `Set-AdfsWebConfig –HRDCookieEnabled –HRDCookieLifetime`aus:.  
  
   -   Wenn **< SingleSignOn-fähig = "&#124;true false"\> /** wurde der Datei " **Web. config** " in Ihrer AD FS 2,0 oder AD FS in der Windows Server 2012-Farm hinzugefügt wurde, müssen Sie keine zusätzlichen Dienst Eigenschaften in Ihrem AD FS in Windows Server 2012 festlegen. R2-Farm. Das einmalige Anmelden ist standardmäßig in AD FS in der Windows Server 2012 R2-Farm aktiviert.  
  
   -   Wenn die localauthenticationtypes-Einstellungen der Datei " **Web. config** " in Ihrer AD FS 2,0 oder AD FS in der Windows Server 2012-Farm hinzugefügt wurden, müssen Sie die folgenden Dienst Eigenschaften in Ihrem AD FS in der Windows Server 2012 R2-Farm konfigurieren:  
  
       -   Integrierte, Forms-, tlsclient-und einfache Transformations Listen in äquivalente AD FS in Windows Server 2012 R2 verfügen über globale Authentifizierungs Richtlinien Einstellungen zur Unterstützung von Verbund Dienst-und Proxy Authentifizierungs Typen. Diese Einstellungen können im AD FS-Verwaltungs-Snap-In unter **Authentifizierungsrichtlinien**konfiguriert werden.  
  
   Nach dem Importieren der ursprünglichen Konfigurationsdaten können Sie die AD FS-Anmeldeseiten nach Bedarf anpassen. Weitere Informationen finden Sie unter [Customizing the AD FS Sign-in Pages](../operations/AD-FS-Customization-in-Windows-Server-2016.md).  
  
## <a name="next-steps"></a>Nächste Schritte
 [Migrieren Active Directory-Verbunddienste (AD FS) Rollen Dienste zu Windows Server 2012 R2](migrate-ad-fs-service-role-to-windows-server-r2.md)   
 [Vorbereiten der Migration des AD FS Verbund Servers](prepare-migrate-ad-fs-server-r2.md)   
 [Migrieren des AD FS Verbund Server Proxys](migrate-fed-server-proxy-r2.md)   
 [Überprüfen der AD FS Migration zu Windows Server 2012 R2](verify-ad-fs-migration.md)