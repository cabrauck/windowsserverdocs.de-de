---
title: Installieren von Active Directory Domain Services auf einem virtuellen Azure-Computer
description: Erstellen einer neuen Active Directory-Gesamtstruktur auf einem virtuellen Computer (VM) auf einem virtuellen Azure-Computer
author: MicrosoftGuyJFlo
ms.author: joflore
manager: mtillman
ms.date: 04/11/2019
ms.technology: identity-adds
ms.topic: article
ms.prod: windows-server
ms.openlocfilehash: e0a10e27e044fd1df7cbdb943964440983ce494c
ms.sourcegitcommit: 6aff3d88ff22ea141a6ea6572a5ad8dd6321f199
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/27/2019
ms.locfileid: "71390649"
---
# <a name="install-a-new-active-directory-forest-using-azure-cli"></a>Installieren Sie eine neue Active Directory Gesamtstruktur mit Azure CLI

AD DS können auf einem virtuellen Azure-Computer (VM) auf die gleiche Weise wie in vielen lokalen Instanzen ausgeführt werden. Dieser Artikel führt Sie durch die Bereitstellung einer neuen AD DS Gesamtstruktur auf zwei neuen Domänen Controllern in einer Azure-Verfügbarkeits Gruppe mithilfe der Azure-Portal und Azure CLI. Viele Kunden finden diese Anleitung hilfreich, wenn Sie ein Lab erstellen oder die Bereitstellung von Domänen Controllern in Azure vorbereiten.

## <a name="components"></a>Komponenten

