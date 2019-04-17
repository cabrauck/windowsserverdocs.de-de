# [Networking](Networking.md)
## [Windows Server unterstützte Netzwerkszenarios](windows-server-supported-networking-scenarios.md)

## [Was ist neu in Netzwerken](What-s-New-in-Networking.md)

## [Netzwerk-Anleitung für Windows Server Core](core-network-guide/core-network-guide-windows-server.md)
### [Kernkomponenten](core-network-guide/Core-Network-Guide.md)
### [Core-Netzwerk-Begleithandbuch](core-network-guide/cncg/Core-Network-companion-Guides.md)
#### [Bereitstellen von Serverzertifikaten für 802.1 X kabelgebundene und drahtlose Bereitstellungen](core-network-guide/cncg/server-certs/Deploy-Server-Certificates-for-802.1X-Wired-and-Wireless-Deployments.md)
##### [Übersicht über die Bereitstellung von Server-Zertifikat](core-network-guide/cncg/server-certs/Server-Certificate-Deployment-Overview.md)
##### [Planen der Server Zertifikat Bereitstellung](core-network-guide/cncg/server-certs/Server-Certificate-Deployment-Planning.md)
##### [Bereitstellung von Serverzertifikaten](core-network-guide/cncg/server-certs/Server-Certificate-Deployment.md)
###### [Installieren des Webservers WEB1](core-network-guide/cncg/server-certs/Install-the-Web-Server-WEB1.md)
###### [Erstellen eines Aliaseintrags (CNAME) in DNS für WEB1](core-network-guide/cncg/server-certs/create-an-Alias-CNAME-Record-in-DNS-for-WEB1.md)
###### [Konfigurieren von WEB1 zum Verteilen von Zertifikatssperrlisten (CRLs)](core-network-guide/cncg/server-certs/Configure-WEB1-to-Distribute-Certificate-Revocation-lists.md)
###### [Vorbereiten der Datei „CAPolicy.inf“](core-network-guide/cncg/server-certs/Prepare-the-CAPolicy-inf-File.md)
###### [Installieren der Zertifizierungsstelle](core-network-guide/cncg/server-certs/Install-the-Certification-Authority.md)
###### [Konfigurieren der CDP- und AIA-Erweiterungen für Zertifizierungsstelle 1](core-network-guide/cncg/server-certs/Configure-the-cdP-and-AIA-Extensions-on-CA1.md)
###### [Kopieren des Zertifikats der Zertifizierungsstelle und Zertifikatssperrliste in das virtuelle Verzeichnis](core-network-guide/cncg/server-certs/copy-the-CA-Certificate-and-CRL-to-the-Virtual-directory.md)
###### [Konfigurieren der Serverzertifikatvorlage](core-network-guide/cncg/server-certs/Configure-the-Server-Certificate-Template.md)
###### [Konfigurieren der automatischen Registrierung von Serverzertifikaten](core-network-guide/cncg/server-certs/Configure-Server-Certificate-Autoenrollment.md)
###### [Aktualisieren von Gruppenrichtlinien](core-network-guide/cncg/server-certs/Refresh-Group-Policy.md)
###### [Überprüfen der Serverregistrierung eines Serverzertifikats](core-network-guide/cncg/server-certs/verify-Server-Enrollment-of-a-Server-Certificate.md)
#### [Bereitstellen von kennwortbasierten 802.1 authentifizierten 802.1X-Funkzugriffs](core-network-guide/cncg/wireless/a-deploy-8021X-wireless-access.md)
##### [Übersicht über Bereitstellung des Funkzugriffs](core-network-guide/cncg/wireless/b-wireless-access-deploy-overview.md)
##### [Prozess der Bereitstellung des Funkzugriffs](core-network-guide/cncg/wireless/c-wireless-access-deploy-process.md)
##### [WLAN-Bereitstellung planen](core-network-guide/cncg/wireless/d-wireless-access-planning.md)
##### [Bereitstellung des Funkzugriffs](core-network-guide/cncg/wireless/e-wireless-access-deployment.md)
#### [Bereitstellen von BranchCache gehostete Cache-Modus](core-network-guide/cncg/bc-hcm/1-Deploy-Bc-Hcm.md)
##### [Übersicht über die Bereitstellung von BranchCache gehostete Cache-Modus](core-network-guide/cncg/bc-hcm/2-Bc-Hcm-Deploy-Overview.md)
##### [BranchCache gehostete Cache Modus-Bereitstellung planen](core-network-guide/cncg/bc-hcm/3-Bc-Hcm-Plan.md)
##### [BranchCache gehostete Cache Modus Bereitstellung](core-network-guide/cncg/bc-hcm/4-Bc-Hcm-Deployment.md)
###### [Installieren der BranchCache-Funktion und Konfigurieren des gehosteten Cache-Servers nach Dienstverbindungspunkt](core-network-guide/cncg/bc-hcm/5-Bc-Feature-Scp.md)
###### [Verschieben und Ändern der Größe des gehosteten Caches (Optional)](core-network-guide/cncg/bc-hcm/6-Bc-move-Resize-Cache.md)
###### [Prehashing und Vorabladen von Inhalt auf dem gehosteten Cacheserver (Optional)](core-network-guide/cncg/bc-hcm/7-Bc-Prehash-Preload.md)
####### [Erstellen von Inhaltsserver-Datenpaketen für Web- und Inhalte (Optional)](core-network-guide/cncg/bc-hcm/8-Bc-Data-Packages.md)
####### [Importieren von Datenpaketen auf dem gehosteten Cacheserver (Optional)](core-network-guide/cncg/bc-hcm/9-Bc-import-Data.md)
###### [Konfigurieren von automatischen gehosteten Clientermittlung Cache nach Dienstverbindungspunkt](core-network-guide/cncg/bc-hcm/10-Bc-Client-By-Scp.md)
##### [Zusätzliche Ressourcen](core-network-guide/cncg/bc-hcm/11-Bc-Hcm-additional-resources.md)

