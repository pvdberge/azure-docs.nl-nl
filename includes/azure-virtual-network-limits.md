---
title: bestand opnemen
description: bestand opnemen
services: networking
author: anavinahar
ms.service: networking
ms.topic: include
ms.date: 01/14/2020
ms.author: anavin
ms.custom: include file
ms.openlocfilehash: b963cc459094e823499e962736550dcea2345ba2
ms.sourcegitcommit: b33c9ad17598d7e4d66fe11d511daa78b4b8b330
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/25/2020
ms.locfileid: "88854054"
---
### <a name="networking-limits---azure-resource-manager"></a><a name="azure-resource-manager-virtual-networking-limits"></a>Netwerklimieten - Azure Resource Manager
De volgende beperkingen gelden alleen voor netwerkresources die worden beheerd via **Azure Resource Manager**. De beperkingen gelden per regio en per abonnement. Meer informatie over het [bekijken van uw huidige resourcegebruik op basis van uw abonnementslimieten](../articles/networking/check-usage-against-limits.md).

> [!NOTE]
> We hebben alle standaardlimieten onlangs verhoogd tot hun maximumlimieten. Als er geen kolom Maximumlimiet bestaat, heeft de resource geen aanpasbare limieten. Als deze limieten in het verleden door de ondersteuning zijn verhoogd en u geen bijgewerkte limieten ziet staan in de volgende tabellen, moet u [een gratis online klantondersteuningsaanvraag openen](../articles/azure-resource-manager/templates/error-resource-quota.md)

