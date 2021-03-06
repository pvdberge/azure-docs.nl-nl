---
title: 'Quickstart: Afbeeldingsinzichten krijgen met behulp van de REST API en Python - Bing Visual Search'
titleSuffix: Azure Cognitive Services
description: Leer hoe u een afbeelding uploadt naar de Bing Visual Search-API en inzichten in de afbeelding verkrijgt.
services: cognitive-services
author: swhite-msft
manager: nitinme
ms.service: cognitive-services
ms.subservice: bing-visual-search
ms.topic: quickstart
ms.date: 05/22/2020
ms.author: scottwhi
ms.custom: devx-track-python
ms.openlocfilehash: 7c76ec8600ade26098206a5d18559e795db53178
ms.sourcegitcommit: 7fe8df79526a0067be4651ce6fa96fa9d4f21355
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/06/2020
ms.locfileid: "87853072"
---
# <a name="quickstart-get-image-insights-using-the-bing-visual-search-rest-api-and-python"></a>Quickstart: afbeeldingsinzichten krijgen met behulp van de Bing Visual Search REST API en Python

Gebruik deze quickstart om uw eerste aanroep naar de Bing Visual Search-API te maken. Met deze Python-toepassing wordt er een afbeelding naar de API geüpload, waarna de geretourneerde gegevens worden weergegeven. Hoewel deze toepassing in Python is geschreven, is de API een RESTful-webservice die compatibel is met vrijwel elke programmeertaal.

## <a name="prerequisites"></a>Vereisten

* [Python 3.x](https://www.python.org/)

[!INCLUDE [cognitive-services-bing-visual-search-signup-requirements](../../../../includes/cognitive-services-bing-visual-search-signup-requirements.md)]

## <a name="initialize-the-application"></a>De toepassing initialiseren

1. Maak een nieuw Python-bestand in uw favoriete IDE of editor en voeg de volgende `import`-instructie toe:

    ```python
    import requests, json
    ```

2. Maak variabelen voor de abonnementssleutel, het eindpunt en het pad voor de afbeelding die u uploadt. Voor de waarde van `BASE_URI` kunt u het globale eindpunt in de volgende code gebruiken of het eindpunt voor het [aangepaste subdomein](../../../cognitive-services/cognitive-services-custom-subdomains.md) gebruiken dat voor uw resource wordt weergegeven in Azure Portal.

    ```python

    BASE_URI = 'https://api.cognitive.microsoft.com/bing/v7.0/images/visualsearch'
    SUBSCRIPTION_KEY = 'your-subscription-key'
    imagePath = 'your-image-path'
    ```
    
3. Wanneer u een lokale afbeelding uploadt, moeten de formuliergegevens de header `Content-Disposition` bevatten. Stel de parameter `name` in op 'afbeelding' en stel de parameter `filename` in op de bestandsnaam van de afbeelding. De inhoud van het formulier bevat de binaire gegevens van de afbeelding. De maximale afbeeldingsgrootte die u kunt uploaden is 1 MB.
    
    ```
    --boundary_1234-abcd
    Content-Disposition: form-data; name="image"; filename="myimagefile.jpg"
    
    ÿØÿà JFIF ÖÆ68g-¤CWŸþ29ÌÄøÖ‘º«™æ±èuZiÀ)"óÓß°Î= ØJ9á+*G¦...
    
    --boundary_1234-abcd--
    ```

4. Maak een woordenlijstobject voor het opslaan van de headerinformatie van uw aanvraag. Verbind uw abonnementssleutel met de `Ocp-Apim-Subscription-Key`-tekenreeks.

    ```python
    HEADERS = {'Ocp-Apim-Subscription-Key': SUBSCRIPTION_KEY}
    ```

5. Maak een andere woordenlijst voor uw afbeelding. Deze wordt geopend en geüpload wanneer u de aanvraag verzendt.

    ```python
    file = {'image' : ('myfile', open(imagePath, 'rb'))}
    ```

## <a name="parse-the-json-response"></a>Het JSON-antwoord parseren

Maak een methode met de naam `print_json()` voor het API-antwoord en druk de JSON af.

```python
def print_json(obj):
    """Print the object as json"""
    print(json.dumps(obj, sort_keys=True, indent=2, separators=(',', ': ')))
```

## <a name="send-the-request"></a>De aanvraag verzenden

Gebruik `requests.post()` om een aanvraag naar de Bing Visual Search-API te verzenden. Neem hierin de tekenreeks voor uw eindpunt, de header en gegevens over het bestand op. Druk `response.json()` af met `print_json()`.

```python
try:
    response = requests.post(BASE_URI, headers=HEADERS, files=file)
    response.raise_for_status()
    print_json(response.json())
    
except Exception as ex:
    raise ex
```

## <a name="next-steps"></a>Volgende stappen

> [!div class="nextstepaction"]
> [Een Visual Search-web-app met één pagina maken](../tutorial-bing-visual-search-single-page-app.md)
