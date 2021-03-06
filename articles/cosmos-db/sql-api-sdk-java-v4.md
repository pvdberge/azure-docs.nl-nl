---
title: Opmerkingen en bronnen voor de release van Java SDK v4 voor SQL API Azure Cosmos DB
description: Meer informatie over de Azure Cosmos DB Java SDK v4 voor SQL-API en SDK, inclusief release datums, pensioen datums en wijzigingen die zijn aangebracht tussen elke versie van de Azure Cosmos DB SQL async Java SDK.
author: anfeldma-ms
ms.service: cosmos-db
ms.subservice: cosmosdb-sql
ms.devlang: java
ms.topic: reference
ms.date: 08/12/2020
ms.author: anfeldma
ms.custom: devx-track-java
ms.openlocfilehash: aabd52d47bfc59de7a1d79bbe5ffbdda90d099bf
ms.sourcegitcommit: 51df05f27adb8f3ce67ad11d75cb0ee0b016dc5d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/14/2020
ms.locfileid: "90060693"
---
# <a name="azure-cosmos-db-java-sdk-v4-for-core-sql-api-release-notes-and-resources"></a>Azure Cosmos DB Java SDK v4 for core (SQL) API: release opmerkingen en bronnen
> [!div class="op_single_selector"]
> * [.NET SDK v3](sql-api-sdk-dotnet-standard.md)
> * [.NET SDK v2](sql-api-sdk-dotnet.md)
> * [.NET Core-SDK v2](sql-api-sdk-dotnet-core.md)
> * [.NET Change feed SDK v2](sql-api-sdk-dotnet-changefeed.md)
> * [Node.js](sql-api-sdk-node.md)
> * [Java SDK v4](sql-api-sdk-java-v4.md)
> * [Async Java-SDK v2](sql-api-sdk-async-java.md)
> * [Sync Java-SDK v2](sql-api-sdk-java.md)
> * [Lente gegevens v2](sql-api-sdk-java-spring-v2.md)
> * [Lente gegevens v3](sql-api-sdk-java-spring-v3.md)
> * [Spark-connector](sql-api-sdk-java-spark.md)
> * [Python](sql-api-sdk-python.md)
> * [REST](/rest/api/cosmos-db/)
> * [REST-resourceprovider](/rest/api/cosmos-db-resource-provider/)
> * [SQL](sql-api-query-reference.md)
> * [Bulk-uitvoerder-.NET v2](sql-api-sdk-bulk-executor-dot-net.md)
> * [Bulk-uitvoerder-java](sql-api-sdk-bulk-executor-java.md)

