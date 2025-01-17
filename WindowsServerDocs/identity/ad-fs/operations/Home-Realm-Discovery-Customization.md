---
ms.assetid: 626e33fc-4ac2-4d38-9ac9-addaa4c8d9bb
title: Anpassung der Startbereichs Ermittlung
description: ''
author: billmath
ms.author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.openlocfilehash: 5a151e46e566d9f5459419771cbd476bb26c248d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71357963"
---
# <a name="home-realm-discovery-customization"></a>Anpassung der Startbereichs Ermittlung


Wenn der AD FS Client zuerst eine Ressource anfordert, hat der Ressourcen Verbund Server keine Informationen zum Bereich des Clients. Der Ressourcen Verbund Server antwortet dem AD FS-Client mit einer Seite zur **Client Bereichs** Ermittlung, auf der der Benutzer den Startbereich aus einer Liste auswählt. Die Listenwerte werden aus der Anzeigenameneigenschaft in den Anspruchsanbieter-Vertrauensstellungen entnommen. Verwenden Sie die folgenden Windows PowerShell-Cmdlets, um die AD FS Home Realm Discovery-Funktion zu ändern und anzupassen.  
  
![Startbereich](media/AD-FS-user-sign-in-customization/ADFS_Blue_Custom4.png)  
  
> [!WARNING]  
> Beachten Sie, dass der für lokale Active Directory-Bereitstellungen angezeigt Anspruchsanbietername der Anzeigename des Verbunddiensts ist.  
  



## <a name="configure-identity-provider-to-use-certain-email-suffixes"></a>Konfigurieren des Identitätsanbieters für die Verwendung bestimmter E-Mail-Suffixe  
Eine Organisation kann einen Verbund mit mehreren Anspruchsanbietern eingehen. AD FS bietet Administratoren nun die Funktion "in @ no__t-0box", die es Administratoren ermöglicht, die Suffixe aufzulisten, z. b. @us.contoso.com, @eu.contoso.com, die von einem Anspruchs Anbieter unterstützt wird, und aktivieren Sie Sie für Suffix @ no__t-3based Discovery. Mit dieser Konfiguration können Endbenutzer Ihr Organisations Konto eingeben, und AD FS wählt automatisch den entsprechenden Anspruchs Anbieter aus.  
  
Verwenden Sie das folgende Windows PowerShell-Cmdlet und die folgende Syntax, um einen Identitäts Anbieter \(idp @ no__t-1 (z. b. `fabrikam`) für die Verwendung bestimmter e-Mail-Suffixe zu konfigurieren.  
  

`Set-AdfsClaimsProviderTrust -TargetName fabrikam -OrganizationalAccountSuffix @("fabrikam.com";"fabrikam2.com") ` 
 
>[!NOTE]
> Legen Sie beim Verbund zwischen zwei AD FS Servern die promptloginfederation-Eigenschaft für die Anspruchs Anbieter-Vertrauensstellung auf forwardpromptandhintsoverwsfederation fest.  Dies ist der Fall, wenn AD FS den login_hint und die Eingabeaufforderung an den IDP weiterleiten.  Dies kann durch Ausführen des folgenden PowerShell-Cmdlets erreicht werden:
>
>`Set-AdfsclaimsProviderTrust -PromptLoginFederation ForwardPromptAndHintsOverWsFederation`

## <a name="configure-an-identity-provider-list-per-relying-party"></a>Konfigurieren einer Identitätsanbieterliste pro vertrauender Seite  
In einigen Szenarios möchte eine Organisation möglicherweise, dass Endbenutzern nur die Anspruchsanbieter angezeigt werden, die für eine Anwendung spezifisch sind, sodass nur eine Untersammlung von Anspruchsanbietern auf der Seite zur Startbereichsermittlung angezeigt wird.  
  
Verwenden Sie zum Konfigurieren einer IDP-Liste pro Vertrauender Seite \(rp @ no__t-1 das folgende Windows PowerShell-Cmdlet und die folgende Syntax.  
  
 
`Set-AdfsRelyingPartyTrust -TargetName claimapp -ClaimsProviderName @("Fabrikam","Active Directory") ` 

  
## <a name="bypass-home-realm-discovery-for-the-intranet"></a>Umgehen der Startbereichsermittlung für das Intranet  
Die meisten Organisationen unterstützen nur ihr internes Active Directory für jeden Benutzer, dessen Zugriff von innerhalb der Firewall erfolgt. In diesen Fällen können Administratoren AD FS so konfigurieren, dass die Startbereichs Ermittlung für das Intranet umgangen wird.  
  
Verwenden Sie das folgende Windows PowerShell-Cmdlet und die folgende Syntax, um die HRD für das Intranet zu umgehen.  
  

`Set-AdfsProperties -IntranetUseLocalClaimsProvider $true ` 
 
  
> [!IMPORTANT]  
> Beachten Sie Folgendes: Wenn eine Identitäts Anbieterliste für eine vertrauende Seite konfiguriert wurde, zeigt AD FS weiterhin die Seite \(hrd @ no__t-1 der Startbereichs Ermittlung an, obwohl die vorherige Einstellung aktiviert wurde und der Benutzer auf das Intranet zugreift. Zum Umgehen der Startbereichsermittlung in diesem Fall müssen Sie sicherstellen, dass Active Directory ebenfalls zur Identitätsanbieterliste für diese vertrauende Seite hinzugefügt wird.  

## <a name="additional-references"></a>Weitere Verweise 
[AD FS Anpassung der Benutzeranmeldung](AD-FS-user-sign-in-customization.md)  
