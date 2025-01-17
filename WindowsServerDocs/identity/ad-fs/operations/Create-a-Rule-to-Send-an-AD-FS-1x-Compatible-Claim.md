---
ms.assetid: 0039fbbb-b981-4526-a550-f3456ff27635
title: Erstellen einer Regel zum Transformieren eines eingehenden Anspruchs
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: d4e3a59ff9154a948143cef32103cae9f1f2d235
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71407597"
---
# <a name="create-a-rule-to-send-an-ad-fs-1x-compatible-claim"></a>Erstellen einer Regel zum Senden eines AD FS 1. x-kompatiblen Anspruchs

In Situationen, in denen Sie Active Directory-Verbunddienste (AD FS) \(ad FS @ no__t-1 verwenden, um Ansprüche auszugeben, die von Verbund Servern mit AD FS 1,0 \(Windows Server 2003 R2 @ no__t-3 oder AD FS 1,1 \(Windows Server 2008 oder Windows empfangen werden. Server 2008 R2 @ no__t-5: Sie müssen folgende Schritte ausführen:  
  
-   Erstellen Sie eine Regel, die einen namens-ID-Anspruchstyp mit dem Format UPN, e-Mail oder allgemeiner Name sendet.  
  
-   Alle anderen gesendeten Ansprüche müssen einen der folgenden Anspruchs Typen aufweisen:  
  
    -   AD FS 1. *e-* Mail-Adresse  
  
    -   AD FS 1. *x* -UPN  
  
    -   Allgemeiner Name  
  
    -   Gruppieren  
  
    -   Jeder andere Anspruchstyp, der mit https://schemas.xmlsoap.org/claims/ beginnt, z. b. https://schemas.xmlsoap.org/claims/EmployeeID  
  
Verwenden Sie je nach den Anforderungen Ihrer Organisation eines der folgenden Verfahren, um eine AD FS 1 zu erstellen. *x* -kompatibler Anspruch der NameID:  
  
-   Erstellen Sie diese Regel, um einen AD FS 1. x-namens-ID-Anspruch mithilfe der **Regel Vorlage "weiterleiten oder Filtern eines eingehenden Anspruchs** " auszugeben.  
  
-   Erstellen Sie diese Regel, um einen AD FS 1. x-namens-ID-Anspruch mithilfe der **Regel Vorlage zum Transformieren eines eingehenden Anspruchs**auszustellen. Diese Regel Vorlage kann in Situationen verwendet werden, in denen Sie den vorhandenen Anspruchstyp in einen neuen Anspruchstyp ändern möchten, der mit AD FS 1 funktioniert.  *x* -Ansprüche.  
  
> [!NOTE]  
> Damit diese Regel erwartungsgemäß funktioniert, müssen Sie sicherstellen, dass die Vertrauensstellung der vertrauenden Seite oder die Anspruchs Anbieter-Vertrauensstellung, bei der Sie diese Regel erstellen, für die Verwendung des **AD FS 1,0-und 1,1-Profils**konfiguriert wurde. 

## <a name="to-create-a-rule-to-issue-an-adfs1x-name-id-claim-using-the-pass-through-or-filter-an-incoming-claim-rule-template-on-a-relying-party-trust-in-windows-server-2016"></a>Erstellen Sie eine Regel, um eine AD FS 1 auszugeben. *x* Name ID-Anspruch mithilfe der Regel Vorlage zum durchlaufen oder Filtern eines eingehenden Anspruchs für eine Vertrauensstellung der vertrauenden Seite in Windows Server 2016 

1.  Klicken Sie in Server-Manager **auf Extras**, und wählen Sie dann **AD FS Verwaltung**aus.  
  
2.  Klicken Sie in der Konsolen Struktur unter **AD FS**auf Vertrauens Stellungen der vertrauenden **Seite**. 
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule9.PNG)  
  
3.  Klicken\-Sie mit der rechten Maustaste auf die ausgewählte Vertrauensstellung, und klicken Sie dann auf **Richtlinie**zum
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule10.PNG)   
  
4.  Klicken Sie im Dialogfeld **Richtlinie für Anspruchs Ausstellung bearbeiten** unter Ausstellungs **Transformationsregeln** auf **Regel hinzufügen** , um den Regel-Assistenten zu starten. 
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule11.PNG)    

5.  Wählen Sie auf der Seite **Regel Vorlage auswählen** unter **Anspruchs Regel Vorlage**die **Option Pass-Through oder einen eingehenden Anspruch Filtern** aus der Liste aus, und klicken Sie dann auf **weiter**.  
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule4.PNG)    

