---
title: Wat is Azure Backup?
description: Geeft een overzicht van de Azure Backup-service en hoe deze bijdraagt aan uw strategie voor bedrijfscontinuïteit en herstel na noodgevallen (BCDR).
ms.topic: overview
ms.date: 04/24/2019
ms.custom: mvc
ms.openlocfilehash: 9954c8fa6affca7d2c2b73d7176280587d749476
ms.sourcegitcommit: 419cf179f9597936378ed5098ef77437dbf16295
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/27/2020
ms.locfileid: "89017886"
---
# <a name="what-is-the-azure-backup-service"></a>Wat is de Azure Backup-service?

De Azure Backup-service biedt eenvoudige, beveiligde en kosteneffectieve oplossingen om een back-up te maken van uw gegevens en die te herstellen vanuit Microsoft Azure-cloud.

> [!VIDEO https://www.youtube.com/embed/elODShatt-c]

## <a name="what-can-i-back-up"></a>Waarvan kan ik een back-up maken?

- **On-premises**: Maak back-ups van bestanden, mappen, systeemstatus met behulp van de [Microsoft Azure Recovery Services-agent (MARS)](backup-support-matrix-mars-agent.md). Of gebruik de DPM- of Azure Backup Server-agent (MABS) voor bescherming van on-premises virtuele machines ([Hyper-V](back-up-hyper-v-virtual-machines-mabs.md) en [VMware](backup-azure-backup-server-vmware.md)) en andere [on-premises werkbelastingen](backup-mabs-protection-matrix.md)
- **Virtuele Azure-machines** - [Maak back-ups van volledige virtuele machines op basis van Windows/Linux](backup-azure-vms-introduction.md) (met back-upextensies) of van bestanden, mappen en systeemstatus met behulp van de [MARS-agent](backup-azure-manage-mars.md).
- **Azure Files-shares** - [Maak back-ups van Azure-bestandsshares in een opslagaccount](backup-afs.md)
- **SQL Server op virtuele Azure-machines** -  [Maak back-ups van SQL Server-databases die worden uitgevoerd op virtuele Azure-machines](backup-azure-sql-database.md)
- **SAP HANA-databases op virtuele Azure-machines** - [Maak back-ups van SAP HANA-databases die worden uitgevoerd op virtuele Azure-machines](backup-azure-sap-hana-database.md)

![Overzicht van Azure Backup](./media/backup-overview/azure-backup-overview.png)

## <a name="why-use-azure-backup"></a>Waarom Azure Backup gebruiken?

Azure Backup biedt deze belangrijke voordelen:

- **Geen on-premises back-up meer nodig**: Azure Backup biedt een eenvoudige oplossing voor het maken van back-ups van uw on-premises resources naar de cloud. Back-ups op korte en lange termijn zonder de noodzaak om complexe on-premises back-upoplossingen te implementeren.
- **Back-ups van Azure IaaS-VM's**: Azure Backup biedt onafhankelijke en geïsoleerde back-ups om te voorkomen dat oorspronkelijke gegevens per ongeluk worden vernietigd. Back-ups worden opgeslagen in een Recovery Services-kluis met ingebouwd beheer van herstelpunten. Configuratie en schaalbaarheid zijn eenvoudig, back-ups zijn geoptimaliseerd en kunt u eenvoudig naar behoefte herstellen.
- **Gemakkelijk schalen**: Azure Backup gebruikt de onderliggende kracht en onbeperkte schaal van de Azure-cloud voor hoge beschikbaarheid, zonder overhead voor onderhoud of bewaking.
- **Onbeperkte gegevensoverdracht**: Azure Backup stelt geen beperking aan de hoeveelheid binnenkomende of uitgaande gegeven die u overbrengt en er worden geen kosten berekend voor de gegevens die worden overgebracht.
  - Uitgaande gegevens zijn gegevens die tijdens een herstelbewerking worden overgebracht uit een Recovery Services-kluis.
  - Als u met de service Azure Import/Export een offline eerste back-up uitvoert voor het importeren van grote hoeveelheden gegevens, zijn er kosten verbonden aan inkomende gegevens.  [Meer informatie](backup-azure-backup-import-export.md).
- **Gegevens veilig houden**: Azure Backup biedt oplossingen voor het beveiligen van gegevens [in-transit](backup-azure-security-feature.md) en [at-rest](backup-azure-security-feature-cloud.md).
- **Gecentraliseerde bewaking en beheer**: Azure Backup biedt [ingebouwde mogelijkheden voor bewaking en waarschuwingen](backup-azure-monitoring-built-in-monitor.md) in een Recovery Services-kluis. Deze mogelijkheden zijn beschikbaar zonder enige extra beheerinfrastructuur. U kunt tevens de schaal van uw bewaking en rapportage vergroten door [Azure Monitor](backup-azure-monitoring-use-azuremonitor.md) te gebruiken.
- **App-consistente back-ups**: Een app-consistente back-up betekent dat een herstelpunt alle vereiste gegevens heeft om de back-up te kunnen herstellen. Azure Backup biedt toepassingsconsistente back-ups, om ervoor te zorgen dat er geen aanvullende correcties nodig zijn om de gegevens te herstellen. Herstellen van toepassingsconsistente gegevens verkort de hersteltijd, zodat u snel weer normaal aan het werk kunt.
- **Korte- en langetermijngegevens bewaren**: U kunt [Recovery Services-kluizen](backup-azure-recovery-services-vault-overview.md) gebruiken voor het bewaren van gegevens voor de korte en de lange termijn.
- **Automatisch opslagbeheer**: voor hybride omgevingen is vaak heterogene opslag vereist, soms on-premises en soms in de cloud. Met Azure Backup zijn er geen kosten voor het gebruik van on-premises opslagapparaten. De back-upopslag wordt automatisch door Azure Backup toegewezen en beheerd en u betaalt naar gebruik. U betaalt dus alleen voor de opslag die u gebruikt. [Lees meer](https://azure.microsoft.com/pricing/details/backup) over prijzen.
- **Meerdere opslagopties**: Azure Backup biedt twee typen replicatie om uw opslag/gegevens maximaal beschikbaar te houden.
  - Met [lokaal redundante opslag LRS](../storage/common/storage-redundancy.md) worden uw gegevens drie keer gerepliceerd (er worden drie kopieën gemaakt van uw gegevens) in een opslagschaaleenheid in een datacenter. Alle kopieën van de gegevens komen binnen dezelfde regio voor. LRS is een goedkope optie voor het beschermen van uw gegevens tegen lokale hardwarefouten.
  - [Geografisch redundante opslag (GRS)](../storage/common/storage-redundancy.md) is de standaardinstelling en is de replicatieoptie die wordt aanbevolen. Met GRS worden uw gegevens gerepliceerd naar een secundaire regio (honderden kilometers verwijderd van de primaire locatie van de brongegevens). GRS is duurder dan LRS, maar biedt een hoger duurzaamheidsniveau voor uw gegevens, zelfs in geval van een regionale onderbreking.

## <a name="next-steps"></a>Volgende stappen

- [Bekijk](backup-architecture.md) de architectuur en componenten voor verschillende back-upscenario's.
- [Controleer](backup-support-matrix.md) ondersteuningsvereisten en -beperkingen voor het maken van back-ups en voor [back-ups van virtuele Azure-machines](backup-support-matrix-iaas.md).
