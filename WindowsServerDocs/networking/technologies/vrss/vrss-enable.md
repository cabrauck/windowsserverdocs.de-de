---
title: Aktivieren von vrss auf einem Virtual Network Adapter
description: In diesem Thema erfahren Sie, wie Sie vrss in Windows Server entweder mithilfe von Geräte-Manager oder Windows PowerShell aktivieren.
ms.prod: windows-server
ms.technology: networking
ms.topic: article
ms.assetid: cb48315c-0204-4927-aa24-64f6789c2e20
manager: dougkim
ms.localizationpriority: medium
ms.date: 09/05/2018
ms.author: pashort
author: shortpatti
ms.openlocfilehash: 8f2886f01e4835cf2edb86fcae0a1fe77bc03d25
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71405258"
---
# <a name="enable-vrss-on-a-virtual-network-adapter"></a>Aktivieren von vrss auf einem Virtual Network Adapter

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016

Der virtuelle RSS-\(vrss @ no__t-1 erfordert Warteschlange für virtuelle Computer \(vmq @ no__t-3-Unterstützung vom physischen Adapter. Wenn VMQ deaktiviert ist oder nicht unterstützt wird, ist die virtuelle Empfangs seitige Skalierung deaktiviert. 

Weitere Informationen finden Sie unter [Planen der Verwendung von vrss](vrss-plan.md).

## <a name="enable-vrss-on-a-vm"></a>Aktivieren von vrss auf einem virtuellen Computer
 
Verwenden Sie die folgenden Verfahren, um vrss entweder mithilfe von Windows PowerShell oder Geräte-Manager zu aktivieren.

-   Geräte-Manager
-   Windows PowerShell
  
### <a name="device-manager"></a>Geräte-Manager

Sie können dieses Verfahren verwenden, um vrss mithilfe von Geräte-Manager zu aktivieren.

>[!NOTE]
>Der erste Schritt in diesem Verfahren ist spezifisch für VMS, auf denen Windows 10 oder Windows Server 2016 ausgeführt wird. Wenn auf Ihrem virtuellen Computer ein anderes Betriebssystem ausgeführt wird, können Sie Geräte-Manager öffnen, indem Sie zuerst die Systemsteuerung öffnen und dann Geräte-Manager suchen und öffnen.
  
1.  Geben Sie auf der Taskleiste des virtuellen Computers in **Geben Sie hier den Suchbegriff** **Gerät**ein. 

2.  Klicken Sie in den Suchergebnissen auf **Geräte-Manager**.

3.  Klicken Sie in Geräte-Manager auf **Netzwerkadapter**erweitern. 

4.  Klicken Sie mit der rechten Maustaste auf den Netzwerkadapter, den Sie konfigurieren möchten, und klicken Sie dann auf **Eigenschaften**.<p>Das Dialogfeld **Eigenschaften** des Netzwerkadapters wird geöffnet.

5.  Klicken Sie in den **Eigenschaften**des Netzwerkadapters auf die Registerkarte **erweitert** . 

6.  Scrollen Sie in der **Eigenschaft**nach unten, und klicken Sie auf **Empfangs seitige Skalierung**. 

7.  Stellen Sie sicher, dass die Auswahl in **Wert** **aktiviert**ist. 

8.  Klicken Sie auf **OK**.
  
> [!NOTE]
> Auf der Registerkarte **erweitert** zeigen einige Netzwerkadapter auch die Anzahl der RSS-Warteschlangen an, die vom Adapter unterstützt werden.

---

### <a name="windows-powershell"></a>Windows PowerShell

Verwenden Sie das folgende Verfahren, um vrss mithilfe von Windows PowerShell zu aktivieren.

1. Öffnen Sie auf dem virtuellen Computer **Windows PowerShell**.

2. Geben Sie den folgenden Befehl ein, und stellen Sie sicher, dass Sie den *Adapter Name* -Wert für den Parameter " **-Name** " durch den Namen des Netzwerkadapters ersetzen, den Sie konfigurieren möchten, und drücken Sie dann die EINGABETASTE. 
  
   ```PowerShell
   Enable-NetAdapterRSS -Name "AdapterName"
   ```

   >[!TIP]
   >Alternativ können Sie den folgenden Befehl verwenden, um vrss zu aktivieren.
   >```PowerShell
   >Set-NetAdapterRSS -Name "AdapterName" -Enabled $True  
   >```

Weitere Informationen finden Sie unter [Windows PowerShell-Befehle für RSS und vrss](vrss-wps.md).

---