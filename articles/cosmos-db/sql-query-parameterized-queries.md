---
title: Query's met para meters in Azure Cosmos DB
description: Meer informatie over hoe SQL-query's met para meters krachtige verwerking en Escapes van gebruikers invoer bieden en voor komen dat gegevens per ongeluk worden blootgesteld via SQL-injectie.
author: timsander1
ms.service: cosmos-db
ms.topic: conceptual
ms.date: 07/29/2020
ms.author: tisande
ms.openlocfilehash: f66bc89ef56dd0c2291903d531a4637210abd8df
ms.sourcegitcommit: 11e2521679415f05d3d2c4c49858940677c57900
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/31/2020
ms.locfileid: "87496981"
---
# <a name="parameterized-queries-in-azure-cosmos-db"></a>Query's met para meters in Azure Cosmos DB

Azure Cosmos DB ondersteunt query's met para meters die worden uitgedrukt in de vertrouwde @-notatie. SQL met para meters biedt een robuuste afhandeling en Escape van de invoer van gebruikers en voor komt onopzettelijke bloot stelling van gegevens via SQL-injectie.

## <a name="examples"></a>Voorbeelden

U kunt bijvoorbeeld een query schrijven die `lastName` en `address.state` als para meters, en deze uitvoeren voor diverse waarden van `lastName` en op `address.state` basis van gebruikers invoer.

```sql
    SELECT *
    FROM Families f
    WHERE f.lastName = @lastName AND f.address.state = @addressState
```

U kunt deze aanvraag vervolgens naar Azure Cosmos DB verzenden als een geparametriseerde JSON-query, zoals in het volgende:

```sql
    {
        "query": "SELECT * FROM Families f WHERE f.lastName = @lastName AND f.address.state = @addressState",
        "parameters": [
            {"name": "@lastName", "value": "Wakefield"},
            {"name": "@addressState", "value": "NY"},
        ]
    }
```

In het volgende voor beeld wordt het bovenste argument met een query met para meters ingesteld:

```sql
    {
        "query": "SELECT TOP @n * FROM Families",
        "parameters": [
            {"name": "@n", "value": 10},
        ]
    }
```

Parameter waarden kunnen bestaan uit een geldige JSON: teken reeksen, getallen, Booleaanse waarden, null, zelfs matrices of geneste JSON. Omdat Azure Cosmos DB schemaloos is, worden para meters niet gevalideerd op basis van elk type.

Hier volgen enkele voor beelden van query's met para meters in elke Azure Cosmos DB-SDK:

- [.NET SDK](https://github.com/Azure/azure-cosmos-dotnet-v3/blob/master/Microsoft.Azure.Cosmos.Samples/Usage/Queries/Program.cs#L195)
- [Java](https://github.com/Azure-Samples/azure-cosmos-java-sql-api-samples/blob/master/src/main/java/com/azure/cosmos/examples/queries/sync/QueriesQuickstart.java#L392-L421)
- [Node.js](https://github.com/Azure/azure-cosmos-js/blob/master/samples/ItemManagement.ts#L58-L79)
- [Python](https://github.com/Azure/azure-sdk-for-python/blob/master/sdk/cosmos/azure-cosmos/samples/document_management.py#L66-L78)

## <a name="next-steps"></a>Volgende stappen

- [.NET-voorbeelden voor Azure Cosmos DB](https://github.com/Azure/azure-cosmos-dotnet-v3)
- [Documentgegevens modelleren](modeling-data.md)