| Resource | Limiet | 
| --- | --- |
| Virtuele netwerken |1000 |
| Subnetten per virtueel netwerk |3000 |
| Peering van virtuele netwerken per virtueel netwerk |500 |
| [Virtuele netwerkgateways (VPN-gateways) per virtueel netwerk](../articles/vpn-gateway/vpn-gateway-about-vpngateways.md#gwsku) |1 |
| [Virtuele netwerkgateways (ExpressRoute-gateways) per virtueel netwerk](../articles/expressroute/expressroute-about-virtual-network-gateways.md#gwsku) |1 |
| DNS-servers per virtueel netwerk |20 |
| Privé-IP-adressen per virtueel netwerk |65.536 |
| Privé-IP-adressen per netwerkinterface |256 |
| Privé-IP-adressen per virtuele machine |256 |
| Openbare IP-adressen per netwerkinterface |256 |
| Openbare IP-adressen per virtuele machine |256 |
| [Gelijktijdige TCP- of UDP-stromen per NIC van een virtuele machine of rolinstantie](../articles/virtual-network/virtual-machine-network-throughput.md#flow-limits-and-recommendations) |500.000 |
| Netwerkinterfacekaarten |65.536 |
| Netwerkbeveiligingsgroepen |5\.000 |
| NSG-regels per NSG |1000 |
| Opgegeven IP-adressen en-bereiken voor bron of doel in een beveiligingsgroep |4000 |
| Toepassingsbeveiligingsgroepen |3000 |
| Toepassingsbeveiligingsgroepen per IP-configuratie, per NIC |20 |
| IP-configuraties per toepassingsbeveiligingsgroep |4000 |
| Toepassingsbeveiligingsgroepen die kunnen worden opgegeven in alle beveiligingsregels van een netwerkbeveiligingsgroep |100 |
| Door de gebruiker gedefinieerde routetabellen |200 |
| Door de gebruiker gedefinieerde routes per routetabel |400 |
| Punt-naar-site-basiscertificaten per Azure VPN Gateway |20 |
| Aftakkingen van virtueel netwerk |100 |
| Netwerkinterface-TAP-configuraties per Virtual Network TAP |100 |

#### <a name="public-ip-address-limits"></a><a name="publicip-address"></a>Limieten van openbaar IP-adres
| Resource | Standaardlimiet | Maximumaantal |
| --- | --- | --- |
| Openbare IP-adressen<sup>1</sup> | 10 voor Basic. | Neem contact op met ondersteuning. |
| Statische openbare IP-adressen<sup>1</sup> | 10 voor Basic. | Neem contact op met ondersteuning. |
| Standaard openbare IP-adressen<sup>1</sup> | 10 | Neem contact op met ondersteuning. |
| Voorvoegsels voor openbare IP | beperkt door het aantal standaard openbare IP-adressen in een abonnement | Neem contact op met ondersteuning. |
| Voorvoegsellengte van het openbare IP-adres | /28 | Neem contact op met ondersteuning. |

<sup>1</sup>Standaardlimieten voor openbare IP-adressen zijn afhankelijk van het type aanbieding, zoals gratis proefversies, betalen per gebruik of CSP. De standaardinstelling voor Enterprise Agreement-abonnementen is bijvoorbeeld 1000.

#### <a name="load-balancer-limits"></a><a name="load-balancer"></a>Load balancer-limieten
De volgende beperkingen gelden alleen voor netwerkresources die worden beheerd via Azure Resource Manager. De beperkingen gelden per regio en per abonnement. Meer informatie over het [bekijken van uw huidige resourcegebruik op basis van uw abonnementslimieten](../articles/networking/check-usage-against-limits.md).

**Standard Load Balancer**

| Resource                                | Limiet         |
|-----------------------------------------|-------------------------------|
| Load balancers                          | 1000                         |
| Regels per resource                      | 1500                         |
| Regels per NIC (voor alle IP-adressen op een NIC) | 300                           |
| Frontend-IP-configuraties              | 600                           |
| Grootte van back-end-pool                       | 1000 IP-configuraties, één virtueel netwerk |
| Backend-resources per load balancer <sup>1<sup> | 150                   |
| Poorten met een hoge beschikbaarheid                 | 1 per interne frontend       |
| Uitgaande regels per load balancer        | 600                           |
| [Niet-actieve TCP-tijd](https://docs.microsoft.com/azure/load-balancer/load-balancer-tcp-idle-timeout#tcp-idle-timeout) | 4 minuten/30 minuten          |

<sup>1</sup>De limiet is maximaal 150 resources, bestaande uit een willekeurige combinatie van zelfstandige VM-resources, resources voor beschikbaarheidssets en plaatsingsgroepen op VM-schaal.

**Basic Load Balancer**

| Resource                                | Limiet        |
|-----------------------------------------|------------------------------|
| Load balancers                          | 1000                        |
| Regels per resource                      | 250                          |
| Regels per NIC (voor alle IP-adressen op een NIC) | 300                          |
| Frontend-IP-configuraties              | 200                          |
| Grootte van back-end-pool                       | 300 IP-configuraties, één beschikbaarheidsset |
| Beschikbaarheidssets per load balancer     | 150                          |

<a name="virtual-networking-limits-classic"></a>De volgende beperkingen gelden alleen voor netwerkresources die worden beheerd via het **klassieke** implementatiemodel voor elk abonnement. Meer informatie over het [bekijken van uw huidige resourcegebruik op basis van uw abonnementslimieten](../articles/networking/check-usage-against-limits.md).

| Resource | Standaardlimiet | Maximumaantal |
| --- | --- | --- |
| Virtuele netwerken |100 |100 |
| Lokale netwerksites |20 |50 |
| DNS-servers per virtueel netwerk |20 |20 |
| Privé-IP-adressen per virtueel netwerk |4096 |4096 |
| Gelijktijdige TCP-of UDP-stromen per NIC van een virtuele machine of rolinstantie |500.000 tot 1.000.000 voor twee of meer NIC's. |500.000 tot 1.000.000 voor twee of meer NIC's. |
| Netwerkbeveiligingsgroepen (NSG's) |200 |200 |
| NSG-regels per NSG |200 |1000 |
| Door de gebruiker gedefinieerde routetabellen |200 |200 |
| Door de gebruiker gedefinieerde routes per routetabel |400 |400 |
| Openbare IP-adressen (dynamisch) |500 |500 |
| Gereserveerde openbare IP-adressen |500 |500 |
| Openbare VIP per implementatie |5 |Contact opnemen met ondersteuning |
| Privé-VIP (interne taakverdeling) per implementatie |1 |1 |
| Toegangsbeheerlijsten voor eindpunt (ACL's) |50 |50 |