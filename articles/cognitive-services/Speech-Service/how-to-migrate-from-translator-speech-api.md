---
title: Migreren van de Translator Speech-API naar de speech-service
titleSuffix: Azure Cognitive Services
description: Meer informatie over het migreren van uw toepassingen van de Translator Speech-API naar de speech-service.
services: cognitive-services
author: aahill
manager: nitinme
ms.service: cognitive-services
ms.subservice: speech-service
ms.topic: conceptual
ms.date: 01/21/2020
ms.author: aahi
ms.openlocfilehash: 305242e13dab23b6a003c5d864073372a052601a
ms.sourcegitcommit: bb0afd0df5563cc53f76a642fd8fc709e366568b
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 05/19/2020
ms.locfileid: "83593168"
---
# <a name="migrate-from-the-translator-speech-api-to-the-speech-service"></a>Migreren van de Translator Speech-API naar de speech-service

Gebruik dit artikel om uw toepassingen van de micro soft-Translator Speech-API naar de [Speech-Service](index.yml)te migreren. In deze hand leiding vindt u een overzicht van de verschillen tussen de Translator Speech-API-en spraak service, en suggesties voor strategieën voor het migreren van uw toepassingen.

> [!NOTE]
> Uw Translator Speech-API-abonnements sleutel wordt niet geaccepteerd door de spraak service. U moet een nieuw abonnement voor de spraak service maken.

## <a name="comparison-of-features"></a>Vergelijking van functies

| Functie                                           | Translator Speech-API                                  | Speech Service | Details                                                                                                                                                                                                                                                                            |
|---------------------------------------------------|-----------------------------------------------------------------|------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Vertaling naar tekst                               | :heavy_check_mark:                                              | :heavy_check_mark:                 |                                                                                                                                                                                                                                                                                    |
| Vertalen naar spraak                             | :heavy_check_mark:                                              | :heavy_check_mark:                 |                                                                                                                                                                                                                                                                                    |
| Globaal eind punt                                   | :heavy_check_mark:                                              | : heavy_minus_sign:                 | De speech-service biedt geen globaal eind punt. Met een globaal eind punt kan verkeer automatisch worden doorgestuurd naar het dichtstbijzijnde regionale eind punt, waardoor de latentie in uw toepassing afneemt.                                                    |
| Regionale eind punten                                | : heavy_minus_sign:                                              | :heavy_check_mark:                 |                                                                                                                                                                                                                                                                                    |
| Tijds limiet voor verbinding                             | 90 minuten                                               | Onbeperkt met de SDK. 10 minuten met een websockets-verbinding.                                                                                                                                                                                                                                                                                   |
| Verificatie sleutel in header                                | :heavy_check_mark:                                              | :heavy_check_mark:                 |                                                                                                                                                                                                                                                                                    |
| Meerdere talen vertaald in één aanvraag | : heavy_minus_sign:                                              | :heavy_check_mark:                 |                                                                                                                                                                                                                                                                                    |
| Sdk's beschikbaar                                    | : heavy_minus_sign:                                              | :heavy_check_mark:                 | Raadpleeg de [documentatie](index.yml) van de speech-service voor beschik bare sdk's.                                                                                                                                                    |
| Websockets verbindingen                            | :heavy_check_mark:                                              | :heavy_check_mark:                 |                                                                                                                                                                                                                                                                                    |
| API voor talen                                     | :heavy_check_mark:                                              | : heavy_minus_sign:                 | De spraak service ondersteunt hetzelfde bereik van talen als beschreven in het [naslag artikel over de Vertaal talen](../translator-speech/languages-reference.md) . |
| Filter en markering voor scheld woorden                       | : heavy_minus_sign:                                              | :heavy_check_mark:                 |                                                                                                                                                                                                                                                                                    |
| . WAV/PCM als invoer                                 | :heavy_check_mark:                                              | :heavy_check_mark:                 |                                                                                                                                                                                                                                                                                    |
| Andere bestands typen als invoer                         | : heavy_minus_sign:                                              | : heavy_minus_sign:                 |                                                                                                                                                                                                                                                                                    |
| Gedeeltelijke resultaten                                   | :heavy_check_mark:                                              | :heavy_check_mark:                 |                                                                                                                                                                                                                                                                                    |
| Timing gegevens                                       | :heavy_check_mark:                                              | : heavy_minus_sign:                 |                                                                                                                                                                 |
| Correlatie-id                                    | :heavy_check_mark:                                              | : heavy_minus_sign:                 |                                                                                                                                                                                                                                                                                    |
| Aangepaste spraak modellen                              | : heavy_minus_sign:                                              | :heavy_check_mark:                 | De speech-service biedt aangepaste spraak modellen waarmee u spraak herkenning kunt aanpassen aan de unieke woorden lijst van uw organisatie.                                                                                                                                           |
| Aangepaste Vertaal modellen                         | : heavy_minus_sign:                                              | :heavy_check_mark:                 | Als u zich abonneert op de micro soft Text Translator-API, kunt u [aangepaste Translator](https://www.microsoft.com/translator/business/customization/) gebruiken om uw eigen gegevens te gebruiken voor nauw keurige vertalingen.                                                 |

## <a name="migration-strategies"></a>Migratiestrategieën

Als u of uw organisatie toepassingen in ontwikkeling of productie heeft die gebruikmaken van de Translator Speech-API, moet u deze bijwerken om de spraak service te gebruiken. Raadpleeg de documentatie van de [Speech-Service](index.yml) voor beschik bare sdk's, code voorbeelden en zelf studies. Houd rekening met het volgende wanneer u migreert:

* De speech-service biedt geen globaal eind punt. Bepaal of uw toepassing efficiënt werkt wanneer er één regionaal eind punt wordt gebruikt voor al het verkeer. Als dat niet het geval is, gebruikt u geolocatie om het meest efficiënte eind punt te bepalen.

* Als uw toepassing gebruik maakt van langdurige verbindingen en de beschik bare Sdk's niet kan gebruiken, kunt u een websockets-verbinding gebruiken. De time-outlimiet van 10 minuten beheren door opnieuw verbinding te maken met de juiste tijden.

* Als uw toepassing gebruikmaakt van de Translator-service en Translator Speech-API om aangepaste Vertaal modellen in te scha kelen, kunt u categorie-Id's rechtstreeks toevoegen met behulp van de spraak service.

* In tegens telling tot de Translator Speech-API, kan de speech-service vertalingen in meerdere talen in één aanvraag volt ooien.

## <a name="next-steps"></a>Volgende stappen

* [De spraak service gratis uitproberen](get-started.md)
* [Quick Start: spraak herkennen in een UWP-app met behulp van de Speech SDK](~/articles/cognitive-services/Speech-Service/quickstarts/speech-to-text-from-microphone.md?pivots=programming-language-csharp&tabs=uwp)

## <a name="see-also"></a>Zie ook

* [Wat is de speech-service](overview.md)
* [Documentatie voor speech-service en spraak SDK](https://docs.microsoft.com/azure/cognitive-services/speech-service/speech-devices-sdk-qsg)
