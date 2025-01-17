---
title: Replikat Server müssen konfiguriert werden, um bestimmte primäre Server zu identifizieren
description: Enthält Anweisungen zum Beheben des Problems, das von dieser Best Practices Analyzer Regel gemeldet wird.
ms.prod: windows-server
ms.service: na
manager: dongill
ms.technology: compute-hyper-v
ms.author: kathydav
ms.topic: article
ms.assetid: 0aeb1f4b-2e75-430b-9557-fe64738c4992
author: KBDAzure
ms.date: 8/16/2016
ms.openlocfilehash: 567b20d00d2f245ae7e9577d9d200dca116a9b4d
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71364736"
---
# <a name="replica-servers-should-be-configured-to-identify-specific-primary-servers-authorized-to-send-replication-traffic"></a>Replikat Server müssen konfiguriert werden, um bestimmte primäre Server zu identifizieren

>Gilt für: Windows Server 2016

Weitere Informationen zu bewährten Methoden und Scans finden Sie unter [Ausführen von Best Practices Analyzer Scans und Verwalten der Scan Ergebnisse](https://go.microsoft.com/fwlink/p/?LinkID=223177).  
  
|Eigenschaft|Details|  
|-|-|  
|**Betriebssystem**|Windows Server 2016|  
|**Produkt/Feature**|Hyper-V|  
|**Zunehmen**|Warnung|  
|**Kategorie**|Konfiguration|  
  
In den folgenden Abschnitten gibt kursiv formatics den UI-Text an, der im Best Practices Analyzer Tool für dieses Problem angezeigt wird.  
  
## <a name="issue"></a>Problem  
*Wie konfiguriert, akzeptiert dieser Replikat Server Replikations Datenverkehr von allen primären Servern und speichert Sie an einem einzigen Speicherort.*  
  
### <a name="impact"></a>Auswirkungen  
*Die gesamte Replikation von allen primären Servern wird an einem Speicherort gespeichert, was zu Datenschutz-oder Sicherheitsproblemen führen kann.*  
  
## <a name="resolution"></a>Auflösung  
*verwenden Sie den Hyper-V-Manager, um neue Autorisierungs Einträge für die primären Server zu erstellen, und geben Sie jeweils separate Speicherorte an. Sie können Platzhalter Zeichen verwenden, um primäre Server in Mengen für jeden Autorisierungs Eintrag zu gruppieren.*  
  
#### <a name="create-authorization-entries-using-hyper-v-manager"></a>Erstellen von Autorisierungs Einträgen mit dem Hyper-V-Manager  
  
1.  Öffnen Sie den Hyper-V-Manager. ( **Klicken Sie**in Server-Manager auf Extras  > **Hyper-V-Manager**.)  
  
2.  Klicken Sie in der Liste der Hosts mit der rechten Maustaste auf das gewünschte, und klicken Sie dann auf **Hyper-V-Einstellungen**.  
  
3.  Klicken Sie im Navigationsbereich auf **Replikationskonfiguration**.  
  
4.  Klicken Sie unter **Autorisierung und Speicher**auf **Replikation von den angegebenen Servern zulassen**.  
  
5.  Klicken Sie unter der Liste der Server auf **Hinzufügen**.  
  
6.  Unter **Autorisierungs Eintrag hinzufügen**:  
  
    -   Geben Sie den voll qualifizierten Namen des ersten Servers ein.  
  
    -   Geben Sie einen dedizierten Speicherort an, um nur die Dateien dieses Servers zu speichern.  
  
7.  Klicken Sie auf **OK**.  
  
8.  Wiederholen Sie diesen Vorgang für jeden primären Server.  
  
9. Klicken Sie erneut auf **OK** , um das Fenster zu schließen und zu schließen.  
  
### <a name="create-authorization-entries-using-windows-powershell"></a>Erstellen von Autorisierungs Einträgen mithilfe von Windows PowerShell  
  
1.  Öffnen Sie Windows PowerShell. (Klicken Sie auf dem Desktop auf Start, und beginnen Sie mit der Eingabe von **Windows PowerShell**.)  
  
2.  Klicken Sie mit der rechten Maustaste auf **Windows PowerShell** und dann auf **als Administrator ausführen**.  
  
3.  Führen Sie einen Befehl ähnlich dem folgenden aus, und ersetzen Sie dabei:  
  
    -   Der primäre Servername von Server01.domain01.contoso.com mit dem voll qualifizierten Domänen Namen des Servers.  
  
    -   Der Speicherort von d:\replicavmstorage mit ihrem Speicherort.  
  
    -   Die Vertrauens Gruppe mit dem Namen "Default" (Standard) mit dem Namen der Gruppe, wenn Sie eine erstellt haben. Wenn nicht, verwenden Sie die Standardeinstellung.  
  
```  
New-VMReplicationAuthorizationEntry server01.domain01.contoso.com D:\ReplicaVMStorage DEFAULT  
```  
  
## <a name="see-also"></a>Siehe auch  
[New-vmreplicationauthorizationentry](https://technet.microsoft.com/library/hh848606.aspx)  
  