* Eine Ressourcengruppe, in der alles abgelegt werden soll.
* Eine [Azure-Virtual Network](https://docs.microsoft.com/azure/virtual-network/virtual-networks-overview.md), ein Subnetz, eine Netzwerk Sicherheitsgruppe und eine Regel zum Zulassen von RDP-Zugriff auf virtuelle Computer.
* Eine [Verfügbarkeits Gruppe](https://docs.microsoft.com/azure/virtual-machines/windows/regions-and-availability#availability-sets) für virtuelle Azure-Computer, in der zwei Active Directory Domain Services (AD DS)-Domänen Controller abgelegt werden.
* Zwei virtuelle Azure-Computer zum Ausführen von AD DS und DNS.

### <a name="items-that-are-not-covered"></a>Nicht abgedeckte Elemente

* [Erstellen einer Site-to-Site-VPN-Verbindung](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) von einem lokalen Standort
* [Sichern von Netzwerk Datenverkehr in Azure](https://docs.microsoft.com/azure/security/azure-security-network-security-best-practices.md)
* [Entwerfen der Standort Topologie](https://docs.microsoft.com/windows-server/identity/ad-ds/plan/designing-the-site-topology)
* [Planen der Platzierung von Betriebs Master Rollen](https://docs.microsoft.com/windows-server/identity/ad-ds/plan/planning-operations-master-role-placement)
* [Bereitstellen von Azure AD Connect zum Synchronisieren von Identitäten mit Azure AD](https://docs.microsoft.com/azure/active-directory/hybrid/how-to-connect-install-express)

## <a name="build-the-test-environment"></a>Erstellen der Testumgebung

Wir verwenden die [Azure-Portal](https://portal.azure.com) und [Azure CLI](https://docs.microsoft.com/cli/azure/overview?view=azure-cli-latest) zum Erstellen der Umgebung.

Der Azure CLI wird zum Erstellen und Verwalten von Azure-Ressourcen über die Befehlszeile oder in Skripts verwendet. In diesem Tutorial wird die Verwendung des Azure CLI zum Bereitstellen virtueller Maschinen mit Windows Server 2019 ausführlich erläutert. Nach Abschluss der Bereitstellung stellen wir eine Verbindung mit den Servern her und installieren AD DS.

Wenn Sie über kein Azure-Abonnement verfügen, können Sie [ein kostenloses Konto erstellen](https://azure.microsoft.com/free) , bevor Sie beginnen.

### <a name="using-azure-cli"></a>Verwenden von Azure CLI

Das folgende Skript automatisiert den Prozess der Erstellung von zwei virtuellen Windows Server 2019-Computern, um Domänen Controller für eine neue Active Directory Gesamtstruktur in Azure zu erstellen. Ein Administrator kann die unten aufgeführten Variablen entsprechend Ihren Anforderungen ändern und als einen Vorgang vervollständigen. Das Skript erstellt die erforderliche Ressourcengruppe, die Netzwerk Sicherheitsgruppe mit einer Datenverkehrs Regel für Remotedesktop, das virtuelle Netzwerk und das Subnetz und die Verfügbarkeits Gruppe. Die virtuellen Computer werden jeweils mit einem Datenträger mit 20 GB erstellt, wobei das Caching für die Installation AD DS deaktiviert ist.

Das folgende Skript kann direkt vom Azure-Portal ausgeführt werden. Wenn Sie die CLI lokal installieren und verwenden möchten, müssen Sie für diesen Schnellstart die Azure CLI Version 2.0.4 oder höher ausführen. Führen `az --version` Sie aus, um die Version zu finden. Wenn Sie installieren oder aktualisieren müssen, finden Sie weitere Informationen unter [install Azure CLI 2,0](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest).

| Variablenname | Zweck |
| :---: | :--- |
| adminUsername | Der Benutzername, der auf den einzelnen virtuellen Computern als lokaler Administrator konfiguriert werden soll. |
| AdminPassword | Klar Text Kennwort, das auf jedem virtuellen Computer als lokales Administrator Kennwort konfiguriert werden soll. |
| resourceGroupName | Der Name, der für die Ressourcengruppe verwendet werden soll. Es sollte kein vorhandener Name dupliziert werden. |
| Speicherort | Der Name des Azure-Standorts, den Sie bereitstellen möchten. Listet die unterstützten Regionen für das aktuelle Abonnement mithilfe von "`az account list-locations`" auf. |
| VNetName | Der Name zum Zuweisen des virtuellen Azure-Netzwerks sollte keinen vorhandenen Namen duplizieren. |
| Vnetaddress | Der für Azure-Netzwerke zu verwendende IP-Bereich. Ein vorhandener Bereich darf nicht dupliziert werden. |
| SubnetName | Name, der dem IP-Subnetz zugewiesen werden soll. Es sollte kein vorhandener Name dupliziert werden. |
| Subnetaddress | Subnetzadresse für die Domänen Controller. Sollte ein Subnetz innerhalb des vnets sein. |
| AvailabilitySet | Name der Verfügbarkeits Gruppe, der die virtuellen Domänen Controller-VMS beitreten werden. |
| VMSize | Standard Größe von virtuellen Azure-Computern, die am Speicherort für die Bereitstellung |
| Datadisksize | Größe (in GB) für den Datenträger, auf dem AD DS installiert wird. |
| Domaincontroller1 | Name des ersten Domänen Controllers. |
| DC1IP | IP-Adresse für den ersten Domänen Controller. |
| DomainController2 | Name des zweiten Domänen Controllers. |
| DC2IP | IP-Adresse für den zweiten Domänen Controller. |

```azurecli
#Update based on your organizational requirements
Location=westus2
ResourceGroupName=ADonAzureVMs
NetworkSecurityGroup=NSG-DomainControllers
VNetName=VNet-AzureVMsWestUS2
VNetAddress=10.10.0.0/16
SubnetName=Subnet-AzureDCsWestUS2
SubnetAddress=10.10.10.0/24
AvailabilitySet=DomainControllers
VMSize=Standard_DS1_v2
DataDiskSize=20
AdminUsername=azureuser
AdminPassword=ChangeMe123456
DomainController1=AZDC01
DC1IP=10.10.10.11
DomainController2=AZDC02
DC2IP=10.10.10.12

# Create a resource group.
az group create --name $ResourceGroupName \
                --location $Location

# Create a network security group
az network nsg create --name $NetworkSecurityGroup \
                      --resource-group $ResourceGroupName \
                      --location $Location

# Create a network security group rule for port 3389.
az network nsg rule create --name PermitRDP \
                           --nsg-name $NetworkSecurityGroup \
                           --priority 1000 \
                           --resource-group $ResourceGroupName \
                           --access Allow \
                           --source-address-prefixes "*" \
                           --source-port-ranges "*" \
                           --direction Inbound \
                           --destination-port-ranges 3389

# Create a virtual network.
az network vnet create --name $VNetName \
                       --resource-group $ResourceGroupName \
                       --address-prefixes $VNetAddress \
                       --location $Location \

# Create a subnet
az network vnet subnet create --address-prefix $SubnetAddress \
                              --name $SubnetName \
                              --resource-group $ResourceGroupName \
                              --vnet-name $VNetName \
                              --network-security-group $NetworkSecurityGroup

# Create an availability set.
az vm availability-set create --name $AvailabilitySet \
                              --resource-group $ResourceGroupName \
                              --location $Location

# Create two virtual machines.
az vm create \
    --resource-group $ResourceGroupName \
    --availability-set $AvailabilitySet \
    --name $DomainController1 \
    --size $VMSize \
    --image Win2019Datacenter \
    --admin-username $AdminUsername \
    --admin-password $AdminPassword \
    --data-disk-sizes-gb $DataDiskSize \
    --data-disk-caching None \
    --nsg $NetworkSecurityGroup \
    --private-ip-address $DC1IP \
    --no-wait

az vm create \
    --resource-group $ResourceGroupName \
    --availability-set $AvailabilitySet \
    --name $DomainController2 \
    --size $VMSize \
    --image Win2019Datacenter \
    --admin-username $AdminUsername \
    --admin-password $AdminPassword \
    --data-disk-sizes-gb $DataDiskSize \
    --data-disk-caching None \
    --nsg $NetworkSecurityGroup \
    --private-ip-address $DC2IP

```

## <a name="dns-and-active-directory"></a>DNS und Active Directory

Wenn die als Teil dieses Prozesses erstellten virtuellen Azure-Computer eine Erweiterung einer vorhandenen lokalen Active Directory-Infrastruktur sind, müssen die DNS-Einstellungen im virtuellen Netzwerk so geändert werden, dass Ihre lokalen DNS-Server vor der Bereitstellung eingeschlossen werden. Dieser Schritt ist wichtig, damit die neu erstellten Domänen Controller in Azure lokale Ressourcen auflösen und die Replikation zulassen können. Weitere Informationen zu DNS, Azure und zum Konfigurieren von Einstellungen finden Sie im Abschnitt [Namensauflösung, der ihren eigenen DNS-Server verwendet](https://docs.microsoft.com/azure/virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances#name-resolution-that-uses-your-own-dns-server).

Nachdem Sie die neuen Domänen Controller in Azure herauf gestuft haben, müssen Sie auf den primären und sekundären DNS-Server für das virtuelle Netzwerk festgelegt werden, und alle lokalen DNS-Server werden in den tertiären und überschreiten herabgestuft. Weitere Informationen zum Ändern von DNS-Servern finden Sie im Artikel [erstellen, ändern oder Löschen eines virtuellen Netzwerks](https://docs.microsoft.com/azure/virtual-network/manage-virtual-network#change-dns-servers).

Informationen zum Erweitern eines lokalen Netzwerks auf Azure finden Sie im Artikel [creating a Site-to-Site VPN Connection @ no__t-1.

## <a name="configure-the-vms-and-install-active-directory-domain-services"></a>Konfigurieren Sie die VMs, und installieren Sie Active Directory Domain Services

Nachdem das Skript abgeschlossen ist, navigieren Sie zum [Azure-Portal](https://portal.azure.com)und dann zu **virtuelle**Computer.

### <a name="configure-the-first-domain-controller"></a>Konfigurieren des ersten Domänen Controllers

Stellen Sie eine Verbindung mit AZDC01 her, indem Sie die im Skript angegebenen Anmelde Informationen verwenden.

* Initialisieren und formatieren Sie den Datenträger als F:
   * Öffnen Sie das Startmenü, und navigieren Sie zu **Computer Verwaltung** .
   * Navigieren Sie zu **Speicher** >  Datenträger**Verwaltung** .
   * Initialisieren des Datenträgers als MBR
   * Erstellen eines neuen einfachen Volumes und Zuweisen des Laufwerk Buchstabens F: Sie können eine Volumebezeichnung angeben, wenn Sie möchten.
* Installieren von Active Directory Domain Services mithilfe Server-Manager
* Herauf Stufen des Domänen Controllers als erster in einer neuen Gesamtstruktur
   * Belassen Sie auf der Seite "Domänen Controller Optionen" die Option Domain Name System (DNS)-Server und globalen Katalog (GC).
   * Angeben eines Kennworts für den Verzeichnisdienst-Wiederherstellungs Modus basierend auf den Anforderungen Ihrer Organisation
   * Ändern Sie die Pfade von C: auf das Laufwerk F:, das Sie erstellt haben, wenn Sie zur Eingabe Ihres Orts aufgefordert werden.
   * Überprüfen Sie die im Assistenten getroffenen Auswahl, und wählen Sie **weiter** aus.

> [!NOTE]
> Durch die Überprüfung der erforderlichen Komponenten wird gewarnt, dass dem physischen Netzwerkadapter keine statischen IP-Adressen zugewiesen sind. Diese können Sie problemlos ignorieren, da statische IPS im virtuellen Azure-Netzwerk zugewiesen werden.

* Wählen Sie **Installieren**

Nachdem der Assistent den Installationsvorgang abgeschlossen hat, wird der virtuelle Computer neu gestartet.

Wenn der virtuelle Computer neu gestartet wird, melden Sie sich mit den verwendeten Anmelde Informationen wieder an, aber dieses Mal als Mitglied der Domäne, die Sie erstellt haben.

   > [!NOTE]
   > Der erste Anmeldevorgang nach der herauf Stufung zu einem Domänen Controller dauert möglicherweise länger als normal und ist in Ordnung. Holen Sie sich einen Tasse Tee, Kaffee, Wasser oder andere Getränke Ihrer Wahl.

Da [virtuelle Azure-Netzwerke IPv6 nicht unterstützen, sollten](https://docs.microsoft.com/azure/virtual-network/virtual-networks-faq#do-vnets-support-ipv6) Sie Ihre VMS so einrichten, dass Sie IPv4 über IPv6 bevorzugen. Informationen zum Ausführen dieser Aufgabe finden Sie im KB-Artikel [Leitfaden zum Konfigurieren von IPv6 in Windows für fortgeschrittene Benutzer](https://support.microsoft.com/help/929852/guidance-for-configuring-ipv6-in-windows-for-advanced-users).

### <a name="configure-the-second-domain-controller"></a>Konfigurieren des zweiten Domänen Controllers

Stellen Sie eine Verbindung mit AZDC02 her, indem Sie die im Skript angegebenen Anmelde Informationen verwenden.

* Initialisieren und formatieren Sie den Datenträger als F:
   * Öffnen Sie das Startmenü, und navigieren Sie zu **Computer Verwaltung** .
   * Navigieren Sie zu **Speicher** >  Datenträger**Verwaltung** .
   * Initialisieren des Datenträgers als MBR
   * Erstellen eines neuen einfachen Volumes und Zuweisen des Laufwerk Buchstabens F: Sie können eine Volumebezeichnung angeben, wenn Sie möchten.
* Installieren von Active Directory Domain Services mithilfe Server-Manager
* Herauf Stufen des Domänen Controllers
   * Hinzufügen eines Domänen Controllers zu einer vorhandenen Domäne contoso.com
   * Angeben von Anmelde Informationen zum Ausführen des Vorgangs
   * Ändern Sie die Pfade von C: auf das Laufwerk F:, das Sie erstellt haben, wenn Sie zur Eingabe Ihres Orts aufgefordert werden.
   * Stellen Sie sicher, dass Domain Name System (DNS)-Server und globaler Katalog (GC) auf der Seite Domänen Controller Optionen aktiviert sind.
   * Angeben eines Kennworts für den Verzeichnisdienst-Wiederherstellungs Modus basierend auf den Anforderungen Ihrer Organisation
   * Überprüfen Sie die im Assistenten getroffenen Auswahl, und wählen Sie **weiter** aus.

> [!NOTE]
> Durch die Überprüfung der erforderlichen Komponenten wird gewarnt, dass dem physischen Netzwerkadapter keine statischen IP-Adressen zugewiesen sind. Diese können Sie problemlos ignorieren, da statische IPS im virtuellen Azure-Netzwerk zugewiesen werden.

* Wählen Sie **Installieren**

Nachdem der Assistent den Installationsvorgang abgeschlossen hat, wird der virtuelle Computer neu gestartet.

Wenn der virtuelle Computer neu gestartet wird, mit den verwendeten Anmelde Informationen, aber dieses Mal als Mitglied der contoso.com-Domäne

Da [virtuelle Azure-Netzwerke IPv6 nicht unterstützen, sollten](https://docs.microsoft.com/azure/virtual-network/virtual-networks-faq#do-vnets-support-ipv6) Sie Ihre VMS so einrichten, dass Sie IPv4 über IPv6 bevorzugen. Informationen zum Ausführen dieser Aufgabe finden Sie im KB-Artikel [Leitfaden zum Konfigurieren von IPv6 in Windows für fortgeschrittene Benutzer](https://support.microsoft.com/help/929852/guidance-for-configuring-ipv6-in-windows-for-advanced-users).

### <a name="configure-dns"></a>Konfigurieren des DNS

Nachdem Sie die neuen Domänen Controller in Azure herauf gestuft haben, müssen Sie auf den primären und sekundären DNS-Server für das virtuelle Netzwerk festgelegt werden, und alle lokalen DNS-Server werden in den tertiären und überschreiten herabgestuft. Weitere Informationen zum Ändern von DNS-Servern finden Sie im Artikel [erstellen, ändern oder Löschen eines virtuellen Netzwerks](https://docs.microsoft.com/azure/virtual-network/manage-virtual-network#change-dns-servers).

### <a name="wrap-up"></a>Zusammenfassung

An diesem Punkt verfügt die Umgebung über ein paar von Domänen Controllern, und wir haben das virtuelle Azure-Netzwerk so konfiguriert, dass der Umgebung weitere Server hinzugefügt werden können. Zu diesem Zeitpunkt sollten Sie Aufgaben nach der Installation von Active Directory Domain Services wie das Konfigurieren von Standorten und Diensten, das überwachen, sichern und Sichern des integrierten Administrator Kontos ausführen.

## <a name="removing-the-environment"></a>Entfernen der Umgebung

Wenn Sie die Umgebung entfernen möchten, nachdem Sie das Testen der oben erstellten Ressourcengruppe abgeschlossen haben, können Sie mit diesem Schritt alle Komponenten entfernen, die Teil dieser Ressourcengruppe sind.

### <a name="remove-using-the-azure-portal"></a>Entfernen mithilfe des Azure-Portal

Navigieren Sie im Azure-Portal zu **Ressourcengruppen** , und wählen Sie die Ressourcengruppe aus, die wir in diesem Beispiel adonazurevms erstellt haben, und klicken Sie dann auf **Ressourcengruppe löschen**. Der Prozess fordert eine Bestätigung an, bevor alle in der Ressourcengruppe enthaltenen Ressourcen gelöscht werden.

### <a name="remove-using-the-azure-cli"></a>Entfernen mithilfe des Azure CLI

Führen Sie in Azure CLI den folgenden Befehl aus:

```azurecli
az group delete --name ADonAzureVMs
```

## <a name="next-steps"></a>Nächste Schritte

* [Sichere Virtualisierung Active Directory Domain Services (AD DS)](../../Introduction-to-Active-Directory-Domain-Services-AD-DS-Virtualization-Level-100.md)
* [Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-get-started-express)
* [Sicherung und Wiederherstellung](https://docs.microsoft.com/azure/virtual-machines/windows/backup-recovery)
* [VPN-Konnektivität Zwischenstand Orten](https://docs.microsoft.com/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal)
* [Chtungs](https://docs.microsoft.com/azure/virtual-machines/windows/monitor)
* [Sicherheit und Richtlinien](https://docs.microsoft.com/azure/virtual-machines/windows/security-policy)
* [Wartung und Updates](https://docs.microsoft.com/azure/virtual-machines/windows/maintenance-and-updates)
