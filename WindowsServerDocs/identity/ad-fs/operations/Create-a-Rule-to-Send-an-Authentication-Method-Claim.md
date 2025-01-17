---
ms.assetid: 96b9f4e6-f01c-4517-8299-017d187d447e
title: Erstellen einer Regel zum Senden eines Authentifizierungsmethodenanspruchs
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 4efcae02b96904c9f869a5ed9e14eba161892b74
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71358156"
---
# <a name="create-a-rule-to-send-an-authentication-method-claim"></a>Erstellen einer Regel zum Senden eines Authentifizierungsmethodenanspruchs


Sie können entweder die Regel Vorlage " **Gruppenmitgliedschaft als Ansprüche senden** " oder " **eingehende Anspruchs Vorlage transformieren** " verwenden, um einen Authentifizierungsmethoden Anspruch zu senden. Die vertrauende Seite kann mithilfe eines Authentifizierungsmethoden Anspruchs den Anmelde Mechanismus bestimmen, den der Benutzer zum Authentifizieren und Abrufen von Ansprüchen von Active Directory-Verbunddienste (AD FS) \(ad FS @ no__t-1 verwendet. Sie können auch das Authentifizierungsmechanismus-Sicherungs Feature von Active Directory-Verbunddienste (AD FS) \(ad FS @ no__t-1 in Windows Server 2012 R2 als Eingabe verwenden, um Authentifizierungsmethoden Ansprüche für Situationen zu generieren, in denen die vertrauende Seite bestimmen möchte. die Zugriffsebene, die auf Smartcardanmeldungen basiert. Ein Entwickler kann beispielsweise unterschiedliche Zugriffsebenen für Verbund Benutzer der Anwendung der vertrauenden Seite zuweisen. Die Zugriffsebenen basieren darauf, ob sich die Benutzer mit Ihren Benutzernamen-und Kennwort-Anmelde Informationen anmelden (im Gegensatz zu ihren Smartcards).  

Verwenden Sie je nach den Anforderungen Ihrer Organisation eines der folgenden Verfahren:  

-   Erstellen Sie diese Regel mithilfe der Regel Vorlage " **Sende Gruppenmitgliedschaft als Ansprüche** " \- Sie können diese Regel Vorlage verwenden, wenn Sie möchten, dass die von Ihnen in dieser Vorlage angegebene Gruppe letztendlich festlegt, welche Authentifizierungsmethode ausgegeben werden soll.  

-   Erstellen Sie diese Regel mithilfe der Regel Vorlage zum **Transformieren eines eingehenden Anspruchs** \- Sie können diese Regel Vorlage verwenden, wenn Sie die vorhandene Authentifizierungsmethode in eine neue Authentifizierungsmethode ändern möchten, die mit einem nicht erkannten Produkt funktioniert. Standard AD FS Authentifizierungsmethoden Ansprüche.  



## <a name="to-create-by-using-the-send-group-membership-as-claims-rule-template-on-a-relying-party-trust-in-windows-server-2016"></a>So erstellen Sie mithilfe der Regel Vorlage "Gruppenmitgliedschaft als Ansprüche senden" für eine Vertrauensstellung der vertrauenden Seite in Windows Server 2016 

1.  Klicken Sie in Server-Manager **auf Extras**, und wählen Sie dann **AD FS Verwaltung**aus.  

2.  Klicken Sie in der Konsolen Struktur unter **AD FS**auf Vertrauens Stellungen der vertrauenden **Seite**. 
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule9.PNG)  

3.  Klicken\-Sie mit der rechten Maustaste auf die ausgewählte Vertrauensstellung, und klicken Sie dann auf **Richtlinie**zum
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule10.PNG)   

4.  Klicken Sie im Dialogfeld **Richtlinie für Anspruchs Ausstellung bearbeiten** unter Ausstellungs **Transformationsregeln** auf **Regel hinzufügen** , um den Regel-Assistenten zu starten. 
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule11.PNG)    

5.  Wählen Sie auf der Seite **Regel Vorlage auswählen** unter **Anspruchs Regel Vorlage**die Option **Gruppenmitgliedschaft als Anspruch senden** aus der Liste aus, und klicken Sie dann auf **weiter**.  
![Regel erstellen](media/Create-a-Rule-to-Send-Group-Membership-as-a-Claim/group3.PNG)      

