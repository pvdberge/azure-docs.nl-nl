---
title: Afbeeldingen ophalen van de Web-Bing Afbeeldingen zoeken-API
titleSuffix: Azure Cognitive Services
description: Gebruik de Bing Afbeeldingen zoeken-API voor het zoeken naar en ophalen van relevante installatie kopieën van het web.
services: cognitive-services
author: aahill
manager: nitinme
ms.assetid: AB1B9898-C94A-4B59-91A1-8623C94BA3D4
ms.service: cognitive-services
ms.subservice: bing-image-search
ms.topic: conceptual
ms.date: 03/04/2019
ms.author: aahi
ms.openlocfilehash: 309bbca762149f8804742d9ef02d4c3e8dfcdc6b
ms.sourcegitcommit: 58faa9fcbd62f3ac37ff0a65ab9357a01051a64f
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 04/29/2020
ms.locfileid: "67542764"
---
# <a name="get-images-from-the-web-with-the-bing-image-search-api"></a>Installatie kopieën van het web ophalen met de Bing Afbeeldingen zoeken-API

Wanneer u de Bing Image Search REST API gebruikt, kunt u installatie kopieën ophalen van het web die aan uw zoek term zijn gerelateerd door de volgende GET-aanvraag te verzenden:

```http
GET https://api.cognitive.microsoft.com/bing/v7.0/images/search?q=sailing+dinghies&mkt=en-us HTTP/1.1
Ocp-Apim-Subscription-Key: 123456789ABCDE
X-MSEdge-ClientIP: 999.999.999.999
X-Search-Location: lat:47.60357;long:-122.3295;re:100
X-MSEdge-ClientID: <blobFromPriorResponseGoesHere>
Host: api.cognitive.microsoft.com
```

