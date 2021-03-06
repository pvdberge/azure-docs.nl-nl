---
title: CREATE EXTERNAL TABLE AS SELECT (CETAS) in Synapse SQL
description: CREATE EXTERNAL TABLE AS SELECT (CETAS) gebruiken met Synapse SQL
services: synapse-analytics
author: filippopovic
ms.service: synapse-analytics
ms.topic: overview
ms.subservice: sql
ms.date: 09/15/2020
ms.author: fipopovi
ms.reviewer: jrasnick
ms.openlocfilehash: d33403f49429398d9bc006187c23bb8091d9b4a1
ms.sourcegitcommit: 53acd9895a4a395efa6d7cd41d7f78e392b9cfbe
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/22/2020
ms.locfileid: "90885348"
---
# <a name="cetas-with-synapse-sql"></a>CETAS met Synapse SQL

U kunt CREATE EXTERNAL TABLE AS SELECT (CETAS) in SQL-pool of SQL on demand (preview) gebruiken om de volgende taken uit te voeren:  

- Een externe tabel maken
- De resultaten van de Transact-SQL-instructie SELECT gelijktijdig exporteren naar:

  - Hadoop
  - Azure Storage Blob
  - Azure Data Lake Storage Gen2

## <a name="cetas-in-sql-pool"></a>CETAS in SQL-pool

Bekijk het artikel [CREATE EXTERNAL TABLE AS SELECT](/sql/t-sql/statements/create-external-table-as-select-transact-sql?toc=/azure/synapse-analytics/toc.json&bc=/azure/synapse-analytics/breadcrumb/toc.json&view=azure-sqldw-latest&preserve-view=true) voor het gebruik en de syntaxis van CETAS in SQL-pool. Raadpleeg daarnaast het artikel [CREATE TABLE AS SELECT](/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse?toc=/azure/synapse-analytics/toc.json&bc=/azure/synapse-analytics/breadcrumb/toc.json&view=azure-sqldw-latest&preserve-view=true) voor meer informatie over CTAS met SQL-pool.
Bekijk het artikel [CREATE EXTERNAL TABLE AS SELECT](/sql/t-sql/statements/create-external-table-as-select-transact-sql?toc=/azure/synapse-analytics/toc.json&bc=/azure/synapse-analytics/breadcrumb/toc.json&view=azure-sqldw-latest&preserve-view=true) voor het gebruik en de syntaxis van CETAS in SQL-pool. Raadpleeg daarnaast het artikel [CREATE TABLE AS SELECT](/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse?toc=/azure/synapse-analytics/toc.json&bc=/azure/synapse-analytics/breadcrumb/toc.json&view=azure-sqldw-latest&preserve-view=true) voor meer informatie over CTAS met SQL-pool.

## <a name="cetas-in-sql-on-demand"></a>CETAS in SQL op aanvraag

Wanneer u SQL on-demand gebruikt, wordt CETAS gebruikt om een externe tabel te maken en queryresultaten te exporteren naar Azure Storage Blob of Azure Data Lake Storage Gen2.

## <a name="syntax"></a>Syntaxis

```syntaxsql
CREATE EXTERNAL TABLE [ [database_name  . [ schema_name ] . ] | schema_name . ] table_name
    WITH (
        LOCATION = 'path_to_folder',  
        DATA_SOURCE = external_data_source_name,  
        FILE_FORMAT = external_file_format_name  
)
    AS <select_statement>  
[;]

<select_statement> ::=  
    [ WITH <common_table_expression> [ ,...n ] ]  
    SELECT <select_criteria>
```

## <a name="arguments"></a>Argumenten

*[ [ *database_name* . [ *schema_name* ] . ] | *schema_name* . ] *table_name**

De uit een tot drie delen bestaande naam van de tabel die u wilt maken. Voor een externe tabel slaat SQL on-demand alleen de metagegevens van de tabel op. Er worden geen werkelijke gegevens verplaatst of opgeslagen in SQL on-demand.

LOCATION = *'path_to_folder'*

Hiermee wordt aangegeven waarheen de resultaten van de SELECT-instructie in de externe gegevensbron moeten worden geschreven. De hoofdmap is de gegevenslocatie die is opgegeven in de externe gegevensbron. LOCATION moet naar een map verwijzen en een navolgende / bevatten. Voorbeeld: aggregated_data/

DATA_SOURCE = *external_data_source_name*

