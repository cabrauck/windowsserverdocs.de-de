---
title: Sicherheitsgruppe „Geschützte Benutzer“
description: Windows Server-Sicherheit
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: security-credential-protection
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 1b0b5180-f65a-43ac-8ef3-66014116f296
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/12/2016
ms.openlocfilehash: 0cbec876ebf8a3ce27bf0d6f099ade6a5d6bc032
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71403779"
---
# <a name="protected-users-security-group"></a>Sicherheitsgruppe „Geschützte Benutzer“

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Dieses Thema für IT-Experten beschreibt die Active Directory-Sicherheitsgruppe „Geschützte Benutzer“ und erklärt deren Funktionsweise. Diese Gruppe wurde in Windows Server 2012 R2-Domänen Controllern eingeführt.

## <a name="BKMK_ProtectedUsers"></a>Übersicht über

Diese Sicherheitsgruppe ist als Teil einer Strategie zum Verwalten der Gefährdung von Anmelde Informationen innerhalb des Unternehmens konzipiert. Für Mitglieder dieser Gruppe gilt automatisch nicht konfigurierbarer Schutz für deren Konten. Eine Mitgliedschaft in der Gruppe der geschützten Benutzer bedeutet standardmäßig eine restriktive und proaktive Sicherheit. Die einzige Methode zum Ändern dieses Schutzes für ein Konto ist die Entfernung dieses Kontos aus der Sicherheitsgruppe.

> [!WARNING]
> Konten für Dienste und Computer sollten nie Mitglied der Gruppe "geschützte Benutzer" sein. Diese Gruppe bietet trotzdem unvollständigen Schutz, da das Kennwort oder Zertifikat immer auf dem Host verfügbar ist. Bei der Authentifizierung tritt ein Fehler auf, \"der Benutzername oder das Kennwort für alle Dienste oder Computer, die der Gruppe der geschützten Benutzer hinzugefügt wurden, nicht korrekt ist @ no__t-1.

Diese Domänen bezogene globale Gruppe löst nicht konfigurierbaren Schutz auf Geräten und Host Computern aus, auf denen Windows Server 2012 R2 ausgeführt wird, und Windows 8.1 oder höher für Benutzer in Domänen mit einem primären Domänen Controller, auf dem Windows Server 2012 R2 ausgeführt wird. Dadurch wird der Standard Speicherbedarf von Anmelde Informationen erheblich reduziert, wenn Benutzer sich mit diesen Schutzvorrichtungen bei Computern anmelden.

