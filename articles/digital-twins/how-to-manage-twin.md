---
title: Digitale tweelingen beheren
titleSuffix: Azure Digital Twins
description: Zie afzonderlijke apparaatdubbels en relaties ophalen, bijwerken en verwijderen.
author: baanders
ms.author: baanders
ms.date: 4/10/2020
ms.topic: how-to
ms.service: digital-twins
ms.openlocfilehash: b88d017110f4d7b9859f2d801c5405ecee1589c5
ms.sourcegitcommit: 58d3b3314df4ba3cabd4d4a6016b22fa5264f05a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/02/2020
ms.locfileid: "89297464"
---
# <a name="manage-digital-twins"></a>Digitale tweelingen beheren

Entiteiten in uw omgeving worden vertegenwoordigd door [Digital apparaatdubbels](concepts-twins-graph.md). Het beheren van uw digitale apparaatdubbels kan het maken, wijzigen en verwijderen omvatten. Als u deze bewerkingen wilt uitvoeren, kunt u de [**DigitalTwins-api's**](how-to-use-apis-sdks.md), de [.net (C#) SDK](https://github.com/Azure/azure-sdk-for-net/tree/master/sdk/digitaltwins/Azure.DigitalTwins.Core)of de [Azure Digital apparaatdubbels cli](how-to-use-cli.md)gebruiken.

Dit artikel richt zich op het beheren van digitale apparaatdubbels; Zie [*How-to: manage the dubbele Graph with relationships*](how-to-manage-graph.md)als u wilt werken met relaties en de [dubbele grafiek](concepts-twins-graph.md) als geheel.

> [!TIP]
> Alle SDK-functies zijn beschikbaar in synchrone en asynchrone versies.

## <a name="create-a-digital-twin"></a>Een digitale dubbele

Als u een dubbele wilt maken, gebruikt u de `CreateDigitalTwin` methode op de service-client als volgt:

```csharp
await client.CreateDigitalTwinAsync("myNewTwinID", initData);
```

Als u een digitale dubbele wilt maken, moet u het volgende opgeven:
* De gewenste ID voor de digitale dubbele
* Het [model](concepts-models.md) dat u wilt gebruiken 

U kunt desgewenst initiële waarden opgeven voor alle eigenschappen van de digitale twee. 

De waarden van het model en de oorspronkelijke eigenschap worden gegeven via de `initData` para meter, een JSON-teken reeks met de relevante gegevens. Ga verder naar de volgende sectie voor meer informatie over het structureren van dit object.

> [!TIP]
> Na het maken of bijwerken van een dubbele, kan er een latentie van Maxi maal 10 seconden zijn voordat de wijzigingen in [query's](how-to-query-graph.md)worden weer gegeven. De `GetDigitalTwin` API ( [verderop in dit artikel](#get-data-for-a-digital-twin)) heeft deze vertraging niet. Gebruik daarom de API-aanroep in plaats van een query uit te voeren om de zojuist gemaakte apparaatdubbels te zien als u een direct antwoord nodig hebt. 

### <a name="initialize-model-and-properties"></a>Model en eigenschappen initialiseren

De twee keer dat er een API wordt gemaakt, accepteert een object dat is geserialiseerd in een geldige JSON-beschrijving van de dubbele eigenschappen. Zie [*concepten: Digital apparaatdubbels en de dubbele grafiek*](concepts-twins-graph.md) voor een beschrijving van de JSON-indeling voor een dubbele. 

Eerst maakt u een gegevens object dat de dubbele en de bijbehorende eigenschaps gegevens vertegenwoordigt. Vervolgens kunt u gebruiken `JsonSerializer` om een geserialiseerde versie van dit door te geven aan de API-aanroep voor de `initdata` para meter.

U kunt een parameter object hand matig of via een beschik bare helper-klasse maken. Hier volgt een voor beeld van elk.

#### <a name="create-twins-using-manually-created-data"></a>Apparaatdubbels maken met hand matig gemaakte gegevens

Als u geen aangepaste helper-klassen wilt gebruiken, kunt u de eigenschappen van een twee voor `Dictionary<string, object>` waarden in een, waarbij de de `string` naam van de eigenschap is en de `object` is een-object dat de eigenschap en de waarde vertegenwoordigt.

```csharp
// Define the model type for the twin to be created
Dictionary<string, object> meta = new Dictionary<string, object>()
{
    { "$model", "dtmi:com:contoso:Room;1" }
};
// Initialize the twin properties
Dictionary<string, object> twin = new Dictionary<string, object>()
{
    { "$metadata", meta },
    { "Temperature", temperature},
    { "Humidity", humidity},
};
client.CreateDigitalTwin("myNewRoomID", JsonSerializer.Serialize<Dictionary<string, object>>(twin));
```

#### <a name="create-twins-with-the-helper-class"></a>Apparaatdubbels maken met de helper-klasse

Met de Help-klasse van `BasicDigitalTwin` kunt u eigenschaps velden rechtstreeks in een ' twee ' object opslaan. Het is mogelijk dat u de lijst met eigenschappen wilt maken met behulp van een `Dictionary<string, object>` , die vervolgens rechtstreeks aan het dubbele object kan worden toegevoegd `CustomProperties` .

```csharp
BasicDigitalTwin twin = new BasicDigitalTwin();
twin.Metadata = new DigitalTwinMetadata();
twin.Metadata.ModelId = "dtmi:example:Room;1";
// Initialize properties
Dictionary<string, object> props = new Dictionary<string, object>();
props.Add("Temperature", 25.0);
props.Add("Humidity", 50.0);
twin.CustomProperties = props;

client.CreateDigitalTwin("myNewRoomID", JsonSerializer.Serialize<BasicDigitalTwin>(twin));
```

>[!NOTE]
> `BasicDigitalTwin` objecten worden geleverd met een `Id` veld. U kunt dit veld leeg laten, maar als u een ID-waarde toevoegt, moet deze overeenkomen met de ID-para meter die is door gegeven aan de `CreateDigitalTwin` aanroep. In het bovenstaande voor beeld ziet dit er als volgt uit:
>
>```csharp
>twin.Id = "myNewRoomID";
>```

## <a name="get-data-for-a-digital-twin"></a>Gegevens ophalen voor een digitale dubbele

U kunt toegang krijgen tot de volledige gegevens van elke digitale dubbele waarde door het volgende aan te roepen:

```csharp
object result = await client.GetDigitalTwin(id);
```

Deze aanroep retourneert twee gegevens als een JSON-teken reeks. 

Alleen eigenschappen die ten minste eenmaal zijn ingesteld, worden geretourneerd wanneer u een dubbele met ophaalt `GetDigitalTwin` .

>[!TIP]
>De `displayName` for a-server maakt deel uit van de meta gegevens van het model en wordt dus niet weer gegeven bij het ophalen van gegevens voor het dubbele exemplaar. Als u deze waarde wilt zien, kunt u [deze uit het model ophalen](how-to-manage-model.md#retrieve-models).

Als u meerdere apparaatdubbels met één API-aanroep wilt ophalen, raadpleegt u de query-API-voor beelden in [*de instructies: Query's uitvoeren op de dubbele grafiek*](how-to-query-graph.md).

Bekijk het volgende model (geschreven in [Digital Apparaatdubbels Definition Language (DTDL)](https://github.com/Azure/opendigitaltwins-dtdl/tree/master/DTDL)) dat een *maan*definieert:

```json
{
    "@id": " dtmi:com:contoso:Moon;1",
    "@type": "Interface",
    "@context": "dtmi:dtdl:context;2",
    "contents": [
        {
            "@type": "Property",
            "name": "radius",
            "schema": "double",
            "writable": true
        },
        {
            "@type": "Property",
            "name": "mass",
            "schema": "double",
            "writable": true
        }
    ]
}
```

Het resultaat van het aanroepen van `object result = await client.DigitalTwins.GetByIdAsync("my-moon");` een *maan*-type van twee kan er als volgt uitzien:

```json
{
  "$dtId": "myMoon-001",
  "$etag": "W/\"e59ce8f5-03c0-4356-aea9-249ecbdc07f9\"",
  "radius": 1737.1,
  "mass": 0.0734,
  "$metadata": {
    "$model": "dtmi:com:contoso:Moon;1",
    "radius": {
      "desiredValue": 1737.1,
      "desiredVersion": 5,
      "ackVersion": 4,
      "ackCode": 200,
      "ackDescription": "OK"
    },
    "mass": {
      "desiredValue": 0.0734,
      "desiredVersion": 8,
      "ackVersion": 8,
      "ackCode": 200,
      "ackDescription": "OK"
    }
  }
}
```

De gedefinieerde eigenschappen van de digitale twee worden geretourneerd als eigenschappen op het hoogste niveau van de digitale twee. Meta gegevens of systeem gegevens die geen deel uitmaken van de DTDL-definitie, worden geretourneerd met een `$` voor voegsel. Eigenschappen van meta gegevens zijn onder andere:
* De ID van de digitale dubbele in dit Azure Digital Apparaatdubbels-exemplaar, zoals `$dtId` .
* `$etag`, een standaard-HTTP-veld dat is toegewezen door de webserver
* Andere eigenschappen in een `$metadata` sectie. Deze omvatten:
    - De DTMI van het model van de digitale twee.
    - Synchronisatie status voor elke Beschrijf bare eigenschap. Dit is vooral nuttig voor apparaten, waar het mogelijk is dat de service en het apparaat afwijkende statussen hebben (bijvoorbeeld wanneer een apparaat offline is). Deze eigenschap is op dit moment alleen van toepassing op fysieke apparaten die zijn verbonden met IoT Hub. Met de gegevens in de sectie meta gegevens is het mogelijk inzicht te krijgen in de volledige status van een eigenschap, evenals de laatste gewijzigde tijds tempels. Zie voor meer informatie over de synchronisatie status [deze IOT hub zelf studie over het](../iot-hub/tutorial-device-twins.md) synchroniseren van de Apparaatstatus.
    - Servicespecifieke meta gegevens, zoals van IoT Hub of Azure Digital Apparaatdubbels. 

U kunt de geretourneerde JSON voor het dubbele parseren met behulp van een JSON-parserings bibliotheek van uw keuze, zoals `System.Text.Json` .

U kunt ook de klasse voor serialisatie helper gebruiken `BasicDigitalTwin` die deel uitmaakt van de SDK, waardoor de belangrijkste dubbele meta gegevens en eigenschappen in het vooraf geparseerde formulier worden geretourneerd. Hier volgt een voorbeeld:

```csharp
Response<string> res = client.GetDigitalTwin(twin_id);
BasicDigitalTwin twin = JsonSerializer.Deserialize<BasicDigitalTwin>(res.Value);
Console.WriteLine($"Model id: {twin.Metadata.ModelId}");
foreach (string prop in twin.CustomProperties.Keys)
{
    if (twin.CustomProperties.TryGetValue(prop, out object value))
        Console.WriteLine($"Property '{prop}': {value}");
}
```

Meer informatie over de hulp klassen voor serialisatie vindt u in [*How to: gebruik de Azure Digital Apparaatdubbels api's en sdk's*](how-to-use-apis-sdks.md).

## <a name="update-a-digital-twin"></a>Een digital twin bijwerken

Als u de eigenschappen van een digitale dubbele eigenschap wilt bijwerken, schrijft u de gegevens die u wilt vervangen in de indeling van de [JSON-patch](http://jsonpatch.com/) . Op deze manier kunt u meerdere eigenschappen tegelijk vervangen. Vervolgens geeft u het JSON-patch document door aan een `Update` methode:

```csharp
await client.UpdateDigitalTwin(id, patch);
```

Een patch-oproep kan zoveel eigenschappen op een enkele dubbele manier bijwerken als u wilt (zelfs al deze). Als u eigenschappen voor meerdere apparaatdubbels wilt bijwerken, hebt u een afzonderlijke update aanroep voor elke dubbele taak nodig.

> [!TIP]
> Na het maken of bijwerken van een dubbele, kan er een latentie van Maxi maal 10 seconden zijn voordat de wijzigingen in [query's](how-to-query-graph.md)worden weer gegeven. De `GetDigitalTwin` API ( [eerder in dit artikel](#get-data-for-a-digital-twin)beschreven) heeft deze vertraging niet. Gebruik daarom de API-aanroep in plaats van een query uit te voeren om de zojuist bijgewerkte apparaatdubbels te zien als u een direct antwoord nodig hebt. 

Hier volgt een voor beeld van de JSON-patch code. Dit document vervangt de *massa* *-en RADIUS-* eigenschaps waarden van de digitale dubbele waarde die wordt toegepast op.

```json
[
  {
    "op": "replace",
    "path": "/mass",
    "value": 0.0799
  },
  {
    "op": "replace",
    "path": "/radius",
    "value": 0.800
  }
]
```

U kunt patches hand matig maken, of met behulp van een serialisatie helper-klasse in de [SDK](how-to-use-apis-sdks.md). Hier volgt een voor beeld van elk.

#### <a name="create-patches-manually"></a>Hand matig patches maken

```csharp
List<object> twinData = new List<object>();
twinData.Add(new Dictionary<string, object>() {
    { "op", "add"},
    { "path", "/Temperature"},
    { "value", 25.0}
});

await client.UpdateDigitalTwinAsync(twinId, JsonConvert.SerializeObject(twinData));
```

#### <a name="create-patches-using-the-helper-class"></a>Patches maken met behulp van de helper-klasse

```csharp
UpdateOperationsUtility uou = new UpdateOperationsUtility();
uou.AppendAddOp("/Temperature", 25.0);
await client.UpdateDigitalTwinAsync(twinId, uou.Serialize());
```

### <a name="update-properties-in-digital-twin-components"></a>Eigenschappen in digitale dubbele onderdelen bijwerken

Intrekken dat een model onderdelen kan bevatten, zodat het kan bestaan uit andere modellen. 

Als u de eigenschappen van een digitale twee onderdelen wilt bijwerken, gebruikt u de syntaxis Path in JSON patch:

```json
[
  {
    "op": "replace",
    "path": "/mycomponentname/mass",
    "value": 0.0799
  }
]
```

### <a name="update-a-digital-twins-model"></a>Een digitaal onderliggend model bijwerken

De `Update` functie kan ook worden gebruikt om een digitale dubbele naar een ander model te migreren. 

Bekijk bijvoorbeeld het volgende document van de JSON-patch dat het meta gegevens veld van de digitale twee vervangt `$model` :

```json
[
  {
    "op": "replace",
    "path": "/$metadata/$model",
    "value": "dtmi:com:contoso:foo;1"
  }
]
```

Deze bewerking slaagt alleen als de digitale dubbele wijziging door de patch voldoet aan het nieuwe model. 

Kijk eens naar het volgende voorbeeld:
1. Stel dat een digitale twee maal een model van *foo_old*. *foo_old* definieert een vereiste eigenschaps *massa*.
2. Het nieuwe model *foo_new* definieert een eigenschaps massa en voegt een nieuwe vereiste *temperatuur*van de eigenschap toe.
3. Na de patch moet de digitale twee eigenschappen een massa-en temperatuur eigenschap hebben. 

Voor de patch voor deze situatie moet het model en de eigenschap Tempe ratuur van twee zaken worden bijgewerkt, zoals:

```json
[
  {
    "op": "replace",
    "path": "$metadata.$model",
    "value": "dtmi:com:contoso:foo_new"
  },
  {
    "op": "add",
    "path": "temperature",
    "value": 60
  }
]
```

### <a name="handle-conflicting-update-calls"></a>Conflicterende Update aanroepen verwerken

Azure Digital Apparaatdubbels zorgt ervoor dat alle inkomende aanvragen na elkaar worden verwerkt. Dit betekent dat zelfs als meerdere functies dezelfde eigenschap op een twee keer proberen bij te werken, u geen expliciete vergrendelings code **hoeft** te schrijven om het conflict af te handelen.

Dit gedrag bevindt zich op twee afzonderlijke basis. 

Stel dat er een scenario is waarin deze drie aanroepen gelijktijdig aankomen: 
*   Eigenschap A op *Twin1* schrijven
*   Schrijf eigenschap B op *Twin1*
*   Eigenschap A op *Twin2* schrijven

De twee aanroepen die *Twin1* wijzigen, worden na elkaar uitgevoerd en er worden wijzigings berichten voor elke wijziging gegenereerd. De aanroep om *Twin2* te wijzigen kan gelijktijdig zonder conflict worden uitgevoerd, zodra deze is binnengekomen.

## <a name="delete-a-digital-twin"></a>Een digitale dubbele

U kunt apparaatdubbels verwijderen met `DeleteDigitalTwin(ID)` . U kunt echter alleen een dubbele waarde verwijderen als deze geen relaties meer heeft. U moet eerst alle relaties verwijderen. 

Hier volgt een voor beeld van de code voor dit:

```csharp
static async Task DeleteTwin(string id)
{
    await FindAndDeleteOutgoingRelationshipsAsync(id);
    await FindAndDeleteIncomingRelationshipsAsync(id);
    try
    {
        await client.DeleteDigitalTwin(id);
    } catch (RequestFailedException exc)
    {
        Console.WriteLine($"*** Error:{exc.Error}/{exc.Message}");
    }
}

public async Task FindAndDeleteOutgoingRelationshipsAsync(string dtId)
{
    // Find the relationships for the twin

    try
    {
        // GetRelationshipsAsync will throw an error if a problem occurs
        AsyncPageable<string> relsJson = client.GetRelationshipsAsync(dtId);

        await foreach (string relJson in relsJson)
        {
            var rel = System.Text.Json.JsonSerializer.Deserialize<BasicRelationship>(relJson);
            await client.DeleteRelationshipAsync(dtId, rel.Id).ConfigureAwait(false);
            Log.Ok($"Deleted relationship {rel.Id} from {dtId}");
        }
    }
    catch (RequestFailedException ex)
    {
        Log.Error($"*** Error {ex.Status}/{ex.ErrorCode} retrieving or deleting relationships for {dtId} due to {ex.Message}");
    }
}

async Task FindAndDeleteIncomingRelationshipsAsync(string dtId)
{
    // Find the relationships for the twin

    try
    {
        // GetRelationshipssAsync will throw an error if a problem occurs
        AsyncPageable<IncomingRelationship> incomingRels = client.GetIncomingRelationshipsAsync(dtId);

        await foreach (IncomingRelationship incomingRel in incomingRels)
        {
            await client.DeleteRelationshipAsync(incomingRel.SourceId, incomingRel.RelationshipId).ConfigureAwait(false);
            Log.Ok($"Deleted incoming relationship {incomingRel.RelationshipId} from {dtId}");
        }
    }
    catch (RequestFailedException ex)
    {
        Log.Error($"*** Error {ex.Status}/{ex.ErrorCode} retrieving or deleting incoming relationships for {dtId} due to {ex.Message}");
    }
}
```

### <a name="delete-all-digital-twins"></a>Alle digitale apparaatdubbels verwijderen

Voor een voor beeld van het verwijderen van alle apparaatdubbels in een keer, downloadt u de voor beeld-app die wordt gebruikt in de [*zelf studie: Verken de basis principes met een voor beeld-client-app*](tutorial-command-line-app.md). Het *CommandLoop.cs* -bestand doet dit in een `CommandDeleteAllTwins` functie.

## <a name="manage-twins-with-cli"></a>Apparaatdubbels beheren met CLI

Apparaatdubbels kan ook worden beheerd met behulp van de Azure Digital Apparaatdubbels CLI. De opdrachten zijn te vinden in [*How to: gebruik de Azure Digital APPARAATDUBBELS cli*](how-to-use-cli.md).

[!INCLUDE [digital-twins-known-issue-cloud-shell](../../includes/digital-twins-known-issue-cloud-shell.md)]

## <a name="next-steps"></a>Volgende stappen

Zie relaties tussen uw digitale apparaatdubbels maken en beheren:
* [*Instructies: de dubbele grafiek met relaties beheren*](how-to-manage-graph.md)