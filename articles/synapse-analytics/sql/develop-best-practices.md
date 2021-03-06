---
title: Aanbevolen procedures voor het ontwikkelen van Synapse-SQL
description: Aanbevelingen en aanbevolen procedures die u moet kennen bij het ontwikkelen voor Synapse SQL.
services: synapse-analytics
author: XiaoyuMSFT
manager: craigg
ms.service: synapse-analytics
ms.topic: conceptual
ms.subservice: sql
ms.date: 04/15/2020
ms.author: xiaoyul
ms.reviewer: igorstan
ms.openlocfilehash: d38029284a05ce3b8f9e9af96d3f632e874f874c
ms.sourcegitcommit: 3fc3457b5a6d5773323237f6a06ccfb6955bfb2d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/11/2020
ms.locfileid: "90032268"
---
# <a name="development-best-practices-for-synapse-sql"></a>Aanbevolen procedures voor het ontwikkelen van Synapse-SQL
In dit artikel worden richt lijnen en aanbevolen procedures beschreven voor het ontwikkelen van uw data warehouse-oplossing. 

## <a name="sql-pool-development-best-practices"></a>Aanbevolen procedures voor het ontwikkelen van SQL-Pools

### <a name="reduce-cost-with-pause-and-scale"></a>Kosten verlagen met onderbreken en schalen

Zie [Compute beheren](../sql-data-warehouse/sql-data-warehouse-manage-compute-overview.md?toc=/azure/synapse-analytics/toc.json&bc=/azure/synapse-analytics/breadcrumb/toc.json) voor meer informatie over kostenverlaging via onderbreking en schaling.

### <a name="maintain-statistics"></a>Statistieken bijhouden

Zorg ervoor dat u uw statistieken dagelijks of na elke belasting bijwerkt.  Het maken en bijwerken van statistieken kan ten koste gaan van prestaties en kosten. Als u vindt dat het te lang duurt om al uw statistieken bij te houden, kunt u beter selectief bepalen welke kolommen statistieken bevatten of welke kolommen veelvuldig moeten worden bijgewerkt.  

Stel dat u datum kolommen wilt bijwerken, waarbij nieuwe waarden dagelijks kunnen worden toegevoegd. 

> [!NOTE]
> U profiteert het meest voor deel door statistieken te hebben over kolommen die deel uitmaken van samen voegingen, kolommen die worden gebruikt in de WHERE-component en kolommen in GROUP BY.

Zie ook [tabel statistieken beheren](develop-tables-statistics.md), [Statistieken maken](/sql/t-sql/statements/create-statistics-transact-sql?toc=/azure/synapse-analytics/toc.json&bc=/azure/synapse-analytics/breadcrumb/toc.json&view=azure-sqldw-latest), [Statistieken bijwerken](/sql/t-sql/statements/update-statistics-transact-sql?toc=/azure/synapse-analytics/toc.json&bc=/azure/synapse-analytics/breadcrumb/toc.json&view=azure-sqldw-latest).

### <a name="hash-distribute-large-tables"></a>Grote tabellen distribueren met hash

Tabellen worden standaard gedistribueerd middels Round Robin.  Zo kunnen gebruikers eenvoudig tabellen gaan maken zonder te hoeven bepalen hoe hun tabellen moeten worden gedistribueerd.  Round Robin-tabellen kunnen voor sommige werk belastingen voldoende worden uitgevoerd. Maar in de meeste gevallen zal het selecteren van een distributie kolom veel betere prestaties uitvoeren.  

Het meestvoorkomende geval waarin een tabel die per kolom is gedistribueerd veel beter presteert dan een Round Robin-tabel, is wanneer twee grote feitentabellen worden samengevoegd.  

Als u bijvoorbeeld een tabel Orders hebt, die wordt gedistribueerd door order_id, en een transactie tabel, die ook wordt gedistribueerd door order_id, wanneer u uw orders tabel koppelt aan de transactie tabel op order_id, wordt deze query een Pass Through-query. 

Dit betekent dat gegevens verplaatsings bewerkingen worden geëlimineerd.  Minder stappen betekent een snellere query.  Minder gegevensverplaatsing maakt query’s ook sneller.