## [BranchCache](branchcache/BranchCache.md)
### [BranchCache Netsh und Windows PowerShell-Befehle](branchcache/BranchCache-Network-Shell-and-Windows-powershell-Commands.md)
### [BranchCache-bereitstellungsanleitung](branchcache/deploy/BranchCache-Deployment-Guide.md)
#### [Auswählen eines BranchCache-Entwurfs](branchcache/plan/Choosing-a-BranchCache-Design.md)
#### [Bereitstellen von BranchCache](branchcache/deploy/Deploy-BranchCache.md)
##### [Installieren und Konfigurieren von Inhaltsservern](branchcache/deploy/Install-and-Configure-Content-Servers.md)
###### [Installieren von Inhaltsservern, die die BranchCache-Funktion verwenden](branchcache/deploy/Install-Content-Servers-that-Use-the-BranchCache-Feature.md)
####### [Installieren der BranchCache-Funktion](branchcache/deploy/Install-the-BranchCache-Feature.md)
####### [Konfigurieren von Windows Server Update Services (WSUS)-Inhaltsservern](branchcache/deploy/configure-wsus-content-servers.md)
###### [Installieren von Dateidienst-Inhaltsservern](branchcache/deploy/Install-File-Services-Content-Servers.md)
####### [Konfigurieren der Serverrolle „Dateidienste“](branchcache/deploy/Configure-the-File-Services-server-role.md)
######## [Installieren eines neuen Dateiservers als Inhaltsserver](branchcache/deploy/Install-a-New-File-Server-as-a-Content-Server.md)
######## [Konfigurieren eines vorhandenen Dateiservers als Inhaltsserver](branchcache/deploy/Configure-an-Existing-File-Server-as-a-Content-Server.md)
####### [Aktivieren von Hashveröffentlichung für Dateiserver](branchcache/deploy/Enable-Hash-Publication-for-File-Servers.md)
######## [Aktivieren von Hashveröffentlichung für Dateiserver, die keine Domänenmitglieder sind](branchcache/deploy/Enable-Hash-Publication-for-Non-Domain-Member-File-Servers.md)
######## [Aktivieren von Hashveröffentlichung für Dateiserver in der Domäne](branchcache/deploy/Enable-Hash-Publication-for-Domain-Member-File-Servers.md)
######### [Erstellen der BranchCache-Dateiserver Organisationseinheit (OU)](branchcache/deploy/create-the-BranchCache-File-Servers-Organizational-Unit.md)
######### [Verschieben von Dateiservern in die BranchCache-Dateiserver OU](branchcache/deploy/move-File-Servers-to-the-BranchCache-File-Servers-Organizational-Unit.md)
######### [Erstellen des Gruppenrichtlinienobjekts (GPO) für die BranchCache-Hash-Veröffentlichung](branchcache/deploy/create-the-BranchCache-Hash-Publication-Group-Policy-Object.md)
######### [Konfigurieren der BranchCache-Hash-Veröffentlichung GPO](branchcache/deploy/Configure-the-BranchCache-Hash-Publication-Group-Policy-Object.md)
####### [Aktivieren von BranchCache auf einer Dateifreigabe (Optional)](branchcache/deploy/enable-bc-on-file-share.md)
##### [Bereitstellen von gehosteten Cacheserver (Optional)](branchcache/deploy/deploy-hosted-cache-servers.md)
##### [Prehashing und Vorabladen von Inhalt auf gehostete Cacheserver (Optional)](branchcache/deploy/prehashing-and-preloading.md)
##### [Konfigurieren von BranchCache-Clientcomputern](branchcache/deploy/Configure-BranchCache-Client-computers.md)
###### [Verwenden von Gruppenrichtlinien zum Konfigurieren von Domänenmitglieds-Clientcomputer](branchcache/deploy/Use-Group-Policy-to-Configure-Domain-Member-Client-computers.md)
###### [Verwenden von Windows PowerShell zum Konfigurieren von Clientcomputern, die keine Domänenmitglieder sind](branchcache/deploy/Use-Windows-powershell-to-Configure-Non-Domain-Member-Client-computers.md)
####### [Konfigurieren von Firewallregeln für Nichtdomänenmitglieder, um BranchCache-Datenverkehr zuzulassen](branchcache/deploy/Configure-Firewall-Rules-for-Non-Domain-Members-to-Allow-BranchCache-Traffic.md)
###### [Überprüfen von Clientcomputereinstellungen](branchcache/deploy/verify-Client-computer-Settings.md)