6.  Geben Sie auf der Seite **Regel konfigurieren** einen Anspruchs Regel Namen ein.  
  
7.  Wählen Sie unter **eingehender Anspruchstyp**die Option **Name ID** in der Liste aus.  
  
8.  Wählen Sie im **Format der eingehenden namens-ID**eine der folgenden AD FS 1 aus. *x*\- kompatible Anspruchs Formate aus der Liste:  
  
    -   **UPN**  
  
    -   **E @ no__t-1mail**  
  
    -   **Allgemeiner Name**  
  
9. Wählen Sie je nach den Anforderungen Ihrer Organisation eine der folgenden Optionen aus:  
  
    -   **Alle Anspruchs Werte weiterleiten**  
  
    -   **Nur einen bestimmten Anspruchs Wert weiterleiten**  
  
    -   **Nur Anspruchs Werte weiterleiten, die einem bestimmten e-Mail-suffixwert entsprechen**  
  
    -   **Nur Anspruchs Werte weiterleiten, die mit einem bestimmten Wert beginnen**  
![Regel erstellen](media/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim/adfs3.PNG)   

10. Klicken Sie auf **Fertig**stellen und dann auf **OK** , um die Regel zu speichern.  

  
## <a name="to-create-a-rule-to-issue-an-adfs1x-name-id-claim-using-the-pass-through-or-filter-an-incoming-claim-rule-template-on-a-claims-provider-trust-in-windows-server-2016"></a>Erstellen Sie eine Regel, um eine AD FS 1 auszugeben. ID-Anspruch des *x* -namens mit der Regel Vorlage zum durchlaufen oder Filtern einer eingehenden Anspruchs Vorlage für eine Anspruchs Anbieter-Vertrauensstellung in Windows Server 2016 
  
1.  Klicken Sie in Server-Manager **auf Extras**, und wählen Sie dann **AD FS Verwaltung**aus.  
  
2.  Klicken Sie in der Konsolen Struktur unter **AD FS**auf **Anspruchs Anbieter**-Vertrauens Stellungen. 
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule1.PNG)  
  
3.  Klicken\-Sie mit der rechten Maustaste auf die ausgewählte Vertrauensstellung und dann auf **Anspruchs Regeln bearbeiten**.
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule2.PNG)   
  
4.  Klicken Sie im Dialogfeld **Anspruchs Regeln bearbeiten** unter **Akzeptanz Transformationsregeln** auf **Regel hinzufügen** , um den Regel-Assistenten zu starten.
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule3.PNG)    

5.  Wählen Sie auf der Seite **Regel Vorlage auswählen** unter **Anspruchs Regel Vorlage**die **Option Pass-Through oder einen eingehenden Anspruch Filtern** aus der Liste aus, und klicken Sie dann auf **weiter**.  
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule4.PNG)    

6.  Geben Sie auf der Seite **Regel konfigurieren** einen Anspruchs Regel Namen ein.  
  
7.  Wählen Sie unter **eingehender Anspruchstyp**die Option **Name ID** in der Liste aus.  
  
8.  Wählen Sie im **Format der eingehenden namens-ID**eine der folgenden AD FS 1 aus. *x*\- kompatible Anspruchs Formate aus der Liste:  
  
    -   **UPN**  
  
    -   **E @ no__t-1mail**  
  
    -   **Allgemeiner Name**  
  
9. Wählen Sie je nach den Anforderungen Ihrer Organisation eine der folgenden Optionen aus:  
  
    -   **Alle Anspruchs Werte weiterleiten**  
  
    -   **Nur einen bestimmten Anspruchs Wert weiterleiten**  
  
    -   **Nur Anspruchs Werte weiterleiten, die einem bestimmten e-Mail-suffixwert entsprechen**  
  
    -   **Nur Anspruchs Werte weiterleiten, die mit einem bestimmten Wert beginnen**  
![Regel erstellen](media/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim/adfs3.PNG)

10. Klicken Sie auf **Fertig**stellen und dann auf **OK** , um die Regel zu speichern.  


## <a name="to-create-a-rule-to-transform-an-incoming-claim-on-a-relying-party-trust-in-windows-server-2016"></a>So erstellen Sie eine Regel zum Transformieren eines eingehenden Anspruchs für eine Vertrauensstellung der vertrauenden Seite in Windows Server 2016 

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
  
