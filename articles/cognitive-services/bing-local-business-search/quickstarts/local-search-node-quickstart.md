---
title: 'Quickstart: Een query naar de API verzenden met behulp van Node.js - Bing Local Business Search'
titleSuffix: Azure Cognitive Services
description: Gebruik deze quickstart om aanvragen te verzenden naar de Bing Local Business Search-API, een Azure Cognitive Service.
services: cognitive-services
author: aahill
manager: nitinme
ms.service: cognitive-services
ms.subservice: bing-local-business
ms.topic: quickstart
ms.date: 05/12/2020
ms.author: aahi
ms.custom: devx-track-javascript
ms.openlocfilehash: d0ee55c0baa6d7ec2ff86aa0e37b10ca4c973b77
ms.sourcegitcommit: 42107c62f721da8550621a4651b3ef6c68704cd3
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/29/2020
ms.locfileid: "87408132"
---
# <a name="quickstart-send-a-query-to-the-bing-local-business-search-api-using-nodejs"></a>Quickstart: Een query verzenden naar de Bing Local Business Search-API met behulp van Node.js

Gebruik deze quickstart om te leren hoe u aanvragen verzendt naar de Bing Local Business Search-API, een Azure Cognitive Service. Hoewel deze eenvoudige app in Node.js is geschreven, is de API een RESTful-webservice die compatibel is met programmeertalen waarin HTTP-aanvragen kunnen worden uitgevoerd en JSON kan worden geparseerd.

In deze voorbeeldtoepassing worden lokale antwoordgegevens opgehaald uit de API voor een zoekquery.

## <a name="prerequisites"></a>Vereisten

* Een Azure-abonnement - [Een gratis abonnement maken](https://azure.microsoft.com/free/cognitive-services/)
* Nieuwste versie van [Node.js](https://nodejs.org/en/download/).
* De [JavaScript-aanvragenbibliotheek](https://github.com/request/request).
* Zodra u een Azure-abonnement hebt, <a href="https://portal.azure.com/#create/Microsoft.CognitiveServicesBingSearch-v7"  title="Een Bing Search-resource maken"  target="_blank">maakt u een Bing Search-resource <span class="docon docon-navigate-external x-hidden-focus"></span></a> in de Azure-portal om uw sleutel en eindpunt op te halen. Nadat de app is geïmplementeerd, klikt u op **Ga naar resource**.


## <a name="code-scenario"></a>Codescenario

Met de volgende code wordt de aanvraag gedefinieerd en verzonden die in de volgende stappen wordt geïmplementeerd:

1. Declareer variabelen om het eindpunt op te geven met een host en pad.
2. Geef de query op en voeg de queryparameter toe.
3. Maak een handlerfunctie voor het antwoord.
4. Definieer de zoekfunctie die de aanvraag maakt en de header `Ocp-Apim-Subscription-Key` toevoegt.
5. Voer de zoekfunctie uit.


```javascript
'use strict';

let https = require('https');

// Replace the subscriptionKey string value with your valid subscription key.
let subscriptionKey = 'your-access-key';

let host = 'api.cognitive.microsoft.com/bing';
let path = '/v7.0/localbusinesses/search';

let mkt = 'en-US';
let q = 'hotel in Bellevue';

let params = '?q=' + encodeURI(q) + "&mkt=" + mkt;

let response_handler = function (response) {
    let body = '';
    response.on('data', function (d) {
        body += d;
    });
    response.on('end', function () {
        let body_ = JSON.parse(body);
        let body__ = JSON.stringify(body_, null, '  ');
        console.log(body__);
    });
    response.on('error', function (e) {
        console.log('Error: ' + e.message);
    });
};

let Search = function () {
    let request_params = {
        method: 'GET',
        hostname: host,
        path: path + params,
        headers: {
            'Ocp-Apim-Subscription-Key': subscriptionKey,
        }
    };

    let req = https.request(request_params, response_handler);
    req.end();
}

Search();

```

## <a name="next-steps"></a>Volgende stappen

* [Quickstart over zoeken naar lokale bedrijven met C#](local-quickstart.md)
* [Quickstart over Bing Local Business Search met Java](local-search-java-quickstart.md)
* [Quickstart over zoeken naar lokale bedrijven met Python](local-search-python-quickstart.md)
