---
title: Opgeslagen procedures gebruiken
description: Tips voor het ontwikkelen van oplossingen door opgeslagen procedures in de SQL-groep Synapse te implementeren.
services: synapse-analytics
author: XiaoyuMSFT
manager: craigg
ms.service: synapse-analytics
ms.topic: conceptual
ms.subservice: sql-dw
ms.date: 04/02/2019
ms.author: xiaoyul
ms.reviewer: igorstan
ms.openlocfilehash: 87c7eaa57f9da87bd83f89953afc09632d42b1f8
ms.sourcegitcommit: 877491bd46921c11dd478bd25fc718ceee2dcc08
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/02/2020
ms.locfileid: "85213394"
---
# <a name="using-stored-procedures-in-synapse-sql-pool"></a>Opgeslagen procedures gebruiken in Synapse SQL-pool

In dit artikel vindt u tips voor het ontwikkelen van oplossingen voor SQL-groepen door het implementeren van opgeslagen procedures.

## <a name="what-to-expect"></a>Wat u kunt verwachten

De SQL-groep ondersteunt veel van de T-SQL-functies die worden gebruikt in SQL Server. Belang rijker is dat er specifieke functies zijn die u kunt gebruiken om de prestaties van uw oplossing te optimaliseren.

Om u te helpen de schaal en prestaties van de SQL-groep te behouden, zijn er aanvullende functies en functionaliteiten die gedrags verschillen hebben.

## <a name="introducing-stored-procedures"></a>Inleiding tot opgeslagen procedures

Opgeslagen procedures zijn een uitstekende manier om uw SQL-code te integreren, die dicht bij de gegevens van uw SQL-groep wordt opgeslagen. Opgeslagen procedures helpen ontwikkel aars ook om hun oplossingen te modularize door de code in te delen in beheer bare eenheden, waardoor een grotere bruikbaarheid van code kan worden vergemakkelijkt. Elke opgeslagen procedure kan ook para meters accepteren om ze nog flexibeler te maken.

SQL-groep biedt een vereenvoudigde en gestroomlijnde implementatie van opgeslagen procedures. Het grootste verschil ten opzichte van SQL Server is dat de opgeslagen procedure geen vooraf gecompileerde code is.

Over het algemeen geldt dat voor data warehouses de compilatie tijd klein is in vergelijking met de tijd die nodig is om query's uit te voeren op grote gegevens volumes. Het is belang rijker om ervoor te zorgen dat de opgeslagen procedure code correct is geoptimaliseerd voor grote query's.

> [!TIP]
> Het doel is om uren, minuten en seconden op te slaan, niet in milliseconden. Het is dus handig om opgeslagen procedures te beschouwen als containers voor SQL-logica.

Wanneer de SQL-groep uw opgeslagen procedure uitvoert, worden de SQL-instructies geparseerd, vertaald en geoptimaliseerd tijdens runtime. Tijdens dit proces wordt elke instructie geconverteerd naar gedistribueerde query's. De SQL-code die wordt uitgevoerd op basis van de gegevens, wijkt af van de query die is verzonden.

## <a name="nesting-stored-procedures"></a>Opgeslagen procedures nesten

Wanneer opgeslagen procedures andere opgeslagen procedures aanroepen of dynamische SQL uitvoeren, wordt de interne opgeslagen procedure of het aanroepen van de code genest.

De SQL-pool ondersteunt Maxi maal acht geneste niveaus. Het nest niveau in SQL Server daarentegen is 32.

De op het hoogste niveau opgeslagen procedure aanroep is gelijk aan nest niveau 1.

```sql
EXEC prc_nesting
```

Als de opgeslagen procedure ook een andere EXEC-aanroep maakt, neemt het nest niveau toe tot twee.

```sql
CREATE PROCEDURE prc_nesting
AS
EXEC prc_nesting_2  -- This call is nest level 2
GO
EXEC prc_nesting
```

Als de tweede procedure vervolgens een aantal dynamische SQL-procedures uitvoert, neemt het nest niveau toe tot drie.

```sql
CREATE PROCEDURE prc_nesting_2
AS
EXEC sp_executesql 'SELECT 'another nest level'  -- This call is nest level 2
GO
EXEC prc_nesting
```

De SQL-pool ondersteunt momenteel geen [@ @NESTLEVEL ](/sql/t-sql/functions/nestlevel-transact-sql?toc=/azure/synapse-analytics/sql-data-warehouse/toc.json&bc=/azure/synapse-analytics/sql-data-warehouse/breadcrumb/toc.json&view=azure-sqldw-latest). Als zodanig moet u het nest niveau bijhouden. Het is niet waarschijnlijk dat u de limiet van acht geneste niveaus overschrijdt. Maar als u dat wel doet, moet u uw code opnieuw instellen zodat deze overeenkomt met de geneste niveaus binnen deze limiet.

## <a name="insertexecute"></a>INSERT..EXESCHATTIGE

De SQL-groep staat niet toe dat u de resultatenset van een opgeslagen procedure gebruikt met een instructie INSERT. Er is echter een andere methode die u kunt gebruiken. Zie het artikel over [tijdelijke tabellen](sql-data-warehouse-tables-temporary.md)voor een voor beeld.

## <a name="limitations"></a>Beperkingen

Er zijn een aantal aspecten van opgeslagen Transact-SQL-procedures die niet in SQL-groep zijn geïmplementeerd. Dit zijn de volgende:

* tijdelijke opgeslagen procedures
* genummerde opgeslagen procedures
* uitgebreide opgeslagen procedures
* Opgeslagen CLR-procedures
* versleutelings optie
* replicatie optie
* tabelwaardeparameter
* alleen-lezen-para meters
* standaard parameters
* uitvoerings contexten
* instructie return

## <a name="next-steps"></a>Volgende stappen

Zie [ontwikkelings overzicht](sql-data-warehouse-overview-develop.md)voor meer tips voor ontwikkel aars.
