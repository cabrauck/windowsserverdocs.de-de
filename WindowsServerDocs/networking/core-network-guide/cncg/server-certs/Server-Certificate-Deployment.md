---
title: Bereitstellung von Serverzertifikaten
description: Dieses Thema ist Teil des Handbuchs Bereitstellen von Server Zertifikaten für drahtlose und drahtlose 802.1 x-bereit Stellungen.
manager: brianlic
ms.topic: article
ms.assetid: 1ae4384b-f4e4-41e8-bc5f-9ac41953bca4
ms.prod: windows-server
ms.technology: networking
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 2105e2ccad69fcfdbc13e3201b4362e5c6b932e1
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71406279"
---
# <a name="server-certificate-deployment"></a>Bereitstellung von Serverzertifikaten

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Führen Sie die folgenden Schritte aus, um eine Stamm Zertifizierungsstelle für Unternehmen zu installieren und Server Zertifikate für die Verwendung mit PEAP und EAP bereitzustellen.  
  
> [!IMPORTANT]  
> Bevor Sie Active Directory Zertifikat Dienste installieren, müssen Sie den Computer benennen, den Computer mit einer statischen IP-Adresse konfigurieren und den Computer der Domäne hinzufügen. Nachdem Sie AD CS installiert haben, können Sie den Computernamen oder die Domänen Mitgliedschaft des Computers nicht mehr ändern. Sie können die IP-Adresse bei Bedarf jedoch ändern. Weitere Informationen zum Ausführen dieser Aufgaben finden Sie im Handbuch zu Windows Server @ no__t-0 2016 [Core Network](../../Core-Network-Guide.md).  

  
-   [Installieren des Webservers WEB1](../../../core-network-guide/cncg/server-certs/Install-the-Web-Server-WEB1.md)  
  
-   [Erstellen eines Aliaseintrags (CNAME) in DNS für WEB1](../../../core-network-guide/cncg/server-certs/Create-an-Alias-CNAME-Record-in-DNS-for-WEB1.md)  
  
-   [Konfigurieren von WEB1 zum Verteilen von Zertifikat Sperr Listen (CRLs)](../../../core-network-guide/cncg/server-certs/Configure-WEB1-to-Distribute-Certificate-Revocation-Lists.md)  
  
-   [Vorbereiten der CAPolicy-INF-Datei](../../../core-network-guide/cncg/server-certs/Prepare-the-CAPolicy-inf-File.md)  
  
-   [Installieren der Zertifizierungsstelle](../../../core-network-guide/cncg/server-certs/Install-the-Certification-Authority.md)  
  
-   [Konfigurieren der CDP-und AIA-Erweiterungen auf CA1](../../../core-network-guide/cncg/server-certs/Configure-the-CDP-and-AIA-Extensions-on-CA1.md)  
  
-   [Kopieren des Zertifizierungsstellenzertifikats und der Zertifikatssperrliste in das virtuelle Verzeichnis](../../../core-network-guide/cncg/server-certs/Copy-the-CA-Certificate-and-CRL-to-the-Virtual-Directory.md)  
  
-   [Konfigurieren der Serverzertifikatvorlage](../../../core-network-guide/cncg/server-certs/Configure-the-Server-Certificate-Template.md)  
  
-   [Konfigurieren der automatischen Registrierung von Serverzertifikaten](../../../core-network-guide/cncg/server-certs/Configure-Server-Certificate-Autoenrollment.md)  
  
-   [Gruppenrichtlinie aktualisieren](../../../core-network-guide/cncg/server-certs/Refresh-Group-Policy.md)  
  
-   [Überprüfen der Server Registrierung eines Serverzertifikats](../../../core-network-guide/cncg/server-certs/Verify-Server-Enrollment-of-a-Server-Certificate.md)  
  
> [!NOTE]  
> Die Verfahren in diesem Handbuch beinhalten keine Anweisungen für Fälle, in denen das Dialogfeld **Benutzerkontensteuerung** geöffnet wird, um die Zustimmung zum Fortfahren abzufragen. Klicken Sie auf **Weiter**, wenn das Dialogfeld während der Ausführung der Verfahren in dieser Anleitung geöffnet wird und als Folge der ausgeführten Aktionen geöffnet wurde.  
  