Weitere Informationen finden Sie unter [Funktionsweise der Gruppe "geschützte Benutzer](#BKMK_HowItWorks) " in diesem Thema.



## <a name="BKMK_Requirements"></a>Anforderungen der Gruppe "geschützte Benutzer"
Zum Bereitstellen von Geräteschutz für Mitglieder der Gruppe "geschützte Benutzer" müssen folgende Anforderungen erfüllt sein:

- Die globale Sicherheitsgruppe der geschützten Benutzer wird zu allen Domänencontrollern in der Kontodomäne repliziert.

- Windows 8.1 und Windows Server 2012 R2 haben standardmäßig Unterstützung hinzugefügt. Die [Microsoft-Sicherheitsempfehlung 2871997](https://technet.microsoft.com/library/security/2871997) bietet Unterstützung für Windows 7, Windows Server 2008 R2 und Windows Server 2012.

Folgende Anforderungen müssen erfüllt sein, damit Mitglieder der Gruppe der geschützten Benutzer Domänencontrollerschutz erhalten:

- Benutzer müssen sich in Domänen befinden, die die Domänen Funktionsebene Windows Server 2012 R2 oder höher aufweisen.

### <a name="adding-protected-user-global-security-group-to-down-level-domains"></a>Hinzufügen geschützter Benutzer globaler Sicherheitsgruppen zu untergeordneten Domänen

Domänen Controller, auf denen ein älteres Betriebssystem als Windows Server 2012 R2 ausgeführt wird, können das Hinzufügen von Mitgliedern zur neuen Sicherheitsgruppe für geschützte Benutzer unterstützen. Dies ermöglicht es den Benutzern, vor dem Upgrade der Domäne vom Geräteschutz zu profitieren. 

> [!Note]
> Domänen Controller werden von den Domänen Controllern nicht unterstützt. 

Die Gruppe "geschützte Benutzer" kann erstellt werden, indem [die Rolle "primärer Domänen Controller (PDC)](https://technet.microsoft.com/library/cc816944(v=ws.10).aspx) " auf einen Domänen Controller mit Windows Server 2012 R2 übertragen wird. Nachdem das Gruppenobjekt auf andere Domänencontroller repliziert wurde, kann die PDC-Emulatorrolle auf einem Domänencontroller gehostet werden, der unter einer älteren Windows Server-Version läuft.

### <a name="BKMK_ADgroup"></a>Eigenschaften der Gruppe "geschützte Benutzer"

Die folgende Tabelle zeigt die Eigenschaften der Gruppe der geschützten Benutzer.

|Attribut|Wert|
|-------|-----|
|Gut bekannte SID/RID|S-1-5-21-<domain>-525|
|Typ|Globale Domäne|
|Standardcontainer|CN=Benutzer, DC=<domain>, DC=|
|Standardmitglieder|Keine|
|Standardmitglied von|Keine|
|Geschützt durch ADMINSDHOLDER?|Nein|
|Speichern, um aus Standardcontainer zu entfernen?|Ja|
|Speichern, um die Verwaltung dieser Gruppe zu Nicht-Dienstadministratoren zu delegieren?|Nein|
|Standardbenutzerrechte|Keine Standardbenutzerrechte.|

## <a name="BKMK_HowItWorks"></a>Funktionsweise der Gruppe "geschützte Benutzer"
In diesem Abschnitt wird erklärt, wie die Gruppe der geschützten Benutzer funktioniert, wenn folgende Voraussetzungen erfüllt sind:

-   Signiert in einem Windows-Gerät

-   Die Benutzerkonto Domäne befindet sich in einer Windows Server 2012 R2-oder einer höheren Domänen Funktionsebene.

### <a name="device-protections-for-signed-in-protected-users"></a>Geräteschutz für signierte geschützte Benutzer
Wenn der angemeldete Benutzer ein Mitglied der Gruppe "geschützte Benutzer" ist, werden die folgenden Schutzmaßnahmen angewendet:

-   Bei der Delegierung von Gruppenrichtlinie Anmelde Informationen (aufwärtssp) werden die nur-Text-Anmelde Informationen des Benutzers nicht zwischengespeichert, auch wenn die Einstellung **Delegieren von Standard Anmelde Informationen zulassen** aktiviert ist.

-   Ab Windows 8.1 und Windows Server 2012 R2 werden die nur-Text-Anmelde Informationen des Benutzers von Windows Digest nicht zwischengespeichert, selbst wenn Windows Digest aktiviert ist.

> [!Note]
> Nach der Installation der [Microsoft-Sicherheitsempfehlung 2871997](https://technet.microsoft.com/library/security/2871997) werden die Anmelde Informationen von Windows Digest weiterhin zwischengespeichert, bis der Registrierungsschlüssel konfiguriert wurde. Siehe [Microsoft-Sicherheitsempfehlung: Aktualisieren Sie, um den Schutz von Anmelde Informationen zu verbessern 13. Mai 2014 @ no__t-0, um Anweisungen zu erhalten.

-   NTLM speichert nicht die nur-Text-Anmelde Informationen des Benutzers oder die unidirektionale NT-Funktion (ntowf).

-   Kerberos erstellt nicht mehr den-oder RC4-Schlüssel. Außerdem werden die nur-Text-Anmelde Informationen des Benutzers oder langfristige Schlüssel nicht zwischengespeichert, nachdem das erste TGT abgerufen wurde.

-   Bei der Anmeldung oder beim Entsperren wird keine zwischengespeicherte Überprüfung erstellt, sodass die Offline Anmeldung nicht mehr unterstützt wird.

Nachdem das Benutzerkonto der Gruppe der geschützten Benutzer hinzugefügt wurde, beginnt der Schutz, wenn sich der Benutzer beim Gerät anmeldet.

### <a name="domain-controller-protections-for-protected-users"></a>Schutz von Domänen Controllern für geschützte Benutzer
Konten, die Mitglieder der Gruppe der geschützten Benutzer sind, die sich bei einer Windows Server 2012 R2-Domäne authentifizieren, können folgende Aktionen nicht ausführen:

-   Authentifizieren mit NTLM-Authentifizierung.

-   Verwenden von DES- oder RC4-Verschlüsselungstypen in Kerberos-Vorauthentifizierung.

-   Delegierung mit eingeschränkter oder nicht eingeschränkter Delegierung.

-   Erneuern der Kerberos-TGTs außerhalb der ursprünglichen Lebensdauer von vier Stunden.

Nicht konfigurierbare Einstellungen zum Ablauf von TGTs werden für jedes Konto in der Gruppe der geschützten Benutzer eingerichtet. Normalerweise legt der Domänencontroller die Lebensdauer und Erneuerung der TGTs basierend auf den Domänenrichtlinien fest, **Max. Gültigkeitsdauer des Benutzertickets** und **Max. Zeitraum, in dem ein Benutzerticket erneuert werden kann**. Für die Gruppe der geschützten Benutzer ist 600 Minuten für diese Domänenrichtlinien eingestellt.

Weitere Informationen finden Sie unter [Konfigurieren geschützter Konten](how-to-configure-protected-accounts.md).

## <a name="troubleshooting"></a>Problembehandlung
Es gibt zwei betriebliche Administrativprotokolle für die Fehlerbehebung von Ereignissen hinsichtlich geschützter Benutzer. Diese neuen Protokolle befinden sich in der Ereignisanzeige und sind standardmäßig deaktiviert. Sie finden Sie unter **Anwendungs- und Dienstprotokolle\Microsoft\Windows\Microsoft\Authentifizierung**.

|Ereignis-ID und Protokoll|Beschreibung|
|----------|--------|
|104<br /><br />**ProtectedUser-Client**|Grund: Das Sicherheitspaket auf dem Client enthält keine Anmeldeinformationen.<br /><br />Der Fehler wird im Clientcomputer protokolliert, wenn das Konto Mitglied der Sicherheitsgruppe der geschützten Benutzer ist. Das Ereignis zeigt an, dass das Sicherheitspaket die Anmeldeinformationen, die für die Serverauthentifizierung erforderlich sind, nicht zwischenspeichert.<br /><br />Zeigt den Paketnamen, Benutzernamen, Domänennamen und den Servernamen an.|
|304<br /><br />**ProtectedUser-Client**|Grund: Das Sicherheitspaket speichert nicht die Anmelde Informationen des geschützten Benutzers.<br /><br />Im Client wird ein Informations Ereignis protokolliert, um anzugeben, dass das Sicherheitspaket die Anmelde Informationen des Benutzers nicht zwischenspeichert. Es wird erwartet, dass Digest (WDigest), Delegierung von Anmeldeinformationen (CredSSP) und NTLM keine Anmeldeinformationen für geschützte Benutzer haben können. Anwendungen können weiterhin erfolgreich nach Anmeldeinformationen fragen.<br /><br />Zeigt den Paketnamen, Benutzernamen und Domänennamen an.|
|100<br /><br />**ProtectedUserFailures-DomainController**|Grund: Ein NTLM-Anmeldefehler ereignet sich für ein Konto in der Sicherheitsgruppe der geschützten Benutzer.<br /><br />Im Domänencontroller wird ein Fehler protokolliert, um anzugeben, dass die NTLM-Authentifizierung fehlgeschlagen ist, da das Konto Mitglied der Sicherheitsgruppe der geschützten Benutzer ist.<br /><br />Zeigt den Kontonamen und den Gerätenamen an.|
|104<br /><br />**ProtectedUserFailures-DomainController**|Grund: DES- oder RC4-Verschlüsselungstypen werden für die Kerberos-Authentifizierung verwendet, und ein Anmeldefehler ereignet sich für einen Benutzer in der Sicherheitsgruppe der geschützten Benutzer.<br /><br />Kerberos-Vorauthentifizierung ist fehlgeschlagen, da DES- und RC4-Verschlüsselungstypen nicht verwendet werden können, wenn das Konto Mitglied der Sicherheitsgruppe der geschützten Benutzer ist.<br /><br />(AES wird akzeptiert.)|
|303<br /><br />**ProtectedUserSuccesses-DomainController**|Grund: Ein Kerberos-Ticket-Granting-Ticket (TGT) wurde erfolgreich für ein Mitglied der Gruppe der geschützten Benutzer ausgegeben.|



## <a name="additional-resources"></a>Zusätzliche Ressourcen

-   [Schutz und Verwaltung von Anmeldeinformationen](credentials-protection-and-management.md)

-   [Authentifizierungsrichtlinien und Authentifizierungsrichtliniensilos](authentication-policies-and-authentication-policy-silos.md)

-   [Konfigurieren geschützter Konten](how-to-configure-protected-accounts.md)


