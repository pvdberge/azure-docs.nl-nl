---
title: 'Zelfstudie: Een geofence maken en apparaten bijhouden op een Microsoft Azure-kaart'
description: Meer informatie over hoe u een geofence kunt instellen. Zie hoe u apparaten ten opzichte van de geofence kunt volgen met behulp van de Azure Maps Spatial-service.
author: anastasia-ms
ms.author: v-stharr
ms.date: 8/11/2020
ms.topic: tutorial
ms.service: azure-maps
services: azure-maps
manager: philmea
ms.custom: mvc
ms.openlocfilehash: 3ea9923dd98a49b1533defa3e95616655b7ea78d
ms.sourcegitcommit: 58d3b3314df4ba3cabd4d4a6016b22fa5264f05a
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/02/2020
ms.locfileid: "89299300"
---
# <a name="tutorial-set-up-a-geofence-by-using-azure-maps"></a>Zelfstudie: Een geofence instellen met behulp van Azure Maps

In deze zelfstudie leert u de basisbeginselen van het maken en gebruiken van Azure Maps Geofence-services in de context van het volgende scenario:

*Een bouwsitebeheerder moet de apparatuur bijhouden die een bouwterrein binnenkomt en verlaat. Telkens wanneer een apparaat de grenzen van het terrein binnengaat of verlaat, wordt er een e-mailbericht verzonden naar de Operations Manager.*

Azure Maps biedt een aantal services ter ondersteuning van het bijhouden van apparatuur die in het bovenstaande scenario het bouwterrein binnengaat en verlaat. In deze zelfstudie behandelen we het volgende:

> [!div class="checklist"]
> * Upload [Geofencing GeoJSON-gegevens](geofence-geojson.md) waarmee de bouwterreinen worden gedefinieerd die we willen bewaken. We gebruiken de [Data Upload API](https://docs.microsoft.com/rest/api/maps/data/uploadpreview) om geofences als veelhoekcoördinaten te uploaden naar uw Azure Maps-account.
> * Het instellen van twee [logische apps](https://docs.microsoft.com/azure/event-grid/handler-webhooks#logic-apps) die, wanneer ze worden geactiveerd, e-mailmeldingen sturen naar de Operations Manager van het bouwterrein wanneer er apparatuur het geofence-gebied binnenkomt of verlaat.
> * Het gebruiken van de [Azure Event Grid](https://docs.microsoft.com/azure/event-grid/overview) om een abonnement te nemen op Enter- en Exit-gebeurtenissen van Azure Maps geofence. We stellen twee Webhook-gebeurtenisabonnementen in die de HTTP-eindpunten aanroepen die in uw twee logische apps zijn gedefinieerd. De logische apps sturen vervolgens de juiste e-mailmeldingen over apparatuur die de geofence verlaat of binnenkomt.
> * Gebruik [Search Geofence Get API](https://docs.microsoft.com/rest/api/maps/spatial/getgeofence) om meldingen te krijgen wanneer een apparaat de geofence-gebieden binnenkomt of verlaat.

## <a name="prerequisites"></a>Vereisten

1. [Een Azure Maps-account maken](quick-demo-map-app.md#create-an-azure-maps-account)
2. [Een primaire sleutel voor een abonnement verkrijgen](quick-demo-map-app.md#get-the-primary-key-for-your-account), ook wel bekend als de primaire sleutel of de abonnementssleutel.

In deze zelfstudie wordt gebruikgemaakt van de [Postman](https://www.postman.com/)-toepassing, maar u kunt ook een andere API-ontwikkelomgeving kiezen.

## <a name="upload-geofencing-geojson-data"></a>Geofencing GeoJSON-gegevens uploaden

In deze zelfstudie gaan we Geofencing GeoJSON-gegevens uploaden die een `FeatureCollection` bevatten. De `FeatureCollection` bevat twee geofences waarmee u veelhoekgebieden binnen het bouwterrein definieert. De eerste geofence heeft geen tijdverloop of beperkingen. Op de tweede kan alleen tijdens kantooruren (9:00-17:00 uur) een query worden uitgevoerd, en deze is niet meer geldig na 1 januari 2022. Zie [Geofencing GeoJSON data](geofence-geojson.md) (Geofencing GeoJSON-gegevens) voor meer informatie over de GeoJSON-indeling.

>[!TIP]
>U kunt uw geofence-gegevens op elk gewenst moment bijwerken. Zie [Data upload-API](https://docs.microsoft.com/rest/api/maps/data/uploadpreview) voor meer informatie over het bijwerken van uw gegevens

1. Open de Postman-app. Selecteer **New** (Nieuw) bovenaan de Postman-app. Selecteer **Collection** (Verzameling) in het venster **Create New** (Nieuwe maken).  Geef de verzameling een naam en selecteer de knop **Create** (Maken).

2. Selecteer nogmaals **New** (Nieuw) om de aanvraag te maken. Selecteer **Request** (Aanvraag) in het venster **Create New** (Nieuwe maken). Voer een **Request name** (Aanvraagnaam) in voor de aanvraag. Selecteer de verzameling die u in de vorige stap hebt gemaakt en selecteer **Save** (Opslaan).

3. Selecteer de HTTP-methode **POST** op het tabblad Builder en voer de volgende URL in om de geofence-gegevens naar de Azure Maps-service te uploaden. Voor deze aanvraag en andere aanvragen die in dit artikel worden vermeld, vervangt u `{Azure-Maps-Primary-Subscription-key}` door uw primaire abonnementssleutel.

    ```HTTP
    https://atlas.microsoft.com/mapData/upload?subscription-key={Azure-Maps-Primary-Subscription-key}&api-version=1.0&dataFormat=geojson
    ```

    De parameter _geojson_ in het URL-pad geeft de gegevensindeling aan van de gegevens die worden geüpload.

4. Klik op het tabblad **Body** (Hoofdtekst). Selecteer **raw** (onbewerkt), en selecteer vervolgens **JSON** als invoerindeling. Kopieer de volgende GeoJSON-gegevens en plak ze in het tekstgebied **Body** (Hoofdtekst):

   ```JSON
   {
      "type": "FeatureCollection",
      "features": [
        {
          "type": "Feature",
          "geometry": {
            "type": "Polygon",
            "coordinates": [
              [
                [
                  -122.13393688201903,
                  47.63829579223815
                ],
                [
                  -122.13389128446579,
                  47.63782047131512
                ],
                [
                  -122.13240802288054,
                  47.63783312249837
                ],
                [
                  -122.13238388299942,
                  47.63829037035086
                ],
                [
                  -122.13393688201903,
                  47.63829579223815
                ]
              ]
            ]
          },
          "properties": {
            "geometryId": "1"
          }
        },
        {
          "type": "Feature",
          "geometry": {
            "type": "Polygon",
            "coordinates": [
              [
                [
                  -122.13374376296996,
                  47.63784758098976
                ],
                [
                  -122.13277012109755,
                  47.63784577367854
                ],
                [
                  -122.13314831256866,
                  47.6382813338708
                ],
                [
                  -122.1334782242775,
                  47.63827591198201
                ],
                [
                  -122.13374376296996,
                  47.63784758098976
                ]
              ]
            ]
          },
          "properties": {
            "geometryId": "2",
            "validityTime": {
            "expiredTime": "2022-01-01T00:00:00",
            "validityPeriod": [
                {
                  "startTime": "2020-07-15T16:00:00",
                  "endTime": "2020-07-15T24:00:00",
                  "recurrenceType": "Daily",
                  "recurrenceFrequency": 1,
                  "businessDayOnly": true
                }
              ]
            }
          }
        }
      ]
   }
   ```

5. Klik op de blauwe **Send**-knop (Verzenden) en wacht tot de aanvraag is verwerkt. Zodra de aanvraag is voltooid, gaat u naar het tabblad **Headers** (Kopteksten) van het antwoord. Kopieer de waarde van de **Location**-sleutel (Locatie), de `status URL`.

    ```http
    https://atlas.microsoft.com/mapData/operations/<operationId>?api-version=1.0
    ```

6. Maak een **GET** HTTP-aanvraag op de `status URL` om de status van de API-aanroep te controleren. U moet uw primaire abonnementssleutel toevoegen aan de URL voor authenticatie. De **GET**-aanvraag moet lijken op de volgende URL:

   ```HTTP
   https://atlas.microsoft.com/mapData/<operationId>/status?api-version=1.0&subscription-key={Subscription-key}
   ```

7. Wanneer de **GET** HTTP-aanvraag met succes wordt uitgevoerd, retourneert deze een `resourceLocation`. De `resourceLocation` bevat de unieke `udid` voor de geüploade inhoud. U moet deze `udid` opslaan om in de laatste sectie van deze zelfstudie een query uit te voeren op de Get Geofence API. U kunt desgewenst de `resourceLocation`-URL gebruiken om in de volgende stap metagegevens van deze resource op te halen.

      ```json
      {
          "status": "Succeeded",
          "resourceLocation": "https://atlas.microsoft.com/mapData/metadata/{udid}?api-version=1.0"
      }
      ```

8. Als u metagegevens van inhoud wilt ophalen, maakt u een **GET** HTTP-aanvraag op de `resourceLocation` URL die is opgehaald in stap 7. Zorg ervoor dat u uw primaire abonnementssleutel toevoegt aan de URL voor authenticatie. De **GET**-aanvraag moet lijken op de volgende URL:

    ```http
   https://atlas.microsoft.com/mapData/metadata/{udid}?api-version=1.0&subscription-key={Azure-Maps-Primary-Subscription-key}
    ```

9. Wanneer de **GET** HTTP-aanvraag slaagt, bevat de hoofdtekst van het antwoord de `udid` die in de `resourceLocation` van stap 7 is opgegeven, de locatie waar de inhoud in de toekomst kan worden gevonden/gedownload, en enkele andere metagegevens over de inhoud, zoals de datum waarop deze is gemaakt/bijgewerkt, de grootte, enzovoort. Een voorbeeld van het totale antwoord is:

    ```json
    {
        "udid": "{udid}",
        "location": "https://atlas.microsoft.com/mapData/{udid}?api-version=1.0",
        "created": "7/15/2020 6:11:43 PM +00:00",
        "updated": "7/15/2020 6:11:45 PM +00:00",
        "sizeInBytes": 1962,
        "uploadStatus": "Completed"
    }
    ```

## <a name="create-logic-app-workflows"></a>Werkstromen voor logische apps maken

In deze sectie worden twee [logische-app](https://docs.microsoft.com/azure/event-grid/handler-webhooks#logic-apps)-eindpunten gemaakt die een e-mailmelding activeren. We laten u zien hoe u de eerste trigger maakt waarmee e-mail meldingen worden verzonden wanneer het eindpunt ervan wordt aangeroepen.

1. Meld u aan bij [Azure Portal](https://portal.azure.com)

2. Klik in de linkerbovenhoek van [Azure Portal](https://portal.azure.com) op **Een resource maken**.

3. Typ **logische app** in het vak *Marketplace doorzoeken*.

4. Selecteer **Logische app** in de *Resultaten*. Klik op de knop **Maken**.

5. Voer op de pagina **Logische app** de volgende waarden in:
    * Het *Abonnement* dat u wilt gebruiken voor deze logische app.
    * De naam van de *Resourcegroep* voor deze logische app. U kunt kiezen om een *Nieuwe* of *Bestaande* resourcegroep te gebruiken.
    * De *Logische-app-naam* van uw logische app. In dit geval gebruiken we `Equipment-Enter` als naam.

    Laat in deze zelfstudie de rest van de waarden op de standaardinstellingen staan.

    :::image type="content" source="./media/tutorial-geofence/logic-app-create.png" alt-text="Een logische app maken":::

6. Klik op de knop **Beoordelen en maken**. Controleer uw instellingen en klik op **Maken** om de implementatie te verzenden. Wanneer de implementatie is voltooid, klikt u op **Naar de resource gaan**. U wordt naar de **Logic App Designer** geleid.

7. Nu selecteren we een triggertype. Schuif naar beneden naar de sectie *Beginnen met een algemene trigger**. Klik op**Wanneer een HTTP-aanvraag wordt ontvangen**.

     :::image type="content" source="./media/tutorial-geofence/logic-app-trigger.png" alt-text="Een HTTP-trigger voor een logische app maken":::

8. Klik op **Opslaan** in de rechterbovenhoek van de Designer. De **HTTP POST-URL** wordt automatisch gegenereerd. Sla de URL op, want u hebt deze in de volgende sectie nodig om een gebeurteniseindpunt te maken.

    :::image type="content" source="./media/tutorial-geofence/logic-app-httprequest.png" alt-text="URL en JSON voor de HTTP-aanvraag van de logische app":::

9. Selecteer **+ Nieuwe stap**. Nu kiezen we een actie. Typ `outlook.com email` in het zoekvak. Schuif in de lijst **Acties** omlaag en klik op **Een e-mailbericht verzenden (V2)** .
  
    :::image type="content" source="./media/tutorial-geofence/logic-app-designer.png" alt-text="Een logische app maken in Designer":::

10. Meld u aan bij uw Outlook.com-account. Zorg ervoor dat u op **Ja** klikt om de logische app toegang te geven tot het account. Vul de velden in voor het verzenden van een e-mail.

    :::image type="content" source="./media/tutorial-geofence/logic-app-email.png" alt-text="Stap e-mail verzenden maken in logische app":::

    >[!TIP]
    > U kunt in uw e-mailmeldingen GeoJSON-antwoordgegevens ophalen, zoals `geometryId` of `deviceId`, door Logic App te configureren voor het lezen van de gegevens die door de Event Grid worden verzonden. Zie voor informatie over het configureren van Logic App voor het consumeren en doorgeven van gebeurtenisgegevens naar e-mailmeldingen [Zelfstudie: E-mailmeldingen over gebeurtenissen van Azure IoT Hub verzenden met Event Grid en Logic Apps](https://docs.microsoft.com/azure/event-grid/publish-iot-hub-events-to-logic-apps).

11. Klik op **Opslaan** in de linkerbovenhoek van de Logic Apps Designer.

12. Herhaal de stappen 3-11 om een tweede logische app te maken om de manager op de hoogte te stellen wanneer apparatuur het bouwterrein verlaat. Noem de logische app `Equipment-Exit`.

## <a name="create-azure-maps-events-subscriptions"></a>Abonnement op Azure Maps-gebeurtenissen maken

Azure Maps ondersteunt drie typen gebeurtenissen. [Hier](https://docs.microsoft.com/azure/event-grid/event-schema-azure-maps) vindt u een overzicht van de gebeurtenistypen die door Azure Maps worden ondersteund.  We moeten twee verschillende gebeurtenisabonnementen maken: één voor Enter-gebeurtenissen en een voor Exit-gebeurtenissen voor de geofence.

Volg de stappen hieronder om een gebeurtenisabonnement te maken voor Enter-gebeurtenissen voor de geofence. U kunt zich op een vergelijkbare manier abonneren op Exit-gebeurtenissen voor de geofence.

1. Navigeer naar uw Azure Maps-account. Selecteer **Abonnementen** op het dashboard. Klik op de naam van uw abonnement en selecteer **gebeurtenissen** in het instellingenmenu.

    :::image type="content" source="./media/tutorial-geofence/events-tab.png" alt-text="Navigeren naar Gebeurtenissen in uw Azure Maps-account":::

2. U maakt een gebeurtenisabonnement door **+ Gebeurtenisabonnement** te selecteren op de gebeurtenissenpagina.

    :::image type="content" source="./media/tutorial-geofence/create-event-subscription.png" alt-text="Een abonnement maken op Azure Maps-gebeurtenissen":::

3. Voer op de pagina **Gebeurtenisabonnement maken** de volgende waarden in:
    * De *Naam* van het gebeurtenisabonnement.
    * Het *Gebeurtenisschema* moet *Gebeurtenisrasterschema* zijn.
    * De *Naam van het systeemonderwerp* voor dit gebeurtenisabonnement. In dit geval gebruiken we `Contoso-Construction`.
    * Kies bij *Filteren op gebeurtenistypen* het gebeurtenistype `Geofence Entered`.
    * Kies `Web Hook` als het *Eindpunttype*.
    * Voor *Eindpunt*kopieert u de HTTP POST-URL voor het Logic App Enter-eindpunt dat u in de vorige sectie hebt gemaakt. Als u bent vergeten deze op te slaan, kunt u teruggaan naar de Logic App Designer en de URL kopiëren uit de HTTP-triggerstap.

    :::image type="content" source="./media/tutorial-geofence/events-subscription.png" alt-text="Abonnement op Azure Maps-gebeurtenissen: details":::

4. Klik op **Create**.

5. Herhaal stap 1-4 voor het Logic App Exit-eindpunt dat u in de vorige sectie hebt gemaakt. Zorg ervoor dat u bij stap 3 `Geofence Exited` kiest als het gebeurtenistype.

## <a name="use-spatial-geofence-get-api"></a>Spatial Geofence Get API gebruiken

Nu gebruiken we de [Spatial Geofence Get API](https://docs.microsoft.com/rest/api/maps/spatial/getgeofence) om e-mailmeldingen te sturen naar de Operations Manager wanneer een apparaat de geofences binnenkomt of verlaat.

Elk apparaat heeft een `deviceId`. In deze zelfstudie volgen we één apparaat, waarvan de unieke ID `device_1` is.

Voor de duidelijkheid laat het volgende diagram de vijf locaties van het apparaat in de loop der tijd zien, te beginnen bij de *Start*-locatie, ergens buiten de geofences. Voor deze zelfstudie wordt de *Start*-locatie niet gedefinieerd, omdat we geen query uitvoeren op het apparaat op die locatie.

Wanneer we een query uitvoeren op [Spatial Geofence Get API](https://docs.microsoft.com/rest/api/maps/spatial/getgeofence) met een apparaatlocatie die aangeeft dat de geofence voor het eerst wordt binnengegaan of verlaten, roept de Event Grid het juiste Logic App-eindpunt aan om een e-mailbericht naar de Operations Manager te sturen.

Elk van de volgende secties doet HTTP GET Geofencing API-aanvragen met behulp van de vijf verschillende locatiecoördinaten van de apparatuur.

![Geofence-kaart in Azure Maps](./media/tutorial-geofence/geofence.png)

### <a name="equipment-location-1-47638237-122132483"></a>Apparaatlocatie 1 (47.638237,-122.132483)

1. Selecteer **New** (Nieuw) bovenaan de Postman-app. Selecteer **Request** (Aanvraag) in het venster **Create New** (Nieuwe maken).  Voer een **Request name** (Aanvraagnaam) in voor de aanvraag. We gebruiken de naam *Location 1*. Selecteer de verzameling die u hebt gemaakt in de sectie [Geofencing GeoJSON-gegevens uploaden](#upload-geofencing-geojson-data)en selecteer **Opslaan**.

2. Selecteer de HTTP-methode **GET** op het tabblad Builder en voer de volgende URL in. Zorg ervoor dat u `{Azure-Maps-Primary-Subscription-key}` vervangt door uw primaire abonnementssleutel en `{udid}` door de `udid` die u heb opgeslagen in de sectie [Geofencing GeoJSON-gegevens uploaden](#upload-geofencing-geojson-data).

   ```HTTP
   https://atlas.microsoft.com/spatial/geofence/json?subscription-key={subscription-key}&api-version=1.0&deviceId=device_01&udid={udid}&lat=47.638237&lon=-122.1324831&searchBuffer=5&isAsync=True&mode=EnterAndExit
   ```

3. Klik op de knop **Verzenden**. De volgende GeoJSON verschijnt in het antwoordvenster.

    ```json
    {
      "geometries": [
        {
          "deviceId": "device_1",
          "udId": "64f71aa5-bbee-942d-e351-651a6679a7da",
          "geometryId": "1",
          "distance": -999.0,
          "nearestLat": 47.638291,
          "nearestLon": -122.132483
        },
        {
          "deviceId": "device_1",
          "udId": "64f71aa5-bbee-942d-e351-651a6679a7da",
          "geometryId": "2",
          "distance": 999.0,
          "nearestLat": 47.638053,
          "nearestLon": -122.13295
        }
      ],
      "expiredGeofenceGeometryId": [],
      "invalidPeriodGeofenceGeometryId": [],
      "isEventPublished": true
    }
    ```

4. In het GeoJSON-antwoord hierboven betekent de negatieve afstand van de geofence van de hoofdsite dat het apparaat zich in de geofence bevindt. De positieve afstand van de subsite-geofence betekent dat de apparatuur zich buiten de subsite-geofence bevindt. Omdat dit de eerste keer is dat het apparaat binnen de geofence van de hoofdsite is gelokaliseerd, wordt de parameter `isEventPublished` ingesteld op `true`, en heeft de Operations Manager een e-mailbericht gekregen dat er apparatuur de geofence is binnengekomen.

### <a name="location-2-4763800-122132531"></a>Locatie 2 (47.63800,-122.132531)

1. Selecteer **New** (Nieuw) bovenaan de Postman-app. Selecteer **Request** (Aanvraag) in het venster **Create New** (Nieuwe maken).  Voer een **Request name** (Aanvraagnaam) in voor de aanvraag. We gebruiken de naam *Location 2*. Selecteer de verzameling die u hebt gemaakt in de sectie [Geofencing GeoJSON-gegevens uploaden](#upload-geofencing-geojson-data)en selecteer **Opslaan**.

2. Selecteer de HTTP-methode **GET** op het tabblad Builder en voer de volgende URL in. Zorg ervoor dat u `{Azure-Maps-Primary-Subscription-key}` vervangt door uw primaire abonnementssleutel en `{udid}` door de `udid` die u heb opgeslagen in de sectie [Geofencing GeoJSON-gegevens uploaden](#upload-geofencing-geojson-data).

   ```HTTP
   https://atlas.microsoft.com/spatial/geofence/json?subscription-key={subscription-key}&api-version=1.0&deviceId=device_01&udId={udId}&lat=47.63800&lon=-122.132531&searchBuffer=5&isAsync=True&mode=EnterAndExit
   ```

3. Klik op de knop **Verzenden**. De volgende GeoJSON verschijnt in het antwoordvenster:

    ```json
    {
      "geometries": [
        {
          "deviceId": "device_01",
          "udId": "64f71aa5-bbee-942d-e351-651a6679a7da",
          "geometryId": "1",
          "distance": -999.0,
          "nearestLat": 47.637997,
          "nearestLon": -122.132399
        },
        {
          "deviceId": "device_01",
          "udId": "64f71aa5-bbee-942d-e351-651a6679a7da",
          "geometryId": "2",
          "distance": 999.0,
          "nearestLat": 47.63789,
          "nearestLon": -122.132809
        }
      ],
      "expiredGeofenceGeometryId": [],
      "invalidPeriodGeofenceGeometryId": [],
      "isEventPublished": false
    }
    ````

4. In het GeoJSON-antwoord hierboven is het apparaat in de geofence van de hoofdsite gebleven en is niet de subsite-geofence binnengegaan. Als gevolg hiervan wordt de parameter `isEventPublished` ingesteld op `false` en ontvangt de Operations Manager geen e-mailmeldingen.

### <a name="location-3-4763810783315048-12213336020708084"></a>Locatie 3 (47.63810783315048,-122.13336020708084)

1. Selecteer **New** (Nieuw) bovenaan de Postman-app. Selecteer **Request** (Aanvraag) in het venster **Create New** (Nieuwe maken).  Voer een **Request name** (Aanvraagnaam) in voor de aanvraag. We gebruiken de naam *Location 3*. Selecteer de verzameling die u hebt gemaakt in de sectie [Geofencing GeoJSON-gegevens uploaden](#upload-geofencing-geojson-data)en selecteer **Opslaan**.

2. Selecteer de HTTP-methode **GET** op het tabblad Builder en voer de volgende URL in. Zorg ervoor dat u `{Azure-Maps-Primary-Subscription-key}` vervangt door uw primaire abonnementssleutel en `{udid}` door de `udid` die u heb opgeslagen in de sectie [Geofencing GeoJSON-gegevens uploaden](#upload-geofencing-geojson-data).

    ```HTTP
      https://atlas.microsoft.com/spatial/geofence/json?subscription-key={subscription-key}&api-version=1.0&deviceId=device_01&udid={udid}&lat=47.63810783315048&lon=-122.13336020708084&searchBuffer=5&isAsync=True&mode=EnterAndExit
      ```

3. Klik op de knop **Verzenden**. De volgende GeoJSON verschijnt in het antwoordvenster:

    ```json
    {
      "geometries": [
        {
          "deviceId": "device_01",
          "udId": "64f71aa5-bbee-942d-e351-651a6679a7da",
          "geometryId": "1",
          "distance": -999.0,
          "nearestLat": 47.638294,
          "nearestLon": -122.133359
        },
        {
          "deviceId": "device_01",
          "udId": "64f71aa5-bbee-942d-e351-651a6679a7da",
          "geometryId": "2",
          "distance": -999.0,
          "nearestLat": 47.638161,
          "nearestLon": -122.133549
        }
      ],
      "expiredGeofenceGeometryId": [],
      "invalidPeriodGeofenceGeometryId": [],
      "isEventPublished": true
    }
    ````

4. In het GeoJSON-antwoord hierboven is het apparaat in de geofence van de hoofdsite gebleven maar is de subsite-geofence binnengegaan. Als gevolg hiervan wordt de parameter `isEventPublished` ingesteld op `true` en krijgt de Operations Manager een e-mailmelding die aangeeft dat het apparatuur een geofence is binnengegaan.

    >[!NOTE]
    >Als het apparaat na kantooruren naar de subsite zou zijn gegaan, zou er geen gebeurtenis worden gepubliceerd en zou de Operations Manager geen meldingen ontvangen.  

### <a name="location-4-47637988-1221338344"></a>Locatie 4 (47.637988,-122.1338344)

1. Selecteer **New** (Nieuw) bovenaan de Postman-app. Selecteer **Request** (Aanvraag) in het venster **Create New** (Nieuwe maken).  Voer een **Request name** (Aanvraagnaam) in voor de aanvraag. We gebruiken de naam *Location 4*. Selecteer de verzameling die u hebt gemaakt in de sectie [Geofencing GeoJSON-gegevens uploaden](#upload-geofencing-geojson-data)en selecteer **Opslaan**.

2. Selecteer de HTTP-methode **GET** op het tabblad Builder en voer de volgende URL in. Zorg ervoor dat u `{Azure-Maps-Primary-Subscription-key}` vervangt door uw primaire abonnementssleutel en `{udid}` door de `udid` die u heb opgeslagen in de sectie [Geofencing GeoJSON-gegevens uploaden](#upload-geofencing-geojson-data).

    ```HTTP
    https://atlas.microsoft.com/spatial/geofence/json?subscription-key={subscription-key}&api-version=1.0&deviceId=device_01&udid={udid}&lat=47.637988&userTime=2023-01-16&lon=-122.1338344&searchBuffer=5&isAsync=True&mode=EnterAndExit
    ```

3. Klik op de knop **Verzenden**. De volgende GeoJSON verschijnt in het antwoordvenster:

    ```json
    {
      "geometries": [
        {
          "deviceId": "device_01",
          "udId": "64f71aa5-bbee-942d-e351-651a6679a7da",
          "geometryId": "1",
          "distance": -999.0,
          "nearestLat": 47.637985,
          "nearestLon": -122.133907
        }
      ],
      "expiredGeofenceGeometryId": [
        "2"
      ],
      "invalidPeriodGeofenceGeometryId": [],
      "isEventPublished": false
    }
    ````

4. In het GeoJSON-antwoord hierboven is het apparaat in de geofence van de hoofdsite gebleven maar heeft de subsite-geofence verlaten. Maar zoals u ziet is de waarde `userTime` later dan de `expiredTime` zoals gedefinieerd in de geofence-gegevens. Als gevolg hiervan wordt de parameter `isEventPublished` ingesteld op `false` en ontvangt de Operations Manager geen e-mailmelding.

### <a name="location-547637988-1221338344"></a>Locatie 5(47.637988,-122.1338344)

1. Selecteer **New** (Nieuw) bovenaan de Postman-app. Selecteer **Request** (Aanvraag) in het venster **Create New** (Nieuwe maken).  Voer een **Request name** (Aanvraagnaam) in voor de aanvraag. We gebruiken de naam *Location 4*. Selecteer de verzameling die u hebt gemaakt in de sectie [Geofencing GeoJSON-gegevens uploaden](#upload-geofencing-geojson-data)en selecteer **Opslaan**.

2. Selecteer de HTTP-methode **GET** op het tabblad Builder en voer de volgende URL in. Zorg ervoor dat u `{Azure-Maps-Primary-Subscription-key}` vervangt door uw primaire abonnementssleutel en `{udid}` door de `udid` die u heb opgeslagen in de sectie [Geofencing GeoJSON-gegevens uploaden](#upload-geofencing-geojson-data).

    ```HTTP
    https://atlas.microsoft.com/spatial/geofence/json?subscription-key={subscription-key}&api-version=1.0&deviceId=device_01&udid={udid}&lat=47.637988&lon=-122.1338344&searchBuffer=5&isAsync=True&mode=EnterAndExit
    ```

3. Klik op de knop **Verzenden**. De volgende GeoJSON verschijnt in het antwoordvenster:

    ```json
    {
      "geometries": [
      {
        "deviceId": "device_01",
        "udId": "64f71aa5-bbee-942d-e351-651a6679a7da",
        "geometryId": "1",
        "distance": -999.0,
        "nearestLat": 47.637985,
        "nearestLon": -122.133907
      },
      {
        "deviceId": "device_01",
        "udId": "64f71aa5-bbee-942d-e351-651a6679a7da",
        "geometryId": "2",
        "distance": 999.0,
        "nearestLat": 47.637945,
        "nearestLon": -122.133683
      }
      ],
      "expiredGeofenceGeometryId": [],
      "invalidPeriodGeofenceGeometryId": [],
      "isEventPublished": true
    }
    ````

4. In het GeoJSON-antwoord hierboven heeft het apparaat de geofence van de hoofdsite verlaten. Als gevolg hiervan wordt de parameter `isEventPublished` ingesteld op `true` en krijgt de Operations Manager een e-mailmelding die aangeeft dat het apparatuur een geofence heeft verlaten.

## <a name="next-steps"></a>Volgende stappen

> [!div class="nextstepaction"]
> [Typen inhoud in Azure Logic Apps afhandelen](https://docs.microsoft.com/azure/logic-apps/logic-apps-content-type)

> [!div class="nextstepaction"]
> [E-mailmeldingen verzenden met Event Grid en Logic Apps](https://docs.microsoft.com/azure/event-grid/publish-iot-hub-events-to-logic-apps)

> [!div class="nextstepaction"]
> [Ondersteunde gebeurtenis-handlers in Event Grid](https://docs.microsoft.com/azure/event-grid/event-handlers).
