---
title: Upgraden naar v3.0 van de Computer Vision-API
titleSuffix: Azure Cognitive Services
description: Lees hoe u een upgrade uitvoert naar Computer Vision v3.0 Read API vanuit v2.0/v2.1.
services: cognitive-services
author: PatrickFarley
manager: nitinme
ms.service: cognitive-services
ms.subservice: computer-vision
ms.topic: sample
ms.date: 08/11/2020
ms.author: pafarley
ROBOTS: NOINDEX
ms.openlocfilehash: 6e695fcfacac19ca82273d84d049bdb2afe14b54
ms.sourcegitcommit: 4913da04fd0f3cf7710ec08d0c1867b62c2effe7
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/14/2020
ms.locfileid: "88214180"
---
# <a name="upgrade-to-computer-vision-v30-read-api-from-v20v21"></a>Upgraden naar Computer Vision v3.0 Read API vanuit v2.0/v2.1

Deze handleiding laat zien hoe uw bestaande REST API-code van Computer Vision v 2.0 of v2.1 kunt bijwerken naar bewerkingen van Read v3.0. 

## <a name="upgrade-batch-read-file-to-read"></a>`Batch Read File` upgraden naar `Read`


1. Wijzig het API-pad voor `Batch Read File` 2.x als volgt:


    |Lezen 2.x |Lezen 3.0  |
    |----------|-----------|
    |https://{endpoint}/vision/**v2.0/read/core/asyncBatchAnalyze**     |https://{endpoint}/vision/**v3.0/read/analyze**[?language]|
    
    Er is een nieuwe optionele _taal_-parameter beschikbaar. Als u de taal van uw document niet kent, of als het document mogelijk meertalig is, neem het dan niet op. 

2. Wijzig het API-pad voor `Get Read Results` in 2.x als volgt:

    |Lezen 2.x |Lezen 3.0  |
    |----------|-----------|
    |https://{endpoint}/vision/**v2.0**/read/**operations**/{operationId}     |https://{endpoint}/vision/**v3.0**/read/**analyzeResults**/{operationId}|

3. Wijzig de code om de JSON-resultaten uit `Get Read Operation Result` te controleren. Wanneer de aanroep naar `Get Read Operation Result` is geslaagd, wordt er een statustekenreeksveld geretourneerd in de JSON-hoofdtekst. De volgende waarden uit v2.0 zijn gewijzigd zodat ze beter aansluiten bij de andere Cognitive Service REST API’s. 
 
    |Lezen 2.x |Lezen 3.0  |
    |----------|-----------|
    |`"NotStarted"` |   `"notStarted"`|
    |`"Running"` | `"running"`|
    |`"Failed"` | `"failed"`|
    |`"Succeeded"` | `"succeeded"`|
    