De Azure Cosmos DB Java SDK v4 for core (SQL) combineert een async API en een API voor synchronisatie in één maven-artefact. De v4-SDK biedt verbeterde prestaties, nieuwe API-functies en async-ondersteuning op basis van project reactor en de [Netty-bibliotheek](https://netty.io/). Gebruikers kunnen betere prestaties verwachten met Azure Cosmos DB Java SDK v4 versus de [Azure Cosmos DB async Java SDK v2](sql-api-sdk-async-java.md) en de [Azure Cosmos DB Java SDK v2 te synchroniseren](sql-api-sdk-java.md).

> [!IMPORTANT]  
> Deze release opmerkingen zijn alleen voor Azure Cosmos DB Java SDK v4. Als u momenteel een oudere versie dan v4 gebruikt, raadpleegt u de gids [Migreren naar Azure Cosmos DB Java SDK v4](migrate-java-v4-sdk.md) voor hulp om te upgraden naar v4.
>
> Hier volgen drie stappen om snel aan de slag te gaan.
> 1. Installeer de [Mini maal ondersteunde Java-runtime, JDK 8](/java/azure/jdk/?view=azure-java-stable) , zodat u de SDK kunt gebruiken.
> 2. Werk aan de [Snelstartgids voor Azure Cosmos DB Java SDK v4](https://docs.microsoft.com/azure/cosmos-db/create-sql-api-java) , waarmee u toegang krijgt tot het maven-artefact en basis Azure Cosmos DB aanvragen doorloopt.
> 3. Lees de Azure Cosmos DB Java SDK v4- [prestatie tips](performance-tips-java-sdk-v4-sql.md) en richt lijnen voor [probleem oplossing](troubleshoot-java-sdk-v4-sql.md) om de SDK voor uw toepassing te optimaliseren.
>
> De [Azure Cosmos DB workshops en Labs](https://aka.ms/cosmosworkshop) zijn een fantastische resource om te leren hoe u Azure Cosmos DB Java SDK v4 kunt gebruiken.
>

## <a name="helpful-content"></a>Nuttige inhoud

| Content | Koppeling |
|---|---|
|**SDK downloaden**| [Maven](https://mvnrepository.com/artifact/com.azure/azure-cosmos) |
|**API-documentatie** | [Naslag documentatie voor Java API](https://docs.microsoft.com/java/api/overview/azure/cosmosdb/client?view=azure-java-stable) |
|**Bijdragen aan SDK** | [Azure SDK voor Java Central opslag plaats op GitHub](https://github.com/Azure/azure-sdk-for-java/tree/master/sdk/cosmos/azure-cosmos) | 
|**Aan de slag** | [Quickstart: Een Java-app bouwen om Azure Cosmos DB SQL API-gegevens te beheren](https://docs.microsoft.com/azure/cosmos-db/create-sql-api-java) <br> [GitHub opslag plaats met Quick Start-code](https://github.com/Azure-Samples/azure-cosmos-java-getting-started) | 
|**Basic-code voorbeelden** | [Azure Cosmos DB: Java-voorbeelden voor de SQL API](sql-api-java-sdk-samples.md) <br> [GitHub opslag plaats met voorbeeld code](https://github.com/Azure-Samples/azure-cosmos-java-sql-api-samples)|
|**Console-app met wijzigings feed**| [Wijzigings feed-Java SDK v4-voor beeld](create-sql-api-java-changefeed.md) <br> [GitHub opslag plaats met voorbeeld code](https://github.com/Azure-Samples/azure-cosmos-java-sql-app-example)| 
|**Voor beeld van web-app**| [Een web-app bouwen met Java SDK v4](sql-api-java-application.md) <br> [GitHub opslag plaats met voorbeeld code](https://github.com/Azure-Samples/azure-cosmos-java-sql-api-todo-app)|
| **Tips voor prestaties**| [Tips voor betere prestaties voor de Java-SDK v4](performance-tips-java-sdk-v4-sql.md)| 
| **Problemen oplossen** | [Problemen met Java-SDK v4 oplossen](troubleshoot-java-sdk-v4-sql.md) |
| **Migreren naar v4 vanuit een oudere SDK** | [Migreren naar Java v4-SDK](migrate-java-v4-sdk.md) |
| **Minimale ondersteunde runtime**|[JDK 8](/java/azure/jdk/?view=azure-java-stable) | 
| **Azure Cosmos DB workshops en Labs** |[Start pagina van Cosmos DB workshops](https://aka.ms/cosmosworkshop)

## <a name="release-history"></a>Release geschiedenis

### <a name="450-beta1-unreleased"></a>4.5.0-bèta versie 1 (niet-vrijgegeven)

### <a name="440-2020-09-12"></a>4.4.0 (2020-09-12)
#### <a name="key-bug-fixes"></a>Oplossingen voor belang rijke fouten
* Vaste RequestTimeoutException bij het inschakelen van `netty-tcnative-boringssl` afhankelijkheid.
* Probleem met het lek van het opgeloste geheugen voor `Delete` bewerkingen in de `GATEWAY` modus.
* Er is een lekkage opgelost `CosmosClient` tijdens het instantiëren wanneer de eind punt-URI ongeldig is.
* Verbeterde `CPU History` Diagnostische gegevens.

### <a name="431-2020-08-13"></a>4.3.1 (2020-08-13)
#### <a name="key-bug-fixes"></a>Oplossingen voor belang rijke fouten
* `GROUP BY`Er is een probleem opgelost met een query, waarbij slechts één pagina werd geretourneerd.
* Vaste teken reeks indeling van de gebruikers agent om te voldoen aan de richt lijnen voor de Central SDK.
* Uitgebreide diagnostische informatie voor het toevoegen van diagnostische gegevens over het query plan.

### <a name="430-2020-07-29"></a>4.3.0 (2020-07-29)
#### <a name="new-features"></a>Nieuwe functies
* Bijgewerkte versie van de reactor-kern bibliotheek naar `3.3.8.RELEASE` . 
* De Netty-bibliotheek versie is bijgewerkt naar `0.9.10.RELEASE` . 
* De versie van de Netty-bibliotheek is bijgewerkt naar `4.1.51.Final` . 
* Er zijn nieuwe overload-Api's toegevoegd voor `upsertItem` met `partitionKey` . 
* Ondersteuning voor open telemetrie-tracering is toegevoegd. 
#### <a name="key-bug-fixes"></a>Oplossingen voor belang rijke fouten
* Er is een probleem opgelost waarbij SSLException wordt gegenereerd in het geval van annulering van aanvragen in de modus GATEWAY.
* Beleid voor opnieuw proberen van geregelde procedures voor het uitvoeren van een aanvraag
* Er is een probleem opgelost waarbij SDK vastloopt in de modus voor fout opsporing op logboek niveau. 
* Vaste periodieke pieken in latentie in directe modus. 
* Er is een fout opgetreden bij het uitvoeren van een hoge client initialisatie tijd. 
* Vaste http-proxy fout bij het aanpassen van de client met de directe modus en de gateway modus. 
* Met vaste mogelijke NPE in gebruikers worden Null-opties door gegeven. 
* TimeUnit toegevoegd aan `requestLatency` in de diagnostische teken reeks.
* Dubbele URI-teken reeks uit de diagnostische teken reeks verwijderd. 
* Vaste diagnose teken reeks in de juiste JSON-indeling voor punt bewerkingen.
* Probleem opgelost met `.single()` de operator, waardoor de reactor keten in het geval van een niet-gevonden uitzonde ring optreedt. 

### <a name="420-2020-07-14"></a>4.2.0 (2020-07-14)
#### <a name="new-features"></a>Nieuwe functies
* De API voor script logboek registratie is ingeschakeld `CosmosStoredProcedureRequestOptions` .
* De `DirectConnectionConfig` standaard waarde is bijgewerkt `idleEndpointTimeout` naar 1U en standaard ingesteld `connectTimeout` op 5s.
#### <a name="key-bug-fixes"></a>Oplossingen voor belang rijke fouten
* Er is een probleem opgelost waarbij `GatewayConnectionConfig` `idleConnectionTimeout` het is overschreven `DirectConnectionConfig` `idleConnectionTimeout` .
* `responseContinuationTokenLimitInKb`Get en set api's in `CosmosQueryRequestOptions` .
* Er is een probleem opgelost in de query-en wijzigings feed bij het opnieuw maken van de verzameling met dezelfde naam.
* Probleem opgelost met top query-ClassCastException.
* Probleem opgelost met order by query NullPointerException.
* Probleem opgelost in de verwerking van geannuleerde aanvragen in de directe modus waardoor reactor `onErrorDropped` wordt aangeroepen. 

### <a name="410-2020-06-25"></a>4.1.0 (2020-06-25)
#### <a name="new-features"></a>Nieuwe functies
* Er is ondersteuning toegevoegd voor de `GROUP BY` query.
* De standaard waarde van maxConnectionsPerEndpoint is verhoogd naar 130 in DirectConnectionConfig.
* De standaard waarde van maxRequestsPerConnection is verhoogd naar 30 in DirectConnectionConfig.
#### <a name="key-bug-fixes"></a>Oplossingen voor belang rijke fouten
* Opgeloste problemen met order by query waarbij dubbele resultaten worden geretourneerd tijdens het hervatten met behulp van vervolg token. 
* Opgeloste problemen met een waarde-query die Null-waarden retourneert voor een genest object.
* Uitzonde ring voor een vaste null-aanwijzer op Request manager in RntbdClientChannelPool.

### <a name="401-2020-06-10"></a>4.0.1 (2020-06-10)
#### <a name="new-features"></a>Nieuwe functies
* De naam is gewijzigd `QueryRequestOptions` in `CosmosQueryRequestOptions` .
* Bijgewerkt `ChangeFeedProcessorBuilder` naar Builder-patroon.
* Bijgewerkt `CosmosPermissionProperties` met de nieuwe container naam en onderliggende bronnen-api's.
* Meer voor beelden & verrijkte documenten toegevoegd `CosmosClientBuilder` . 
* `CosmosDatabase`  &  `CosmosContainer` Api's bijgewerkt met throughputProperties voor ondersteuning bij automatisch schalen/auto pilot. 
* De naam is gewijzigd `CosmosClientException` in `CosmosException` . 
* Vervangen `AccessCondition`  &  `AccessConditionType` door `ifMatchETag()`  &  `ifNoneMatchETag()` api's. 
* Alle typen zijn samengevoegd `Cosmos*AsyncResponse`  &  `CosmosResponse` tot één `CosmosResponse` type.
* De naam is gewijzigd `CosmosResponseDiagnostics` in `CosmosDiagnostics` .  
* Ingepakt `FeedResponseDiagnostics` in `CosmosDiagnostics` . 
* De `jackson` afhankelijkheid van Azure-Cosmos is verwijderd & afhankelijk zijn van Azure core. 
* Vervangen `CosmosKeyCredential` door `AzureKeyCredential` type. 
* Api's zijn toegevoegd `ProxyOptions` aan `GatewayConnectionConfig` . 
* Bijgewerkte SDK voor gebruik `Instant` van type in plaats van `OffsetDateTime` . 
* Nieuw opsommings type toegevoegd `OperationKind` . 
* De naam is gewijzigd `FeedOptions` in `QueryRequestOptions` . 
* Api's zijn toegevoegd `getETag()`  &  `getTimestamp()` aan de `Cosmos*Properties` typen. 
* Er zijn `userAgent` gegevens toegevoegd in `CosmosException`  &  `CosmosDiagnostics` . 
* Het nieuwe regel teken is bijgewerkt `Diagnostics` naar het nieuwe regel teken van het systeem. 
* `readAll*`Api's zijn verwijderd. gebruik in plaats daarvan de query alle api's selecteren.
* De `ChangeFeedProcessor` API voor de schattings vertraging is toegevoegd.   
* Ondersteuning voor automatisch schalen/auto pilot-inrichting voor door Voer is toegevoegd aan SDK.  
* Vervangen `ConnectionPolicy` door nieuwe verbindings configuraties. Blootgestelde `DirectConnectionConfig`  &  `GatewayConnectionConfig` api's via `CosmosClientBuilder` voor directe & gateway modus verbindings configuraties.
* Verplaatst `JsonSerializable`  &  `Resource` naar implementatie pakket. 
* `contentResponseOnWriteEnabled`API toegevoegd aan CosmosClientBuilder, waarmee de inhoud van de volledige reactie voor schrijf bewerkingen wordt uitgeschakeld.
* Blootgestelde `getETag()` api's op antwoord typen.
* Verplaatst `CosmosAuthorizationTokenResolver` naar implementatie. 
* De naam van de API is gewijzigd `preferredLocations`  &  `multipleWriteLocations` in `preferredRegions`  &  `multipleWriteRegions` . 
* `reactor-core`Is bijgewerkt naar 3.3.5. release, `reactor-netty` naar 0.9.7. release & `netty` naar 4.1.49. Final verse. 
* Er is ondersteuning toegevoegd voor `analyticalStoreTimeToLive` in SDK.     
* `CosmosClientException` wordt uitgebreid `AzureException` . 
* `maxItemCount`  &  `requestContinuationToken` Api's zijn uit `FeedOptions` plaats daarvan verwijderd met behulp `byPage()` van api's van `CosmosPagedFlux`  &  `CosmosPagedIterable` .
* Geïntroduceerd `CosmosPermissionProperties` in het open bare Opper vlak voor `Permission` api's.
* Verwijderd `SqlParameterList` type & vervangen door `List`
* Opgelost meerdere geheugen lekken in directe TCP-client. 
* Er is ondersteuning toegevoegd voor `DISTINCT` query's. 
* Externe afhankelijkheden zijn verwijderd op `fasterxml.uuid, guava, commons-io, commons-collection4, commons-text` .  
* Verplaatst `CosmosPagedFlux`  &  `CosmosPagedIterable` naar het `utils` pakket. 
* De Netty is bijgewerkt naar 4.1.45. Final & project-reactor naar 3.3.3-versie.
* De open bare rest-contracten worden bijgewerkt naar `Final` klassen.
* Er is ondersteuning toegevoegd voor geavanceerde diagnostische gegevens voor punt bewerkingen.
* Pakket bijgewerkt naar `com.azure.cosmos`
* `models`Pakket toegevoegd voor model/rest-contracten
* `utils`Pakket toegevoegd voor `CosmosPagedFlux`  &  `CosmosPagedIterable` typen. 
* Bijgewerkte open bare Api's voor gebruik `Duration` in de SDK.
* Alle rest contracten aan het `models` pakket zijn toegevoegd.
* `RetryOptions` de naam is gewijzigd in `ThrottlingRetryOptions` .
* `CosmosPagedFlux`  &  `CosmosPagedIterable` Paginerings typen zijn toegevoegd voor query-api's. 
* Er is ondersteuning toegevoegd voor het delen van TransportClient over meerdere exemplaren van CosmosClients met een nieuwe API in de `CosmosClientBuilder#connectionSharingAcrossClientsEnabled(true)`
* Query optimalisatie door dubbele serialisatie/deserialisatie te verwijderen. 
* De antwoord headers worden geoptimaliseerd door onnodig kopiëren terug en heen te verwijderen. 
* Geoptimaliseerde `ByteBuffer` serialisatie/deserialisatie door tussenliggende teken reeks-exemplaren te verwijderen.

#### <a name="key-bug-fixes"></a>Oplossingen voor belang rijke fouten
* Uitzonde `toString()` ring voor Connection Policy null-pointer.
* Probleem opgelost bij het parseren van de query resultaten in het geval van een waarde in de volg orde van query's. 
* Problemen met opgeloste socket lekkage met directe TCP-client.
* Opgelost `orderByQuery` met vervolg token fout.
* `ChangeFeedProcessor` fout oplossing voor het afsplitsen van partities & wanneer de partitie niet is gevonden.
* `ChangeFeedProcessor` fout oplossing bij het synchroniseren van lease-updates tussen verschillende threads.
* Er is een `ArrayIndexOutOfBound` uitzonde ring opgetreden in StoreReader vanwege een vaste race

## <a name="faq"></a>Veelgestelde vragen
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="next-steps"></a>Volgende stappen
Zie [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service-pagina voor meer informatie over Cosmos db.