6.  Geben Sie auf der Seite **Regel konfigurieren** einen Anspruchs Regel Namen ein.  

7.  Klicken Sie auf **Durchsuchen**, wählen Sie die Gruppe aus, deren Mitglieder diesen Authentifizierungsmethoden Anspruch erhalten sollen, und klicken Sie dann auf **OK**.  

8.  Wählen Sie unter **Typ des ausgehenden Anspruchs**in der Liste die Option **Authentifizierungsmethode** aus.  

9. Geben Sie unter **Wert des ausgehenden Anspruchs**einen der standardmäßigen Uniform Resource Identifier \(uri @ no__t-2-Werte in der folgenden Tabelle ein, klicken Sie auf **Fertig**stellen, und klicken Sie dann auf **OK** , um die Regel zu speichern.  

|                            Tatsächliche Authentifizierungsmethode                             |                                Entsprechender URI                                 |
|-------------------------------------------------------------------------------------|----------------------------------------------------------------------------------|
|                        Authentifizierung mit Benutzername und Kennwort                        | https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password  |
|                               Windows-Authentifizierung                                |  https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/windows  |
| Transport Layer Security \(tls @ no__t-1 gegenseitige Authentifizierung, die X. 509-Zertifikate verwendet | https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/tlsclient |
|                  X. 509 @ no__t-0basierte Authentifizierung, die TLS nicht verwendet                  |   https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/x509    |

![Regel erstellen](media/Create-a-Rule-to-Send-an-Authentication-Method-Claim/auth2.PNG)

## <a name="to-create-by-using-the-send-group-membership-as-claims-rule-template-on-a-claims-provider-trust-in-windows-server-2016"></a>So erstellen Sie mithilfe der Regel Vorlage "Gruppenmitgliedschaft als Ansprüche senden" für eine Anspruchs Anbieter-Vertrauensstellung in Windows Server 2016 

1.  Klicken Sie in Server-Manager **auf Extras**, und wählen Sie dann **AD FS Verwaltung**aus.  

2.  Klicken Sie in der Konsolen Struktur unter **AD FS**auf **Anspruchs Anbieter**-Vertrauens Stellungen. 
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule1.PNG)  

3.  Klicken\-Sie mit der rechten Maustaste auf die ausgewählte Vertrauensstellung und dann auf **Anspruchs Regeln bearbeiten**.
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule2.PNG)   

4.  Klicken Sie im Dialogfeld **Anspruchs Regeln bearbeiten** unter **Akzeptanz Transformationsregeln** auf **Regel hinzufügen** , um den Regel-Assistenten zu starten.
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule3.PNG)    

5.  Wählen Sie auf der Seite **Regel Vorlage auswählen** unter **Anspruchs Regel Vorlage**die Option **Gruppenmitgliedschaft als Anspruch senden** aus der Liste aus, und klicken Sie dann auf **weiter**.  
![Regel erstellen](media/Create-a-Rule-to-Send-Group-Membership-as-a-Claim/group3.PNG)     

6.  Geben Sie auf der Seite **Regel konfigurieren** einen Anspruchs Regel Namen ein.  

7.  Klicken Sie auf **Durchsuchen**, wählen Sie die Gruppe aus, deren Mitglieder diesen Authentifizierungsmethoden Anspruch erhalten sollen, und klicken Sie dann auf **OK**.  

8.  Wählen Sie unter **Typ des ausgehenden Anspruchs**in der Liste die Option **Authentifizierungsmethode** aus.  