4. Wijzig uw code om de JSON met definitieve herkenningsresultaten uit `Get Read Operation Result` te interpreteren. 

    Let op de volgende wijzigingen in de JSON:
    
    - In v2.x retourneert `"Get Read Operation Result"` de OCR-JSON wanneer de status `"Succeeded"` is. In v3.0 is dit veld `"succeeded"`.
    - Om de hoofdmap voor de paginamatrix te verkrijgen, wijzigt u de JSON-hiërarchie van `"recognitionResults"` in `"analyzeResult"`/`"readResults"`. De JSON-hiërarchie voor regels en woorden per pagina blijft ongewijzigd, dus er zijn geen codewijzigingen nodig.
    -   De naam van de paginahoek `"clockwiseOrientation"` is gewijzigd in `"angle"` en het bereik is gewijzigd van 0 tot 360 graden in -180 tot 180 graden. Afhankelijk van uw code moet u al dan niet wijzigingen aanbrengen, aangezien de meeste wiskundige functies beide bereiken kunnen verwerken.
    -   De v3.0-API introduceert ook de volgende verbeteringen die u optioneel kunt benutten: -`"createdDateTime"` en `"lastUpdatedDateTime"` worden toegevoegd zodat u de verwerkingsduur kunt bijhouden. Raadpleeg de documentatie voor meer informatie. 
        - `"version"` toont de versie van de API die wordt gebruikt om resultaten te genereren
        - Er is een `"confidence"` per woord toegevoegd. Deze waarde wordt gekalibreerd zodat de waarde 0,95 betekent dat de kans 95% is dat de herkenning correct is. De betrouwbaarheidsscore kan worden gebruikt om te selecteren welke tekst er moet worden verzonden voor menselijke beoordeling. 
    
    
        In 2.X is de uitvoerindeling als volgt: 
    
    ```json
    {
        {
                "status": "Succeeded",
                "recognitionResults": [
                    {
                    "page": 1,
                    "language": "en",
                    "clockwiseOrientation": 349.59,
                    "width": 2661,
                    "height": 1901,
                    "unit": "pixel",
                    "lines": [
                        {
                        "boundingBox": [
                            67,
                            646,
                            2582,
                            713,
                            2580,
                            876,
                            67,
                            821
                        ],
                        "text": "The quick brown fox jumps",
                        "words": [
                            {
                            "boundingBox": [
                                143,
                                650,
                                435,
                                661,
                                436,
                                823,
                                144,
                                824
                            ],
                            "text": "The",
                            },
            // The rest of result is omitted for brevity 
            
    }
    ```
    
    In v3.0 is het aangepast:
    
    ```json
    {
        {
            "status": "succeeded",
            "createdDateTime": "2020-05-28T05:13:21Z",
            "lastUpdatedDateTime": "2020-05-28T05:13:22Z",
            "analyzeResult": {
            "version": "3.0.0",
            "readResults": [
                {
                "page": 1,
                "language": "en",
                "angle": 0.8551,
                "width": 2661,
                "height": 1901,
                "unit": "pixel",
                "lines": [
                    {
                    "boundingBox": [
                        67,
                        646,
                        2582,
                        713,
                        2580,
                        876,
                        67,
                        821
                    ],
                    "text": "The quick brown fox jumps",
                    "words": [
                        {
                        "boundingBox": [
                            143,
                            650,
                            435,
                            661,
                            436,
                            823,
                            144,
                            824
                        ],
                        "text": "The",
                        "confidence": 0.958
                        },
        // The rest of result is omitted for brevity 
        
    }
    ```

## <a name="upgrade-from-recognize-text-to-read"></a>Upgraden van `Recognize Text` naar `Read`
`Recognize Text` is een *preview*-bewerking die wordt *afgeschaft in alle versies van de Computer Vision-API*. U moet migreren van `Recognize Text` naar `Read` (v3.0) of `Batch Read File` (v2.0, v2.1). v3.0 van `Read` bevat nieuwere, betere modellen voor tekstherkenning en aanvullende functies, en wordt dus aanbevolen. Upgraden van `Recognize Text` naar `Read`:

1. Wijzig het API-pad voor `Recognize Text` v2.x als volgt:


    |Tekst herkennen 2.x |Lezen 3.0  |
    |----------|-----------|
    |https://{endpoint}/vision/**v2.0/recognizeText[?mode]**|https://{endpoint}/vision/**v3.0/read/analyze**[?language]|
    
    De _modus_-parameter wordt niet ondersteund in `Read`. Zowel handgeschreven als gedrukte tekst worden automatisch ondersteund.
    
    Er is een nieuwe optionele _taal_-parameter beschikbaar in v3.0. Als u de taal van uw document niet kent, of als het document mogelijk meertalig is, neem het dan niet op. 

2. Wijzig het API-pad voor `Get Recognize Text Operation Result` v2.x als volgt:

    |Tekst herkennen 2.x |Lezen 3.0  |
    |----------|-----------|
    |https://{endpoint}/vision/**v2.0/textOperations/** {operationId}|https://{endpoint}/vision/**v3.0/read/analyzeResults**/{operationId}|

3. Wijzig de code om de JSON-resultaten uit `Get Recognize Text Operation Result` te controleren. Wanneer de aanroep naar `Get Read Operation Result` is geslaagd, wordt er een statustekenreeksveld geretourneerd in de JSON-hoofdtekst. 
 
    |Tekst herkennen 2.x |Lezen 3.0  |
    |----------|-----------|
    |`"NotStarted"` |   `"notStarted"`|
    |`"Running"` | `"running"`|
    |`"Failed"` | `"failed"`|
    |`"Succeeded"` | `"succeeded"`|