Gebruik de [q](https://docs.microsoft.com/rest/api/cognitiveservices-bingsearch/bing-images-api-v7-reference#query) -query parameter voor uw zoek term met URL-code ring. Als u bijvoorbeeld *zeil dinghies*invoert, stelt `q` u in op `sailing+dinghies` of `sailing%20dinghies`.

> [!IMPORTANT]
> * Alle aanvragen moeten worden gemaakt van een server en niet van een client.
> * Als dit de eerste keer is dat u een van de Bing zoeken-Api's aanroept, neemt u de header van de client-ID niet op. Neem alleen de client-ID op als u eerder een Bing API hebt aangeroepen die een client-ID voor de combi natie van gebruikers en apparaten heeft geretourneerd.

## <a name="get-images-from-a-specific-web-domain"></a>Installatie kopieën ophalen van een specifiek webdomein

Als u afbeeldingen uit een bepaald domein wilt opvragen, gebruikt de query-operator [site:](https://msdn.microsoft.com/library/ff795613.aspx).

```http
GET https://api.cognitive.microsoft.com/bing/v7.0/images/search?q=sailing+dinghies+site:contososailing.com&mkt=en-us HTTP/1.1
```

> [!NOTE]
> Antwoorden op query's die gebruikmaken `site:` van de operator, bevatten mogelijk inhoud voor volwassenen, ongeacht de instelling van [SafeSearch](https://docs.microsoft.com/rest/api/cognitiveservices-bingsearch/bing-images-api-v7-reference#safesearch) . Gebruik `site:` alleen als u op de hoogte bent van de inhoud van het domein.

## <a name="filter-images"></a>Afbeeldingen filteren

 De Afbeeldingen zoeken-API retourneert standaard alle installatie kopieën die relevant zijn voor de query. Als u de installatie kopieën wilt filteren die door Bing worden geretourneerd (bijvoorbeeld om alleen afbeeldingen met een transparante achtergrond of een specifieke grootte te retour neren), gebruikt u de volgende query parameters:

* [aspect](https://docs.microsoft.com/rest/api/cognitiveservices-bingsearch/bing-images-api-v7-reference#aspect): filter afbeeldingen op hoogte-breedte verhouding (bijvoorbeeld Standard-of Wide Screen-afbeeldingen).
* [Color](https://docs.microsoft.com/rest/api/cognitiveservices-bingsearch/bing-images-api-v7-reference#color): filter afbeeldingen op dominante kleur of zwart en wit.
* [versheid](https://docs.microsoft.com/rest/api/cognitiveservices-bingsearch/bing-images-api-v7-reference#freshness): filter afbeeldingen op leeftijd (bijvoorbeeld afbeeldingen die zijn gedetecteerd door Bing in de afgelopen week).
* [hoogte](https://docs.microsoft.com/rest/api/cognitiveservices-bingsearch/bing-images-api-v7-reference#height), [breedte](https://docs.microsoft.com/rest/api/cognitiveservices-bingsearch/bing-images-api-v7-reference#width): filter afbeeldingen op breedte en hoogte.
* [imageContent](https://docs.microsoft.com/rest/api/cognitiveservices-bingsearch/bing-images-api-v7-reference#imagecontent): filter afbeeldingen op inhoud (bijvoorbeeld afbeeldingen waarin alleen het gezicht van een persoon wordt weer gegeven).
* [imageType](https://docs.microsoft.com/rest/api/cognitiveservices-bingsearch/bing-images-api-v7-reference#imagetype): filter afbeeldingen op type (bijvoorbeeld illustraties, GIF-animaties of transparante achtergronden).
* [licentie](https://docs.microsoft.com/rest/api/cognitiveservices-bingsearch/bing-images-api-v7-reference#license): filter afbeeldingen op het type licentie dat is gekoppeld aan de site.
* [grootte](https://docs.microsoft.com/rest/api/cognitiveservices-bingsearch/bing-images-api-v7-reference#size): filter afbeeldingen op grootte, zoals kleine afbeeldingen tot 200x200 pixels.

Als u afbeeldingen uit een bepaald domein wilt opvragen, gebruikt de query-operator [site:](https://msdn.microsoft.com/library/ff795613.aspx).

In het volgende voor beeld ziet u hoe u kleine afbeeldingen kunt ophalen uit ContosoSailing.com die Bing in de afgelopen week is gedetecteerd.  

```http
GET https://api.cognitive.microsoft.com/bing/v7.0/images/search?q=sailing+dinghies+site:contososailing.com&size=small&freshness=week&mkt=en-us HTTP/1.1  
Ocp-Apim-Subscription-Key: 123456789ABCDE  
X-MSEdge-ClientIP: 999.999.999.999  
X-Search-Location: lat:47.60357;long:-122.3295;re:100  
X-MSEdge-ClientID: <blobFromPriorResponseGoesHere>  
Host: api.cognitive.microsoft.com  
```

## <a name="bing-image-search-response-format"></a>Indeling van Bing Image Search-antwoord

Het antwoord bericht van Bing bevat een antwoord op een [installatie kopie](https://docs.microsoft.com/rest/api/cognitiveservices-bingsearch/bing-images-api-v7-reference#images) met een lijst met installatie kopieën die Cognitive Services vastgesteld dat deze relevant zijn voor de query. Elk [afbeeldings](https://docs.microsoft.com/rest/api/cognitiveservices-bingsearch/bing-images-api-v7-reference#image) object in de lijst bevat de volgende informatie over de afbeelding: de URL, de grootte, de afmetingen, de coderings indeling, een URL naar een miniatuur van de afbeelding en de afmetingen van de miniatuur.

> [!NOTE]
> * Afbeeldingen moeten worden weer gegeven in de volg orde die in het antwoord is opgenomen.
> * Omdat URL-indelingen en-para meters kunnen worden gewijzigd zonder kennisgeving, gebruikt u alle Url's als-is. U mag geen afhankelijkheden maken voor de URL-indeling of para meters, tenzij anders wordt vermeld.

```json
{
    "name": "Rich Passage Sailing Dinghy",
    "webSearchUrl": "https:\/\/www.bing.com\/cr?IG=73118C8B4E3...",
    "thumbnailUrl": "https:\/\/tse1.mm.bing.net\/th?id=OIP.GNarK7m...",
    "datePublished": "2011-10-29T11:26:00",
    "contentUrl": "http:\/\/www.bing.com\/cr?IG=73118C8B4E3D4C3...",
    "hostPageUrl": "http:\/\/www.bing.com\/cr?IG=73118C8B4E3D4C3687...",
    "contentSize": "79239 B",
    "encodingFormat": "jpeg",
    "hostPageDisplayUrl": "en.contoso.org\/wiki\/File:Rich_Passage...",
    "width": 526,
    "height": 688,
    "thumbnail": {
        "width": 229,
        "height": 300
    },
    "imageInsightsToken": "ccid_GNarK7ma*mid_CCF85447ADA6...",
    "insightsSourcesSummary": {
        "shoppingSourcesCount": 0,
        "recipeSourcesCount": 0
    },
    "imageId": "CCF85447ADA6FFF9E96E7DF0B796F7A86E34593",
    "accentColor": "376094"
},
```

Wanneer u de Bing Afbeeldingen zoeken-API aanroept, retourneert Bing een lijst met resultaten. De lijst is een subset van het totale aantal resultaten die relevant zijn voor de query. Het veld `totalEstimatedMatches` in de respons bevat een schatting van het aantal afbeeldingen dat beschikbaar is om weer te geven. Zie [paginerings installatie kopieën](../paging-images.md)voor meer informatie over het door lopen van de rest van de installatie kopieën.

## <a name="next-steps"></a>Volgende stappen

Als u de Bing Afbeeldingen zoeken-API nog niet eerder hebt uitgevoerd, kunt u een [Snelstartgids](../quickstarts/csharp.md)proberen. Als u op zoek bent naar iets complexere, probeert u de zelf studie om een [Web-app met één pagina](../tutorial-bing-image-search-single-page-app.md)te maken.
