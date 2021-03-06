---
title: Overwegingen bij netwerken-specifieke HSM voor Azure | Microsoft Docs
description: Overzicht van netwerk overwegingen die van toepassing zijn op specifieke HSM-implementaties van Azure
services: dedicated-hsm
author: msmbaldwin
manager: rkarlin
ms.custom: mvc, seodec18
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 12/06/2018
ms.author: mbaldwin
ms.openlocfilehash: 06cd02177d7d5c478f3378eb05517f1a37297e92
ms.sourcegitcommit: 877491bd46921c11dd478bd25fc718ceee2dcc08
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/02/2020
ms.locfileid: "84300729"
---
# <a name="azure-dedicated-hsm-networking"></a>Speciaal voor Azure toegewezen HSM-netwerken

Voor de toegewezen HSM van Azure is een zeer veilige netwerk omgeving vereist. Dit is waar, ongeacht of het vanuit de Azure-Cloud wordt weer gegeven in de IT-omgeving van de klant (on-premises), met gedistribueerde toepassingen of voor scenario's met hoge Beschik baarheid. Azure-netwerken bieden dit en er zijn vier verschillende gebieden die moeten worden opgelost.

- HSM-apparaten maken binnen uw Virtual Network (VNet) in azure
- On-premises verbinding maken met Cloud bronnen voor de configuratie en het beheer van HSM-apparaten
- Virtuele netwerken maken en verbinden voor het onderling verbinden van toepassings bronnen en HSM-apparaten
- Virtuele netwerken met elkaar verbinden in verschillende regio's voor intersite-communicatie en daarnaast scenario's met hoge Beschik baarheid inschakelen

## <a name="virtual-network-for-your-dedicated-hsms"></a>Virtueel netwerk voor uw toegewezen Hsm's

Toegewijde Hsm's zijn geïntegreerd in een Virtual Network en in het eigen privé netwerk van de klant in azure geplaatst. Hiermee hebt u toegang tot de apparaten van virtuele machines of reken bronnen in het virtuele netwerk.  
Zie voor meer informatie over het integreren van Azure-Services in het virtuele netwerk en de mogelijkheden die het biedt, [Virtual Network voor Azure Services](../virtual-network/virtual-network-for-azure-services.md) -documentatie.

### <a name="virtual-networks"></a>Virtuele netwerken

Voordat u een toegewezen HSM-apparaat inricht, moet u eerst een Virtual Network maken in azure of gebruiken dat al aanwezig is in het abonnement van de klant. Het virtuele netwerk definieert de beveiligings verbinding voor het toegewezen HSM-apparaat. Zie de [documentatie van virtueel netwerk](../virtual-network/virtual-networks-overview.md)voor meer informatie over het maken van virtuele netwerken.

### <a name="subnets"></a>Subnetten

Met subnetten wordt het virtuele netwerk gesegmenteerd tot afzonderlijke adres ruimten die kunnen worden gebruikt door de Azure-resources die u in deze ruimte plaatst. Toegewezen Hsm's worden geïmplementeerd in een subnet in het virtuele netwerk. Elk toegewezen HSM-apparaat dat in het subnet van de klant wordt geïmplementeerd, ontvangt een privé IP-adres van dit subnet. Het subnet waarin het HSM-apparaat wordt geïmplementeerd, moet expliciet worden gedelegeerd naar de service: micro soft. HardwareSecurityModules/dedicatedHSMs. Hiermee worden bepaalde machtigingen verleend aan de HSM-service voor implementatie in het subnet. Delegering naar toegewezen Hsm's legt bepaalde beleids beperkingen op het subnet voor. Netwerk beveiligings groepen (Nsg's) en door de gebruiker gedefinieerde routes (Udr's) worden momenteel niet ondersteund op gedelegeerde subnetten. Als gevolg hiervan kan het eenmaal worden gebruikt voor het implementeren van HSM-bronnen zodra een subnet is gedelegeerd naar een toegewezen Hsm's. De implementatie van andere resources van de klant in het subnet zal mislukken.


### <a name="expressroute-gateway"></a>ExpressRoute-gateway

Een vereiste van de huidige architectuur is het configureren van een er-gateway in het subnet klanten waar een HSM-apparaat moet worden geplaatst om de integratie van het HSM-apparaat in te scha kelen in Azure. Deze er-gateway kan niet worden gebruikt voor het verbinden van on-premises locaties met de HSM-apparaten van klanten in Azure.

## <a name="connecting-your-on-premises-it-to-azure"></a>Uw on-premises verbinding maken met Azure