## [DirectAccess](../remote/remote-access/da-stub.md) 

## [Domain Name System (DNS)](dns/dns-top.md)
### [Neues in DNS-Client unter Windows Server](dns/What-s-New-in-DNS-Client.md)
### [Neues in DNS-Server in Windows Server](dns/What-s-New-in-DNS-Server.md)
### [DNS-Richtlinie Szenario Richtlinien](dns/deploy/DNS-Policy-Scenario-Guide.md)
#### [DNS-Richtlinien (Übersicht)](dns/deploy/DNS-Policies-Overview.md)
#### [Verwenden von DNS-Richtlinien für GeoLocation-Datenverkehrsverwaltung mit Primärservern](dns/deploy/primary-geo-location.md)
#### [Verwenden von DNS-Richtlinien für GeoLocation-Datenverkehrsverwaltung mit primären und sekundären Bereitstellungen](dns/deploy/primary-secondary-geo-location.md)
#### [Verwenden von DNS-Richtlinien für intelligente DNS-Antworten basierend auf der Tageszeit](dns/deploy/dns-tod-intelligent.md)
#### [DNS-Antworten basierend auf der Tageszeit mit einem Azure-Cloud-app-server](dns/deploy/dns-tod-azure-cloud-app-server.md)
#### [Verwenden von DNS-Richtlinien für Split-Brain DNS-Bereitstellung](dns/deploy/split-brain-DNS-deployment.md)
#### [Verwenden von DNS-Richtlinien für Split-Brain DNS in Active Directory](dns/deploy/dns-sb-with-ad.md)
#### [Verwenden von DNS-Richtlinien für das Anwenden von Filtern auf DNS-Abfragen](dns/deploy/apply-filters-on-dns-queries.md)
#### [Verwenden von DNS-Richtlinien für app-Netzwerklastenausgleich](dns/deploy/app-lb.md)
#### [Verwenden von DNS-Richtlinien für app-den Anwendungslastenausgleich mit GeoLocation Informationen](dns/deploy/app-lb-geo.md)

## [Dynamic Host Configuration-Protokoll (DHCP)](technologies/dhcp/dhcp-top.md)
### [Neues in DHCP](technologies/dhcp/What-s-New-in-DHCP.md)
#### [DHCP-Subnetz Auswahloptionen](technologies/dhcp/dhcp-subnet-options.md)
#### [DHCP-Protokollierungsereignisse für DNS-Eintragsregistrierungen](technologies/dhcp/dhcp-dns-events.md)
### [Bereitstellung von DHCP mit Windows PowerShell](technologies/dhcp/dhcp-deploy-wps.md)