Hiermee geeft u de naam op van het object voor de externe gegevensbron die de locatie bevat waar de externe gegevens worden opgeslagen. Als u een externe gegevensbron wilt maken, gebruikt u [CREATE EXTERNAL DATA SOURCE (Transact-SQL)](develop-tables-external-tables.md#create-external-data-source).

FILE_FORMAT = *external_file_format_name*

Hiermee geeft u de naam op van het object voor de externe bestandsindeling dat de indeling van het externe gegevensbestand bevat. Als u een externe bestandsindeling wilt maken, gebruikt u [CREATE EXTERNAL FILE FORMAT (Transact-SQL)](develop-tables-external-tables.md#create-external-file-format). Alleen externe bestandsindelingen met FORMAT-TYPE=PARQUET en FORMAT_TYPE=DELIMITEDTEXT worden momenteel ondersteund.

WITH *<common_table_expression>*

Hiermee geeft u een tijdelijke benoemde resultatenset op, ook wel een algemene tabelexpressie (Common Table Expression of CTE) genoemd. Zie [WITH common_table_expression (Transact-SQL)](/sql/t-sql/queries/with-common-table-expression-transact-sql?toc=/azure/synapse-analytics/toc.json&bc=/azure/synapse-analytics/breadcrumb/toc.json&view=azure-sqldw-latest&preserve-view=true) voor meer informatie.

SELECT <select_criteria>

Hiermee wordt de nieuwe tabel gevuld met de resultaten van een SELECT-instructie. *select_criteria* is de hoofdtekst van de SELECT-instructie die bepaalt welke gegevens naar de nieuwe tabel moeten worden gekopieerd. Zie [SELECT (Transact-SQL)](/sql/t-sql/queries/select-transact-sql?toc=/azure/synapse-analytics/toc.json&bc=/azure/synapse-analytics/breadcrumb/toc.json&view=azure-sqldw-latest&preserve-view=true) voor informatie over SELECT-instructies.

> [!NOTE]
> ORDER BY-component in SELECT wordt niet ondersteund voor CETAS.

## <a name="permissions"></a>Machtigingen

CETAS werkt alleen als u over machtigingen beschikt om mapinhoud weer te geven en naar de map LOCATION te schrijven.

## <a name="examples"></a>Voorbeelden

In deze voorbeelden wordt CETAS gebruikt om de totale populatie die is samengevoegd op jaar en staat op te slaan in de map aggregated_data die zich in de gegevensbron population_ds bevindt.

Dit voorbeeld is afhankelijk van de referentie, de gegevensbron en de externe bestandsindeling die eerder zijn gemaakt. Raadpleeg het document over [externe tabellen](develop-tables-external-tables.md). Als u de queryresultaten in een andere map in dezelfde gegevensbron wilt opslaan, wijzigt u het argument LOCATION. 

Als u de resultaten in een ander opslagaccount wilt opslaan, moet u voor het argument DATA_SOURCE een andere gegevensbron maken en gebruiken.

> [!NOTE]
> In de volgende voorbeelden wordt gebruikgemaakt van een openbaar Azure Open Data-opslagaccount. Het is alleen-lezen. Als u deze query's wilt uitvoeren, moet u de gegevensbron opgeven waarvoor u over schrijfmachtigingen beschikt.

```sql
-- use CETAS to export select statement with OPENROWSET result to  storage
CREATE EXTERNAL TABLE population_by_year_state
WITH (
    LOCATION = 'aggregated_data/',
    DATA_SOURCE = population_ds,  
    FILE_FORMAT = census_file_format
)  
AS
SELECT decennialTime, stateName, SUM(population) AS population
FROM
    OPENROWSET(BULK 'https://azureopendatastorage.blob.core.windows.net/censusdatacontainer/release/us_population_county/year=*/*.parquet',
    FORMAT='PARQUET') AS [r]
GROUP BY decennialTime, stateName
GO

-- you can query the newly created external table
SELECT * FROM population_by_year_state
```

In het volgende voorbeeld wordt een externe tabel gebruikt als de bron voor CETAS. Het is afhankelijk van de referentie, de gegevensbron, de externe bestandsindeling en de externe tabel die eerder zijn gemaakt. Raadpleeg het document over [externe tabellen](develop-tables-external-tables.md).

```sql
-- use CETAS with select from external table
CREATE EXTERNAL TABLE population_by_year_state
WITH (
    LOCATION = 'aggregated_data/',
    DATA_SOURCE = population_ds,  
    FILE_FORMAT = census_file_format
)  
AS
SELECT decennialTime, stateName, SUM(population) AS population
FROM census_external_table
GROUP BY decennialTime, stateName
GO

-- you can query the newly created external table
SELECT * FROM population_by_year_state
```

## <a name="supported-data-types"></a>Ondersteunde gegevenstypen

CETAS kan worden gebruikt om resultatensets met de volgende SQL-gegevenstypen op te slaan:

- binair
- varbinary
- char
- varchar
- date
- tijd
- datetime2
- decimal
- numeriek
- float
- werkelijk
- bigint
- int
- smallint
- tinyint
- bit

> [!NOTE]
> LOB's kunnen niet met CETAS worden gebruikt.

De volgende gegevenstypen kunnen niet worden gebruikt in het gedeelte met SELECT van CETAS:

- nchar
- nvarchar
- datum/tijd
- smalldatetime
- datetimeoffset
- money
- smallmoney
- uniqueidentifier

## <a name="next-steps"></a>Volgende stappen

U kunt proberen om query's uit te voeren op [externe tabellen van Apache Spark voor Azure Synapse](develop-storage-files-spark-tables.md).