> [!TIP]
> Zorg er bij het laden van een distributietabel voor dat uw inkomende gegevens niet zijn gedistribueerd volgens de verdeelsleutel. Dit vertraagt het laden.  

Raadpleeg de volgende koppelingen voor meer informatie over het selecteren van een distributie kolom kan de prestaties verbeteren en het definiëren van een gedistribueerde tabel in de WITH-component van uw instructie CREATE TABLES.

Zie ook [tabel Overzicht](develop-tables-overview.md), [tabel distributie](../sql-data-warehouse/sql-data-warehouse-tables-distribute.md?toc=/azure/synapse-analytics/toc.json&bc=/azure/synapse-analytics/breadcrumb/toc.json), [selecteren van tabel distributie](https://blogs.msdn.microsoft.com/sqlcat/20../../choosing-hash-distributed-table-vs-round-robin-distributed-table-in-azure-sql-dw-service/), [Create Table](/sql/t-sql/statements/create-table-azure-sql-data-warehouse?toc=/azure/synapse-analytics/toc.json&bc=/azure/synapse-analytics/breadcrumb/toc.json&view=azure-sqldw-latest)en [Create Table als selecteren](/sql/t-sql/statements/create-table-as-select-azure-sql-data-warehouse?toc=/azure/synapse-analytics/toc.json&bc=/azure/synapse-analytics/breadcrumb/toc.json&view=azure-sqldw-latest).

### <a name="do-not-over-partition"></a>Niet te veel partities maken
Hoewel het partitioneren van gegevens effectief kan zijn voor het onderhouden van uw gegevens via partitie wisseling of het optimaliseren van scans met behulp van partitie-eliminatie, waardoor er te veel partities zijn, kunnen de query's worden vertraagd.  Vaak is het mogelijk dat de strategie voor het partitioneren van hoge granulariteit goed werkt op SQL Server niet goed werkt voor de SQL-groep.  

> [!NOTE]
> Vaak is het mogelijk dat de strategie voor het partitioneren van hoge granulariteit goed werkt op SQL Server niet goed werkt voor de SQL-groep.  

Te veel partities kunnen ook geclusterde columnstore-indexen minder effectief maken als elke partitie minder dan 1 miljoen rijen bevat. Met SQL pool worden uw gegevens naar 60-data bases gepartitioneerd. 

Als u dus een tabel met 100-partities maakt, is het resultaat 6000 partities.  Elke workload is verschillend, en daarom kunt u het beste experimenteren met partities om te zien wat het beste werkt voor uw workload.  

Een van de opties die u moet overwegen, is het gebruik van een granulariteit die lager is dan wat mogelijk in SQL Server heeft gewerkt.  U zou bijvoorbeeld wekelijkse of maandelijkse partities kunnen gebruiken in plaats van dagelijkse partities.

Zie ook [tabel partities](../sql-data-warehouse/sql-data-warehouse-tables-partition.md?toc=/azure/synapse-analytics/toc.json&bc=/azure/synapse-analytics/breadcrumb/toc.json).

### <a name="minimize-transaction-sizes"></a>Transactiegrootten minimaliseren

De instructies INSERT, UPDATE en DELETE worden in een transactie uitgevoerd en wanneer ze mislukken, moeten ze worden teruggedraaid.  Om de kans op een lange terugdraaiactie te verkleinen, kunt u transactiegrootten minimaliseren waar mogelijk.  Dit kan door de instructies INSERT, UPDATE en DELETE op te delen.  

Als u bijvoorbeeld een INVOEG actie hebt die u verwacht één uur te maken, kunt u het invoegen in vier delen opsplitsen, waardoor elke uitvoer tot 15 minuten wordt verkort.

> [!TIP]
> Maak gebruik van speciale instructies voor minimale registratie, zoals CTAS, TRUNCATE, DROP TABLE en INSERT, om tabellen leeg te maken, zodat het risico op terugdraaien wordt verkleind.  

Een andere manier om terugdraaiacties te voorkomen, is door alleen-metagegevensbewerkingen, zoals schakelen tussen partities, te gebruiken voor gegevensbeheer.  

In plaats van een DELETE-instructie uit te voeren om alle rijen in een tabel met een order_date in oktober 2001 te verwijderen, kunt u bijvoorbeeld uw gegevens maandelijks partitioneren en vervolgens de partitie met gegevens omwisselen voor een lege partitie uit een andere tabel (zie voorbeelden ALTER TABLE).  

Overweeg voor ongepartitioneerde tabellen een CTAS toe te passen om de gegevens die u wilt behouden naar een tabel te schrijven, in plaats van DELETE te gebruiken.  Als een CTAS net zo lang duurt, heeft dit de voorkeur, aangezien het een veel veiligere bewerking is dankzij de minimale transactieregistratie en snel kan worden geannuleerd, indien nodig.

Zie ook [informatie over trans acties](develop-transactions.md), [optimalisatie van trans acties](../sql-data-warehouse/sql-data-warehouse-develop-best-practices-transactions.md?toc=/azure/synapse-analytics/toc.json&bc=/azure/synapse-analytics/breadcrumb/toc.json), [tabel partities](../sql-data-warehouse/sql-data-warehouse-tables-partition.md?toc=/azure/synapse-analytics/toc.json&bc=/azure/synapse-analytics/breadcrumb/toc.json), [Truncate Table](/sql/t-sql/statements/truncate-table-transact-sql?toc=/azure/synapse-analytics/toc.json&bc=/azure/synapse-analytics/breadcrumb/toc.json&view=azure-sqldw-latest), [ALTER TABLE](/sql/t-sql/statements/alter-table-transact-sql?toc=/azure/synapse-analytics/toc.json&bc=/azure/synapse-analytics/breadcrumb/toc.json&view=azure-sqldw-latest)en [create table as select (CTAS)](../sql-data-warehouse/sql-data-warehouse-develop-ctas.md?toc=/azure/synapse-analytics/toc.json&bc=/azure/synapse-analytics/breadcrumb/toc.json).

### <a name="use-the-smallest-possible-column-size"></a>De kleinst mogelijke kolomgrootte gebruiken

Als u bij het definiëren van uw DDL het kleinste gegevenstype gebruikt dat uw gegevens ondersteunt, worden de prestaties van uw query's verbeterd.  Dit is met name belangrijk voor CHAR- en VARCHAR-kolommen.  

Als de langste waarde in een kolom 25 tekens is, definieert u uw kolom als VARCHAR(25).  U kunt alle tekenkolommen beter niet volgens een grote standaardlengte definiëren.  Definieer daarnaast kolommen als VARCHAR als dat alles is wat nodig is in plaats van NVARCHAR.

Zie ook [tabel Overzicht](develop-tables-overview.md), [tabel gegevens typen](develop-tables-data-types.md)en [Create Table](/sql/t-sql/statements/create-table-azure-sql-data-warehouse?toc=/azure/synapse-analytics/toc.json&bc=/azure/synapse-analytics/breadcrumb/toc.json&view=azure-sqldw-latest).

### <a name="optimize-clustered-columnstore-tables"></a>Geclusterde columnstore-tabellen optimaliseren

Geclusterde column Store-indexen zijn een van de meest efficiënte manieren om uw gegevens in de SQL-groep op te slaan.  Tabellen in SQL-groep worden standaard gemaakt als geclusterde column Store.  

Een goede segmentkwaliteit is belangrijk om de beste resultaten te behalen voor query’s voor columnstore-tabellen.  Wanneer rijen naar columnstore-tabellen worden geschreven onder geheugendruk, kan dit ten koste gaan van de kwaliteit van columnstore-segmenten.  

Segmentkwaliteit kan worden gemeten aan de hand van het aantal rijen in een gecomprimeerde rijengroep.  Zie het artikel [oorzaken van slechte kwaliteit van Column store-index](../sql-data-warehouse/sql-data-warehouse-tables-index.md?toc=/azure/synapse-analytics/toc.json&bc=/azure/synapse-analytics/breadcrumb/toc.json#causes-of-poor-columnstore-index-quality) en [tabel indexen](../sql-data-warehouse/sql-data-warehouse-tables-index.md?toc=/azure/synapse-analytics/toc.json&bc=/azure/synapse-analytics/breadcrumb/toc.json) voor stapsgewijze instructies voor het detecteren en verbeteren van segment kwaliteit voor geclusterde column Store-tabellen.  

Omdat column Store-segmenten van hoge kwaliteit belang rijk zijn, is het een goed idee om gebruikers-Id's te gebruiken die zich in de middel lange of grote resource klasse bevinden voor het laden van gegevens. Als u lagere [Data Warehouse-eenheden](resource-consumption-models.md) gebruikt, wilt u een grotere resource klasse toewijzen aan de gebruiker die u wilt laden.

Aangezien column Store-tabellen doorgaans geen gegevens naar een gecomprimeerd column Store-segment pushen totdat er meer dan 1.000.000 rijen per tabel zijn en elke tabel in de SQL-groep is gepartitioneerd in 60 tabellen, profiteren column Store-tabellen niet voor een query tenzij de tabel meer dan 60.000.000 rijen heeft.  

> [!TIP]
> Voor tabellen met minder dan 60.000.000 rijen is het mogelijk dat een column store-index niet de optimale oplossing is.  

Als u uw gegevens partitioneert, houd er dan ook rekening mee dat elke partitie 1 miljoen rijen nodig heeft om voordeel te halen uit een geclusterde columnstore-index.  Als een tabel 100 partities heeft, moet deze ten minste 6.000.000.000 rijen hebben om te profiteren van een geclusterde column Store (60 distributies *100 partities* 1.000.000 rijen).  

Als uw tabel niet 6.000.000.000 rijen bevat, verlaagt u het aantal partities of kunt u in plaats daarvan een heap-tabel gebruiken.  Het is ook mogelijk dat u experimenteert om te zien of er betere prestaties kunnen worden verkregen door gebruik te maken van een heap-tabel met secundaire indexen in plaats van een column Store-tabel.

Query’s worden sneller uitgevoerd voor een columnstore-tabel als u alleen de kolommen selecteert die u nodig hebt.  

Zie ook [tabel indexen](../sql-data-warehouse/sql-data-warehouse-tables-index.md?toc=/azure/synapse-analytics/toc.json&bc=/azure/synapse-analytics/breadcrumb/toc.json), [gids column Store-indexen](/sql/relational-databases/indexes/columnstore-indexes-overview?toc=/azure/synapse-analytics/toc.json&bc=/azure/synapse-analytics/breadcrumb/toc.json&view=azure-sqldw-latest), [Column Store-indexen opnieuw samen stellen](../sql-data-warehouse/sql-data-warehouse-tables-index.md?toc=/azure/synapse-analytics/toc.json&bc=/azure/synapse-analytics/breadcrumb/toc.json#rebuilding-indexes-to-improve-segment-quality).

## <a name="sql-on-demand-development-best-practices"></a>Aanbevolen procedures voor het ontwikkelen van SQL op aanvraag

### <a name="general-considerations"></a>Algemene overwegingen

Met SQL on-Demand kunt u bestanden in uw Azure Storage-accounts opvragen. Het bevat geen lokale opslag-of opname mogelijkheden, wat inhoudt dat alle bestanden die de query streeft, extern zijn voor SQL op aanvraag. Daarom is het mogelijk dat alles met betrekking tot het lezen van bestanden uit de opslag invloed heeft op de prestaties van query's.

### <a name="colocate-azure-storage-account-and-sql-on-demand"></a>Azure Storage account en SQL on-demand zoeken

Als u de latentie wilt minimaliseren, gaat u naar uw Azure Storage-account en uw SQL on-demand-eind punt. Opslag accounts en eind punten die zijn ingericht tijdens het maken van de werk ruimte bevinden zich in dezelfde regio.

Voor optimale prestaties kunt u, als u toegang krijgt tot andere opslag accounts met SQL on-demand, ervoor zorgen dat ze zich in dezelfde regio bevinden. Anders wordt de latentie verhoogd voor de netwerk overdracht van de gegevens van de externe regio naar de regio van het eind punt.

### <a name="azure-storage-throttling"></a>Azure Storage beperking

Meerdere toepassingen en services kunnen toegang krijgen tot uw opslag account. Wanneer de gecombineerde IOPS of door Voer die door toepassingen, services en SQL on-demand-werk belasting worden gegenereerd, de limieten van het opslag account overschrijden, wordt er sprake van opslag beperking. Als er sprake is van opslag beperking, is er een aanzienlijk negatief effect op de query prestaties.

Zodra de beperking is gedetecteerd, heeft SQL op aanvraag ingebouwde verwerking van dit scenario. Op aanvraag van SQL on-demand worden de opslag ruimte in een langzamer tempo opgeslagen totdat de beperking is opgelost. 

Voor een optimale query-uitvoering is het echter raadzaam dat u het opslag account met andere workloads tijdens het uitvoeren van query's niet stressert.

### <a name="prepare-files-for-querying"></a>Bestanden voorbereiden voor het uitvoeren van query's

Als dat mogelijk is, kunt u bestanden voorbereiden voor betere prestaties:

- Converteer CSV naar Parquet: Parquet is de kolom indeling. Omdat het gecomprimeerd is, heeft het kleinere bestands grootten dan CSV-bestanden met dezelfde gegevens, en heeft SQL on-demand minder tijd en opslag aanvragen nodig om het te lezen.
- Als een query is gericht op één groot bestand, is het van belang om deze te splitsen in meerdere kleinere bestanden.
- Probeer de grootte van het CSV-bestand onder de 10 GB te houden.
- Het verdient de voor keur om even grote bestanden te hebben voor één OPENROWSET-pad of een externe tabel locatie.
- Uw gegevens partitioneren door partities op te slaan in verschillende mappen of bestands namen. Controleer de [functies bestands naam en bestandspad gebruiken om specifieke partities te bereiken](#use-fileinfo-and-filepath-functions-to-target-specific-partitions).

### <a name="use-fileinfo-and-filepath-functions-to-target-specific-partitions"></a>De functies file info en filepath gebruiken om specifieke partities te bereiken

Gegevens zijn vaak ingedeeld in partities. U kunt SQL op aanvraag een instructie geven om specifieke mappen en bestanden op te vragen. Hiermee beperkt u het aantal bestanden en de hoeveelheid gegevens die de query moet lezen en verwerken. 

Hierdoor krijgt u betere prestaties. Controleer voor meer informatie de functies [filename](query-data-storage.md#filename-function) en [filepath](query-data-storage.md#filepath-function) en voor beelden voor het [uitvoeren van query's op specifieke bestanden](query-specific-files.md).

Als uw gegevens in de opslag niet zijn gepartitioneerd, kunt u overwegen deze te partitioneren zodat u de query's met betrekking tot die bestanden optimaliseert.

Bij het uitvoeren van een [query op gepartitioneerde Apache Spark voor externe tabellen van Azure Synapse](develop-storage-files-spark-tables.md) vanuit SQL op aanvraag, worden automatisch alleen de benodigde bestanden voor de query gericht.

### <a name="use-cetas-to-enhance-query-performance-and-joins"></a>CETAS gebruiken om de query prestaties te verbeteren en samen te voegen

[CETAS](develop-tables-cetas.md) is een van de belangrijkste functies die beschikbaar zijn in SQL on-demand. CETAS is een parallelle bewerking die meta gegevens van externe tabellen maakt en het resultaat van de SELECT-query exporteert naar een set bestanden in uw opslag account.

U kunt CETAS gebruiken om een regel matig gebruikt deel van query's op te slaan, zoals gekoppelde referentie tabellen, naar een nieuwe set bestanden. Later kunt u deel nemen aan deze afzonderlijke externe tabel in plaats van het herhalen van algemene samen voegingen in meerdere query's. 

Naarmate CETAS Parquet-bestanden genereert, worden er automatisch statistieken gemaakt wanneer de eerste query de externe tabel bedoelt en krijgt u betere prestaties.

### <a name="next-steps"></a>Volgende stappen

Als u informatie nodig hebt die niet in dit artikel wordt vermeld, gebruikt u de ' zoeken naar docs ' aan de linkerkant van deze pagina om alle documenten van de SQL-groep te doorzoeken.  De [pagina van micro soft Q&een vraag voor SQL-groep](https://docs.microsoft.com/answers/topics/azure-synapse-analytics.html) is een plek waar u vragen kunt stellen aan andere gebruikers en de product groep van de SQL-groep.  

We controleren het forum regelmatig om er zeker van te zijn dat uw vragen worden beantwoord door een andere gebruiker of een van ons.  Als u liever vragen hebt over Stack Overflow, hebben we ook een [Azure SQL-groep stack overflow forum](https://stackoverflow.com/questions/tagged/azure-sqldw).
 