## [High-Performance Networking (HPN)](technologies/hpn/hpn-top.md)
### [Netzwerk-Offload- und Optimierungstechnologien](technologies/hpn/network-offload-and-optimization.md)
#### [Nur Software (SO)-Features und -Technologien](technologies/hpn/hpn-software-only-features.md)
#### [Integration von Software und Hardware (SH)-Features und -Technologien](technologies/hpn/hpn-software-hardware-features.md)
#### [Hardware Only (HO)-Features und -Technologien](technologies/hpn/hpn-hardware-only-features.md)
#### [NIC erweiterte Eigenschaften](technologies/hpn/hpn-nic-advanced-properties.md)

### [Insider preview](technologies/hpn/hpn-insider-preview.md)
### [Empfangen von Segmentkoaleszenz (RSC) im vSwitch](technologies/hpn/rsc-in-the-vswitch.md)

### [Konvergente NIC-Anleitung](technologies/conv-nic/cnic-top.md)
#### [Konfiguration mit einer Netzwerkkarte](technologies/conv-nic/cnic-single.md)
#### [Konfiguration eines Netzwerkadapters Datacenter](technologies/conv-nic/cnic-datacenter.md)
#### [Physische Switch-Konfiguration](technologies/conv-nic/cnic-app-switch-config.md)
#### [Problembehandlung bei NIC zusammengeführt](technologies/conv-nic/cnic-app-troubleshoot.md)

### [Data Center Bridging \(DCB\)](technologies/dcb/dcb-top.md)
#### [Installieren von DCB](technologies/dcb/dcb-install.md)
#### [Verwalten von DCB](technologies/dcb/dcb-manage.md)

### [Virtual Receive Side Scaling (vRSS)](technologies/vrss/vrss-top.md)
#### [Planen der Verwendung von vRSS](technologies/vrss/vrss-plan.md)
#### [Aktivieren von vRSS auf einem virtuellen Netzwerkadapter](technologies/vrss/vrss-enable.md)
#### [Verwalten von vRSS](technologies/vrss/vrss-manage.md)
#### [vRSS – häufig gestellte Fragen](technologies/vrss/vrss-faq.md)
#### [Windows PowerShell-Befehlen für RSS- und vRSS](technologies/vrss/vrss-wps.md)
#### [Beheben von vRSS-Problemen](technologies/vrss/vrss-resolve-issues.md)

## [Host Compute-Netzwerk (HCN)-Dienst-API](technologies/hcn/hcn-top.md)   
### [Allgemeine HCN-Szenarien](technologies/hcn/hcn-scenarios.md)
### [RPC-Kontexthandles für HCN](technologies/hcn/hcn-declaration-handles.md)
### [HCN JSON-Dokumentschemas](technologies/hcn/hcn-json-document-schemas.md)
### [Beispiel für von C#-generierten Code](technologies/hcn/example-c-sharp.md)
### [Beispiel für von Go generierten Code](technologies/hcn/example-go.md)

## [Virtueller Hyper-V-Switch](technologies/vswitch-stub.md)

## [IP-Adressverwaltung (IPAM)](technologies/ipam/ipam-top.md)
### [Neues in IPAM](technologies/ipam/What-s-New-in-IPAM.md)
### [Verwalten von IPAM](technologies/ipam/Manage-IPAM.md)
#### [Verwaltung von DNS-Ressourceneinträgen](technologies/ipam/DNS-Resource-Record-Management.md)
##### [Hinzufügen eines DNS-Ressourceneintrags](technologies/ipam/add-a-DNS-Resource-Record.md)
##### [Löschen von DNS-Ressourceneinträgen](technologies/ipam/delete-DNS-Resource-Records.md)
##### [Filtern der Ansicht von DNS-Ressourceneinträgen](technologies/ipam/Filter-the-View-of-DNS-Resource-Records.md)
##### [Anzeigen von DNS-Ressourceneinträgen für eine bestimmte IP-Adresse](technologies/ipam/View-DNS-Resource-Records-for-a-Specific-IP-address.md)
#### [DNS-Zonenverwaltung](technologies/ipam/DNS-Zone-Management.md)
##### [Erstellen einer DNS-zone](technologies/ipam/create-a-DNS-Zone.md)
##### [Bearbeiten einer DNS-zone](technologies/ipam/edit-a-DNS-Zone.md)
##### [Anzeigen von DNS-Ressourceneinträgen für eine DNS-zone](technologies/ipam/View-DNS-Resource-Records-for-a-DNS-Zone.md)
##### [Anzeigen von DNS-Zonen](technologies/ipam/View-DNS-Zones.md)
#### [Verwalten von Ressourcen in mehreren ActiveDirectory-Gesamtstrukturen](technologies/ipam/Manage-Resources-in-Multiple-active-directory-forests.md)
#### [Endgültiges Löschen von Nutzungsdaten](technologies/ipam/Purge-Utilization-Data.md)
#### [Rollenbasierte Zugriffssteuerung](technologies/ipam/Role-based-Access-Control.md)
##### [Verwalten der rollenbasierten Zugriffssteuerung mit Server-Manager](technologies/ipam/Manage-Role-Based-Access-Control-with-server-manager.md)
###### [Erstellen einer Benutzerrolle für die Zugriffssteuerung](technologies/ipam/create-a-User-Role-for-Access-Control.md)
###### [Erstellen einer Zugriffsrichtlinie](technologies/ipam/create-an-Access-Policy.md)
###### [Festlegen des Zugriffsbereichs für eine DNS-zone](technologies/ipam/Set-Access-Scope-for-a-DNS-Zone.md)
###### [Festlegen des Zugriffsbereichs für DNS-Ressourceneinträgen](technologies/ipam/Set-Access-Scope-for-DNS-Resource-Records.md)
###### [Anzeigen von Rollen und Rollenberechtigungen](technologies/ipam/View-Roles-and-Role-Permissions.md)
##### [Verwalten der rollenbasierten Zugriffssteuerung mit Windows PowerShell](technologies/ipam/Manage-Role-Based-Access-Control-with-Windows-powershell.md)

