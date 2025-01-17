---
title: Grundlegendes zu Funktionen
description: In diesem Thema wird das Konzept der Funktionen in System Insights definiert und die in Windows Server 2019 verfügbaren Standardfunktionen vorgestellt.
ms.custom: na
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: system-insights
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ''
author: gawatu
ms.author: gawatu
manager: mallikarjun.chadalapaka
ms.date: 6/05/2018
ms.openlocfilehash: 90622fba1fc33966bd064c19056204013ff0c33b
ms.sourcegitcommit: f6490192d686f0a1e0c2ebe471f98e30105c0844
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/10/2019
ms.locfileid: "70869157"
---
# <a name="understanding-capabilities"></a>Grundlegendes zu Funktionen

>Gilt für: Windows Server 2019

In diesem Thema wird das Konzept der Funktionen in System Insights definiert und die in Windows Server 2019 verfügbaren Standardfunktionen vorgestellt. 

In diesem Thema werden auch die Datenquellen, Vorhersagezeit Achsen und Vorhersage Status beschrieben, die für die Standardfunktionen verwendet werden. 

## <a name="capability-overview"></a>Übersicht über die Funktionen
Eine System Insights-Funktion ist ein Machine Learning-oder Statistik Modell, das Systemdaten analysiert, um Ihnen einen besseren Einblick in die Funktionsweise Ihrer Bereitstellung zu verschaffen. System Insights führt einen anfänglichen Satz von Standardfunktionen ein und ermöglicht das dynamische Hinzufügen neuer Funktionen, ohne dass das Betriebssystem aktualisiert werden muss. 

>[!NOTE]
>Ausführliche Informationen zum Erstellen, hinzufügen und Aktualisieren von Funktionen finden Sie [hier](adding-and-developing-capabilities.md). [das Dokument zur Verwaltung von Funktionen](managing-capabilities.md) bietet weitere allgemeine Informationen zu dieser Funktionalität.

Außerdem wird jede Funktion lokal auf einer Windows Server-Instanz ausgeführt, und jede Funktion kann einzeln verwaltet werden.

### <a name="capability-outputs"></a>Funktions Ausgaben
Wenn eine Funktion aufgerufen wird, stellt Sie eine Ausgabe bereit, um das Ergebnis der Analyse oder Vorhersage zu erläutern. Jede Ausgabe muss einen **Status** und eine **Statusbeschreibung** enthalten, um die Vorhersage zu beschreiben, und jedes Ergebnis kann optional Funktions spezifische Daten enthalten, die mit der Vorhersage verknüpft sind. Die **Statusbeschreibung** enthält eine kontextbezogene Erläuterung für den **Status**, und die Funktion meldet entweder den Status " **OK**", " **Warnung**" oder " **kritisch** ". Außerdem kann eine Funktion einen **Fehler** oder **keinen** Status verwenden, wenn keine Vorhersage erstellt wurde. Im folgenden finden Sie die Funktionsstatus und ihre grundlegende Bedeutung: 

- **OK** : alles sieht gut aus.
- **Warnung** : Es ist keine sofortige Beachtung erforderlich, aber Sie sollten sich einen Blick darauf machen. 
- **Kritisch** : Sie sollten sich bald einen Einblick machen. 
- **Fehler** : ein unbekanntes Problem hat dazu geführt, dass die Funktion fehlgeschlagen ist. 
- **None** : Es wurde keine Vorhersage erstellt. Dies kann auf fehlende oder andere Funktions spezifische Gründe zurückzuführen sein, die keine Vorhersage treffen. 

