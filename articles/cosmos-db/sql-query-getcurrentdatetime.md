---
title: GetCurrentDateTime in Azure Cosmos DB-query taal
description: Meer informatie over de SQL-functie GetCurrentDateTime in Azure Cosmos DB.
author: ginamr
ms.service: cosmos-db
ms.topic: conceptual
ms.date: 08/18/2020
ms.author: girobins
ms.custom: query-reference
ms.openlocfilehash: ec0b8ccaceed4abe3dd2784463f507f3bc76d890
ms.sourcegitcommit: d661149f8db075800242bef070ea30f82448981e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/19/2020
ms.locfileid: "88606950"
---
# <a name="getcurrentdatetime-azure-cosmos-db"></a>GetCurrentDateTime (Azure Cosmos DB)

Retourneert de huidige UTC-datum en-tijd (Coordinated Universal Time) als een ISO 8601-teken reeks.
  
## <a name="syntax"></a>Syntax
  
```sql
GetCurrentDateTime ()
```

## <a name="return-types"></a>Retour typen
  
  Retourneert de huidige UTC-datum en-8601 tijd in de notatie `YYYY-MM-DDThh:mm:ss.fffffffZ` waar:
  
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

GetCurrentDateTime () is een niet-deterministische functie. Het geretourneerde resultaat is UTC. Nauw keurigheid is 7 cijfers, met een nauw keurigheid van 100 nano seconden.

Deze systeem functie maakt geen gebruik van de index.

## <a name="examples"></a>Voorbeelden
  
In het volgende voor beeld ziet u hoe u de huidige UTC-datum tijd kunt ophalen met behulp van de ingebouwde functie GetCurrentDateTime ().
  
```sql
SELECT GetCurrentDateTime() AS currentUtcDateTime
```  
  
 Hier volgt een voor beeld van een resultatenset.
  
```json
[{
  "currentUtcDateTime": "2019-05-03T20:36:17.1234567Z"
}]  
```  

## <a name="next-steps"></a>Volgende stappen

- [Datum-en tijd functies Azure Cosmos DB](sql-query-date-time-functions.md)
- [Systeem functies Azure Cosmos DB](sql-query-system-functions.md)
- [Inleiding tot Azure Cosmos DB](introduction.md)