## [Netzwerklastenausgleich](technologies/Network-Load-Balancing.md)



## [Netzwerkrichtlinienserver (Network Policy Server, NPS)](technologies/nps/nps-top.md)
### [NPS: Bewährte Methoden](technologies/nps/nps-best-practices.md)
### [Erste Schritte mit NPS](technologies/nps/nps-getstart-top.md)
#### [Verbindungsverarbeitung-Anforderung](technologies/nps/nps-crp-top.md)
##### [Verbindungsanforderungsrichtlinien](technologies/nps/nps-crp-crpolicies.md)
##### [Bereichsnamen](technologies/nps/nps-crp-realm-names.md)
##### [RADIUS-Remoteservergruppen](technologies/nps/nps-crp-rrsg.md)
#### [Netzwerkrichtlinien](technologies/nps/nps-np-overview.md)
##### [Zugriffsberechtigung](technologies/nps/nps-np-access.md)
#### [NPS-Vorlagen](technologies/nps/nps-templates.md)
#### [RADIUS-clients](technologies/nps/nps-radius-clients.md)
### [Planen des Netzwerkzeitprotokolls (NPS)](technologies/nps/nps-plan-top.md)
#### [Planen eines NPS als RADIUS-Server](technologies/nps/nps-plan-server.md)
#### [Planen eines NPS als RADIUS-Proxy](technologies/nps/nps-plan-proxy.md)
### [Bereitstellen von NPS](technologies/nps/nps-deploy.md)
### [Verwalten von NPS](technologies/nps/nps-manage-top.md)
#### [Netzwerkrichtlinienserver-Verwaltung mit Verwaltungstools](technologies/nps/nps-admintools.md)
#### [Konfigurieren von Verbindungsanforderungsrichtlinien](technologies/nps/nps-crp-configure.md)
#### [Konfigurieren von Firewalls für RADIUS-Datenverkehr](technologies/nps/nps-firewalls-configure.md)
#### [Konfigurieren von Netzwerkrichtlinien](technologies/nps/nps-np-configure.md)
#### [Konfigurieren von NPS-Kontoführung](technologies/nps/nps-accounting-configure.md)
#### [Konfigurieren von RADIUS-clients](technologies/nps/nps-radius-clients-configure.md)
#### [Konfigurieren von RADIUS-Remoteservergruppen](technologies/nps/nps-crp-rrsg-configure.md)
#### [Verwalten von mit NPS verwendeten Zertifikaten](technologies/nps/nps-manage-certificates.md)
##### [Konfigurieren von Zertifikatvorlagen für PEAP- und EAP-Anforderungen](technologies/nps/nps-manage-cert-requirements.md)
#### [Verwalten von NPSs](technologies/nps/nps-manage-servers.md)
##### [Konfigurieren von NPS auf einem mehrfach vernetzten computer](technologies/nps/nps-multihomed-configure.md)
##### [Konfigurieren von NPS UDP-Portinformationen](technologies/nps/nps-udp-ports-configure.md)
##### [Deaktivieren von NAS-Benachrichtigungen](technologies/nps/nps-disable-nas-notifications.md)
##### [Exportieren einer NPS-Konfiguration für den Import auf einem anderen Server](technologies/nps/nps-manage-export.md)
##### [Erhöhen der durch NPS verarbeiteten gleichzeitigen Authentifizierungen](technologies/nps/nps-concurrent-auth.md)
##### [Installieren von NPS](technologies/nps/nps-manage-install.md)
##### [NPS-Proxy Server-Lastenausgleich](technologies/nps/nps-manage-proxy-lb.md)
##### [Registrieren eines Netzwerkrichtlinienservers in einer Active Directory-Domäne](technologies/nps/nps-manage-register.md)
##### [Aufheben der Registrierung eines NPS aus einer Active Directory-Domäne](technologies/nps/nps-manage-unregister.md)
##### [Verwenden regulärer Ausdrücke in NPS](technologies/nps/nps-crp-reg-expressions.md)
##### [Überprüfen der Konfiguration nach NPS-Änderungen](technologies/nps/nps-manage-verify.md)
##### [NPS-Datensammlung](technologies/nps/nps-data-collection.md)
#### [Verwalten von NPS-Vorlagen](technologies/nps/nps-manage-templates.md)