9. Geben Sie unter **Wert des ausgehenden Anspruchs**einen der standardmäßigen Uniform Resource Identifier \(uri @ no__t-2-Werte in der folgenden Tabelle ein, klicken Sie auf **Fertig**stellen, und klicken Sie dann auf **OK** , um die Regel zu speichern.  

|                            Tatsächliche Authentifizierungsmethode                             |                                Entsprechender URI                                 |
|-------------------------------------------------------------------------------------|----------------------------------------------------------------------------------|
|                        Authentifizierung mit Benutzername und Kennwort                        | https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password  |
|                               Windows-Authentifizierung                                |  https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/windows  |
| Transport Layer Security \(tls @ no__t-1 gegenseitige Authentifizierung, die X. 509-Zertifikate verwendet | https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/tlsclient |
|                  X. 509 @ no__t-0basierte Authentifizierung, die TLS nicht verwendet                  |   https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/x509    |

![Regel erstellen](media/Create-a-Rule-to-Send-an-Authentication-Method-Claim/auth2.PNG)


## <a name="to-create-this-rule-by-using-the-transform-an-incoming-claim-rule-template-on-a-relying-party-trust-in-windows-server-2016"></a>So erstellen Sie diese Regel mithilfe der Regel Vorlage zum Transformieren eines eingehenden Anspruchs für eine Vertrauensstellung der vertrauenden Seite in Windows Server 2016 

1.  Klicken Sie in Server-Manager **auf Extras**, und wählen Sie dann **AD FS Verwaltung**aus.  

2.  Klicken Sie in der Konsolen Struktur unter **AD FS**auf Vertrauens Stellungen der vertrauenden **Seite**. 
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule9.PNG)  

3.  Klicken\-Sie mit der rechten Maustaste auf die ausgewählte Vertrauensstellung, und klicken Sie dann auf **Richtlinie**zum
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule10.PNG)   

4.  Klicken Sie im Dialogfeld **Richtlinie für Anspruchs Ausstellung bearbeiten** unter Ausstellungs **Transformationsregeln** auf **Regel hinzufügen** , um den Regel-Assistenten zu starten. 
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule11.PNG)    

5.  Wählen Sie auf der Seite **Regel Vorlage auswählen** unter **Anspruchs Regel Vorlage**die **Option eingehenden Anspruch** in der Liste umwandeln aus, und klicken Sie dann auf **weiter**.  
![Regel erstellen](media/Create-a-Rule-to-Transform-an-Incoming-Claim/transform3.PNG)      

6.  Geben Sie auf der Seite **Regel konfigurieren** einen Anspruchs Regel Namen ein.  

7.  Wählen Sie unter **Typ des eingehenden Anspruchs**in der Liste die Option **Authentifizierungsmethode** aus.  

8.  Wählen Sie unter **Typ des ausgehenden Anspruchs**in der Liste die Option **Authentifizierungsmethode** aus.  

9. Wählen Sie **einen eingehenden Anspruchs Wert durch einen anderen ausgehenden Anspruchs Wert ersetzen**aus, und führen Sie dann die folgenden Schritte aus:  

    1.  Geben Sie unter **eingehender Anspruchs Wert**einen der folgenden URI-Werte ein, die auf dem ursprünglich verwendeten Authentifizierungsmethoden-URI basieren, klicken Sie auf **Fertig**stellen, und klicken Sie dann auf **OK** , um die Regel zu speichern.  

    2.  Geben Sie unter **Wert des ausgehenden Anspruchs**einen der Standard-URI-Werte in der folgenden Tabelle ein, der von der neuen bevorzugten Authentifizierungsmethode abhängt, klicken Sie auf **Fertig**stellen, und klicken Sie dann auf **OK** , um die Regel zu speichern.  

|              Tatsächliche Authentifizierungsmethode              |                                Entsprechender URI                                 |
|--------------------------------------------------------|----------------------------------------------------------------------------------|
|         Authentifizierung mit Benutzername und Kennwort          | https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password  |
|                 Windows-Authentifizierung                 |  https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/windows  |
| Gegenseitige TLS-Authentifizierung, die X. 509-Zertifikate verwendet | https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/tlsclient |
|   X. 509 @ no__t-0basierte Authentifizierung, die TLS nicht verwendet    |   https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/x509    |

![Regel erstellen](media/Create-a-Rule-to-Send-an-Authentication-Method-Claim/auth4.PNG)

> [!NOTE]  
> Andere URI-Werte können zusätzlich zu den Werten in der Tabelle verwendet werden. Die URI-Werte, die in der vorherigen Tabelle angezeigt werden, entsprechen den URIs, die von der vertrauenden Seite standardmäßig akzeptiert werden.  

