---
ms.assetid: 399a8bbe-3375-4bb0-b55b-5f46e7050028
title: 'Replikationsfehler 1396: Anmeldefehler. Der Zielkontoname ist falsch'
description: ''
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adds
ms.openlocfilehash: a8af10fd54f557e4f4a2127dbd1cc178d53d93a4
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71402482"
---
# <a name="replication-error-1396-logon-failure-the-target-account-name-is-incorrect"></a>Replikationsfehler 1396: Anmeldefehler. Der Zielkontoname ist falsch

>Gilt für: Windows Server 2016, Windows Server 2012 R2, Windows Server 2012


<developerConceptualDocument xmlns="https://ddue.schemas.microsoft.com/authoring/2003/5" xmlns:xlink="https://www.w3.org/1999/xlink" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="https://ddue.schemas.microsoft.com/authoring/2003/5 http://clixdevr3.blob.core.windows.net/ddueschema/developer.xsd"> <introduction> @ no__t-2 @ no__t-3<para>In diesem Artikel werden die Symptome, Ursachen und Fehlerbehebung Active Directory Replikation mit dem Win32-Fehler 1396 beschrieben: &quot;Anmeldung fehlgeschlagen: Der Name des Ziel Kontos ist falsch. &quot; </para>
    <list class="bullet"> <listItem> @ no__t-2 @ no__t-3<para>
          <link xlink:href="d3a01966-74c9-4c49-ba11-354b9acf7519#BKMK_Symptoms">Symptome</link>
 @ no__t-2</para>
      </listItem> <listItem> @ no__t-2 @ no__t-3<para>
          <link xlink:href="d3a01966-74c9-4c49-ba11-354b9acf7519#BKMK_Causes">Bewirkt</link>
 @ no__t-2</para>
      </listItem> <listItem> @ no__t-2 @ no__t-3<para>
          <link xlink:href="d3a01966-74c9-4c49-ba11-354b9acf7519#BKMK_Resolutions">Auflösungen</link>
 @ no__t-2</para>
      </listItem>
    </list>
  </introduction>
  <section address="BKMK_Symptoms">
    <title>symptome @ no__t-1 @ no__t-2 @ no__t-3<para />
      <list class="ordered">