## [Network Shell (Netsh)](technologies/netsh/netsh.md)
### [Netsh-Befehlssyntax, Kontexte und Formatierung](technologies/netsh/netsh-contexts.md)
### [Beispielbatchdatei für Network Shell (Netsh)](technologies/netsh/netsh-wins.md)
### [Netsh http-Befehle](technologies/netsh/netsh-http.md)
### [Netsh Interface Portproxy-Befehle](technologies/netsh/netsh-interface-portproxy.md)

## [Netzwerk-Subsystem-Leistungsoptimierung](technologies/network-subsystem/net-sub-performance-top.md)
### [Auswählen einer Netzwerkkarte](technologies/network-subsystem/net-sub-choose-nic.md)
### [Konfigurieren der Reihenfolge von Netzwerkschnittstellen](technologies/network-subsystem/net-sub-interface-metric.md)
### [Leistung optimieren von Netzwerkkarten](technologies/network-subsystem/net-sub-performance-tuning-nics.md)
### [Netzwerkbezogene Leistungsindikatoren](technologies/network-subsystem/net-sub-performance-counters.md)
### [Leistungstools für Netzwerkauslastungen](technologies/network-subsystem/net-sub-performance-tools.md)

## [NIC Teaming](technologies/nic-teaming/NIC-Teaming.md)
### [NIC-Teaming-MAC-Adresse verwenden und Verwaltung](technologies/nic-teaming/NIC-Teaming-MAC-address-Use-and-Management.md)
### [Erstellen eines neuen NIC-Teams auf einem Hostcomputer oder einer VM](technologies/nic-teaming/create-a-New-NIC-Team-on-a-Host-computer-or-VM.md)
### [Problembehandlung beim NIC-Teamvorgang](technologies/nic-teaming/Troubleshooting-NIC-Teaming.md)

## [Quality of Service (QoS)-Richtlinie](technologies/qos/qos-policy-top.md)
### [Erste Schritte mit QoS-Richtlinie](technologies/qos/qos-policy-get-started.md)
#### [Funktionsweise von QoS-Richtlinien](technologies/qos/qos-policy-works.md)
#### [QoS-Richtlinie Architektur](technologies/qos/qos-policy-architecture.md)
#### [QoS-Richtlinie Szenarien](technologies/qos/qos-policy-scenarios.md)
###[Verwalten von QoS-Richtlinie](technologies/qos/qos-policy-manage.md)
#### [QoS-Richtlinie Ereignissen und Fehlern](technologies/qos/qos-policy-errors.md)
### [QoS-Richtlinie – häufig gestellte Fragen](technologies/qos/qos-policy-faq.md)

## [Software-Defined Networking (SDN)](sdn/index.yml)

### [SDN in Windows Server-Übersicht](sdn/software-defined-networking.md)

