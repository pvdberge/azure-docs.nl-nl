---
title: Kiezen tussen ingerichte door Voer en serverloos op Azure Cosmos DB
description: Meer informatie over het kiezen van een ingerichte door Voer en serverloze voor uw werk belasting.
author: ThomasWeiss
ms.author: thweiss
ms.service: cosmos-db
ms.topic: conceptual
ms.date: 08/19/2020
ms.openlocfilehash: 0adb346a693beaa905438cfdc1249c1646c28811
ms.sourcegitcommit: d661149f8db075800242bef070ea30f82448981e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/19/2020
ms.locfileid: "88608779"
---
# <a name="how-to-choose-between-provisioned-throughput-and-serverless"></a>Kiezen tussen ingerichte door Voer en serverloos

Azure Cosmos DB is beschikbaar in twee verschillende capaciteits modi: [ingerichte door Voer](set-throughput.md) en [serverloos](serverless.md). U kunt exact dezelfde database bewerkingen uitvoeren in beide modi, maar de manier waarop deze bewerkingen worden gefactureerd, is een wortel verschil. In de volgende video worden de belangrijkste verschillen tussen deze modi beschreven en hoe deze worden aangepast aan verschillende soorten workloads:

> [!VIDEO https://www.youtube.com/embed/CgYQo6uHyt0]

> [!NOTE]
> Serverloze wordt momenteel alleen ondersteund door de Azure Cosmos DB core-API (SQL).

## <a name="detailed-comparison"></a>Gedetailleerde vergelijking

| Criteria | Ingerichte doorvoer | Serverloos |
| --- | --- | --- |
| Status | Algemeen beschikbaar | In preview |
| Geschikt voor | Essentiële werk belastingen waarvoor voorspel bare prestaties zijn vereist | Kleine tot middel grote niet-kritieke workloads met licht verkeer |
| Hoe het werkt | Voor elk van uw containers voorziet u een bepaalde hoeveelheid door Voer, uitgedrukt in [aanvraag eenheden](request-units.md) per seconde. Elke seconde is deze hoeveelheid aanvraag eenheden beschikbaar voor uw database bewerkingen. Ingerichte door Voer kan hand matig worden bijgewerkt of automatisch worden aangepast met automatische [schaling](provision-throughput-autoscale.md). | U voert uw database bewerkingen uit op uw containers zonder dat u enige capaciteit hoeft in te richten. |
| Beperkingen per account | Maximum aantal Azure-regio's: onbeperkt | Maximum aantal Azure-regio's: 1 |
| Beperkingen per container | Maximale door Voer: onbeperkt<br>Maximale opslag: onbeperkt | Maximale door Voer: 5.000 RU/s<br>Maximale opslag: 50 GB |
| Prestaties | 99,99% tot 99,999% Beschik baarheid gedekt door SLA<br>< 10 MS latentie voor punt-en schrijf bewerkingen onder SLA<br>99,99% gegarandeerde door Voer gedekt door SLA | 99,9% tot 99,99% Beschik baarheid gedekt door SLA<br>< 10 MS-latentie voor punt-en < 30 MS voor schrijf bewerkingen die worden gedekt door SLO<br>95% burstie gedekt door SLO |
| Factureringsmodel | Facturering geschiedt per uur voor de ingerichte RU/s, ongeacht het aantal verbruikte i/o's. | Facturering geschiedt per uur voor het bedrag van RUs dat door uw database bewerkingen wordt gebruikt. |

> [!IMPORTANT]
> Sommige van de beperkingen voor serverloze worden mogelijk gesoepeld of verwijderd wanneer de server niet algemeen beschikbaar is en **uw feedback** helpt ons te beslissen. Neem contact op met uw ervaring en vertel ons meer over uw serverloos: [azurecosmosdbserverless@service.microsoft.com](mailto:azurecosmosdbserverless@service.microsoft.com) .

## <a name="burstability-and-expected-consumption"></a>Burstie en verwacht verbruik

In sommige gevallen is het mogelijk niet duidelijk of ingerichte door Voer of serverloos moet worden gekozen voor een bepaalde werk belasting. Om u te helpen bij deze beslissing, kunt u het volgende schatten:

- De vereisten voor de **burstie** van uw werk belasting, dat is de maximale hoeveelheid RUs die u in één seconde moet gebruiken
- Uw totale **verwachte verbruik**, dat wil zeggen wat het totale aantal RUs is dat u gedurende een maand kunt gebruiken (dit kan worden geschat met behulp van de tabel die [hier](plan-manage-costs.md#estimating-serverless-costs)wordt weer gegeven).

Als uw werk belasting vereist dat er meer dan 5.000 RU per seconde is, moet de ingerichte door voer worden gekozen, omdat serverloze containers de bovenstaande limiet niet mogen overschrijden. Als dat niet het geval is, kunt u de kosten van beide modi vergelijken op basis van het verwachte verbruik.

**Voor beeld 1**: een werk belasting gaat naar maxi maal 10.000 ru/s, en verbruikt een totaal van 20.000.000 RUs voor een maand.

- Alleen de ingerichte doorvoer modus kan een door Voer van 10.000 RU/s leveren.

**Voor beeld 2**: een werk belasting wordt naar verwachting van maxi maal 500 ru/s, en het totaal van 20.000.000 RUs voor een maand verbruikt.

- In de ingerichte doorvoer modus, zou u een container met 500 RU/s inrichten voor een maandelijkse prijs van: $0,008 * 5 * 730 = **$29,20**
- In de serverloze modus betaalt u voor het verbruikte RUs: $0,25 * 20 = **$5,00**

**Voor beeld 3**: een werk belasting gaat naar maxi maal 500 ru/s, en verbruikt een totaal van 250.000.000 RUs voor een maand.

- In de ingerichte doorvoer modus, zou u een container met 500 RU/s inrichten voor een maandelijkse prijs van: $0,008 * 5 * 730 = **$29,20**
- In de serverloze modus betaalt u voor het verbruikte RUs: $0,25 * 250 = **$62,50**

(deze voor beelden zijn niet administratief voor de opslag kosten, wat gelijk is aan de twee modi)

> [!NOTE]
> De kosten die in het vorige voor beeld worden weer gegeven, zijn alleen bedoeld voor demonstratie doeleinden. Zie de [pagina met prijzen](https://azure.microsoft.com/pricing/details/cosmos-db/) voor de meest recente prijs informatie.

## <a name="next-steps"></a>Volgende stappen

- Meer informatie over het [inrichten van de door Voer op Azure Cosmos DB](set-throughput.md)
- Meer informatie over [Azure Cosmos DB serverloos](serverless.md)
- Vertrouwd raken met het concept van [aanvraag eenheden](request-units.md)
