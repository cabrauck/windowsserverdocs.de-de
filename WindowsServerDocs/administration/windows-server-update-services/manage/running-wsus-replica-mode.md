---
title: Ausführen des WSUS-Replikatmodus
description: 'Thema zu Windows Server Update Service (WSUS): Konfigurieren des Replikat Modus '
ms.prod: windows-server
ms.reviewer: na
ms.suite: na
ms.technology: manage-wsus
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: d218cd6b-3b6b-4429-913b-31d412ce3356
author: coreyp-at-msft
ms.author: coreyp
manager: dongill
ms.date: 10/16/2017
ms.openlocfilehash: 5323210962298ff3f2d0b159cba7726adfbb89d1
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71361622"
---
# <a name="running-wsus-replica-mode"></a>Ausführen des WSUS-Replikatmodus

>Gilt für: Windows Server (halbjährlicher Kanal), Windows Server 2016, Windows Server 2012 R2, Windows Server 2012

Ein WSUS-Server im Replikat Modus erbt die Update Genehmigungen und Computer Gruppen, die auf einem Verwaltungs Server erstellt wurden. In einem Szenario, in dem der Replikat Modus verwendet wird, verfügen Sie in der Regel über einen einzelnen Verwaltungs Server, und ein oder mehrere untergeordnete WSUS-Replikat Server werden in der gesamten Organisation basierend auf der Standort-oder Organisations Sie genehmigen Updates und erstellen Computer Gruppen auf dem Verwaltungs Server, auf dem die Replikat Modus-Server dann gespiegelt werden. Server im Replikat Modus können nur während der WSUS-Installation eingerichtet werden. Wenn Sie dieses Szenario implementiert haben, ist es wahrscheinlich, dass es in Ihrer Organisation wichtig ist, dass Update Genehmigungen und Computer Gruppen zentral verwaltet werden.

Wenn Ihr WSUS-Server im Replikat Modus ausgeführt wird, können Sie nur eingeschränkte Verwaltungsfunktionen auf dem Server ausführen, die hauptsächlich aus folgenden Elementen bestehen:

-   Hinzufügen und Entfernen von Computern zu Computer Gruppen. Die Mitgliedschaft in der Computergruppe wird nicht an Replikat Server verteilt, sondern nur Computer Gruppen selbst. Auf einem Replikat Modus-Server erben Sie daher die Computer Gruppen, die Sie auf dem-Verwaltungs Server erstellt haben. Die Computer Gruppen sind jedoch leer. Anschließend müssen Sie die Client Computer, die eine Verbindung mit dem Replikat Server herstellen, den Computer Gruppen zuweisen.

-   Festlegen eines Synchronisierungszeitplans

-   Angeben von Proxy/Server-Einstellungen

-   Angeben der Update Quelle. Dabei kann es sich um einen anderen Server als den Verwaltungs Server handeln.

-   Aufrufen verfügbarer Updates

-   Überwachen der Update-, Synchronisierungs-, Computer Status-und WSUS-Einstellungen auf dem Server

-   Ausführen aller standardmäßigen WSUS-Berichte auf Replikat Modus-Servern



