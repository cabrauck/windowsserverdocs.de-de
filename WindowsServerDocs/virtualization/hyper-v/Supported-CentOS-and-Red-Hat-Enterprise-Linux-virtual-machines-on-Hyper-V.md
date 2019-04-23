---
title: Unterstützt von CentOS und Red Hat Enterprise Linux-VMs auf Hyper-V
description: Listet die Versionen von Linux Integration services für unterstützte CentOS und Red Hat Enterprise, Verteilungen
ms.prod: windows-server-threshold
ms.service: na
ms.technology: compute-hyper-v
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4bf8783d-dee5-4b3e-8cce-2b11b117c189
author: danihalfin
ms.author: daniha
ms.date: 12/20/2017
ms.openlocfilehash: 6bf15e5bfff4b875c4debd3c682bbdccd81a7bb6
ms.sourcegitcommit: 0d0b32c8986ba7db9536e0b8648d4ddf9b03e452
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/17/2019
ms.locfileid: "59869431"
---
# <a name="supported-centos-and-red-hat-enterprise-linux-virtual-machines-on-hyper-v"></a>Unterstützt von CentOS und Red Hat Enterprise Linux-VMs auf Hyper-V

>Gilt für: Windows Server 2016 Hyper-V Server 2016, Windows Server 2012 R2, Hyper-V Server 2012 R2, Windows Server 2012 Hyper-V Server 2012, Windows Server 2008 R2, Windows 10, Windows 8.1, Windows 8, Windows 7.1, Windows 7

Die folgende Verteilung featurezuordnungen Geben Sie an die Funktionen, die in integrierten und herunterladbare Versionen von Linux-Integrationsdienste vorhanden sind. Nach den Tabellen werden die bekannten Probleme und problemumgehungen für die einzelnen Verteilungspunkte aufgeführt.

