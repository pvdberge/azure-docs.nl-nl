---
title: 'Azure Cosmos DB: SQL async Java API, SDK & resources'
description: Meer informatie over de SQL async Java API en SDK, inclusief release datums, pensioen datums en wijzigingen die zijn aangebracht tussen elke versie van de Azure Cosmos DB SQL async Java SDK.
author: anfeldma-ms
ms.service: cosmos-db
ms.subservice: cosmosdb-sql
ms.devlang: java
ms.topic: reference
ms.date: 08/12/2020
ms.author: anfeldma
ms.custom: devx-track-java
ms.openlocfilehash: b8f45fe07b825008b673534bcc3b28b9364c4cae
ms.sourcegitcommit: 02ca0f340a44b7e18acca1351c8e81f3cca4a370
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/19/2020
ms.locfileid: "88587290"
---
# <a name="azure-cosmos-db-async-java-sdk-for-sql-api-release-notes-and-resources"></a>Azure Cosmos DB asynchrone Java-SDK voor SQL API: release opmerkingen en bronnen
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
> * BERUST (/rest/api
> * [REST-resourceprovider](/azure/azure-resource-manager/management/azure-services-resource-providers)
> * [SQL](sql-api-query-reference.md)
> * [Bulk-uitvoerder-.NET v2](sql-api-sdk-bulk-executor-dot-net.md)
> * [Bulk-uitvoerder-java](sql-api-sdk-bulk-executor-java.md)

De SQL API async Java SDK wijkt af van de SQL API Java SDK door asynchrone bewerkingen te bieden met ondersteuning voor de [Netty-bibliotheek](https://netty.io/). De vooraf bestaande [SQL API Java-SDK](sql-api-sdk-java.md) biedt geen ondersteuning voor asynchrone bewerkingen. 

> [!IMPORTANT]  
> Dit is *niet* de meest recente Java-SDK voor Azure Cosmos db. Overweeg [Azure Cosmos DB Java SDK v4](sql-api-sdk-java-v4.md) te gebruiken voor uw project. Als u een upgrade wilt uitvoeren, volgt u de instructies in de hand leiding [Migrate to Azure Cosmos DB Java SDK v4](migrate-java-v4-sdk.md) and the [reactor VS RxJava](https://github.com/Azure-Samples/azure-cosmos-java-sql-api-samples/blob/master/reactor-rxjava-guide.md) . 
>

| |  |
|---|---|
| **SDK downloaden** | [Maven](https://mvnrepository.com/artifact/com.microsoft.azure/azure-cosmosdb) |
|**API-documentatie** |[Naslag documentatie voor Java API](https://docs.microsoft.com/java/api/com.microsoft.azure.cosmosdb.rx.asyncdocumentclient?view=azure-java-stable) | 
|**Bijdragen aan SDK** | [GitHub](https://github.com/Azure/azure-cosmosdb-java) | 
|**Aan de slag** | [Aan de slag met de asynchrone Java-SDK](https://github.com/Azure-Samples/azure-cosmos-db-sql-api-async-java-getting-started) | 
|**Codevoorbeeld** | [GitHub](https://github.com/Azure/azure-cosmosdb-java#usage-code-sample)| 
| **Tips voor prestaties**| [GitHub Leesmij](https://github.com/Azure/azure-cosmosdb-java#guide-for-prod)| 
| **Minimale ondersteunde runtime**|[JDK 8](/java/azure/jdk/?view=azure-java-stable) | 

[!INCLUDE [Release notes](~/azure-cosmosdb-java-v2/changelog/README.md)]
## <a name="faq"></a>Veelgestelde vragen
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a>Zie ook
Zie [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) service-pagina voor meer informatie over Cosmos db.

