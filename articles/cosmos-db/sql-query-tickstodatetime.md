---
title: TicksToDateTime in Azure Cosmos DB-query taal
description: Meer informatie over de SQL-functie TicksToDateTime in Azure Cosmos DB.
author: timsander1
ms.service: cosmos-db
ms.topic: conceptual
ms.date: 08/18/2020
ms.author: tisande
ms.custom: query-reference
ms.openlocfilehash: 89a8dba97725049b86fc6b38c09e0dd125bb48d1
ms.sourcegitcommit: d661149f8db075800242bef070ea30f82448981e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/19/2020
ms.locfileid: "88608772"
---
# <a name="tickstodatetime-azure-cosmos-db"></a>TicksToDateTime (Azure Cosmos DB)

Converteert de opgegeven waarde voor Ticks naar een datum/tijd.
  
## <a name="syntax"></a>Syntaxis
  
```sql
TicksToDateTime (<Ticks>)
```

## <a name="arguments"></a>Argumenten

*Ticks*  

Een ondertekende numerieke waarde, het huidige aantal 100 nano seconden-maat streepjes dat is verstreken sinds de UNIX-epoche. Met andere woorden: het is het aantal 100 nano seconden-maat streepjes dat sinds 00:00:00 donderdag, 1 januari 1970, is verstreken.

## <a name="return-types"></a>Retour typen

Retourneert de UTC-datum en-8601 tijd teken reeks waarde in de notatie `YYYY-MM-DDThh:mm:ss.fffffffZ` waar:
  
  |Indeling|Beschrijving|
  |-|-|
  |DD|jaar met vier cijfers|
  |MM|maand van twee cijfers (01 = januari, etc.)|
  |AFSCHRIJVING|2-cijferige dag van de maand (01 tot en met 31)|
  |T|de aanzienlijke voor het begin van de tijd elementen|
  |hh|twee cijfers per uur (00 tot en met 23)|
  |mm|twee cijfers minuten (00 tot en met 59)|
  |ss|seconden van twee cijfers (00 tot en met 59)|
  |.fffffff|aantal seconden van zeven cijfers|
  |Z|UTC (Coordinated Universal Time)||
  
  Zie [ISO_8601](https://en.wikipedia.org/wiki/ISO_8601) voor meer informatie over de ISO 8601-indeling.

## <a name="remarks"></a>Opmerkingen

TicksToDateTime wordt geretourneerd `undefined` als de opgegeven waarde voor de tickas ongeldig is.

## <a name="examples"></a>Voorbeelden
  
In het volgende voor beeld worden de maat streepjes geconverteerd naar een datum/tijd:

```sql
SELECT TicksToDateTime(15943368134575530) AS DateTime
```

```json
[
    {
        "DateTime": "2020-07-09T23:20:13.4575530Z"
    }
]
```  

## <a name="next-steps"></a>Volgende stappen

- [Datum-en tijd functies Azure Cosmos DB](sql-query-date-time-functions.md)
- [Systeem functies Azure Cosmos DB](sql-query-system-functions.md)
- [Inleiding tot Azure Cosmos DB](introduction.md)