Die integrierten Red Hat Enterprise Linux Integration Services-Treiber für Hyper-V (verfügbar seit Red Hat Enterprise Linux 6.4) sind ausreichend für Red Hat Enterprise Linux-Gäste über die synthetischen Geräte für hohe Leistung auf Hyper-V-Hosts ausgeführt werden. Diese integrierten Treiber sind von Red Hat für diesen Zweck zertifiziert. Zertifizierte Konfigurationen können auf dieser Red Hat-Webseite angezeigt werden: [Red Hat und Zertifizierungskatalogs](https://access.redhat.com/ecosystem/search/#/ecosystem/Red%20Hat%20Enterprise%20Linux?sort=sortTitle%20asc&vendors=Microsoft&category=Server). Ist es nicht notwendig, herunterladen und Installieren von Linux Integration Services-Pakete aus dem Microsoft Download Center, und dies also möglicherweise beschränken Ihre Red Hat-Unterstützung in Red Hat-Knowledgebase-Artikel 1067 beschrieben: [Red Hat-Knowledgebase 1067](https://access.redhat.com/articles/1067).

Aufgrund potentieller Konflikte zwischen der integrierten LIS-Unterstützung und die herunterladbare LIS-Unterstützung bei der Aktualisierung des Kernels Deaktivieren von automatischen Updates, deinstallieren Sie die LIS herunterladbare Pakete, aktualisieren Sie den Kernel, Neustart, und installieren, die die neuesten LIS release, und ein Neustart erneut aus.

>[!NOTE]
>Offizielle Informationen zur Zertifizierung von Red Hat Enterprise Linux steht über den [Red Hat-Kundenportal](https://access.redhat.com/ecosystem/search/#/category/Server?sort=sortTitle%20asc&query=windows%20server&ecosystem=Red%20Hat%20Enterprise%20Linux).

In diesem Abschnitt:

* [RHEL/CentOS 7.x-Serie](Supported-CentOS-and-Red-Hat-Enterprise-Linux-virtual-machines-on-Hyper-V.md#BKMK_7x)

* [RHEL/CentOS 6.x-Serie](Supported-CentOS-and-Red-Hat-Enterprise-Linux-virtual-machines-on-Hyper-V.md#BKMK_6x)

* [RHEL/CentOS 5.x-Reihe](Supported-CentOS-and-Red-Hat-Enterprise-Linux-virtual-machines-on-Hyper-V.md#BKMK_5x)

* [Hinweise](Supported-CentOS-and-Red-Hat-Enterprise-Linux-virtual-machines-on-Hyper-V.md#BKMK_notes)

## <a name="table-legend"></a>Tabellenlegende

* **Integrierte** -LIS als Teil dieser Linux-Verteilung enthalten sind. Die Versionsnummern von Kernel-Modul für den integrierten LIS (siehe **Lsmod**, z. B.) unterscheiden sich die Versionsnummer für das von Microsoft bereitgestelltes LIS-Download-Paket. Ein Konflikt, nicht dass die integrierten LIS veraltet ist.

* &#10004;-Funktion

* (*leere*)-Funktion nicht verfügbar.

## <a name="BKMK_7x"></a>RHEL/CentOS 7.x-Serie

Diese Serie bietet nur 64-Bit-Kernel.

|**Funktion**|**Windows Server-version**|**7.5-7.6**|**7.3-7.4**|**7.0-7.2**|**7.5-7.6**|**7.4**|**7.3**|**7.2**|**7.1**|**7.0**|
|-|-|-|-|-|-|-|-|-|-|-|
|**Verfügbarkeit**||[LIS 4.2](https://www.microsoft.com/download/details.aspx?id=55106)|[LIS 4.2](https://www.microsoft.com/download/details.aspx?id=55106)|[LIS 4.2](https://www.microsoft.com/download/details.aspx?id=55106)|Erstellt|Erstellt|Erstellt|Erstellt|Erstellt|Erstellt||
|**[Core](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#BKMK_core)**|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Windows Server 2016 – genaue Uhrzeit|2019, 2016|&#10004;|&#10004;|||||||
|**[Netzwerkfunktionen](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#BKMK_Networking)**|||||||
|Großrahmen|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|VLAN-Kennzeichnung und trunking|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Livemigration|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Statische IP-Injection|2019, 2016, 2012 R2, 2012|&#10004;Hinweis 2|&#10004;Hinweis 2|&#10004;Hinweis 2|&#10004;Hinweis 2|&#10004;Hinweis 2|&#10004;Hinweis 2|&#10004;Hinweis 2|&#10004;Hinweis 2|&#10004;Hinweis 2|
|vRSS|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;||
|Segmentierung von TCP und Prüfsumme Abladungen|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;||
|SR-IOV|2019, 2016|&#10004;|&#10004;||&#10004;|&#10004;|&#10004;|||
|**[Speicher](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#BKMK_Storage)**||||
|VHDX resize|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Virtueller Fibre Channel|2019, 2016, 2012 R2|&#10004;Hinweis 3|&#10004;Hinweis 3|&#10004;Hinweis 3|&#10004;Hinweis 3|&#10004;Hinweis 3|&#10004;Hinweis 3|&#10004;Hinweis 3|&#10004;Hinweis 3|&#10004;Hinweis 3|
|VM-Sicherung|2019, 2016, 2012 R2|&#10004;Hinweis 5|&#10004;Hinweis 5|&#10004;Hinweis 5|&#10004;Beachten Sie 4,5|&#10004;Hinweis 4, 5|&#10004;Hinweis 4, 5|&#10004;Hinweis 4, 5|&#10004;Hinweis 4, 5|&#10004;Hinweis 4, 5|
|TRIM-Unterstützung|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|||
|SCSI WWN|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|||||
|**[Arbeitsspeicher](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#BKMK_Memory)**||||
|Kernel-Unterstützung für PAE|2019, 2016, 2012 R2, 2012, 2008 R2|Nicht zutreffend|Nicht zutreffend|Nicht zutreffend|Nicht zutreffend|Nicht zutreffend|Nicht zutreffend|Nicht zutreffend|Nicht zutreffend|Nicht zutreffend|
|Konfiguration der MMIO-Lücke|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Dynamischer Arbeitsspeicher - Hot-Add-|2019, 2016, 2012 R2, 2012|&#10004;Beachten Sie, 8, 9, 10|&#10004;Beachten Sie, 8, 9, 10|&#10004;Beachten Sie, 8, 9, 10|&#10004;Hinweis 9, 10|&#10004;Hinweis 9, 10|&#10004;Hinweis 9, 10|&#10004;Hinweis 9, 10|&#10004;Hinweis 9, 10|&#10004;Beachten Sie, 8, 9, 10|
|Dynamische Speichererweiterungsfunktion-|2019, 2016, 2012 R2, 2012|&#10004;Beachten Sie, 8, 9, 10|&#10004;Beachten Sie, 8, 9, 10|&#10004;Beachten Sie, 8, 9, 10|&#10004;Hinweis 9, 10|&#10004;Hinweis 9, 10|&#10004;Hinweis 9, 10|&#10004;Hinweis 9, 10|&#10004;Hinweis 9, 10|&#10004;Beachten Sie, 8, 9, 10|
|Laufzeitspeichers|2019, 2016|&#10004;|&#10004;|&#10004;|||||||
|**[Video](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#BKMK_Video)**||||
|Hyper-V-spezifischer Videogerät|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|**[Sonstige](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#BKMK_Misc)**||||
|Schlüssel-Wert-Paar|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Nicht maskierbarer Interrupt|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Kopieren von Dateien vom Host zum Gast|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;||
|Lsvmbus-Befehl|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|||||||
|Hyper-V-Sockets|2019, 2016|&#10004;|&#10004;|&#10004;|||||||
|PCI-Pass-Through-/ DDA|2019, 2016|&#10004;|&#10004;||&#10004;|&#10004;|&#10004;||||
|**[Virtuelle Computer der Generation 2](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#BKMK_gen2)**|||||
|Mit UEFI Boot|2019, 2016, 2012 R2|&#10004;Beachten Sie 14|&#10004;Beachten Sie 14|&#10004;Beachten Sie 14|&#10004;Beachten Sie 14|&#10004;Beachten Sie 14|&#10004;Beachten Sie 14|&#10004;Beachten Sie 14|&#10004;Beachten Sie 14|&#10004;Beachten Sie 14|
|Sicherer Start|2019, 2016|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|

## <a name="BKMK_6x"></a>RHEL/CentOS 6.x-Serie

Der 32-Bit-Kernel für diese Reihe wird PAE aktiviert. Es gibt keine integrierte Unterstützung von LIS für RHEL/CentOS 6.0 – 6.3.

|**Funktion**|**Windows Server-version**|**6.4-6.10**|**6.0-6.3**|**6.10, 6.9, 6.8**|**6.6, 6.7**|**6.5**|**6.4**|
|-|-|-|-|-|-|-|-|
|**Verfügbarkeit**||[LIS 4.2](https://www.microsoft.com/download/details.aspx?id=55106)|[LIS 4.2](https://www.microsoft.com/download/details.aspx?id=55106)|Erstellt|Erstellt|Erstellt|Erstellt|
|**[Core](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#BKMK_core)**|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Windows Server 2016 – genaue Uhrzeit|2019, 2016||||||
|**[Netzwerkfunktionen](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#BKMK_Networking)**|
|Großrahmen|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|VLAN-Kennzeichnung und trunking|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;Hinweis 1|&#10004;Hinweis 1|&#10004;Hinweis 1|&#10004;Hinweis 1|&#10004;Hinweis 1|&#10004;Hinweis 1|
|Livemigration|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Statische IP-Injection|2019, 2016, 2012 R2, 2012|&#10004;Hinweis 2|&#10004;Hinweis 2|&#10004;Hinweis 2|&#10004;Hinweis 2|&#10004;Hinweis 2|&#10004;Hinweis 2|
|vRSS|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|||
|Segmentierung von TCP und Prüfsumme Abladungen|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|||
|SR-IOV|2019, 2016|||||||
|**[Speicher](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#BKMK_Storage)**|
|VHDX resize|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;||
|Virtueller Fibre Channel|2019, 2016, 2012 R2|&#10004;Hinweis 3|&#10004;Hinweis 3|&#10004;Hinweis 3|&#10004;Hinweis 3|&#10004;Hinweis 3||
|VM-Sicherung|2019, 2016, 2012 R2|&#10004;Hinweis 5|&#10004;Hinweis 5|&#10004;Hinweis 4, 5|&#10004;Hinweis 4, 5|&#10004;Beachten Sie, 4, 5, 6|&#10004;Beachten Sie, 4, 5, 6|
|TRIM-Unterstützung|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;||||
|SCSI WWN|2019, 2016, 2012 R2|&#10004;|&#10004;|||||
|**[Arbeitsspeicher](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#BKMK_Memory)**|
|Kernel-Unterstützung für PAE|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Konfiguration der MMIO-Lücke|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Dynamischer Arbeitsspeicher - Hot-Add-|2019, 2016, 2012 R2, 2012|&#10004;Beachten Sie, 7, 9, 10|&#10004;Beachten Sie, 7, 9, 10|&#10004;Beachten Sie, 7, 9, 10|&#10004;Beachten Sie, 7, 8, 9, 10|&#10004;Beachten Sie, 7, 8, 9, 10||
|Dynamische Speichererweiterungsfunktion-|2019, 2016, 2012 R2, 2012|&#10004;Beachten Sie, 7, 9, 10|&#10004;Beachten Sie, 7, 9, 10|&#10004;Beachten Sie, 7, 9, 10|&#10004;Beachten Sie, 7, 9, 10|&#10004;Beachten Sie, 7, 9, 10|&#10004;Beachten Sie, 7, 9, 10, 11|
|Laufzeitspeichers|2019, 2016|||||||
|**[Video](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#BKMK_Video)**|
|Hyper-V-spezifischer Videogerät|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;||
|**[Sonstige](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#BKMK_Misc)**|
|Schlüssel-Wert-Paar|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;Hinweis 12|&#10004;Hinweis 12|&#10004;Hinweis 12, 13|&#10004;Hinweis 12, 13|
|Nicht maskierbarer Interrupt|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|&#10004;|
|Kopieren von Dateien vom Host zum Gast|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|&#10004;|||
|Lsvmbus-Befehl|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;||||||
|Hyper-V-Sockets|2019, 2016|&#10004;|&#10004;|||||
|PCI-Pass-Through-/ DDA|2019, 2016|||||||
|**[Virtuelle Computer der Generation 2](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#BKMK_gen2)**|
|Mit UEFI Boot|2012 R2|||||||
||2019, 2016|&#10004;Beachten Sie 14|&#10004;Beachten Sie 14|&#10004;Beachten Sie 14||||
|Sicherer Start|2019, 2016||||||

## <a name="BKMK_5x"></a>RHEL/CentOS 5.x-Reihe

Diese Serie bietet es sich um eine unterstützte 32-Bit-PAE-Kernelversion, die für Sie verfügbar. Es gibt keine integrierte Unterstützung von LIS für RHEL/CentOS vor 5.9.

|**Funktion**|**Windows Server-version**|5.2 -5.11|**5.2-5.11**|**5.9 - 5.11**|
|-|-|-|-|-|
|**Verfügbarkeit**||[LIS 4.2](https://www.microsoft.com/download/details.aspx?id=55106)|[LIS 4.1](https://www.microsoft.com/download/details.aspx?id=51612)|Erstellt|
|**[Core](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#BKMK_core)**|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|
|Windows Server 2016 – genaue Uhrzeit|2019, 2016||||
|**[Netzwerkfunktionen](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#BKMK_Networking)**|
|Großrahmen|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|
|VLAN-Kennzeichnung und trunking|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;Hinweis 1|&#10004;Hinweis 1|&#10004;Hinweis 1|
|Livemigration|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|
|Statische IP-Injection|2019, 2016, 2012 R2, 2012|&#10004;Hinweis 2|&#10004;Hinweis 2|&#10004;Hinweis 2|
|vRSS|2019, 2016, 2012 R2||||
|Segmentierung von TCP und Prüfsumme Abladungen|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;||
|SR-IOV|2019, 2016||||||
|**[Speicher](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#BKMK_Storage)**|
|VHDX resize|2019, 2016, 2012 R2|&#10004;|&#10004;||
|Virtueller Fibre Channel|2019, 2016, 2012 R2|&#10004;Hinweis 3|&#10004;Hinweis 3||
|VM-Sicherung|2019, 2016, 2012 R2|&#10004;Hinweis 5, 15|&#10004;Hinweis 5|&#10004;Beachten Sie, 4, 5, 6|
|TRIM-Unterstützung|2019, 2016, 2012 R2||||
|SCSI WWN|2019, 2016, 2012 R2||||
|**[Arbeitsspeicher](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#BKMK_Memory)**|
|Kernel-Unterstützung für PAE|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;|&#10004;|
|Konfiguration der MMIO-Lücke|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|
|Dynamischer Arbeitsspeicher - Hot-Add-|2019, 2016, 2012 R2, 2012||||
|Dynamische Speichererweiterungsfunktion-|2019, 2016, 2012 R2, 2012|&#10004;Beachten Sie, 7, 9, 10, 11|&#10004;Beachten Sie, 7, 9, 10, 11||
|Laufzeitspeichers|2019, 2016||||
|**[Video](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#BKMK_Video)**|
|Hyper-V-spezifischer Videogerät|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;||
|**[Sonstige](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#BKMK_Misc)**|
|Schlüssel-Wert-Paar|2019, 2016, 2012 R2, 2012, 2008 R2|&#10004;|&#10004;||
|Nicht maskierbarer Interrupt|2019, 2016, 2012 R2|&#10004;|&#10004;|&#10004;|
|Kopieren von Dateien vom Host zum Gast|2019, 2016, 2012 R2|&#10004;|&#10004;||
|Lsvmbus-Befehl|2019, 2016, 2012 R2, 2012, 2008 R2||||
|Hyper-V-Sockets|2019, 2016||||
|PCI-Pass-Through-/ DDA|2019, 2016||||||
|**[Virtuelle Computer der Generation 2](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md#BKMK_gen2)**|
|Mit UEFI Boot|2019, 2016, 2012 R2||||
|Sicherer Start|2019, 2016||||

## <a name="BKMK_notes"></a>Anmerkungen zu dieser Version

1. Für diese RHEL/CentOS-Version, VLAN-Tags funktioniert, VLAN Trunking jedoch nicht.

2. Statische IP-Injection funktioniert möglicherweise nicht, wenn Netzwerk-Manager für einen bestimmten synthetische Netzwerkadapter auf dem virtuellen Computer konfiguriert wurde. Für statische IP-Adresse reibungslos funktioniert Injection stellen Sie sicher, dass entweder den Netzwerk-Manager entweder vollständig ausgeschaltet ist oder für einen bestimmten Netzwerkadapter durch seine Ifcfg-EthX-Datei deaktiviert wurde.

3. Unter Windows Server 2012 R2 bei der Verwendung von virtuellen Fibre Channel-Geräten sicher, dass die logische Gerätenummer (LUN 0)-0 aufgefüllt wurde. Virtuelle Linux-Computer sind möglicherweise nicht Fibre Channel-Geräten nativ bereitstellen können, wenn die LUN 0 nicht aufgefüllt wurde.

4. Für integrierte LIS muss das Paket "Hyper-v-Daemons" für diese Funktion installiert sein.

5. Wenn offene Dateihandles vorhanden, während eines Sicherungsvorgangs für die Livemigration einer virtuellen Maschine aus, und klicken Sie dann in einigen Fällen Ecke sind, möglicherweise die gesicherten virtuellen Festplatten auf eine Datei System konsistenzprüfung (Fsck) bei der Wiederherstellung werden. Live Sicherungsvorgänge können im Hintergrund fehl, wenn es sich bei dem virtuellen Computer eine angefügte iSCSI-Gerät oder direkt angeschlossenen Speicher (auch bekannt als Pass-Through-Datenträger) ist.

6. Während der Download des Linux-Integrationsdienste bevorzugt wird, live-Unterstützung von Sicherungen für RHEL/CentOS 5.9 - 5.11/6.4/6.5 steht auch über [Hyper-V-Sicherung Essentials für Linux](https://github.com/LIS/backupessentials/tree/1.0).

7. Unterstützung für dynamischen Speicher ist nur verfügbar, auf 64-Bit-Computern.

8. Hot-Add-Unterstützung ist in dieser Verteilung standardmäßig nicht aktiviert. Auf der Ebene "heiß"-Add-Unterstützung aktivieren, Sie eine Regel Udev unter /etc/udev/rules.d/ wie folgt hinzufügen müssen:

   1. Erstellen Sie eine Datei **/etc/udev/rules.d/100-balloon.rules**. Sie können einen beliebigen anderen gewünschten Namen für die Datei verwenden.

   2. Fügen Sie in der Datei den folgenden Inhalt hinzu: `SUBSYSTEM=="memory", ACTION=="add", ATTR{state}="online"`

   3. Starten Sie das System zum Aktivieren der Unterstützung: Hinzufügen von "heiß".

   Während der Linux Integration Services-Download für die Installation mit dieser Regel erstellt wird, wird die Regel auch entfernt, wenn LIS deinstalliert wird, damit die Regel erneut erstellt werden muss, wenn dynamischer Arbeitsspeicher nach der Deinstallation erforderlich ist.

9. Dynamic Memory-Vorgängen können fehlschlagen, wenn das Gastbetriebssystem für den Arbeitsspeicher zu niedrig ausgeführt wird. Es folgen einige bewährten Methoden:

   * Arbeitsspeicher beim Start und der minimale Arbeitsspeicher sollte gleich oder größer als die Größe des Arbeitsspeichers, die von der Verteilung Anbieter empfohlen wird.

   * Anwendungen, die in der Regel den gesamten verfügbaren Arbeitsspeicher auf einem System zu nutzen sind mit der Nutzung von bis zu 80 Prozent des verfügbaren Arbeitsspeichers beschränkt.

10. Wenn Sie dynamischen Arbeitsspeicher auf einem Windows Server 2016 oder Windows Server 2012 R2-Betriebssystem verwenden, geben Sie **startspeicher**, **mindestens Erforderlicher Arbeitsspeicher**, und **Maximaler Serverarbeitsspeicher** die Parameter in Vielfachen von 128 MB (Megabyte). Geschieht dies nicht zu um hot-add-Fehlern führen kann, und Arbeitsspeicher, erhöhen Sie in einem Gastbetriebssystem möglicherweise nicht angezeigt.

11. Bestimmte Verteilungen, einschließlich der Verwendung von LIS 4.0 und 4.1, Erweiterung unterstützen nur und bieten keine Unterstützung: Hinzufügen von "heiß". In diesem Fall kann das Feature für dynamischen Arbeitsspeicher verwendet werden, durch den Start-Arbeitsspeicher-Parameter auf ein Wert, der gleich dem Maximum-Arbeitsspeicher-Parameter festlegen. Dies führt alle erforderlichen Speicher wird von "heiß" hinzugefügt, mit dem virtuellen Computer bei Neustarts und dann später je nach den Arbeitsspeicherbedarf des Hosts, Hyper-V kann frei zuordnen oder Arbeitsspeicher vom Gast mithilfe der Erweiterung. Konfigurieren Sie **Startspeicher** und **mindestens Erforderlicher Arbeitsspeicher** mindestens mit den empfohlenen Wert für die Verteilung.

12. Um Schlüssel/Wert-Paar (KVP)-Infrastruktur zu aktivieren, installieren Sie das Rpm-Paket Hypervkvpd oder Hyper-v-Daemons aus Ihrem RHEL ISO. Alternativ kann das Paket direkt aus dem RHEL-Repositorys installiert werden.

13. Die Schlüssel/Wert-Paar (KVP)-Infrastruktur möglicherweise ohne eine Linux-Software-Aktualisierung nicht ordnungsgemäß. Wenden Sie sich an Ihren Händler, um das Softwareupdate zu erhalten, falls Sie Probleme mit diesem Feature finden Sie unter.

14. Unter Windows Server 2012 R2 Generation 2 standardmäßig aktiviertem sicheren Start über virtuelle Computer verfügen, und einige virtuelle Linux-Computer wird nicht gestartet werden, es sei denn, die Option für den sicheren Start deaktiviert ist. Sie können den sicheren Start im Deaktivieren der **Firmware** Abschnitt der Einstellungen für den virtuellen Computer in **Hyper-V-Manager** oder Sie können mithilfe von Powershell deaktivieren:

   ```Powershell
   Set-VMFirmware -VMName "VMname" -EnableSecureBoot Off

   ```

   Der Linux-Integrationsdienste Download kann auf vorhandenen VMs der 2. Generation angewendet werden, aber Generation 2-Funktion ist nicht übermitteln.

15. In Red Hat Enterprise Linux oder CentOS 5.2 sind 5.3 und 5.4 die Dateisystem fixieren Funktionen nicht verfügbar ist, damit Live-VM-Sicherung auch nicht verfügbar ist.

Siehe auch

* [Set-VMFirmware](https://technet.microsoft.com/library/dn464287.aspx)

* [Virtuelle Debian-Computer unterstützt auf Hyper-V](Supported-Debian-virtual-machines-on-Hyper-V.md)

* [Unterstützte Oracle Linux-VMs auf Hyper-V](Supported-Oracle-Linux-virtual-machines-on-Hyper-V.md)

* [Unterstützte SUSE-Computer auf Hyper-V](Supported-SUSE-virtual-machines-on-Hyper-V.md)

* [Unterstützte Ubuntu-VMs auf Hyper-V](Supported-Ubuntu-virtual-machines-on-Hyper-V.md)

* [Unterstützte FreeBSD-Maschinen in Hyper-V](Supported-FreeBSD-virtual-machines-on-Hyper-V.md)

* [Eine Beschreibung für Linux und FreeBSD-VMs auf Hyper-V-Funktion](Feature-Descriptions-for-Linux-and-FreeBSD-virtual-machines-on-Hyper-V.md)

* [Bewährte Methoden für die Ausführung von Linux in Hyper-V](Best-Practices-for-running-Linux-on-Hyper-V.md)

* [Red Hat-Hardware-Zertifizierung](https://hardware.redhat.com/&quicksearch=Microsoft)