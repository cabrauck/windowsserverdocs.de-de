---
title: Konfigurieren des Serverspeichers
description: Beschreibt die Verwendung von Windows Server Essentials
ms.custom: na
ms.date: 10/03/2016
ms.prod: windows-server-2016-essentials
ms.reviewer: na
ms.suite: na
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ef7ddcdd-3a74-40ca-9487-c3a6fc5155a5
author: nnamuhcs
ms.author: coreyp
manager: dongill
ms.openlocfilehash: 718080c050dadc20837ab6b11a677029227e1709
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2019
ms.locfileid: "70865042"
---
# <a name="configure-server-storage"></a>Konfigurieren des Serverspeichers

>Gilt für: Windows Server 2016 Essentials, Windows Server 2012 R2 Essentials, Windows Server 2012 Essentials

## <a name="sample-hard-disk-configurations"></a>Beispiele für Festplattenkonfigurationen  
 Die folgende Tabelle enthält Beispiele für Festplattenkonfiguration. Die Schätzwerte basieren auf typischer Verwendung und Funktionalität, berücksichtigen jedoch keine Aspekte, die sich auf die optimale Leistung auswirken. Sie können unter Berücksichtigung der Vorgaben und Anforderungen des Kunden einen beliebigen Typ von unterstützter Festplatte für diese Konfigurationen verwenden (z. B. SATA oder SCSI).  
  
> [!IMPORTANT]
>   Windows Server Essentials muss als Volume "C:" installiert sein, und die Volumegröße muss mindestens 60 GB betragen. Es wird empfohlen, zwei Partitionen auf dem Betriebssystemlaufwerk zu erstellen und ":C" (Systempartition) nicht zum Speichern von Geschäftsdaten zu verwenden.  
  
|Serverebene|Datenträgerkonfiguration|  
|------------------|------------------------|  
|Eingabe|-Zwei physische Datenträger<br /><br /> : Konfiguriert als RAID 1-Spiegel Satz, der Folgendes enthält:<br /><br /> -C: Volume? 60 GB<br /><br /> -D: Volume? 1000 GB|  
|Mittel|-Drei physische Datenträger<br /><br /> : Konfiguriert als RAID 5-Gruppe, die Folgendes enthält:<br /><br /> -C: Volume? 60 GB<br /><br /> -D: Volume? 1500 GB|  
|Hoch|-Mindestens fünf physische Datenträger insgesamt<br /><br /> -Zwei Datenträger in einem RAID 1-Spiegel Satz, der das Volume "C:" enthält? 100 GB<br /><br /> -Alle verbleibenden Datenträger in einem RAID 5-Satz, der Folgendes enthält:<br /><br /> -D: Volume? 1500 GB<br /><br /> -E: Volume? 1500 GB|  
  
 Diese Empfehlungen berücksichtigen die Größe des installierten Betriebssystems, die durchschnittliche Größe des vom Server verwendeten Datenspeichers sowie das während der Lebensdauer des Servers erwartete Wachstum des Datenspeichers. Die Volumes können Partitionen auf einem physischen Datenträger sein, oder sie können sich auf separaten physischen Datenträgern befinden. Da der Server wichtige Daten für Ihren Kunden speichert, wird empfohlen, mehrere physische Datenträger zu verwenden und die Daten Ihres Kunden mithilfe von Hardware-RAID oder Speicherplätzen zu schützen.  
  
## <a name="configuring-your-server-backup"></a>Konfigurieren der Serversicherung  
 Neben den internen Festplatten auf dem Server sollten Kunden die Verwendung externer USB-Festplatten für Datensicherungen in Betracht ziehen. Idealerweise besitzt der Kunde mindestens zwei externe Festplatten mit ausreichender Kapazität zum Sichern aller Daten auf dem Server. Wenn externe Festplatten verwendet werden, kann der Kunde jeweils eine Festplatte an einem anderen Standort aufbewahren, um die Daten noch besser zu schützen.  
  
## <a name="partition-configuration"></a>Partitionskonfiguration  
 Während der Erstkonfiguration des Servers wird in der größten Datenpartition auf Datenträger 0 eine Reihe von Standardordnern erstellt, zu denen freigegebene Ordner und Ordner für die Clientcomputersicherung gehören.  
  
## <a name="see-also"></a>Siehe auch  

 [Einführung in das Windows Server Essentials ADK](Getting-Started-with-the-Windows-Server-Essentials-ADK.md)   
 [Erstellen und Anpassen des Bilds](Creating-and-Customizing-the-Image.md)   
 [Weitere Anpassungen](Additional-Customizations.md)   
 [Vorbereiten des Images für die Bereitstellung](Preparing-the-Image-for-Deployment.md)   
 [Testen der Benutzerfreundlichkeit](Testing-the-Customer-Experience.md)

 [Einführung in das Windows Server Essentials ADK](../install/Getting-Started-with-the-Windows-Server-Essentials-ADK.md)   
 [Erstellen und Anpassen des Bilds](../install/Creating-and-Customizing-the-Image.md)   
 [Weitere Anpassungen](../install/Additional-Customizations.md)   
 [Vorbereiten des Images für die Bereitstellung](../install/Preparing-the-Image-for-Deployment.md)   
 [Testen der Benutzerfreundlichkeit](../install/Testing-the-Customer-Experience.md)