7.  Wählen Sie unter Typ des **eingehenden Anspruchs**den Typ des eingehenden Anspruchs aus, den Sie in der Liste transformieren möchten.  
  
8.  Wählen Sie unter **Typ des ausgehenden Anspruchs**die Option **Name ID** in der Liste aus.  
  
9. Wählen Sie im **Format der ausgehenden namens-ID**eine der folgenden AD FS 1 aus. *x*\- kompatible Anspruchs Formate aus der Liste:  
  
    -   **UPN**  
  
    -   **E @ no__t-1mail**  
  
    -   **Allgemeiner Name**  
  
10. Wählen Sie je nach den Anforderungen Ihrer Organisation eine der folgenden Optionen aus:  
  
    -   **Alle Anspruchs Werte weiterleiten**  
  
    -   **Einen eingehenden Anspruchs Wert durch einen anderen ausgehenden Anspruchs Wert ersetzen**  
  
    -   **Ersetzen eingehender e @ no__t-1mail-suffixansprüche durch ein neues e @ no__t-2mail-Suffix**  
![Regel erstellen](media/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim/adfs4.PNG)

11. Klicken Sie auf **Fertig**stellen und dann auf **OK** , um die Regel zu speichern.  

  


## <a name="to-create-a-rule-to-transform-an-incoming-claim-on-a-claims-provider-trust-in-windows-server-2016"></a>So erstellen Sie eine Regel zum Transformieren eines eingehenden Anspruchs für eine Anspruchs Anbieter-Vertrauensstellung in Windows Server 2016 
  
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
  
7.  Wählen Sie unter Typ des **eingehenden Anspruchs**den Typ des eingehenden Anspruchs aus, den Sie in der Liste transformieren möchten.  
  
8.  Wählen Sie unter **Typ des ausgehenden Anspruchs**die Option **Name ID** in der Liste aus.  
  
9. Wählen Sie im **Format der ausgehenden namens-ID**eine der folgenden AD FS 1 aus. *x*\- kompatible Anspruchs Formate aus der Liste:  
  
    -   **UPN**  
  
    -   **E @ no__t-1mail**  
  
    -   **Allgemeiner Name**  
  
10. Wählen Sie je nach den Anforderungen Ihrer Organisation eine der folgenden Optionen aus:  
  
    -   **Alle Anspruchs Werte weiterleiten**  
  
    -   **Einen eingehenden Anspruchs Wert durch einen anderen ausgehenden Anspruchs Wert ersetzen**  
  
    -   **Ersetzen eingehender e @ no__t-1mail-suffixansprüche durch ein neues e @ no__t-2mail-Suffix**  
![Regel erstellen](media/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim/adfs4.PNG)    

11. Klicken Sie auf **Fertig**stellen und dann auf **OK** , um die Regel zu speichern.  













  
## <a name="to-create-a-rule-to-issue-an-adfs1x-name-id-claim-using-the-pass-through-or-filter-an-incoming-claim-rule-template-on-windows-server-2012-r2"></a>Erstellen Sie eine Regel, um eine AD FS 1 auszugeben. ID-Anspruch des *x* -namens mit der Regel Vorlage zum durchlaufen oder Filtern einer eingehenden Anspruchs Vorlage auf Windows Server 2012 R2
  
1.  Klicken Sie in Server-Manager **auf Extras, und**klicken Sie dann auf **AD FS Verwaltung**.  
  
2.  Klicken Sie in der Konsolen Struktur **unter\\AD FS Vertrauens**Stellungen entweder auf **Anspruchs Anbieter** -Vertrauens Stellungen oder Vertrauens Stellungen der vertrauenden **Seite**, und klicken Sie dann auf eine bestimmte Vertrauensstellung in der Liste, in der Sie diese Regel erstellen möchten.  
  
3.  Klicken\-Sie mit der rechten Maustaste auf die ausgewählte Vertrauensstellung und dann auf **Anspruchs Regeln bearbeiten**.  
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule6.PNG) 
  
4.  Wählen Sie im Dialogfeld **Anspruchs Regeln bearbeiten** je nach der zu bearbeitenden Vertrauensstellung und dem Regelsatz, in dem Sie diese Regel erstellen möchten, eine der folgenden Registerkarten aus, und klicken Sie dann auf **Regel hinzufügen** , um den Regel-Assistenten zu starten, der diesem Regelsatz zugeordnet ist. :  
  
    -   **Akzeptanz Transformationsregeln**  
  
    -   **Ausstellungs Transformationsregeln**  
  
    -   **Ausstellungs Autorisierungs Regeln**  
  
    -   **Delegierungs Autorisierungs Regeln**  
