---
ms.assetid: cd4d4902-dcdf-49dd-8059-82a56bf4b585
title: Exportieren des Teils eines privaten Schlüssels aus einem Serverauthentifizierungszertifikat
description: ''
author: billmath
manager: femila
ms.date: 05/31/2017
ms.topic: article
ms.prod: windows-server
ms.technology: identity-adfs
ms.author: billmath
ms.openlocfilehash: 8e1bbeddc4bae1c420b6cc78b52d6b873320ae8f
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71359581"
---
# <a name="export-the-private-key-portion-of-a-server-authentication-certificate"></a>Exportieren des Teils eines privaten Schlüssels aus einem Serverauthentifizierungszertifikat

Jeder Verbund Server in einer Active Directory-Verbunddienste (AD FS) \(ad FS @ no__t-1-Farm muss Zugriff auf den privaten Schlüssel des Server Authentifizierungs Zertifikats haben. Wenn Sie eine Serverfarm mit Verbund Servern oder Webservern implementieren, benötigen Sie ein einzelnes Authentifizierungszertifikat. Dieses Zertifikat muss von einer Unternehmens Zertifizierungsstelle \(ca @ no__t-1 ausgestellt werden, und es muss über einen exportierbaren privaten Schlüssel verfügen. Der private Schlüssel des Serverauthentifizierungszertifikats muss exportierbar sein, damit er für alle Server in der Farm zur Verfügung gestellt werden kann.  
  
Dasselbe Konzept gilt für Verbund Server Proxy-Farmen in dem Sinne, dass alle Verbund Server Proxys in einer Farm den privaten Schlüsselteil desselben Server Authentifizierungs Zertifikats gemeinsam nutzen müssen.  
  
> [!NOTE]  
> Das AD FS-Verwaltungs-Snap @ no__t-0in bezieht sich auf Server Authentifizierungs Zertifikate für Verbund Server als Dienst Kommunikations Zertifikate.  
  
Abhängig von der Rolle, die dieser Computer wieder gibt, verwenden Sie dieses Verfahren auf dem Verbund Server Computer oder dem Verbund Server Proxy-Computer, auf dem Sie das Server Authentifizierungszertifikat mit dem privaten Schlüssel installiert haben. Wenn das Verfahren abgeschlossen ist, können Sie dieses Zertifikat dann auf der Standardwebsite jedes Servers in der Farm importieren. Weitere Informationen finden Sie unter [Importieren eines Server Authentifizierungs Zertifikats auf die Standard Website](Import-a-Server-Authentication-Certificate-to-the-Default-Web-Site.md).  
  
Sie müssen mindestens Mitglied der Gruppe **Administratoren** oder einer entsprechenden Gruppe auf dem lokalen Computer sein, um dieses Verfahren ausführen zu können.  Ausführliche Informationen zur Verwendung der entsprechenden Konten und Gruppenmitgliedschaften finden Sie unter [lokale und Domänen Standard Gruppen](https://go.microsoft.com/fwlink/?LinkId=83477).   
  
### <a name="to-export-the-private-key-portion-of-a-server-authentication-certificate"></a>So exportieren Sie den Bereich mit dem privaten Schlüssel eines Serverauthentifizierungszertifikats  
  
1. Geben Sie auf dem **Start** Bildschirm**Internetinformationsdienste \(iis @ no__t-3 Manager**ein, und drücken Sie dann die EINGABETASTE.  
  
2. Klicken Sie in der Konsolenstruktur auf **ComputerName**.  
  
3. Doppelklicken Sie im mittleren Bereich auf **Server Zertifikate**no__t-0.  
  
4. Klicken Sie im mittleren Bereich mit der rechten Maustaste auf das Zertifikat, das Sie exportieren möchten, und klicken Sie dann auf **exportieren**.  
  
5. Klicken Sie im Dialogfeld **Zertifikat exportieren** auf die **...** .  
  
6. Geben Sie unter **Dateiname den Namen** **C: \\** <em>nameof Certificate</em>ein, und klicken Sie dann auf **Öffnen**.  
  
7. Geben Sie das Kennwort für das Zertifikat ein, bestätigen Sie das Kennwort, und klicken Sie dann auf **OK**.  
  
8. Überprüfen Sie den Erfolg Ihres Exportvorgangs, indem Sie bestätigen, dass die von Ihnen angegebene Daten am angegebenen Standort erstellt wird.  
  
   > [!IMPORTANT]  
   > Damit dieses Zertifikat in den lokalen Zertifikatspeicher auf dem neuen Server importiert werden, müssen Sie die Datei auf ein physisches Speichermedium übertragen und ihre Sicherheit während des Transports auf den neuen Server sichern. Es ist äußerst wichtig, die Sicherheit des privaten Schlüssels zu gewähren. Wenn dieser Schlüssel gefährdet ist, wird die Sicherheit der gesamten AD FS Bereitstellung \(einschließlich der Ressourcen in Ihrer Organisation und in den Ressourcen Partnerorganisationen @ no__t-1 beeinträchtigt.  
  
9. Importieren Sie das exportierte Serverauthentifizierungszertifikat in den Zertifikatspeicher auf dem neuen Server, bevor Sie den Verbunddienst installieren. Weitere Informationen zum Importieren des Zertifikats finden Sie unter Importieren eines Server Zertifikats \([http: @no__t -2\/GO.Microsoft.com @ no__t-4fwlink @ no__t-5? linkid @ no__t-6108283](https://go.microsoft.com/fwlink/?LinkId=108283)\).  
  
## <a name="additional-references"></a>Weitere Verweise  
[Prüfliste: Einrichten eines Verbundservers](Checklist--Setting-Up-a-Federation-Server.md)  
  
[Prüfliste: Einrichten eines Verbundserverproxys](Checklist--Setting-Up-a-Federation-Server-Proxy.md)  
  
[Zertifikatanforderungen für Verbundserver](https://technet.microsoft.com/library/dd807040.aspx)  
  
[Zertifikatanforderungen für Verbundserverproxys](https://technet.microsoft.com/library/dd807054.aspx)  
  