## <a name="to-create-this-rule-by-using-the-transform-an-incoming-claim-rule-template-on-a-claims-provider-trust-in-windows-server-2016"></a>So erstellen Sie diese Regel mithilfe der Regel Vorlage zum Transformieren eines eingehenden Anspruchs für eine Anspruchs Anbieter-Vertrauensstellung in Windows Server 2016 

1.  Klicken Sie in Server-Manager **auf Extras**, und wählen Sie dann **AD FS Verwaltung**aus.  

2.  Klicken Sie in der Konsolen Struktur unter **AD FS**auf **Anspruchs Anbieter**-Vertrauens Stellungen. 
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule1.PNG)  

3.  Klicken\-Sie mit der rechten Maustaste auf die ausgewählte Vertrauensstellung und dann auf **Anspruchs Regeln bearbeiten**.
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule2.PNG)   

4.  Klicken Sie im Dialogfeld **Anspruchs Regeln bearbeiten** unter **Akzeptanz Transformationsregeln** auf **Regel hinzufügen** , um den Regel-Assistenten zu starten.
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule3.PNG)    

5.  Wählen Sie auf der Seite **Regel Vorlage auswählen** unter **Anspruchs Regel Vorlage**die **Option eingehenden Anspruch** in der Liste umwandeln aus, und klicken Sie dann auf **weiter**.  
![Regel erstellen](media/Create-a-Rule-to-Transform-an-Incoming-Claim/transform3.PNG)      

6.  Geben Sie auf der Seite **Regel konfigurieren** einen Anspruchs Regel Namen ein.  

7.  Wählen Sie unter **Typ des eingehenden Anspruchs**in der Liste die Option **Authentifizierungsmethode** aus.  

8.  Wählen Sie unter **Typ des ausgehenden Anspruchs**in der Liste die Option **Authentifizierungsmethode** aus.  

9. Wählen Sie **einen eingehenden Anspruchs Wert durch einen anderen ausgehenden Anspruchs Wert ersetzen**aus, und führen Sie dann die folgenden Schritte aus:  

    1.  Geben Sie unter **eingehender Anspruchs Wert**einen der folgenden URI-Werte ein, die auf dem ursprünglich verwendeten Authentifizierungsmethoden-URI basieren, klicken Sie auf **Fertig**stellen, und klicken Sie dann auf **OK** , um die Regel zu speichern.  

    2.  Geben Sie unter **Wert des ausgehenden Anspruchs**einen der Standard-URI-Werte in der folgenden Tabelle ein, der von der neuen bevorzugten Authentifizierungsmethode abhängt, klicken Sie auf **Fertig**stellen, und klicken Sie dann auf **OK** , um die Regel zu speichern.  

|              Tatsächliche Authentifizierungsmethode              |                                Entsprechender URI                                 |
|--------------------------------------------------------|----------------------------------------------------------------------------------|
|         Authentifizierung mit Benutzername und Kennwort          | https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password  |
|                 Windows-Authentifizierung                 |  https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/windows  |
| Gegenseitige TLS-Authentifizierung, die X. 509-Zertifikate verwendet | https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/tlsclient |
|   X. 509 @ no__t-0basierte Authentifizierung, die TLS nicht verwendet    |   https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/x509    |

![Regel erstellen](media/Create-a-Rule-to-Send-an-Authentication-Method-Claim/auth4.PNG)























## <a name="to-create-this-rule-by-using-the-send-group-membership-as-claims-rule-template-in-windows-server-2012-r2"></a>So erstellen Sie diese Regel mithilfe der Regel Vorlage "Gruppenmitgliedschaft als Ansprüche senden" in Windows Server 2012 R2  

1.  Klicken Sie in Server-Manager **auf Extras**, und wählen Sie dann **AD FS Verwaltung**aus.  

2.  Klicken Sie in der Konsolen Struktur **unter\\AD FS Vertrauens**Stellungen entweder auf **Anspruchs Anbieter** -Vertrauens Stellungen oder Vertrauens Stellungen der vertrauenden **Seite**, und klicken Sie dann auf eine bestimmte Vertrauensstellung in der Liste, in der Sie diese Regel erstellen möchten.  