Außerdem werden alle Funktions spezifischen Daten, die im Ergebnis enthalten sind, in einer vom Benutzer zugänglichen JSON-Datei platziert, und der Dateipfad [kann mithilfe von PowerShell gefunden werden](https://docs.microsoft.com/windows-server/manage/system-insights/managing-capabilities#retrieving-capability-results). 

## <a name="default-capabilities"></a>Standardfunktionen
In Windows Server 2019 werden mit System Insights vier Standardfunktionen eingeführt, die sich auf die Kapazitäts Vorhersage konzentrieren:

- **CPU-Kapazitäts Vorhersage** : prognostiziert CPU-Auslastung. 
- Netzwerk **Kapazitäts Vorhersage** : prognostiziert die Netzwerk Auslastung für jeden Netzwerkadapter. 
- **Prognose zur Gesamtspeicher** Auslastung: prognostiziert den gesamten Speicherverbrauch auf allen lokalen Laufwerken. 
- **Prognose für den Volumenverbrauch** : prognostiziert den Speicherverbrauch für jedes Volume.

Jede Funktion analysiert Vergangenheits Daten, um die zukünftige Verwendung vorherzusagen. **alle Vorhersagefunktionen sind so konzipiert, dass Sie langfristige Trends und nicht das kurzfristige Verhalten prognostizieren**und Administratoren dabei helfen, Hardware richtig bereitzustellen und zu optimieren. Ihre Arbeits Auslastungen, um zukünftige Ressourcenkonflikte zu vermeiden. Da diese Funktionen sich auf die langfristige Verwendung konzentrieren, analysieren diese Funktionen tägliche Daten. 

### <a name="forecasting-model"></a>Vorhersagemodell
Die Standardfunktionen verwenden ein Planungsmodell, um die zukünftige Verwendung vorherzusagen, und für jede Vorhersage wird das Modell lokal auf den Daten des Computers trainiert. Dieses Modell ist so konzipiert, dass langfristige Trends erkannt werden, und das erneute trainieren auf jeder Windows Server-Instanz ermöglicht die Anpassung an das spezifische Verhalten und die benutzerspezifischen Aspekte der einzelnen Computer.

>[!NOTE]
>Wenn Sie bestimmen, welcher Modelltyp verwendet werden muss, testen Sie viele Modelle mithilfe eines Datasets, das Zehntausende von Computern enthält. Nachdem Sie diese Modelle analysiert und optimiert haben, haben wir uns entschieden, ein Modell für die automatische Regression zu verwenden, da es hochgradig präzise und visuell intuitive Vorhersagen erzeugt, ohne zu viel Zeit zum trainieren zu benötigen. Dieses Modell erfordert jedoch drei Wochen Trainingsdaten, sodass jede Funktion einen grundlegenden linearen Trend verwendet, bis drei Wochen Daten verfügbar sind.

### <a name="forecasting-timelines"></a>Vorhersagezeit Achsen
Die Standardfunktionen prognostizieren eine bestimmte Anzahl von Tagen in der Zukunft, basierend auf der Anzahl der Tage, für die Daten erfasst wurden. In der folgenden Tabelle werden die vorhersagbaren Zeitachsen dieser Funktionen angezeigt:

| Größe der Eingabedaten | Prognose Länge |
| --------------- | --------------- |
| 0-5 Tage | Es erfolgt keine Vorhersage. |
| 6-180 Tage | 1/3 * Größe der Eingabedaten |
| 180-365 Tage | 60 Tage | 

### <a name="forecasting-data"></a>Prognosedaten
Jede Funktion analysiert tägliche Daten, um die zukünftige Nutzung zu prognostizieren. CPU, Netzwerk und sogar die Speicherauslastung können sich jedoch im Laufe des Tages ändern und dynamisch an die Arbeits Auslastungen auf dem Computer angepasst werden. Da die Nutzung im Laufe des Tages nicht konstant ist, ist es wichtig, die tägliche Nutzung in einem einzelnen Datenpunkt ordnungsgemäß darzustellen. In der folgenden Tabelle werden die spezifischen Datenpunkte und die Art der Datenverarbeitung ausführlich erläutert:


| Funktionsname | Datenquelle (n) | Filter Logik |
| --------------- | -------------- | ---------------- |
 Prognose des Volumen Verbrauchs          | Volumegröße                    | Maximale tägliche Nutzung              
 Prognose der Speichernutzung Gesamt   | Summe der Volumegrößen, Summe der Datenträger Größen              | Maximale tägliche Nutzung             
 Prognose der CPU-Kapazität                | % Processor Time  | Maximal 2 Stunden Durchschnitt pro Tag   
 Prognose zur Netzwerkkapazität         | Gesamtanzahl Bytes/Sek.         | Maximal 2 Stunden Durchschnitt pro Tag  

Wenn Sie die oben beschriebene Filter Logik auswerten, ist es wichtig zu beachten, dass jede Funktion Administratoren informieren möchte, wenn die zukünftige Verwendung die verfügbare Kapazität überschreitet – obwohl CPU-Zeitüberschreitung eine Auslastung von 100% erreicht hat, CPU-Auslastung möglicherweise nicht verursachte Leistungsminderung oder Ressourcenkonflikte. Bei CPU-und Netzwerkverbindungen sollte die hohe Nutzung statt der momentanen Spitzen unterstützt werden. Eine Durchschnitts Auslastung der CPU-und Netzwerk Auslastung im ganzen Tag würde jedoch wichtige Verwendungs Informationen verlieren, weil eine hohe CPU-Auslastung oder Netzwerk Auslastung eine erhebliche Auswirkung auf die Leistung Ihrer kritischen Workloads haben könnte. Der maximale Wert von 2 Stunden pro Tag vermeidet diese extreme und erzeugt nach wie vor sinnvolle Daten für jede zu analysierende Funktion.

Bei der Volume-und Gesamtspeicher Auslastung kann die Speicherauslastung jedoch die verfügbare Kapazität nicht überschreiten, auch wenn dies nicht der Fall ist, sodass die maximale tägliche Nutzung für diese Funktionen verwendet wird. 

### <a name="forecasting-statuses"></a>Vorhersage Status
Alle System Insights-Funktionen müssen einen Status ausgeben, der mit jeder Vorhersage verknüpft ist. Jede Standardfunktion verwendet die folgende Logik zum Definieren der einzelnen Vorhersage Status:
- **OK**: Die Vorhersage überschreitet die verfügbare Kapazität nicht.
- **Warnung**: Die Vorhersage überschreitet die verfügbare Kapazität in den nächsten 30 Tagen. 
- **Kritisch**: Die Vorhersage überschreitet die verfügbare Kapazität in den nächsten 7 Tagen. 
- **Fehler**: Unerwarteter Fehler bei der Funktion. 
- **Keine**: Es sind nicht genügend Daten vorhanden, um eine Vorhersage zu treffen. Dies kann auf fehlende Daten zurückzuführen sein oder daran, dass in jüngster Zeit keine Daten gemeldet wurden.

>[!NOTE]
>Wenn eine Funktions Vorhersage für mehrere Instanzen ist (z. b. mehrere Volumes oder Netzwerkadapter), gibt der Status den schwerwiegendsten Status für alle Instanzen an. Einzelne Statuswerte für jedes Volume oder jeden Netzwerkadapter werden im Windows Admin Center oder innerhalb der Daten angezeigt, die in der Ausgabe der einzelnen Funktionen enthalten sind. Anweisungen zum Analysieren der JSON-Ausgabe der Standardfunktionen finden Sie in [diesem Blog](https://aka.ms/systeminsights-mitigationscripts). 


## <a name="see-also"></a>Siehe auch
Weitere Informationen zu System Insights finden Sie in den folgenden Ressourcen:

- [Übersicht über System Einblicke](overview.md)
- [Verwalten von Funktionen](managing-capabilities.md)
- [Hinzufügen und Entwickeln von Funktionen](adding-and-developing-capabilities.md)
- [FAQ zu System Insights](faq.md)
