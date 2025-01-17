---
title: 'AD-Gesamtstruktur Wiederherstellung: RID-Pools werden erhöht'
description: ''
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.date: 08/09/2018
ms.topic: article
ms.prod: windows-server
ms.assetid: c37bc129-a5e0-4219-9ba7-b4cf3a9fc9a4
ms.technology: identity-adds
ms.openlocfilehash: aa1f5e8b40aa43fa2601bc6f11efe2fcd4ccd05e
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71369060"
---
# <a name="ad-forest-recovery---raising-the-value-of-available-rid-pools"></a>AD-Gesamtstruktur Wiederherstellung: erhöhen des Werts verfügbarer RID-Pools 

>Gilt für: Windows Server 2016, Windows Server 2012 und 2012 R2, Windows Server 2008 und 2008 R2

Verwenden Sie das folgende Verfahren, um den Wert der RID-Pools (relative ID) zu erhöhen, die der RID-Betriebs Master nach der Wiederherstellung des Domänen Controllers zuweist. Wenn Sie den Wert der verfügbaren RID-Pools erhöhen, können Sie sicherstellen, dass kein Domänen Controller eine Rid für einen Sicherheits Prinzipal zuweist, der nach der Sicherung erstellt wurde, die zum Wiederherstellen der Domäne verwendet wurde. 

## <a name="about-active-directory-rid-pools-and-ridavailablepool"></a>Informationen zu Active Directory RID-Pools und ridavailablepool

Jede Domäne verfügt über ein Objekt **CN = RID Manager $, CN = System, DC**=<*domain_name*>. Dieses Objekt verfügt über ein Attribut mit dem Namen **ridavailablepool**. Dieser Attribut Wert behält den globalen RID-Raum für eine gesamte Domäne bei. Der Wert ist eine große Ganzzahl mit oberen und unteren teilen. Der obere Teil definiert die Anzahl der Sicherheits Prinzipale, die für jede Domäne zugeordnet werden können (0x3fffffff oder direkt über 1 Milliarde). Der untere Teil ist die Anzahl der RIDs, die in der Domäne zugeordnet wurden. 
  
> [!NOTE]
> In Windows Server 2016 und 2012 wird die Anzahl der Sicherheits Prinzipale, die zugewiesen werden können, auf einen Wert über 2 Milliarden festgestellt. Weitere Informationen finden Sie unter [Verwalten der RID-Ausstellung](https://technet.microsoft.com/library/jj574229.aspx). 
  
- Beispiel Wert: 4611686014132422708  
- Niedriger Teil: 2100 (Anfang des nächsten RID-Pools, der zugeordnet werden soll)  
- Oberer Teil: 1073741823 (Gesamtzahl der RIDs, die in einer Domäne erstellt werden können)  
  
Wenn Sie den Wert der großen Ganzzahl vergrößern, erhöhen Sie den Wert des unteren Teils. Wenn Sie z. b. 100.000 zum Beispiel Wert 4611686014132422708 für eine Summe von 4611686014132522708 hinzufügen, ist der neue niedrige Teil 102100. Dies weist darauf hin, dass der nächste RID-Pool, der vom RID-Master zugewiesen wird, mit 102100 anstelle von 2100 beginnt. 
  
### <a name="to-raise-the-value-of-available-rid-pools-using-adsiedit-and-the-calculator"></a>So erhöhen Sie den Wert verfügbarer RID-Pools mithilfe von ADSIEdit und dem Rechner

1. Öffnen Sie Server-Manager, klicken Sie auf **Extras und dann auf** **ADSI-Bearbeitung**.
2. Klicken Sie mit der rechten Maustaste auf **Verbinden mit** , und verbinden Sie den Standard namens Kontext, und klicken Sie auf **OK**.
   ![adsi Edit @ no__t-1 
3. Navigieren Sie zum folgenden Distinguished Name-Pfad: **CN = RID Manager $, CN = System, DC = <domain name>** .
   ![adsi Edit @ no__t-1 
3. Klicken Sie mit der rechten Maustaste, und wählen Sie die Eigenschaften CN = RID Manager $ aus. 
4. Wählen Sie das Attribut **ridavailablepool**aus, klicken Sie auf **Bearbeiten**, und kopieren Sie dann den großen ganzzahligen Wert in die Zwischenablage.
   ![adsi Edit @ no__t-1  
5. Starten Sie den Rechner, und wählen Sie im Menü **Ansicht** die Option **wissenschaftlicher Modus**aus. 
6. Fügen Sie 100.000 zum aktuellen Wert hinzu.
   ![adsi Edit @ no__t-1 
7. Wenn Sie Strg + c oder den Befehl **Kopieren** im Menü **Bearbeiten** verwenden, kopieren Sie den Wert in die Zwischenablage. 
8. Fügen Sie im Dialogfeld "Bearbeiten" von ADSIEdit den neuen Wert ein. 
   ![adsi Edit @ no__t-1 
9. Klicken Sie im Dialogfeld auf OK **, und über** nehmen Sie das Eigenschaften Blatt, um das **ridavailablepool** -Attribut zu aktualisieren. 
  
### <a name="to-raise-the-value-of-available-rid-pools-using-ldp"></a>So erhöhen Sie den Wert der verfügbaren RID-Pools mithilfe von LDP  
  
1. Geben Sie an der Eingabeaufforderung den folgenden Befehl ein, und drücken Sie die EINGABETASTE:  
   **LDP**  
2. Klicken Sie auf **Verbindung**, auf **verbinden**, geben Sie den Namen des RID-Managers ein, und klicken Sie dann auf **OK**. 
   ![LDP @ NO__T-1
3. Klicken Sie auf **Verbindung**und dann auf **binden**, wählen Sie **mit Anmelde Informationen binden** aus, und geben **Sie Ihre**Administrator Anmelde Informationen ein. 
   ![LDP @ NO__T-1
4. KlickenSie auf Ansicht **und dann** auf Struktur, und geben Sie dann den folgenden Distinguished Name-Pfad ein  CN = RID Manager $, CN = System, DC =*Domänen Name*  
   ![LDP @ NO__T-1
5. Klicken Sie auf **Durchsuchen**und dann auf **ändern**. 
6. Fügen Sie 100.000 zum aktuellen **ridavailablepool** -Wert hinzu, und geben Sie dann die Summe in **Werte**ein. 
7. Geben Sie in **DN**`cn=RID Manager$,cn=System,dc=` *< Domänen Namen @ no__t-3*ein. 
8. Geben Sie unter **Eingabe Attribut bearbeiten**`rIDAvailablePool` ein. 
9. Wählen Sie als Vorgang **ersetzen** aus, und drücken Sie dann die **Eingabe**Taste.
   ![LDP @ NO__T-1 
10. Klicken Sie auf **Ausführen** , um den Vorgang auszuführen. Klicken Sie auf **Schließen**.
11. Klicken Sie zum Überprüfen der Änderung auf **Ansicht**, klicken **Sie auf Struktur, und**geben Sie dann den folgenden Distinguished Name-Pfad ein:   CN = RID-Manager $, CN = System, DC =*Domänen Name*.   Überprüfen Sie das **ridavailablepool** -Attribut. 
   ![LDP @ NO__T-1

## <a name="next-steps"></a>Nächste Schritte

- [Wiederherstellung der AD-Gesamtstruktur: Leitfaden](AD-Forest-Recovery-Guide.md)
- [Wiederherstellung der AD-Gesamtstruktur: Verfahren](AD-Forest-Recovery-Procedures.md)