3.  Klicken\-Sie mit der rechten Maustaste auf die ausgewählte Vertrauensstellung und dann auf **Anspruchs Regeln bearbeiten**.
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule6.PNG)  

4.  Wählen Sie im Dialogfeld **Anspruchs Regeln bearbeiten** je nach der zu bearbeitenden Vertrauensstellung und dem Regelsatz, in dem Sie diese Regel erstellen möchten, eine der folgenden Registerkarten aus, und klicken Sie dann auf **Regel hinzufügen** , um den Regel-Assistenten zu starten, der diesem Regelsatz zugeordnet ist. :  

    -   **Akzeptanz Transformationsregeln**  

    -   **Ausstellungs Transformationsregeln**  

    -   **Ausstellungs Autorisierungs Regeln**  

    -   **Delegierungs Autorisierungs Regeln**  
![Regel erstellen](media/Create-a-Rule-to-Permit-All-Users/permitall5.PNG)

5.  Wählen Sie auf der Seite **Regel Vorlage auswählen** unter **Anspruchs Regel Vorlage**die Option **Gruppenmitgliedschaft als Anspruch senden** aus der Liste aus, und klicken Sie dann auf **weiter**.  
![Regel erstellen](media/Create-a-Rule-to-Send-Group-Membership-as-a-Claim/group1.PNG)

6.  Geben Sie auf der Seite **Regel konfigurieren** einen Anspruchs Regel Namen ein.  

7.  Klicken Sie auf **Durchsuchen**, wählen Sie die Gruppe aus, deren Mitglieder diesen Authentifizierungsmethoden Anspruch erhalten sollen, und klicken Sie dann auf **OK**.  

8.  Wählen Sie unter **Typ des ausgehenden Anspruchs**in der Liste die Option **Authentifizierungsmethode** aus.  