4. Wijzig uw code om de JSON met definitieve herkenningsresultaten uit `Get Recognize Text Operation Result` te interpreteren om `Get Read Operation Result` te ondersteunen.

    Let op de volgende wijzigingen in de JSON:    

    - In v2.x retourneert `"Get Read Operation Result"` de OCR-JSON wanneer de status `"Succeeded"` is. In v3.0 is dit veld `"succeeded"`.
    - Om de hoofdmap voor de paginamatrix te verkrijgen, wijzigt u de JSON-hiërarchie van `"recognitionResult"` in `"analyzeResult"`/`"readResults"`. De JSON-hiërarchie voor regels en woorden per pagina blijft ongewijzigd, dus er zijn geen codewijzigingen nodig.
    -   De v3.0-API introduceert ook de volgende verbeteringen die u optioneel kunt benutten. Raadpleeg de API-referentie voor meer informatie: -`"createdDateTime"` en `"lastUpdatedDateTime"` worden toegevoegd zodat u de verwerkingsduur kunt bijhouden. Raadpleeg de documentatie voor meer informatie. 
        - `"version"` toont de versie van de API die wordt gebruikt om resultaten te genereren
        - Er is een `"confidence"` per woord toegevoegd. Deze waarde wordt gekalibreerd zodat de waarde 0,95 betekent dat de kans 95% is dat de herkenning correct is. De betrouwbaarheidsscore kan worden gebruikt om te selecteren welke tekst er moet worden verzonden voor menselijke beoordeling. 
        - `"angle"`: de algemene richting van de tekst met de klok mee, gemeten in graden tussen -180 en 180.
        -  `"width"` en `"height"` geven u de afmetingen van uw document, en `"unit"` geeft de eenheid van die afmetingen (pixel of inch, afhankelijk van het documenttype).
        - `"page"`: documenten met meerdere pagina’s worden ondersteund.
        - `"language"`: de invoertaal van het document (uit de optionele _taal_-parameter).


    In 2.X is de uitvoerindeling als volgt: 
    
    ```json
    {
        {
                "status": "Succeeded",
                "recognitionResult": [
                    {
                    "lines": [
                        {
                        "boundingBox": [
                            67,
                            646,
                            2582,
                            713,
                            2580,
                            876,
                            67,
                            821
                        ],
                        "text": "The quick brown fox jumps",
                        "words": [
                            {
                            "boundingBox": [
                                143,
                                650,
                                435,
                                661,
                                436,
                                823,
                                144,
                                824
                            ],
                            "text": "The",
                            },
            // The rest of result is omitted for brevity 
            
    }
    ```
    
    In v3.0 is het aangepast:
    
    ```json
    {
        {
            "status": "succeeded",
            "createdDateTime": "2020-05-28T05:13:21Z",
            "lastUpdatedDateTime": "2020-05-28T05:13:22Z",
            "analyzeResult": {
            "version": "3.0.0",
            "readResults": [
                {
                "page": 1,
                "angle": 0.8551,
                "width": 2661,
                "height": 1901,
                "unit": "pixel",
                "lines": [
                    {
                    "boundingBox": [
                        67,
                        646,
                        2582,
                        713,
                        2580,
                        876,
                        67,
                        821
                    ],
                    "text": "The quick brown fox jumps",
                    "words": [
                        {
                        "boundingBox": [
                            143,
                            650,
                            435,
                            661,
                            436,
                            823,
                            144,
                            824
                        ],
                        "text": "The",
                        "confidence": 0.958
                        },
        // The rest of result is omitted for brevity 
        
    }
    ```
    
## <a name="all-other-operations"></a>Alle overige bewerkingen

Er zijn geen andere wijzigingen die fouten veroorzaken tussen v2.X en v3.0 van de Computer Vision-API. U kunt gewoon het API-pad wijzigen om `v2.0` te vervangen door `v3.0`.