### [SDN-Technologien](sdn/technologies/Software-Defined-Networking-Technologies.md)
#### [Hyper-V-Netzwerkvirtualisierung](sdn/technologies/hyper-v-network-virtualization/Hyper-V-Network-Virtualization.md)
##### [Übersicht über Hyper-V-Netzwerkvirtualisierung](sdn/technologies/hyper-v-network-virtualization/hyperv-network-virtualization-overview-windows-server.md)
##### [Hyper-V-Netzwerk-Virtualisierung technische details](sdn/technologies/hyper-v-network-virtualization/hyperv-network-virtualization-technical-details-windows-server.md)
##### [Neues in Hyper-V-Netzwerkvirtualisierung](sdn/technologies/hyper-v-network-virtualization/whats-new-hyperv-network-virtualization-windows-server.md)
#### [Interner DNS-Dienst (iDNS) für SDN](sdn/technologies/Idns-for-Sdn.md)
#### [Netzwerkcontroller](sdn/technologies/network-controller/Network-Controller.md)
##### [Netzwerk-Netzwerkcontroller – hohen Verfügbarkeit](sdn/technologies/network-controller/network-controller-high-availability.md)
##### [Installieren der Serverrolle „Netzwerkcontroller“ mit Server-Manager](sdn/technologies/network-controller/Install-the-Network-Controller-server-role-using-server-manager.md)
##### [Schritte nach der Bereitstellung für den Netzwerkcontroller](sdn/technologies/network-controller/post-deploy-steps-nc.md)
#### [Virtualisierung der Netzwerkfunktion](sdn/technologies/network-function-virtualization/Network-Function-Virtualization.md)
##### [Datacenter Firewall (Übersicht)](sdn/technologies/network-function-virtualization/Datacenter-Firewall-Overview.md)
##### [RAS-Gateway für SDN](sdn/technologies/network-function-virtualization/RAS-Gateway-for-SDN.md)
###### [Neuigkeiten in RAS-Gateway](sdn/technologies/network-function-virtualization/What-s-New-in-RAS-Gateway.md)
###### [RAS-Gateway: Bereitstellungsarchitektur](sdn/technologies/network-function-virtualization/RAS-Gateway-Deployment-Architecture.md)
###### [RAS-Gateway: hohe Verfügbarkeit](sdn/technologies/network-function-virtualization/RAS-Gateway-High-Availability.md)
##### [Softwarelastenausgleich (SLB) für SDN](sdn/technologies/network-function-virtualization/software-load-balancing-for-sdn.md)
#### [Switch Embedded Teaming (SET) für SDN](sdn/technologies/Set-for-Sdn.md)
#### [Container-Networking](sdn/technologies/Containers/Container-networking-overview.md)

### [Planen für die SDN](sdn/plan/Plan-a-Software-Defined-Network-Infrastructure.md)
#### [Installation und Anforderungen an die Vorbereitungen zur Bereitstellung von Netzwerkcontrollern](sdn/plan/Installation-and-Preparation-Requirements-for-Deploying-Network-Controller.md)

### [Bereitstellen von SDN](sdn/deploy/Deploy-Software-Defined-Networking.md)
#### [Bereitstellen einer SDN-Infrastruktur](sdn/deploy/Deploy-a-Software-Defined-Network-Infrastructure.md)
##### [Bereitstellen einer SDN-Infrastruktur mithilfe von Skripts](sdn/deploy/Deploy-a-Software-Defined-Network-infrastructure-using-scripts.md)
#### [Bereitstellen von SDN-Technologien, die mit Windows PowerShell](sdn/deploy/Deploy-Software-Defined-Network-Technologies-using-Windows-powershell.md)
##### [Bereitstellen des Netzwerkcontrollers mithilfe von Windows PowerShell](sdn/deploy/Deploy-Network-Controller-using-Windows-powershell.md)

### [Verwalten von SDN](sdn/manage/manage-sdn.md)
#### [Verwalten von virtuellen Mandantennetzwerken](sdn/manage/Manage-Tenant-Virtual-Networks.md)
##### [Grundlegendes zur Verwendung von virtuellen Netzwerken und VLANs](sdn/manage/Understanding-Usage-of-Virtual-Networks-and-VLANs.md)
##### [Verwendung Zugriffssteuerungslisten (ACLs) zum Verwalten von Datacenter-Netzwerk-Datenverkehr](sdn/manage/use-acls-for-traffic-flow.md)
##### [Erstellen, Löschen oder Aktualisieren von virtuellen Mandantennetzwerken](sdn/manage/create,-delete,-or-Update-Tenant-Virtual-Networks.md)
##### [Hinzufügen eines Gateways zu einem virtuellen Mandantennetzwerk](sdn/manage/add-a-Virtual-Gateway-to-a-Tenant-Virtual-Network.md)
##### [Verbinden von Containerendpunkten mit einem virtuellen Mandantennetzwerk](sdn/manage/Connect-container-endpoints-to-a-Tenant-Virtual-Network.md)
##### [Konfigurieren der Verschlüsselung für ein virtuelles Subnetz](sdn/vnet-encryption/sdn-config-vnet-encryption.md)
##### [Egress-Messung in einem virtuellen Netzwerk](sdn/manage/sdn-egress.md)