![Regel erstellen](media/Create-a-Rule-to-Permit-All-Users/permitall5.PNG)    

5.  Wählen Sie auf der Seite **Regel Vorlage auswählen** unter **Anspruchs Regel Vorlage**die **Option Pass-Through oder einen eingehenden Anspruch Filtern** aus der Liste aus, und klicken Sie dann auf **weiter**.  
![Regel erstellen](media/Create-a-Rule-to-Pass-Through-or-Filter-an-Incoming-Claim/claimrule7.PNG)  
  
6.  Geben Sie auf der Seite **Regel konfigurieren** einen Anspruchs Regel Namen ein.  
  
7.  Wählen Sie unter **eingehender Anspruchstyp**die Option **Name ID** in der Liste aus.  
  
8.  Wählen Sie im **Format der eingehenden namens-ID**eine der folgenden AD FS 1 aus. *x*\- kompatible Anspruchs Formate aus der Liste:  
  
    -   **UPN**  
  
    -   **E @ no__t-1mail**  
  
    -   **Allgemeiner Name**  
  
9. Wählen Sie je nach den Anforderungen Ihrer Organisation eine der folgenden Optionen aus:  
  
    -   **Alle Anspruchs Werte weiterleiten**  
  
    -   **Nur einen bestimmten Anspruchs Wert weiterleiten**  
  
    -   **Nur Anspruchs Werte weiterleiten, die einem bestimmten e-Mail-suffixwert entsprechen**  
  
    -   **Nur Anspruchs Werte weiterleiten, die mit einem bestimmten Wert beginnen**  
![Regel erstellen](media/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim/adfs1.PNG)

10. Klicken Sie auf **Fertig**stellen und dann auf **OK** , um die Regel zu speichern.  

  
## <a name="to-create-a-rule-to-issue-an-adfs1x-name-id-claim-using-the-transform-an-incoming-claim-rule-template-in-windows-server-2012-r2"></a>Erstellen Sie eine Regel, um eine AD FS 1 auszugeben. ID-Anspruch des *x* -namens mit der Regel Vorlage zum Transformieren eines eingehenden Anspruchs in Windows Server 2012 R2  
  
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
  
7.  Wählen Sie unter Typ des **eingehenden Anspruchs**den Typ des eingehenden Anspruchs aus, den Sie in der Liste transformieren möchten.  
  
8.  Wählen Sie unter **Typ des ausgehenden Anspruchs**die Option **Name ID** in der Liste aus.  
  
9. Wählen Sie im **Format der ausgehenden namens-ID**eine der folgenden AD FS 1 aus. *x*\- kompatible Anspruchs Formate aus der Liste:  
  
    -   **UPN**  
  
    -   **E @ no__t-1mail**  
  
    -   **Allgemeiner Name**  
  
10. Wählen Sie je nach den Anforderungen Ihrer Organisation eine der folgenden Optionen aus:  
  
    -   **Alle Anspruchs Werte weiterleiten**  
  
    -   **Einen eingehenden Anspruchs Wert durch einen anderen ausgehenden Anspruchs Wert ersetzen**  
  
    -   **Ersetzen eingehender e @ no__t-1mail-suffixansprüche durch ein neues e @ no__t-2mail-Suffix**  
![Regel erstellen](media/Create-a-Rule-to-Send-an-AD-FS-1x-Compatible-Claim/adfs2.PNG)    

11. Klicken Sie auf **Fertig**stellen und dann auf **OK** , um die Regel zu speichern.  

## <a name="additional-references"></a>Weitere Verweise 
[Konfigurieren von Anspruchsregeln](Configure-Claim-Rules.md)  
 
[Prüfliste: Erstellen von Anspruchsregeln für eine Vertrauensstellung der vertrauenden Seite](https://technet.microsoft.com/library/ee913578.aspx)  

[Prüfliste: Erstellen von Anspruchsregeln für eine Anspruchsanbieter-Vertrauensstellung](https://technet.microsoft.com/library/ee913564.aspx)  
  
[Wann sollte eine Autorisierungs Anspruchs Regel verwendet werden?](../../ad-fs/technical-reference/When-to-Use-an-Authorization-Claim-Rule.md)  

[Rolle von Ansprüchen](../../ad-fs/technical-reference/The-Role-of-Claims.md)  
  
[Rolle von Anspruchsregeln](../../ad-fs/technical-reference/The-Role-of-Claim-Rules.md) 