Bij het maken van cloud resources is het een typische vereiste voor een particuliere verbinding met on-premises IT-resources. In het geval van een toegewezen HSM is dit voornamelijk van toepassing op de HSM-client software voor het configureren van de HSM-apparaten en ook voor activiteiten zoals back-ups en het ophalen van logboeken van Hsm's voor analyse. Een belang rijke beslissings punt is hier de aard van de verbinding.  De meest flexibele optie is site-naar-site-VPN, omdat er waarschijnlijk meerdere on-premises resources zijn die beveiligde communicatie met resources (inclusief Hsm's) vereisen in de Azure-Cloud. Hiervoor moet een klant organisatie een VPN-apparaat hebben om de verbinding te vergemakkelijken. Een punt-naar-site-VPN-verbinding kan worden gebruikt als er slechts één eind punt on-premises is, zoals één beheer werkstation.
Zie [VPN gateway plannings opties](../vpn-gateway/vpn-gateway-about-vpngateways.md?toc=%2fazure%2fvirtual-network%2ftoc.json#planningtable)voor meer informatie over connectiviteits opties.

> [!NOTE]
> ExpressRoute is op dit moment geen optie voor verbinding met on-premises resources. Ook moet worden opgemerkt dat de ExpressRoute-gateway die wordt gebruikt zoals hierboven wordt beschreven, niet is voor verbindingen met een on-premises infra structuur.

### <a name="point-to-site-vpn"></a>Punt-naar-site-VPN

Een punt-naar-site virtueel particulier netwerk is de eenvoudigste vorm van een veilige verbinding met één eind punt on-premises. Dit kan relevant zijn als u slechts één beheer werkstation voor op Azure gebaseerde specifieke Hsm's wilt hebben.

### <a name="site-to-site-vpn"></a>Site-naar-site-VPN

Met een site-naar-site virtueel particulier netwerk kunt u beveiligde communicatie tussen op Azure gebaseerde specifieke Hsm's en uw on-premises IT-service. Een reden hiervoor is dat er een back-upfaciliteit is voor de on-premises HSM en dat er een verbinding nodig is tussen de twee voor het uitvoeren van de back-up.

## <a name="connecting-virtual-networks"></a>Verbinding maken met virtuele netwerken

Een typische implementatie architectuur voor een toegewezen HSM begint met één virtueel netwerk en een overeenkomend subnet waarin de HSM-apparaten zijn gemaakt en ingericht. Binnen dezelfde regio zijn er ook extra virtuele netwerken en subnetten voor toepassings onderdelen die gebruikmaken van de toegewezen HSM. Als u communicatie over deze netwerken wilt inschakelen, gebruiken we Virtual Network-peering.

### <a name="virtual-network-peering"></a>Peering op virtueel netwerk

Wanneer er meerdere virtuele netwerken binnen een regio zijn die toegang moeten hebben tot de resources van elkaar, kan Virtual Network peering worden gebruikt voor het maken van beveiligde communicatie kanalen.  Peering van virtuele netwerken biedt niet alleen beveiligde communicatie, maar zorgt ook voor een verbinding met lage latentie en hoge band breedte tussen de resources in Azure.

![netwerk peering](media/networking/peering.png)

## <a name="connecting-across-azure-regions"></a>Verbinding maken tussen Azure-regio's

De HSM-apparaten kunnen via software bibliotheken het verkeer omleiden naar een alternatieve HSM. Het omleiden van verkeer is handig als apparaten mislukken of toegang tot een apparaat verloren zijn gegaan. Scenario's voor storingen op regionaal niveau kunnen worden verholpen door Hsm's in andere regio's te implementeren en communicatie tussen virtuele netwerken tussen regio's in te scha kelen.

### <a name="cross-region-ha-using-vpn-gateway"></a>Kruis regio HA met behulp van VPN-gateway

Voor wereld wijd gedistribueerde toepassingen of voor regionale failover-scenario's met hoge Beschik baarheid is het vereist om virtuele netwerken te verbinden tussen regio's. Met de speciale HSM van Azure kunt u hoge Beschik baarheid bereiken met behulp van een VPN Gateway dat een beveiligde tunnel biedt tussen de twee virtuele netwerken. Zie het artikel [Wat is VPN gateway?](../vpn-gateway/design.md#V2V) voor meer informatie over Vnet-naar-vnet-verbindingen met behulp van VPN gateway.

> [!NOTE]
> Globale Vnet-peering is niet beschikbaar in scenario's voor connectiviteit tussen regio's met specifieke Hsm's op dit moment en VPN-gateway moet in plaats daarvan worden gebruikt. 

![Global-vnet](media/networking/global-vnet.png)

## <a name="next-steps"></a>Volgende stappen

- [Veelgestelde vragen](faq.md)
- [Ondersteuning](supportability.md)
- [Hoge beschikbaarheid](high-availability.md)
- [Fysieke beveiliging](physical-security.md)
- [Controle](monitoring.md)
- [Implementatie architectuur](deployment-architecture.md)