#### [Verwalten von Mandantenworkloads](sdn/manage/Manage-Tenant-Workloads.md)
##### [Erstellen einer VM und Verbinden mit einem virtuellen Mandantennetzwerk oder VLAN](sdn/manage/create-a-Tenant-VM.md)
##### [Konfigurieren von QoS für die Netzwerkkarte einer Mandanten-VM](sdn/manage/Configure-QoS-for-Tenant-VM-Network-Adapter.md)
##### [Rechenzentrumsfirewall ACLs konfigurieren](sdn/manage/Configure-Datacenter-Firewall-Acls.md)
##### [Konfigurieren der Software Load Balancer für Lastenausgleich und Netzwerkadressübersetzung (NAT)](sdn/manage/Configure-SLB-and-Nat.md)
##### [Verwenden virtueller Netzwerkgeräte in einem virtuellen Netzwerk](sdn/manage/Use-Network-Virtual-Appliances-on-a-VN.md)
##### [Gastclustering in einem virtuellen Netzwerk](sdn/manage/guest-clustering.md)
#### [Aktualisieren, Sichern und Wiederherstellen einer SDN-Infrastruktur](sdn/manage/Update-Backup-Restore.md)

### [Sicherheit für SDN](sdn/security/sdn-security-top.md)
#### [Sichern des Netzwerk-Controllers](sdn/security/nc-security.md)
#### [Verwalten von Zertifikaten für SDN](sdn/security/sdn-manage-certs.md)
#### [Kerberos mit Dienstprinzipalname (SPN)](sdn/security/kerberos-with-spn.md)
#### [SDN Firewall Überwachung](sdn/security/sdn-firewall-auditing.md)

### [Virtuelles Netzwerk peering](sdn/vnet-peering/sdn-vnet-peering.md)
#### [Konfigurieren von virtuellem Netzwerkpeering](sdn/vnet-peering/sdn-configure-vnet-peering.md)

### [Windows Server 2019 Gateway-Leistung](sdn/gateway-performance.md)
### [Gateway-Bandbreite-Zuordnung](sdn/gateway-allocation.md)

### [Problembehandlung für SDN](sdn/troubleshoot/Troubleshoot-Software-Defined-Networking.md)
#### [Problembehandlung für die Windows Server-Software Defined Networking-Stapel](sdn/troubleshoot/troubleshoot-windows-server-software-defined-networking-stack.md)

### [Systemcenter-Technologien für SDN](sdn/Sc-Tech-for-Sdn.md)
### [Microsoft Azure und SDN](sdn/Azure_and_Sdn.md)
### [Kontaktieren des Datencenter- und Cloud Networking-Teams](sdn/contact-sdn-team.md)

## [Virtual Private Networking (VPN)](technologies/vpn-stub.md)

## [Windows Internet Name Service (WINS)](technologies/wins/wins-top.md)

## [Windows-Zeitdienst](windows-time-service/windows-time-service-top.md)
### [Insider Preview - Windows-Zeitdienst in Windows Server 2019](windows-time-service/insider-preview.md)
### [Genaue Uhrzeit für Windows Server2016](windows-time-service/accurate-time.md)
### [Unterstützte Grenze für hochpräzise Uhrzeit](windows-time-service/support-boundary.md)
### [Konfigurieren von Systemen für hohe Genauigkeit](windows-time-service/configuring-systems-for-high-accuracy.md)
### [Windows-Zeitdienst für Weg](windows-time-service/windows-time-for-traceability.md)
### [Technische Referenz zu Windows-Zeitdienst service](windows-time-service/windows-time-service-tech-ref.md)
#### [Funktionsweise von Windows-Zeitdienst](windows-time-service/How-the-Windows-Time-Service-Works.md)
#### [Windows-Zeitdienst: Tools und Einstellungen](windows-time-service/Windows-Time-Service-Tools-and-Settings.md)