9. Geben Sie unter **Wert des ausgehenden Anspruchs**einen der standardmäßigen Uniform Resource Identifier \(uri @ no__t-2-Werte in der folgenden Tabelle ein, klicken Sie auf **Fertig**stellen, und klicken Sie dann auf **OK** , um die Regel zu speichern.  

|                            Tatsächliche Authentifizierungsmethode                             |                                Entsprechender URI                                 |
|-------------------------------------------------------------------------------------|----------------------------------------------------------------------------------|
|                        Authentifizierung mit Benutzername und Kennwort                        | https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password  |
|                               Windows-Authentifizierung                                |  https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/windows  |
| Transport Layer Security \(tls @ no__t-1 gegenseitige Authentifizierung, die X. 509-Zertifikate verwendet | https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/tlsclient |
|                  X. 509 @ no__t-0basierte Authentifizierung, die TLS nicht verwendet                  |   https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/x509    |

![Regel erstellen](media/Create-a-Rule-to-Send-an-Authentication-Method-Claim/auth1.PNG)

> [!NOTE]  
> Andere URI-Werte können zusätzlich zu den Werten in der Tabelle verwendet werden. Die URI-Werte, die in der vorherigen Tabelle angezeigt werden, entsprechen den URIs, die von der vertrauenden Seite standardmäßig akzeptiert werden.  

## <a name="to-create-this-rule-by-using-the-transform-an-incoming-claim-rule-template-in-windows-server-2012-r2"></a>So erstellen Sie diese Regel mithilfe der Regel Vorlage zum Transformieren eines eingehenden Anspruchs in Windows Server 2012 R2  



1.  Klicken Sie in Server-Manager **auf Extras, und**klicken Sie dann auf **AD FS Verwaltung**.  

2.  Klicken Sie in der Konsolen Struktur **unter\\AD FS Vertrauens**Stellungen entweder auf **Anspruchs Anbieter** -Vertrauens Stellungen oder Vertrauens Stellungen der vertrauenden **Seite**, und klicken Sie dann auf eine bestimmte Vertrauensstellung in der Liste, in der Sie diese Regel erstellen möchten.  

3.  Klicken\-Sie mit der rechten Maustaste auf die ausgewählte Vertrauensstellung und dann auf **Anspruchs Regeln bearbeiten**.  
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule6.PNG) 

4.  Wählen Sie im Dialogfeld **Anspruchs Regeln bearbeiten** eine der folgenden Registerkarten aus, die von der zu bearbeitenden Vertrauensstellung und dem Regelsatz abhängt, den Sie diese Regel erstellen möchten, und klicken Sie dann auf **Regel hinzufügen** , um den Regel-Assistenten zu starten, der diesem Regelsatz zugeordnet ist. :  

    -   **Akzeptanz Transformationsregeln**  

    -   **Ausstellungs Transformationsregeln**  

    -   **Ausstellungs Autorisierungs Regeln**  

    -   **Delegierungs Autorisierungs Regeln**  
![Regel erstellen](media/Create-a-Rule-to-Permit-All-Users/permitall5.PNG)

5.  Wählen Sie auf der Seite **Regel Vorlage auswählen** unter **Anspruchs Regel Vorlage**die **Option eingehenden Anspruch** in der Liste umwandeln aus, und klicken Sie dann auf **weiter**.  
![Regel erstellen](media/Create-a-Rule-to-Transform-an-Incoming-Claim/transform1.PNG)    

6.  Geben Sie auf der Seite **Regel konfigurieren** einen Anspruchs Regel Namen ein.  

7.  Wählen Sie unter **Typ des eingehenden Anspruchs**in der Liste die Option **Authentifizierungsmethode** aus.  

8.  Wählen Sie unter **Typ des ausgehenden Anspruchs**in der Liste die Option **Authentifizierungsmethode** aus.  

9. Wählen Sie **einen eingehenden Anspruchs Wert durch einen anderen ausgehenden Anspruchs Wert ersetzen**aus, und führen Sie dann die folgenden Schritte aus:  

    1.  Geben Sie unter **eingehender Anspruchs Wert**einen der folgenden URI-Werte ein, die auf dem ursprünglich verwendeten Authentifizierungsmethoden-URI basieren, klicken Sie auf **Fertig**stellen, und klicken Sie dann auf **OK** , um die Regel zu speichern.  

    2.  Geben Sie unter **Wert des ausgehenden Anspruchs**einen der Standard-URI-Werte in der folgenden Tabelle ein, der von der neuen bevorzugten Authentifizierungsmethode abhängt, klicken Sie auf **Fertig**stellen, und klicken Sie dann auf **OK** , um die Regel zu speichern.  

|              Tatsächliche Authentifizierungsmethode              |                                Entsprechender URI                                 |
|--------------------------------------------------------|----------------------------------------------------------------------------------|
|         Authentifizierung mit Benutzername und Kennwort          | https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/password  |
|                 Windows-Authentifizierung                 |  https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/windows  |
| Gegenseitige TLS-Authentifizierung, die X. 509-Zertifikate verwendet | https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/tlsclient |
|   X. 509 @ no__t-0basierte Authentifizierung, die TLS nicht verwendet    |   https://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/x509    |

![Regel erstellen](media/Create-a-Rule-to-Send-an-Authentication-Method-Claim/auth3.PNG)

> [!NOTE]  
> Andere URI-Werte können zusätzlich zu den Werten in der Tabelle verwendet werden. Die URI-Werte, die in der vorherigen Tabelle angezeigt werden, entsprechen den URIs, die von der vertrauenden Seite standardmäßig akzeptiert werden.  

## <a name="additional-references"></a>Weitere Verweise 
[Konfigurieren von Anspruchsregeln](Configure-Claim-Rules.md)  

[Prüfliste: Erstellen von Anspruchsregeln für eine Vertrauensstellung der vertrauenden Seite](https://technet.microsoft.com/library/ee913578.aspx)  

[Prüfliste: Erstellen von Anspruchsregeln für eine Anspruchsanbieter-Vertrauensstellung](https://technet.microsoft.com/library/ee913564.aspx)  

[Wann sollte eine Autorisierungs Anspruchs Regel verwendet werden?](../../ad-fs/technical-reference/When-to-Use-an-Authorization-Claim-Rule.md)  

[Rolle von Ansprüchen](../../ad-fs/technical-reference/The-Role-of-Claims.md)  

[Rolle von Anspruchsregeln](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md) 
