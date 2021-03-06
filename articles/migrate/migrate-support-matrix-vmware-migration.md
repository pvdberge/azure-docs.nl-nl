---
title: Ondersteuning voor VMware-migratie in Azure Migrate
description: Meer informatie over ondersteuning voor de migratie van virtuele VMware-machines in Azure Migrate.
ms.topic: conceptual
ms.date: 06/08/2020
ms.openlocfilehash: 430b491780e10840274f16315b159a8095c11889
ms.sourcegitcommit: f845ca2f4b626ef9db73b88ca71279ac80538559
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/09/2020
ms.locfileid: "89612524"
---
# <a name="support-matrix-for-vmware-migration"></a>Ondersteunings matrix voor VMware-migratie

In dit artikel vindt u een overzicht van de ondersteunings instellingen en beperkingen voor het migreren van virtuele VMware-machines met [Azure migrate: Server migratie](migrate-services-overview.md#azure-migrate-server-migration-tool) . Als u op zoek bent naar informatie over het beoordelen van virtuele VMware-machines voor migratie naar Azure, raadpleegt u de [ondersteunings matrix voor evaluatie](migrate-support-matrix-vmware.md).


## <a name="migration-options"></a>Migratieopties

U kunt virtuele VMware-machines op een aantal manieren migreren:

- **Met behulp van migratie zonder agent**: migreert u de virtuele machines en hoeft u niets te installeren. U implementeert het [Azure migrate-apparaat](migrate-appliance.md) voor migratie zonder agent.
- **Met behulp van migratie op basis**van een agent: Installeer een agent op de virtuele machine voor replicatie. Voor migratie op basis van een agent implementeert u een [replicatie-apparaat](migrate-replication-appliance.md).

Lees [dit artikel](server-migrate-overview.md) als u wilt weten welke methode u wilt gebruiken.

## <a name="migration-limitations"></a>Migratiebeperkingen

- U kunt Maxi maal 10 Vm's tegelijk selecteren voor replicatie. Als u meer machines wilt migreren, repliceert u in groepen van 10.
- Voor VMware-agentloze migratie kunt u Maxi maal 300 replicaties tegelijk uitvoeren.

## <a name="agentless-migration"></a>Migratie zonder agent 

In deze sectie vindt u een overzicht van de vereisten voor migratie zonder agent.

### <a name="vmware-requirements-agentless"></a>VMware-vereisten (zonder agent)

De tabel bevat een overzicht van de vereisten voor VMware-Hyper Visor.

**VMware** | **Details**
--- | ---
**VMware vCenter Server** | Versie 5,5, 6,0, 6,5 of 6,7.
**ESXI-host VMware vSphere** | Versie 5,5, 6,0, 6,5 of 6,7.
**vCenter Server machtigingen** | Migratie zonder agent maakt gebruik van het [migratie toestel](migrate-appliance.md). Het apparaat heeft deze machtigingen nodig in vCenter Server:<br/><br/> - **Data Store. browse**: bladeren door VM-logboek bestanden toestaan om problemen met het maken en verwijderen van moment opnamen op te lossen.<br/><br/> - **Data Store. File Management**: bewerkingen voor lezen/schrijven/verwijderen/naam wijzigen in de Data Store-browser toestaan om problemen met het maken en verwijderen van moment opnamen op te lossen.<br/><br/> - **VirtualMachine.Config. Change tracking**: het inschakelen of uitschakelen van het bijhouden van wijzigingen van VM-schijven toestaan om gewijzigde gegevens blokken tussen moment opnamen op te halen.<br/><br/> - **VirtualMachine.Config. DiskLease**: sta bewerkingen voor de schijf-lease voor een virtuele machine toe om de schijf te lezen met de VMware vSphere Virtual Disk Development Kit (vddk).<br/><br/> - **VirtualMachine. provisioning. DiskAccess**: (met name voor vSphere 6,0 en hoger) toestaan dat een schijf op een VM wordt geopend voor wille keurige Lees toegang op de schijf met behulp van de VdDK.<br/><br/> - **VirtualMachine. provisioning. DiskRandomRead**: het openen van een schijf op een virtuele machine toestaan om de schijf te lezen met behulp van de VdDK.<br/><br/> - **VirtualMachine. provisioning. DiskRandomAccess**: het openen van een schijf op een virtuele machine toestaan om de schijf te lezen met behulp van de VdDK.<br/><br/> - **VirtualMachine. provisioning. GetVmFiles**: Hiermee staat u lees bewerkingen toe voor bestanden die zijn gekoppeld aan een virtuele machine, om de logboeken te downloaden en problemen op te lossen.<br/><br/> - **VirtualMachine. State. \* **: het maken en beheren van VM-moment opnamen voor replicatie toestaan.<br/><br/> - **Virtuele machine. interactie. uitgeschakeld**: de VM mag worden uitgeschakeld tijdens de migratie naar Azure.



### <a name="vm-requirements-agentless"></a>VM-vereisten (zonder agent)

De tabel bevat een overzicht van de migratie vereisten zonder agent voor virtuele VMware-machines.

**Ondersteuning** | **Details**
--- | ---
**Ondersteunde besturingssystemen** | U kunt [Windows](https://support.microsoft.com/help/2721672/microsoft-server-software-support-for-microsoft-azure-virtual-machines) -en [Linux](../virtual-machines/linux/endorsed-distros.md) -besturings systemen migreren die worden ondersteund door Azure.
**Windows-Vm's in azure** | Mogelijk moet u [enkele wijzigingen aanbrengen](prepare-for-migration.md#verify-required-changes-before-migrating) op vm's vóór de migratie. 
**Virtuele Linux-machines in azure** | Voor sommige Vm's zijn mogelijk wijzigingen vereist zodat ze kunnen worden uitgevoerd in Azure.<br/><br/> Voor Linux worden de wijzigingen automatisch door Azure Migrate voor deze besturings systemen aangebracht:<br/> -Red Hat Enterprise Linux 6.5 +, 7.0 +<br/> -CentOS 6.5 +, 7.0 +</br> -SUSE Linux Enterprise Server 12 SP1 +<br/> -Ubuntu 14.04 LTS, 16.04 LTS, 18.04 LTS<br/> -Debian 7, 8. Voor andere besturings systemen voert u de [vereiste wijzigingen](prepare-for-migration.md#verify-required-changes-before-migrating) hand matig uit.
**Linux-opstart** | Als/boot zich op een toegewezen partitie bevindt, moet deze zich op de besturingssysteem schijf bevinden en niet over meerdere schijven worden verspreid.<br/> Als/boot deel uitmaakt van de hoofd partitie (/), moet de partitie '/' zich op de besturingssysteem schijf bevindt en niet over andere schijven beschikken.
**UEFI-opstart** | Vm's met UEFI-opstart bewerkingen worden niet ondersteund voor migratie.
**Schijfgrootte** | 2 TB besturingssysteem schijf; 8 TB voor gegevens schijven.
**Schijf limieten** |  Maxi maal 60 schijven per VM.
**Versleutelde schijven/volumes** | Vm's met versleutelde schijven/volumes worden niet ondersteund voor migratie.
**Gedeeld schijf cluster** | Niet ondersteund.
**Onafhankelijke schijven** | Niet ondersteund.
**RDM/passthrough-schijven** | Als Vm's een RDM-of passthrough-schijf hebben, worden deze schijven niet gerepliceerd naar Azure.
**NFS** | NFS-volumes die zijn gekoppeld als volumes op de Vm's, worden niet gerepliceerd.
**iSCSI-doelen** | Vm's met iSCSI-doelen worden niet ondersteund voor migratie zonder agent.
**Multipath IO** | Niet ondersteund.
**Storage vMotion** | Niet ondersteund. De replicatie wordt niet uitgevoerd als een virtuele machine gebruikmaakt van Storage vMotion.
**Team kaarten** | Niet ondersteund.
**IPv6** | Niet ondersteund.
**Doel schijf** | Vm's kunnen alleen worden gemigreerd naar Managed disks (standaard HDD, standaard SSD, Premium SSD) in Azure.
**Gelijktijdige replicatie** | 300 Vm's per vCenter Server. Als u meer hebt, migreert u deze in batches van 300.


### <a name="appliance-requirements-agentless"></a>Vereisten voor apparaten (zonder agent)

Migratie zonder agent maakt gebruik van het [Azure migrate apparaat](migrate-appliance.md). U kunt het apparaat als een virtuele VMware-machine implementeren met behulp van een eicellen-sjabloon, geïmporteerd in vCenter Server of een [Power shell-script](deploy-appliance-script.md)gebruiken.

- Meer informatie over de [vereisten voor apparaten](migrate-appliance.md#appliance---vmware) voor VMware.
- Meer informatie over Url's die het apparaat nodig heeft voor toegang tot [open bare](migrate-appliance.md#public-cloud-urls) en [overheids](migrate-appliance.md#government-cloud-urls) Clouds.
- In Azure Government moet u het apparaat implementeren [met behulp van het script](deploy-appliance-script-government.md).

### <a name="port-requirements-agentless"></a>Poort vereisten (zonder agent)

**Apparaat** | **Verbinding**
--- | ---
Apparaat | Uitgaande verbindingen op poort 443 voor het uploaden van gerepliceerde gegevens naar Azure en om te communiceren met Azure Migrate services die replicatie en migratie coördineren.
vCenter-server | Binnenkomende verbindingen op poort 443 om het apparaat in staat te stellen de replicatie te organiseren-moment opnamen maken, gegevens kopiëren, moment opnamen van de release
vSphere/ESXI-host | Inkomend op TCP-poort 902 voor het apparaat om gegevens van moment opnamen te repliceren.

## <a name="agent-based-migration"></a>Migratie op basis van een agent 


In deze sectie vindt u een overzicht van de vereisten voor migratie op basis van een agent.


### <a name="vmware-requirements-agent-based"></a>VMware-vereisten (op agent gebaseerd)

Deze tabel geeft een overzicht van de evaluatie-ondersteuning en beperkingen voor VMware Virtualization-servers.

**VMware-vereisten** | **Details**
--- | ---
**VMware vCenter Server** | Versie 5,5, 6,0, 6,5 of 6,7.
**ESXI-host VMware vSphere** | Versie 5,5, 6,0, 6,5 of 6,7.
**vCenter Server machtigingen** | Een alleen-lezen account voor vCenter Server.

### <a name="vm-requirements-agent-based"></a>VM-vereisten (op agent gebaseerd)

De tabel bevat een overzicht van de VMware VM-ondersteuning voor VMware-Vm's die u wilt migreren met behulp van migratie op basis van een agent.

**Ondersteuning** | **Details**
--- | ---
**Machine workload** | Azure Migrate ondersteunt de migratie van elke werk belasting (bijvoorbeeld Active Directory, SQL Server, enzovoort) die wordt uitgevoerd op een ondersteunde computer.
**Besturingssystemen** | Raadpleeg de ondersteuning van het [besturings systeem](../site-recovery/vmware-physical-azure-support-matrix.md#replicated-machines) voor site Recovery voor de meest recente informatie. Azure Migrate biedt dezelfde ondersteuning voor het VM-besturings systeem.
**Linux-bestands systeem/gast opslag** | Raadpleeg de ondersteuning van het Linux- [Bestands systeem](../site-recovery/vmware-physical-azure-support-matrix.md#linux-file-systemsguest-storage) voor site Recovery voor de meest recente informatie. Azure Migrate heeft dezelfde ondersteuning voor het Linux-bestands systeem.
**Netwerk/opslag** | Raadpleeg de vereisten voor het [netwerk](../site-recovery/vmware-physical-azure-support-matrix.md#network) en de [opslag](../site-recovery/vmware-physical-azure-support-matrix.md#storage) voor site Recovery voor de meest recente informatie. Azure Migrate biedt identieke netwerk-en opslag vereisten.
**Azure-vereisten** | Bekijk de vereisten voor het Azure- [netwerk](../site-recovery/vmware-physical-azure-support-matrix.md#azure-vm-network-after-failover), de [opslag](../site-recovery/vmware-physical-azure-support-matrix.md#azure-storage)en de [reken kracht](../site-recovery/vmware-physical-azure-support-matrix.md#azure-compute) voor site Recovery voor de meest recente informatie. Azure Migrate heeft identieke vereisten voor VMware-migratie.
**Mobility-service** | De Mobility Service-agent moet zijn geïnstalleerd op elke virtuele machine die u wilt migreren.
**UEFI-opstart** | Ondersteund.
**UEFI-beveiligd opstarten**         | Niet ondersteund voor migratie.
**Doel schijf** | Vm's kunnen alleen worden gemigreerd naar Managed disks (standaard HDD, standaard SSD, Premium SSD) in Azure.
**Schijfgrootte** | 2 TB besturingssysteem schijf; 8 TB voor gegevens schijven.
**Schijf limieten** |  Maxi maal 63 schijven per VM.
**Versleutelde schijven/volumes** | Vm's met versleutelde schijven/volumes worden niet ondersteund voor migratie.
**Gedeeld schijf cluster** | Niet ondersteund.
**Onafhankelijke schijven** | Ondersteund.
**Passthrough-schijven** | Ondersteund.
**NFS** | NFS-volumes die zijn gekoppeld als volumes op de Vm's, worden niet gerepliceerd.
**iSCSI-doelen** | Ondersteund.
**Multipath IO** | Niet ondersteund.
**Storage vMotion** | Ondersteund
**Team kaarten** | Niet ondersteund.
**IPv6** | Niet ondersteund.




### <a name="appliance-requirements-agent-based"></a>Vereisten voor apparaten (op agent gebaseerd)

Wanneer u het replicatie apparaat instelt met behulp van de eicellen-sjabloon die is opgegeven in de Azure Migrate hub, voert het apparaat Windows Server 2016 uit en voldoet aan de ondersteunings vereisten. Als u het replicatie apparaat hand matig instelt op een fysieke server, moet u ervoor zorgen dat het voldoet aan de vereisten.

- Meer informatie over de [vereisten voor replicatie-apparaten](migrate-replication-appliance.md#appliance-requirements) voor VMware.
- MySQL moet op het apparaat zijn geïnstalleerd. Meer informatie over [installatie opties](migrate-replication-appliance.md#mysql-installation).
- Meer informatie over Url's die het replicatie-apparaat moet openen in [open bare](migrate-replication-appliance.md#url-access) en [overheids](migrate-replication-appliance.md#azure-government-url-access) Clouds.
- Controleer de [poorten](migrate-replication-appliance.md#port-access) waarvoor het replicatie apparaat toegang moet hebben.

### <a name="port-requirements-agent-based"></a>Poort vereisten (op agent gebaseerd)

**Apparaat** | **Verbinding**
--- | ---
VM's | De Mobility-service die wordt uitgevoerd op Vm's communiceert met het on-premises replicatie apparaat (configuratie server) op poort HTTPS 443 inkomend voor replicatie beheer.<br/><br/> Vm's verzenden replicatie gegevens naar de proces server (die wordt uitgevoerd op de computer van de configuratie server) op poort HTTPS 9443-binnenkomend. Deze poort kan worden gewijzigd.
Replicatie apparaat | Het replicatie apparaat organiseert de replicatie met Azure via poort HTTPS 443 uitgaand.
Proces server | De proces server ontvangt replicatie gegevens, optimaliseert en versleutelt deze en verzendt deze naar Azure Storage via poort 443 uitgaand.<br/> Standaard wordt de proces server uitgevoerd op het replicatie apparaat.

## <a name="azure-vm-requirements"></a>Vereisten voor Azure-VM's

Alle on-premises Vm's die naar Azure worden gerepliceerd, met zonder agent of migratie op basis van een agent, moeten voldoen aan de vereisten van de Azure-VM die in deze tabel worden samenvatten. 

**Onderdeel** | **Vereisten** 
--- | --- | ---
Gastbesturingssysteem | Controleert ondersteunde VMware-VM-besturings systemen voor migratie.<br/> U kunt elke werk belasting migreren die wordt uitgevoerd op een ondersteund besturings systeem. 
Architectuur van gast besturingssysteem | 64-bits. 
Grootte van de besturingssysteemschijf | Maxi maal 2.048 GB. 
Aantal besturingssysteemschijven | 1 
Aantal gegevensschijven | 64 of minder. 
Grootte van de gegevens schijf | Maxi maal 8.095 GB
Netwerkadapters | Meerdere adapters worden ondersteund.
Gedeelde VHD | Niet ondersteund. 
FC-schijf | Niet ondersteund. 
BitLocker | Niet ondersteund.<br/><br/> BitLocker moet worden uitgeschakeld voordat u de computer migreert.
VM-naam | Van 1 tot 63 tekens.<br/><br/> Alleen letters, cijfers en afbreekstreepjes.<br/><br/> De naam van de computer moet beginnen en eindigen met een letter of cijfer. 
Verbinding maken na migratie-Windows | Verbinding maken met virtuele Azure-machines na de migratie:<br/><br/> -Schakel voor de migratie RDP in op de on-premises VM.<br/><br/> Zorg dat TCP- en UDP-regels zijn toegevoegd voor het profiel **Openbaar** en dat RDP is toegestaan in **Windows Firewall** > **Toegestane apps** voor alle profielen.<br/><br/> Schakel voor site-naar-site-VPN-toegang RDP in en sta RDP toe in **Windows Firewall**  ->  **toegestane apps en functies** voor **domein-en particuliere** netwerken.<br/><br/> Controleer bovendien of het SAN-beleid van het besturings systeem is ingesteld op **OnlineAll**. [Meer informatie](prepare-for-migration.md).
Verbinding maken na migratie-Linux | Verbinding maken met virtuele Azure-machines na de migratie met SSH:<br/><br/> Controleer voordat u de migratie op de on-premises computer controleert of de Secure shell-service is ingesteld op Start en of de firewall regels een SSH-verbinding toestaan.<br/><br/> Nadat de failover is uitgevoerd op de Azure-VM, moet u binnenkomende verbindingen met de SSH-poort toestaan voor de regels voor de netwerk beveiligings groep op de virtuele machine die is mislukt en voor het Azure-subnet waarmee deze is verbonden.<br/><br/> Voeg bovendien een openbaar IP-adres voor de virtuele machine toe.  


## <a name="next-steps"></a>Volgende stappen

[Selecteer](server-migrate-overview.md) een optie voor VMware-migratie.