<listItem><para>Dcdiag meldet, dass der Active Directory Replications-Test mit Fehler 1396 fehlgeschlagen ist: Anmeldefehler: Der Name des Ziel Kontos ist falsch. &quot;</para><code>Testing server: &lt;Site name&gt;&lt;DC Name&gt;
Starting test: Replications
[Replications Check,&lt;DC Name&gt;] A recent replication attempt failed:
From &lt;source DC&gt; to &lt;destination DC&gt;
Naming Context: CN=&lt;DN path of naming context&gt;
<codeFeaturedElement>The replication generated an error (1396):
Logon Failure: The target account name is incorrect.</codeFeaturedElement>
The failure occurred at &lt;date&gt; &lt;time&gt;.
The last success occurred at &lt;date&gt; &lt;time&gt;.
XX failures have occurred since the last success</code></listItem><listItem><para>REPADMIN. EXE meldet, dass der letzte Replikations Versuch mit dem Status 1396 fehlgeschlagen ist.</para><para>Repadmin-Befehle, die häufig den 1396-Status angeben, enthalten u. a. die folgenden:</para><table xmlns:caps="https://schemas.microsoft.com/build/caps/2013/11"><tbody><tr><TD><list class="bullet"><listItem><para>REPADMIN/ADD</para></listItem><listItem><para>REPADMIN/REPLSUM</para></listItem><listItem><para>REPADMIN/REHOST</para></listItem><listItem><para>REPADMIN/SHOWVECTOR/LATENCY</para></listItem></list></TD><TD><list class="bullet"><listItem><para>REPADMIN/SHOWREPS</para></listItem><listItem><para>REPADMIN/SHOWREPL</para></listItem><listItem><para>REPADMIN/SYNCALL</para></listItem></list></TD></tr></tbody></table><para>Beispielausgabe von &quot;repadmin/SHOWREPS @ no__t-1, @no__t die die eingehende Replikation von "Configuration Manager" zu "" in "" darstellt. Der Name des Ziel Kontos ist falsch. &quot;-Fehler wird unten angezeigt:</para><code>Default-First-Site-NameCONTOSO-DC1
DSA Options: IS_GC 
Site Options: (none)
DSA object GUID: b6dc8589-7e00-4a5d-b688-045aef63ec01
DSA invocationID: b6dc8589-7e00-4a5d-b688-045aef63ec01
==== INBOUND NEIGHBORS ======================================
DC=contoso,DC=com
Default-First-Site-NameCONTOSO-DC2 via RPC
DSA object GUID: 74fbe06c-932c-46b5-831b-af9e31f496b2
Last attempt @ &lt;date&gt; &lt;time&gt; failed, <codeFeaturedElement>result 1396 (0x574):
Logon Failure: The target account name is incorrect.</codeFeaturedElement>
&lt;#&gt; consecutive failure(s).
Last success @ &lt;date&gt; &lt;time&gt;.
</code></listItem><listItem><para>Der Befehl " <ui>Jetzt replizieren</ui> " in Active Directory Websites und Dienste gibt &quot;logon-Fehler zurück: Der Name des Ziel Kontos ist falsch. &quot;</para><para>Wenn Sie von einem Quell Domänen Controller mit der rechten Maustaste auf das Verbindungs Objekt klicken und <ui>Jetzt replizieren</ui> auswählen, tritt ein Fehler &quot;logon auf: Der Name des Ziel Kontos ist falsch. &quot; Die Bildschirm Fehlermeldung wird unten angezeigt:</para><para>Text des Dialog Titels:</para><para>Jetzt replizieren</para><para>Text der Dialog Meldung: </para><para>Fehler beim Versuch, den namens Kontext &lt;partition-DNS-Pfad @ no__t-1 vom Domänen Controller &lt;source DC @ no__t-3 an den Domänen Controller zu synchronisieren &lt;destination DC @ no__t-5: Anmeldefehler: Der Name des Ziel Kontos ist falsch. Dieser Vorgang wird nicht fortgesetzt. </para></listItem><listItem><para>NTDS-KCC-, NTDS-allgemeine oder Microsoft-Windows-ActiveDirectory_DomainService-Ereignisse mit dem 1396-Status werden im Verzeichnisdienste-Protokoll Ereignisanzeige protokolliert.</para><para>Active Directory Ereignisse, die den 1396-Status häufig erwähnen, sind u. a. die folgenden:</para><table xmlns:caps="https://schemas.microsoft.com/build/caps/2013/11"><thead><tr><TD><para>Ereignis-ID</para></TD><TD><para>Ereignisquelle</para></TD><TD><para>Ereignis Zeichenfolge</para></TD></tr></thead><tbody><tr><TD><para>1125</para></TD><TD><para>Microsoft-Windows-ActiveDirectory_DomainService</para></TD><TD><para>Die Assistent zum Installieren von Active Directory Domain Services (Dcpromo) konnte keine Verbindung mit dem folgenden Domänen Controller herstellen.</para></TD></tr><tr><TD><para>1645</para><para>Dieses Ereignis listet den dreiteiligen SPN auf.</para></TD><TD><para>NTDS-Replikation</para></TD><TD><para>Active Directory hat den authentifizierten Remoteprozeduraufruf (RPC) zu einer anderen Domäne nicht ausgeführt, weil der gewünschte Dienstprinzipalname (SPN) für den Zieldomänencontroller im Schlüsselverteilungscenter (KDC)-Domänencontroller, der zum SPN gehört, nicht registriert ist.</para></TD></tr><tr><TD><para>1655</para></TD><TD><para>Microsoft-Windows-ActiveDirectory_DomainService</para></TD><TD><para>Active Directory Domain Services versuchte, mit dem folgenden globalen Katalog zu kommunizieren, und die Versuche waren nicht erfolgreich.</para></TD></tr><tr><TD><para>2847</para></TD><TD><para>Microsoft-Windows-ActiveDirectory_DomainService</para></TD><TD><para>Die Konsistenzprüfung hat eine Replikations Verbindung für den lokalen schreibgeschützten Verzeichnisdienst gefunden und versucht, Sie Remote auf der folgenden Verzeichnisdienst Instanz zu aktualisieren. Der Vorgang ist fehlgeschlagen. Der Vorgang wird wiederholt.</para></TD></tr><tr><TD><para>1925</para></TD><TD><para>NTDS-KCC</para></TD><TD><para>Der Versuch, einen Replikations Link für die folgende beschreibbare Verzeichnis Partition einzurichten, ist fehlgeschlagen.</para></TD></tr><tr><TD><para>1926</para></TD><TD><para>NTDS-KCC</para></TD><TD><para>Der Versuch, einen Replikations Link mit einer schreibgeschützten Verzeichnis Partition mit den folgenden Parametern zu erstellen, ist fehlgeschlagen.</para></TD></tr><tr><TD><para>5781</para></TD><TD><para>NETLOGON</para></TD><TD><para> Der Server kann seinen Namen nicht in DNS registrieren.</para></TD></tr></tbody></table></listItem><listItem><para>DCPROMO schlägt mit einem Bildschirm Fehler fehl</para><para>Text des Dialog Titels:</para><para>Active Directory Installation fehlgeschlagen</para><para>Text der Dialog Meldung:</para><para>Fehler beim Ausführen des Vorgangs: Der Verzeichnisdienst konnte das Server Objekt für CN = NTDS Settings, CN = serverbeinggestuft, CN = Servers, CN = site, CN = Sites, CN = Configuration, DC =%% amp; quot; DC = com auf Server ReplicationSourceDC.contoso.com nicht erstellen. </para><para>Stellen Sie sicher, dass die bereitgestellten Netzwerk Anmelde Informationen über ausreichende Zugriffsrechte für das Hinzufügen eines </para><para>
&quot;logon-Fehler: Der Name des Ziel Kontos ist falsch. [mailto:johndoe@mydomain.com](&quot;)</para><para>In diesem Fall werden die Ereignis-ID 1645, 1168 und 1125 auf dem Server protokolliert, der höher gestuft wird.</para></listItem><listItem><para>Zuordnen eines Laufwerks mithilfe von " <embeddedLabel>net use</embeddedLabel>":</para><code>C:&gt;net use z: &lt;server_name&gt;c$
System error 1396 has occurred.
Logon Failure: The target account name is incorrect.</code><para>In diesem Fall kann der Server auch die Ereignis-ID 333 im System Ereignisprotokoll protokollieren und eine große Menge an virtuellem Arbeitsspeicher für eine Anwendung verwenden, wie z. b. SQL Server.</para></listItem><listItem><para>Die DC-Zeit ist falsch.</para></listItem><listItem><para>Der KDC startet nicht auf einem RODC, nachdem das krbtgt-Konto für den RODC wieder hergestellt wurde, das gelöscht wurde. Nach einer Wiederherstellung wird z. b. Fehler 1396 angezeigt. </para><para>
Die Ereignis-ID 1645 wird auf dem RODC protokolliert. </para><para>
Dcdiag meldet außerdem eine Fehlermeldung, dass das RODC-krbtgt-Konto nicht aktualisiert werden kann. </para></listItem>
</list>
    </content>
  </section>
  <section address="BKMK_Causes">
    <title>bewirkt @ no__t-1 @ no__t-2 @ no__t-3<para />
      <list class="ordered">
        <listItem>
          <para>Der SPN ist nicht im globalen Katalog vorhanden, der vom KDC durchsucht wird, wenn der Client versucht, sich mithilfe von Kerberos zu authentifizieren.</para>
          <para>Im Zusammenhang mit Active Directory Replikation ist der Kerberos-Client der Ziel-DC. der KDC, der die SPN-Suche ausführt, ist wahrscheinlich der Ziel-DC selbst, kann jedoch ein Remote-DC sein.</para>
        </listItem>
        <listItem>
          <para>Das Benutzer-oder Dienst Konto, das den zu suchenden Dienst Prinzipal Namen enthalten soll, ist nicht im globalen Katalog vorhanden, der vom KDC im Auftrag des Zieldomänen Controllers, der die Replikation versucht, durchsucht wurde.</para>
          <para>Im Zusammenhang mit Active Directory Replikation ist das Computer Konto des Quell Domänen Controllers in dem globalen Katalog, der vom Domänen Controller für den Zieldomänen Controller nach der eingehenden Replikation durchsucht wird, nicht vorhanden</para>
        </listItem>
        <listItem>
          <para>Auf dem Ziel-DC fehlt ein LSA-Geheimnis für die Domäne der Quell Domänen Controller.</para>
        </listItem>
        <listItem>
          <para>Der SPN, der gesucht wird, ist auf einem anderen Computer Konto als der Quell Domänen Controller vorhanden.</para>
        </listItem>
      </list>
    </content>
  </section>
  <section address="BKMK_Resolutions">
    <title>auflösungen @ no__t-1 @ no__t-2 @ no__t-3 @ no__t-4 @ no__t-5<para>Überprüfen Sie das Verzeichnisdienst-Ereignisprotokoll auf dem Ziel-DC für das NTDS-Replikations Ereignis 1645. Beachten Sie Folgendes:</para>
          <para>Der Name des Ziel-DC.</para>
          <para>Der SPN, der gesucht wird (E3514235-4B06-11d1-AB04-00C04FC2DCD2/&lt;objekt-GUID für Quell Domänen Controller NTDS-Einstellungs Objekt @ no__t-1 @ no__t-2 @ no__t-3target Domäne @ no__t-4Amp; gt;. &amp;Amp; lt; TLD @ no__t-6amp; gt; @ &lt;target Domäne @ no__t-8. &lt;tld @ no__t-10</para>
          <para>Der vom Ziel-DC verwendete KDC</para>
        </listItem>
        <listItem>
          <para>Geben Sie in der Konsole des KDC, der in Schritt 1 identifiziert wurde, Folgendes ein: </para>
          <code>nltest /dsgetdc &lt;forest root DNS domain name &gt; /gc</code>
          <para>Führen Sie den NLTEST-Serverlocatorpunkt-Test direkt nach einem Replikations Versuch aus, der mit dem Fehler 1396 auf dem Ziel-DC fehlschlägt. </para>
          <para>Dadurch sollte der GC identifiziert werden, mit dem der KDC SPN-suchen ausführt. </para>
          <para>Der GC, der vom KDC durchsucht wird, kann auch in Microsoft-Windows-ActiveDirectory_DomainService-Ereignis 1655 aufgezeichnet werden.</para>
        </listItem>
        <listItem>
          <para>Suchen Sie nach dem in Schritt 1 ermittelten Dienst Prinzipal Namen im globalen Katalog, der in Schritt 2 erkannt wurde.</para>
          <code>C:&gt;repadmin /showattr Server_Name DC=corp,DC=contoso,dc=com &lt;GC used by KDC&gt; &lt;DN path of forest root domain&gt; /filter:&quot;(serviceprincipalname=&lt;SPN cited in the NTDS Replication event 1645&gt;)&quot; /gc /subtree /atts:cn,serviceprincipalname</code>
          <para>oder</para>
          <code>C:&gt;dsquery * forestroot -scope subtree -filter &quot;(serviceprincipalname=E3514235-4B06-11D1-AB04-00C04FC2DCD2/65cead9f-4949-46a3-a49a-f1fbfe13d2b3*)&quot; -attr * -s Server_Name.europe.corp.contoso.com</code>
          <para>Vergewissern Sie sich, dass das Host Objekt für den SPN vorhanden ist.</para>
          <para>Überprüfen Sie den DN-Pfad für das Host Objekt, z. b., ob das Objekt cnf/Konflikt hat oder sich im verlorenen und gefundenen Container befindet.</para>
          <para>Vergewissern Sie sich, dass die Quell Domänen Controller Active Directory Replikations-SPN nur auf dem Computer Konto der Quell Domänen Controller</para>
          <para>Wenn der Replikations-SPN fehlt, stellen Sie fest, ob der Quell Domänen Controller seinen SPN bei sich selbst registriert hat und ob der SPN auf der vom KDC verwendeten GC aufgrund einer einfachen Replikations Latenz oder eines Replikations Fehlers fehlt.</para>
        </listItem>
        <listItem>
          <para>Überprüfen Sie die Integrität des sicheren Kanals und den Vertrauens Zustand.</para>
        </listItem>
      </list>
    </content>
  </section>
  <relatedTopics> @ no__t-1 @ no__t-2troubleshooting Active Directory Vorgänge, die mit Fehler 1396 fehlschlagen: Anmeldefehler: Der Name des Ziel Kontos ist falsch. </linkText>
      <linkUri><a href="https://support.microsoft.com/kb/2183411/en-gb" data-raw-source="https://support.microsoft.com/kb/2183411/en-gb">https://support.microsoft.com/kb/2183411/en-gb</a></linkUri>
    </externalLink>
  </relatedTopics> @ no__t-6


