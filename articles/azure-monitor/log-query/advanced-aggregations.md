---
title: Geavanceerde aggregaties in Azure Monitor-logboek query's | Microsoft Docs
description: Hierin worden een aantal geavanceerde aggregatie opties beschreven die beschikbaar zijn voor Azure Monitor-logboek query's.
ms.subservice: logs
ms.topic: conceptual
author: bwren
ms.author: bwren
ms.date: 08/16/2018
ms.openlocfilehash: dba058dce09e958a2ae769d927a5569fb3e42113
ms.sourcegitcommit: a76ff927bd57d2fcc122fa36f7cb21eb22154cfa
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/28/2020
ms.locfileid: "87324553"
---
# <a name="advanced-aggregations-in-azure-monitor-log-queries"></a>Geavanceerde aggregaties in Azure Monitor-logboek query's

> [!NOTE]
> U moet [aggregaties in azure monitor query's](./aggregations.md) volt ooien voordat u deze les voltooit.

[!INCLUDE [log-analytics-demo-environment](../../../includes/log-analytics-demo-environment.md)]

In dit artikel worden enkele van de meer geavanceerde aggregatie opties beschreven die beschikbaar zijn voor Azure Monitor query's.

## <a name="generating-lists-and-sets"></a>Lijsten en sets genereren
U kunt gebruiken `makelist` om gegevens te draaien op basis van de volg orde van de waarden in een bepaalde kolom. Het is bijvoorbeeld mogelijk dat u de meest voorkomende volg orde van gebeurtenissen op uw computers wilt verkennen. U kunt de gegevens in feite op elke computer in de juiste volg orde van EventIDs draaien. 

```Kusto
Event
| where TimeGenerated > ago(12h)
| order by TimeGenerated desc
| summarize makelist(EventID) by Computer
```

|Computer|list_EventID|
|---|---|
| Computer1 | [704, 701, 1501, 1500, 1085, 704, 704, 701] |
| Computer2 | [326.105.302.301.300.102] |
| ... | ... |

`makelist`Hiermee wordt een lijst gegenereerd in de volg orde waarin er gegevens aan zijn door gegeven. Als u gebeurtenissen van oudste naar nieuwste wilt sorteren, gebruikt u `asc` in de instructie order in plaats van `desc` . 

Het is ook handig om een lijst met alleen unieke waarden te maken. Dit wordt een _set_ genoemd en kan worden gegenereerd met `makeset` :

```Kusto
Event
| where TimeGenerated > ago(12h)
| order by TimeGenerated desc
| summarize makeset(EventID) by Computer
```

|Computer|list_EventID|
|---|---|
| Computer1 | [704, 701, 1501, 1500, 1085] |
| Computer2 | [326.105.302.301.300.102] |
| ... | ... |

Net `makelist` als `makeset` bij beschik bare gegevens, worden ook de matrices gegenereerd op basis van de volg orde van de rijen die erin worden door gegeven.

## <a name="expanding-lists"></a>Lijsten uitbreiden
De omgekeerde bewerking van `makelist` of `makeset` is `mvexpand` , die een lijst met waarden uitbreidt om rijen te scheiden. Het kan worden uitgebreid over een wille keurig aantal dynamische kolommen, zowel JSON als matrix. U kunt bijvoorbeeld de *heartbeat* -tabel controleren op oplossingen die gegevens verzenden van computers die in het afgelopen uur een heartbeat hebben verzonden:

```Kusto
Heartbeat
| where TimeGenerated > ago(1h)
| project Computer, Solutions
```

| Computer | Oplossingen | 
|--------------|----------------------|
| Computer1 | ' Beveiliging ', ' updates ', ' change tracking ' |
| Computer2 | ' Beveiliging ', ' updates ' |
| computer3 | "antimalware", "change tracking" |
| ... | ... |

Gebruik `mvexpand` om elke waarde in een afzonderlijke rij weer te geven in plaats van een door komma's gescheiden lijst:

```Kusto
Heartbeat
| where TimeGenerated > ago(1h)
| project Computer, split(Solutions, ",")
| mvexpand Solutions
```

| Computer | Oplossingen | 
|--------------|----------------------|
| Computer1 | beveiligingsprincipal |
| Computer1 | updates |
| Computer1 | Change tracking |
| Computer2 | beveiligingsprincipal |
| Computer2 | updates |
| computer3 | Assen |
| computer3 | Change tracking |
| ... | ... |


U kunt vervolgens `makelist` opnieuw gebruiken om items te groeperen en deze keer zien de lijst met computers per oplossing:

```Kusto
Heartbeat
| where TimeGenerated > ago(1h)
| project Computer, split(Solutions, ",")
| mvexpand Solutions
| summarize makelist(Computer) by tostring(Solutions) 
```

|Oplossingen | list_Computer |
|--------------|----------------------|
| beveiligingsprincipal | ["Computer1", "computer2"] |
| updates | ["Computer1", "computer2"] |
| Change tracking | ["Computer1", "computer3"] |
| Assen | ["computer3"] |
| ... | ... |

## <a name="handling-missing-bins"></a>Ontbrekende opslag locaties verwerken
Een handige toepassing van `mvexpand` is de nood zaak om standaard waarden in te vullen voor ontbrekende opslag locaties. Stel bijvoorbeeld dat u op zoek bent naar de uptime van een bepaalde machine door de heartbeat te verkennen. U wilt ook de bron van de heartbeat zien die zich in de kolom _categorie_ bevindt. Normaal gesp roken gebruiken we een eenvoudige samenvattings instructie als volgt:

```Kusto
Heartbeat
| where TimeGenerated > ago(12h)
| summarize count() by Category, bin(TimeGenerated, 1h)
```

| Categorie | TimeGenerated | count_ |
|--------------|----------------------|--------|
| Directe agent | 2017-06-06T17:00:00Z | 15 |
| Directe agent | 2017-06-06T18:00:00Z | 60 |
| Directe agent | 2017-06-06T20:00:00Z | 55 |
| Directe agent | 2017-06-06T21:00:00Z | 57 |
| Directe agent | 2017-06-06T22:00:00Z | 60 |
| ... | ... | ... |

In deze resultaten wordt de Bucket die is gekoppeld aan "2017-06-06T19:00:00Z ontbreekt omdat er geen heartbeat-gegevens voor dat uur zijn. Gebruik de `make-series` functie om een standaard waarde toe te wijzen aan lege buckets. Hiermee wordt een rij gegenereerd voor elke categorie met twee extra matrix kolommen, één voor waarden en één voor overeenkomende tijds verzamelingen:

```Kusto
Heartbeat
| make-series count() default=0 on TimeGenerated in range(ago(1d), now(), 1h) by Category 
```

| Categorie | count_ | TimeGenerated |
|---|---|---|
| Directe agent | [15, 60, 0, 55, 60, 57, 60,...] | ["2017-06-06T17:00:00.0000000 Z", "2017-06-06T18:00:00.0000000 Z", "2017-06-06T19:00:00.0000000 Z", "2017-06-06T20:00:00.0000000 Z", "2017-06-06T21:00:00.0000000 Z",...] |
| ... | ... | ... |

Het derde element van de *count_* matrix is 0 zoals verwacht, en er is een overeenkomende tijds tempel van "2017-06-06T19:00:00.0000000 z" in de _TimeGenerated_ -matrix. Het is moeilijk om deze matrix indeling te lezen. Gebruik `mvexpand` om de matrices uit te breiden en dezelfde indelings uitvoer te produceren als gegenereerd door `summarize` :

```Kusto
Heartbeat
| make-series count() default=0 on TimeGenerated in range(ago(1d), now(), 1h) by Category 
| mvexpand TimeGenerated, count_
| project Category, TimeGenerated, count_
```

| Categorie | TimeGenerated | count_ |
|--------------|----------------------|--------|
| Directe agent | 2017-06-06T17:00:00Z | 15 |
| Directe agent | 2017-06-06T18:00:00Z | 60 |
| Directe agent | 2017-06-06T19:00:00Z | 0 |
| Directe agent | 2017-06-06T20:00:00Z | 55 |
| Directe agent | 2017-06-06T21:00:00Z | 57 |
| Directe agent | 2017-06-06T22:00:00Z | 60 |
| ... | ... | ... |



## <a name="narrowing-results-to-a-set-of-elements-let-makeset-toscalar-in"></a>De resultaten beperken tot een set met elementen: `let` , `makeset` , `toscalar` ,`in`
Een veelvoorkomend scenario is door de namen van bepaalde entiteiten te selecteren op basis van een set criteria en vervolgens een andere gegevensset te filteren die is ingesteld op die entiteit. U kunt bijvoorbeeld computers vinden waarvan bekend is dat deze updates bevatten en IP-adressen identificeren die op deze computers worden genoemd:


```Kusto
let ComputersNeedingUpdate = toscalar(
    Update
    | summarize makeset(Computer)
    | project set_Computer
);
WindowsFirewall
| where Computer in (ComputersNeedingUpdate)
```

## <a name="next-steps"></a>Volgende stappen

Zie andere lessen voor het gebruik van de [Kusto-query taal](/azure/kusto/query/) met Azure monitor-logboek gegevens:

- [Tekenreeksbewerkingen](string-operations.md)
- [Datum- en tijdbewerkingen](datetime-operations.md)
- [Aggregatiefuncties](aggregations.md)
- [Geavanceerde aggregaties]()
- [JSON en gegevensstructuren](json-data-structures.md)
- [Samenvoegingen](joins.md)
- [Grafieken](charts.md)

