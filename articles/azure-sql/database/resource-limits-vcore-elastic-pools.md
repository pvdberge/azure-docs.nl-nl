---
title: vCore-resourcelimieten voor elastische pools
description: Op deze pagina worden enkele algemene limieten voor vCore bronnen voor elastische Pools in Azure SQL Database beschreven.
services: sql-database
ms.service: sql-database
ms.subservice: elastic-pools
ms.custom: sqldbrb=1
ms.devlang: ''
ms.topic: conceptual
author: oslake
ms.author: moslake
ms.reviewer: carlrab, sstein
ms.date: 07/21/2020
ms.openlocfilehash: f71daab55139f6b4690df50472928db466774cb3
ms.sourcegitcommit: 0e8a4671aa3f5a9a54231fea48bcfb432a1e528c
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/24/2020
ms.locfileid: "87128264"
---
# <a name="resource-limits-for-elastic-pools-using-the-vcore-purchasing-model"></a>Resource limieten voor elastische Pools met behulp van het vCore-aankoop model
[!INCLUDE[appliesto-sqldb](../includes/appliesto-sqldb.md)]

In dit artikel vindt u gedetailleerde resource limieten voor Azure SQL Database elastische Pools en gepoolde data bases met behulp van het vCore-aankoop model.

Zie [SQL database DTU-resource limieten-elastische Pools](resource-limits-dtu-elastic-pools.md)voor meer informatie over de limieten voor DTU-aankoop modellen.

> [!IMPORTANT]
> In sommige gevallen moet u mogelijk een Data Base verkleinen om ongebruikte ruimte te claimen. Zie [Bestands ruimte beheren in Azure SQL database](file-space-manage.md)voor meer informatie.

U kunt de servicelaag, de reken grootte (Service doelstelling) en de opslag hoeveelheid instellen met behulp van de [Azure Portal](elastic-pool-manage.md#azure-portal), [Power shell](elastic-pool-manage.md#powershell), de [Azure cli](elastic-pool-manage.md#azure-cli)of de [rest API](elastic-pool-manage.md#rest-api).

> [!IMPORTANT]
> Zie [een elastische pool schalen](elastic-pool-scale.md)voor meer informatie over schaling en overwegingen.

## <a name="general-purpose---provisioned-compute---gen4"></a>Algemeen beoogde, ingerichte Compute-Gen4

> [!IMPORTANT]
> Nieuwe Gen4-data bases worden niet meer ondersteund in de Australië-oost-of Brazilië-zuid regio's.

### <a name="general-purpose-service-tier-generation-4-compute-platform-part-1"></a>Service tier voor algemeen gebruik: generatie 4 Compute platform (deel 1)

|Berekenings grootte (Service doelstelling)|GP_Gen4_1|GP_Gen4_2|GP_Gen4_3|GP_Gen4_4|GP_Gen4_5|GP_Gen4_6
|:--- | --: |--: |--: |--: |--: |--: |
|Compute genereren|Gen4|Gen4|Gen4|Gen4|Gen4|Gen4|
|vCores|1|2|3|4|5|6|
|Geheugen (GB)|7|14|21|28|35|42|
|Maximum aantal Db's per pool <sup>1</sup>|100|200|500|500|500|500|
|Column Store-ondersteuning|Ja|Ja|Ja|Ja|Ja|Ja|
|OLTP-opslag in het geheugen (GB)|N.v.t.|N.v.t.|N.v.t.|N.v.t.|N.v.t.|N.v.t.|
|Maximale gegevens grootte (GB)|512|756|1536|1536|1536|2048|
|Maximale logboek grootte|154|227|461|461|461|614|
|Maximale gegevens grootte TempDB (GB)|32|64|96|128|160|192|
|Opslagtype|Premium-opslag (extern)|Premium-opslag (extern)|Premium-opslag (extern)|Premium-opslag (extern)|Premium-opslag (extern)|Premium-opslag (extern)|
|I/o-latentie (bij benadering)|5-7 MS (schrijven)<br>5-10 MS (lezen)|5-7 MS (schrijven)<br>5-10 MS (lezen)|5-7 MS (schrijven)<br>5-10 MS (lezen)|5-7 MS (schrijven)<br>5-10 MS (lezen)|5-7 MS (schrijven)<br>5-10 MS (lezen)|5-7 MS (schrijven)<br>5-10 MS (lezen)|
|Max. aantal gegevens IOPS per pool <sup>2</sup> |400|800|1200|1600|2000|2400|
|Maximale logboek frequentie per pool (MBps)|4,7|9.4|14,1|18,8|23,4|28,1|
|Maxi maal aantal gelijktijdige werk nemers per pool (aanvragen) <sup>3</sup> |210|420|630|840|1050|1260|
|Maxi maal aantal gelijktijdige aanmeldingen per pool <sup>3</sup> |210|420|630|840|1050|1260|
|Maximaal aantal gelijktijdige sessies|30.000|30.000|30.000|30.000|30.000|30.000|
|Min/max vCore keuzen voor elastische pool per data base|0, 0,25, 0,5, 1|0, 0,25, 0,5, 1, 2|0, 0,25, 0,5, 1... 3|0, 0,25, 0,5, 1... 4|0, 0,25, 0,5, 1... 5|0, 0,25, 0,5, 1... 6|
|Aantal replica's|1|1|1|1|1|1|
|Meerdere AZ|N.v.t.|N.v.t.|N.v.t.|N.v.t.|N.v.t.|N.v.t.|
|Uitschalen voor leesbewerking|N.v.t.|N.v.t.|N.v.t.|N.v.t.|N.v.t.|N.v.t.|
|Opgenomen back-upopslag|1X-DB-grootte|1X-DB-grootte|1X-DB-grootte|1X-DB-grootte|1X-DB-grootte|1X-DB-grootte|

<sup>1</sup> Zie [resource beheer in compacte elastische Pools](elastic-pool-resource-management.md) voor aanvullende overwegingen.

<sup>2</sup> de maximale waarde voor i/o-grootten tussen 8 KB en 64 kB. Werkelijke IOPS zijn werk belasting afhankelijk. Zie [Data io governance](resource-limits-logical-server.md#resource-governance)voor meer informatie.

<sup>3</sup> Zie [enkele database resource limieten](resource-limits-vcore-single-databases.md)voor het maximum aantal gelijktijdige werk rollen (aanvragen) voor elke afzonderlijke data base. Als de elastische pool bijvoorbeeld gebruikmaakt van GEN5 en het maximum aantal vCore per data base is ingesteld op 2, is de waarde voor maximum aantal gelijktijdige werk nemers 200.  Als het maximum aantal vCore per data base is ingesteld op 0,5, is de waarde voor het maximum aantal gelijktijdige werkers 50 sinds op GEN5 een maximum van 100 gelijktijdige werk nemers per vCore. Voor andere maximale vCore-instellingen per data base die minder dan 1 vCore of minder zijn, is het aantal gelijktijdige werk nemers op dezelfde manier opnieuw geschaald.

### <a name="general-purpose-service-tier-generation-4-compute-platform-part-2"></a>Service tier voor algemeen gebruik: generatie 4 Compute platform (deel 2)

|Berekenings grootte (Service doelstelling)|GP_Gen4_7|GP_Gen4_8|GP_Gen4_9|GP_Gen4_10|GP_Gen4_16|GP_Gen4_24|
|:--- | --: |--: |--: |--: |--: |--: |
|Compute genereren|Gen4|Gen4|Gen4|Gen4|Gen4|Gen4|
|vCores|7|8|9|10|16|24|
|Geheugen (GB)|49|56|63|70|112|159,5|
|Maximum aantal Db's per pool <sup>1</sup>|500|500|500|500|500|500|
|Column Store-ondersteuning|Ja|Ja|Ja|Ja|Ja|Ja|
|OLTP-opslag in het geheugen (GB)|N.v.t.|N.v.t.|N.v.t.|N.v.t.|N.v.t.|N.v.t.|
|Maximale gegevens grootte (GB)|2048|2048|2048|2048|3584|4096|
|Maximale logboek grootte (GB)|614|614|614|614|1075|1229|
|Maximale gegevens grootte TempDB (GB)|224|256|288|320|512|768|
|Opslagtype|Premium-opslag (extern)|Premium-opslag (extern)|Premium-opslag (extern)|Premium-opslag (extern)|Premium-opslag (extern)|Premium-opslag (extern)|
|I/o-latentie (bij benadering)|5-7 MS (schrijven)<br>5-10 MS (lezen)|5-7 MS (schrijven)<br>5-10 MS (lezen)|5-7 MS (schrijven)<br>5-10 MS (lezen)|5-7 MS (schrijven)<br>5-10 MS (lezen)|5-7 MS (schrijven)<br>5-10 MS (lezen)|5-7 MS (schrijven)<br>5-10 MS (lezen)|
|Max. aantal gegevens IOPS per pool <sup>2</sup>|2800|3200|3600|4000|6400|9600|
|Maximale logboek frequentie per pool (MBps)|32,8|37,5|37,5|37,5|37,5|37,5|
|Maxi maal aantal gelijktijdige werk nemers per pool (aanvragen) <sup>3</sup>|1470|1680|1890|2100|3360|5040|
|Maximum aantal gelijktijdige aanmeldings groepen (aanvragen) <sup>3</sup>|1470|1680|1890|2100|3360|5040|
|Maximaal aantal gelijktijdige sessies|30.000|30.000|30.000|30.000|30.000|30.000|
|Min/max vCore keuzen voor elastische pool per data base|0, 0,25, 0,5, 1... 7|0, 0,25, 0,5, 1... 8|0, 0,25, 0,5, 1... 9|0, 0,25, 0,5, 1... 10|0, 0,25, 0,5, 1... 10, 16|0, 0,25, 0,5, 1... 10, 16, 24|
|Aantal replica's|1|1|1|1|1|1|
|Meerdere AZ|N.v.t.|N.v.t.|N.v.t.|N.v.t.|N.v.t.|N.v.t.|
|Uitschalen voor leesbewerking|N.v.t.|N.v.t.|N.v.t.|N.v.t.|N.v.t.|N.v.t.|
|Opgenomen back-upopslag|1X-DB-grootte|1X-DB-grootte|1X-DB-grootte|1X-DB-grootte|1X-DB-grootte|1X-DB-grootte|

<sup>1</sup> Zie [resource beheer in compacte elastische Pools](elastic-pool-resource-management.md) voor aanvullende overwegingen.

<sup>2</sup> de maximale waarde voor i/o-grootten tussen 8 KB en 64 kB. Werkelijke IOPS zijn werk belasting afhankelijk. Zie [Data io governance](resource-limits-logical-server.md#resource-governance)voor meer informatie.    

<sup>3</sup> Zie [enkele database resource limieten](resource-limits-vcore-single-databases.md)voor het maximum aantal gelijktijdige werk rollen (aanvragen) voor elke afzonderlijke data base. Als de elastische pool bijvoorbeeld gebruikmaakt van GEN5 en het maximum aantal vCore per data base is ingesteld op 2, is de waarde voor maximum aantal gelijktijdige werk nemers 200.  Als het maximum aantal vCore per data base is ingesteld op 0,5, is de waarde voor het maximum aantal gelijktijdige werkers 50 sinds op GEN5 een maximum van 100 gelijktijdige werk nemers per vCore. Voor andere maximale vCore-instellingen per data base die minder dan 1 vCore of minder zijn, is het aantal gelijktijdige werk nemers op dezelfde manier opnieuw geschaald.

## <a name="general-purpose---provisioned-compute---gen5"></a>Algemeen beoogde, ingerichte Compute-GEN5

### <a name="general-purpose-service-tier-generation-5-compute-platform-part-1"></a>Service tier voor algemeen gebruik: generatie 5 Compute platform (deel 1)

|Berekenings grootte (Service doelstelling)|GP_Gen5_2|GP_Gen5_4|GP_Gen5_6|GP_Gen5_8|GP_Gen5_10|GP_Gen5_12|GP_Gen5_14|
|:--- | --: |--: |--: |--: |---: | --: |--: |
|Compute genereren|GEN5|GEN5|GEN5|GEN5|GEN5|GEN5|GEN5|
|vCores|2|4|6|8|10|12|14|
|Geheugen (GB)|10,4|20,8|31,1|41,5|51,9|62,3|72,7|
|Maximum aantal Db's per pool <sup>1</sup>|100|200|500|500|500|500|500|
|Column Store-ondersteuning|Ja|Ja|Ja|Ja|Ja|Ja|Ja|
|OLTP-opslag in het geheugen (GB)|N.v.t.|N.v.t.|N.v.t.|N.v.t.|N.v.t.|N.v.t.|N.v.t.|
|Maximale gegevens grootte (GB)|512|756|1536|1536|1536|2048|2048|
|Maximale logboek grootte (GB)|154|227|461|461|461|614|614|
|Maximale gegevens grootte TempDB (GB)|64|128|192|256|320|384|448|
|Opslagtype|Premium-opslag (extern)|Premium-opslag (extern)|Premium-opslag (extern)|Premium-opslag (extern)|Premium-opslag (extern)|Premium-opslag (extern)|Premium-opslag (extern)|
|I/o-latentie (bij benadering)|5-7 MS (schrijven)<br>5-10 MS (lezen)|5-7 MS (schrijven)<br>5-10 MS (lezen)|5-7 MS (schrijven)<br>5-10 MS (lezen)|5-7 MS (schrijven)<br>5-10 MS (lezen)|5-7 MS (schrijven)<br>5-10 MS (lezen)|5-7 MS (schrijven)<br>5-10 MS (lezen)|5-7 MS (schrijven)<br>5-10 MS (lezen)|
|Max. aantal gegevens IOPS per pool <sup>2</sup>|800|1600|2400|3200|4000|4800|5600|
|Maximale logboek frequentie per pool (MBps)|9.4|18,8|28,1|37,5|37,5|37,5|37,5|
|Maxi maal aantal gelijktijdige werk nemers per pool (aanvragen) <sup>3</sup>|210|420|630|840|1050|1260|1470|
|Maxi maal aantal gelijktijdige aanmeldingen per groep (aanvragen) <sup>3</sup>|210|420|630|840|1050|1260|1470|
|Maximaal aantal gelijktijdige sessies|30.000|30.000|30.000|30.000|30.000|30.000|30.000|
|Min/max vCore keuzen voor elastische pool per data base|0, 0,25, 0,5, 1, 2|0, 0,25, 0,5, 1... 4|0, 0,25, 0,5, 1... 6|0, 0,25, 0,5, 1... 8|0, 0,25, 0,5, 1... 10|0, 0,25, 0,5, 1... 12|0, 0,25, 0,5, 1... 14|
|Aantal replica's|1|1|1|1|1|1|1|
|Meerdere AZ|N.v.t.|N.v.t.|N.v.t.|N.v.t.|N.v.t.|N.v.t.|N.v.t.|
|Uitschalen voor leesbewerking|N.v.t.|N.v.t.|N.v.t.|N.v.t.|N.v.t.|N.v.t.|N.v.t.|
|Opgenomen back-upopslag|1X-DB-grootte|1X-DB-grootte|1X-DB-grootte|1X-DB-grootte|1X-DB-grootte|1X-DB-grootte|1X-DB-grootte|

<sup>1</sup> Zie [resource beheer in compacte elastische Pools](elastic-pool-resource-management.md) voor aanvullende overwegingen.

<sup>2</sup> de maximale waarde voor i/o-grootten tussen 8 KB en 64 kB. Werkelijke IOPS zijn werk belasting afhankelijk. Zie [Data io governance](resource-limits-logical-server.md#resource-governance)voor meer informatie.

<sup>3</sup> Zie [enkele database resource limieten](resource-limits-vcore-single-databases.md)voor het maximum aantal gelijktijdige werk rollen (aanvragen) voor elke afzonderlijke data base. Als de elastische pool bijvoorbeeld gebruikmaakt van GEN5 en het maximum aantal vCore per data base is ingesteld op 2, is de waarde voor maximum aantal gelijktijdige werk nemers 200.  Als het maximum aantal vCore per data base is ingesteld op 0,5, is de waarde voor het maximum aantal gelijktijdige werkers 50 sinds op GEN5 een maximum van 100 gelijktijdige werk nemers per vCore. Voor andere maximale vCore-instellingen per data base die minder dan 1 vCore of minder zijn, is het aantal gelijktijdige werk nemers op dezelfde manier opnieuw geschaald.

### <a name="general-purpose-service-tier-generation-5-compute-platform-part-2"></a>Service tier voor algemeen gebruik: generatie 5 Compute platform (deel 2)

|Berekenings grootte (Service doelstelling)|GP_Gen5_16|GP_Gen5_18|GP_Gen5_20|GP_Gen5_24|GP_Gen5_32|GP_Gen5_40|GP_Gen5_80|
|:--- | --: |--: |--: |--: |---: | --: |--: |
|Compute genereren|GEN5|GEN5|GEN5|GEN5|GEN5|GEN5|GEN5|
|vCores|16|18|20|24|32|40|80|
|Geheugen (GB)|83|93,4|103,8|124,6|166,1|207,6|415,2|
|Maximum aantal Db's per pool <sup>1</sup>|500|500|500|500|500|500|500|
|Column Store-ondersteuning|Ja|Ja|Ja|Ja|Ja|Ja|Ja|
|OLTP-opslag in het geheugen (GB)|N.v.t.|N.v.t.|N.v.t.|N.v.t.|N.v.t.|N.v.t.|N.v.t.|
|Maximale gegevens grootte (GB)|2048|3072|3072|3072|4096|4096|4096|
|Maximale logboek grootte (GB)|614|922|922|922|1229|1229|1229|
|Maximale gegevens grootte TempDB (GB)|512|576|640|768|1024|1280|2560|
|Opslagtype|Premium-opslag (extern)|Premium-opslag (extern)|Premium-opslag (extern)|Premium-opslag (extern)|Premium-opslag (extern)|Premium-opslag (extern)|Premium-opslag (extern)|
|I/o-latentie (bij benadering)|5-7 MS (schrijven)<br>5-10 MS (lezen)|5-7 MS (schrijven)<br>5-10 MS (lezen)|5-7 MS (schrijven)<br>5-10 MS (lezen)|5-7 MS (schrijven)<br>5-10 MS (lezen)|5-7 MS (schrijven)<br>5-10 MS (lezen)|5-7 MS (schrijven)<br>5-10 MS (lezen)|5-7 MS (schrijven)<br>5-10 MS (lezen)|
|Max. aantal gegevens IOPS per pool <sup>2</sup> |6.400|7.200|8,000|9600|12.800|16.000|16.000|
|Maximale logboek frequentie per pool (MBps)|37,5|37,5|37,5|37,5|37,5|37,5|37,5|
|Maxi maal aantal gelijktijdige werk nemers per pool (aanvragen) <sup>3</sup>|1680|1890|2100|2520|3360|4200|8400|
|Maxi maal aantal gelijktijdige aanmeldingen per groep (aanvragen) <sup>3</sup>|1680|1890|2100|2520|3360|4200|8400|
|Maximaal aantal gelijktijdige sessies|30.000|30.000|30.000|30.000|30.000|30.000|30.000|
|Min/max vCore keuzen voor elastische pool per data base|0, 0,25, 0,5, 1... 16|0, 0,25, 0,5, 1... 18|0, 0,25, 0,5, 1... 20|0, 0,25, 0,5, 1... 20, 24|0, 0,25, 0,5, 1... 20, 24, 32|0, 0,25, 0,5, 1... 16, 24, 32, 40|0, 0,25, 0,5, 1... 16, 24, 32, 40, 80|
|Aantal replica's|1|1|1|1|1|1|1|
|Meerdere AZ|N.v.t.|N.v.t.|N.v.t.|N.v.t.|N.v.t.|N.v.t.|N.v.t.|
|Uitschalen voor leesbewerking|N.v.t.|N.v.t.|N.v.t.|N.v.t.|N.v.t.|N.v.t.|N.v.t.|
|Opgenomen back-upopslag|1X-DB-grootte|1X-DB-grootte|1X-DB-grootte|1X-DB-grootte|1X-DB-grootte|1X-DB-grootte|1X-DB-grootte|

<sup>1</sup> Zie [resource beheer in compacte elastische Pools](elastic-pool-resource-management.md) voor aanvullende overwegingen.

<sup>2</sup> de maximale waarde voor i/o-grootten tussen 8 KB en 64 kB. Werkelijke IOPS zijn werk belasting afhankelijk. Zie [Data io governance](resource-limits-logical-server.md#resource-governance)voor meer informatie.

<sup>3</sup> Zie [enkele database resource limieten](resource-limits-vcore-single-databases.md)voor het maximum aantal gelijktijdige werk rollen (aanvragen) voor elke afzonderlijke data base. Als de elastische pool bijvoorbeeld gebruikmaakt van GEN5 en het maximum aantal vCore per data base is ingesteld op 2, is de waarde voor maximum aantal gelijktijdige werk nemers 200.  Als het maximum aantal vCore per data base is ingesteld op 0,5, is de waarde voor het maximum aantal gelijktijdige werkers 50 sinds op GEN5 een maximum van 100 gelijktijdige werk nemers per vCore. Voor andere maximale vCore-instellingen per data base die minder dan 1 vCore of minder zijn, is het aantal gelijktijdige werk nemers op dezelfde manier opnieuw geschaald.

## <a name="general-purpose---provisioned-compute---fsv2-series"></a>Algemeen beoogde, ingerichte Compute-Fsv2-serie

### <a name="fsv2-series-compute-generation-part-1"></a>Generatie van Fsv2-Series (deel 1)

|Berekenings grootte (Service doelstelling)|GP_Fsv2_8|GP_Fsv2_10|GP_Fsv2_12|GP_Fsv2_14| GP_Fsv2_16|
|:---| ---:|---:|---:|---:|---:|
|Compute genereren|Fsv2-serie|Fsv2-serie|Fsv2-serie|Fsv2-serie|Fsv2-serie|
|vCores|8|10|12|14|16|
|Geheugen (GB)|15,1|18,9|22,7|26,5|30,2|
|Maximum aantal Db's per pool <sup>1</sup>|500|500|500|500|500|
|Column Store-ondersteuning|Ja|Ja|Ja|Ja|Ja|
|OLTP-opslag in het geheugen (GB)|N.v.t.|N.v.t.|N.v.t.|N.v.t.|N.v.t.|
|Maximale gegevens grootte (GB)|1024|1024|1024|1024|1536|
|Maximale logboek grootte (GB)|336|336|336|336|512|
|Maximale gegevens grootte TempDB (GB)|333|333|333|333|333|
|Opslagtype|Externe SSD|Externe SSD|Externe SSD|Externe SSD|Externe SSD|
|I/o-latentie (bij benadering)|5-7 MS (schrijven)<br>5-10 MS (lezen)|5-7 MS (schrijven)<br>5-10 MS (lezen)|5-7 MS (schrijven)<br>5-10 MS (lezen)|5-7 MS (schrijven)<br>5-10 MS (lezen)|5-7 MS (schrijven)<br>5-10 MS (lezen)|
|Max. aantal gegevens IOPS per pool <sup>2</sup>|2560|3200|3840|4480|5120|
|Maximale logboek frequentie per pool (MBps)|30|30|30|30|30|
|Maxi maal aantal gelijktijdige werk nemers per pool (aanvragen) <sup>3</sup>|400|500|600|700|800|
|Maxi maal aantal gelijktijdige aanmeldingen per groep (aanvragen) <sup>3</sup>|800|1000|1200|1400|1600|
|Maximaal aantal gelijktijdige sessies|30.000|30.000|30.000|30.000|30.000|
|Min/max vCore keuzen voor elastische pool per data base|0-8|0-10|0-12|0-14|0-16|
|Aantal replica's|1|1|1|1|1|
|Meerdere AZ|N.v.t.|N.v.t.|N.v.t.|N.v.t.|N.v.t.|
|Uitschalen voor leesbewerking|N.v.t.|N.v.t.|N.v.t.|N.v.t.|N.v.t.|
|Opgenomen back-upopslag|1X-DB-grootte|1X-DB-grootte|1X-DB-grootte|1X-DB-grootte|1X-DB-grootte|


<sup>1</sup> Zie [resource beheer in compacte elastische Pools](elastic-pool-resource-management.md) voor aanvullende overwegingen.

<sup>2</sup> de maximale waarde voor i/o-grootten tussen 8 KB en 64 kB. Werkelijke IOPS zijn werk belasting afhankelijk. Zie [Data io governance](resource-limits-logical-server.md#resource-governance)voor meer informatie.

<sup>3</sup> Zie [enkele database resource limieten](resource-limits-vcore-single-databases.md)voor het maximum aantal gelijktijdige werk rollen (aanvragen) voor elke afzonderlijke data base. Als de elastische pool bijvoorbeeld gebruikmaakt van GEN5 en het maximum aantal vCore per data base is ingesteld op 2, is de waarde voor maximum aantal gelijktijdige werk nemers 200.  Als het maximum aantal vCore per data base is ingesteld op 0,5, is de waarde voor het maximum aantal gelijktijdige werkers 50 sinds op GEN5 een maximum van 100 gelijktijdige werk nemers per vCore. Voor andere maximale vCore-instellingen per data base die minder dan 1 vCore of minder zijn, is het aantal gelijktijdige werk nemers op dezelfde manier opnieuw geschaald.

### <a name="fsv2-series-compute-generation-part-2"></a>Generatie van Fsv2-Series (deel 2)

|Berekenings grootte (Service doelstelling)|GP_Fsv2_18|GP_Fsv2_20|GP_Fsv2_24|GP_Fsv2_32| GP_Fsv2_36|GP_Fsv2_72|
|:---| ---:|---:|---:|---:|---:|---:|
|Compute genereren|Fsv2-serie|Fsv2-serie|Fsv2-serie|Fsv2-serie|Fsv2-serie|Fsv2-serie|
|vCores|18|20|24|32|36|72|
|Geheugen (GB)|34,0|37,8|45,4|60,5|68,0|136,0|
|Maximum aantal Db's per pool <sup>1</sup>|500|500|500|500|500|
|Column Store-ondersteuning|Ja|Ja|Ja|Ja|Ja|Ja|
|OLTP-opslag in het geheugen (GB)|N.v.t.|N.v.t.|N.v.t.|N.v.t.|N.v.t.|N.v.t.|
|Maximale gegevens grootte (GB)|1536|1536|1536|3072|3072|4096|
|Maximale logboek grootte (GB)|512|512|512|1024|1024|1024|
|Maximale gegevens grootte TempDB (GB)|83,25|92,5|111|148|166,5|333|
|Opslagtype|Externe SSD|Externe SSD|Externe SSD|Externe SSD|Externe SSD|Externe SSD|
|I/o-latentie (bij benadering)|5-7 MS (schrijven)<br>5-10 MS (lezen)|5-7 MS (schrijven)<br>5-10 MS (lezen)|5-7 MS (schrijven)<br>5-10 MS (lezen)|5-7 MS (schrijven)<br>5-10 MS (lezen)|5-7 MS (schrijven)<br>5-10 MS (lezen)|5-7 MS (schrijven)<br>5-10 MS (lezen)|
|Max. aantal gegevens IOPS per pool <sup>2</sup>|5760|6400|7680|10240|11520|23040|
|Maximale logboek frequentie per pool (MBps)|30|30|30|30|30|30|
|Maxi maal aantal gelijktijdige werk nemers per pool (aanvragen) <sup>3</sup>|900|1000|1200|1600|1800|3600|
|Maxi maal aantal gelijktijdige aanmeldingen per groep (aanvragen) <sup>3</sup>|1800|2000|2400|3200|3600|7200|
|Maximaal aantal gelijktijdige sessies|30.000|30.000|30.000|30.000|30.000|30.000|
|Min/max vCore keuzen voor elastische pool per data base|0-18|0-20|0-24|0-32|0-36|0-72|
|Aantal replica's|1|1|1|1|1|1|
|Meerdere AZ|N.v.t.|N.v.t.|N.v.t.|N.v.t.|N.v.t.|N.v.t.|
|Uitschalen voor leesbewerking|N.v.t.|N.v.t.|N.v.t.|N.v.t.|N.v.t.|N.v.t.|
|Opgenomen back-upopslag|1X-DB-grootte|1X-DB-grootte|1X-DB-grootte|1X-DB-grootte|1X-DB-grootte|1X-DB-grootte|

<sup>1</sup> Zie [resource beheer in compacte elastische Pools](elastic-pool-resource-management.md) voor aanvullende overwegingen.

<sup>2</sup> de maximale waarde voor i/o-grootten tussen 8 KB en 64 kB. Werkelijke IOPS zijn werk belasting afhankelijk. Zie [Data io governance](resource-limits-logical-server.md#resource-governance)voor meer informatie.

<sup>3</sup> Zie [enkele database resource limieten](resource-limits-vcore-single-databases.md)voor het maximum aantal gelijktijdige werk rollen (aanvragen) voor elke afzonderlijke data base. Als de elastische pool bijvoorbeeld gebruikmaakt van GEN5 en het maximum aantal vCore per data base is ingesteld op 2, is de waarde voor maximum aantal gelijktijdige werk nemers 200.  Als het maximum aantal vCore per data base is ingesteld op 0,5, is de waarde voor het maximum aantal gelijktijdige werkers 50 sinds op GEN5 een maximum van 100 gelijktijdige werk nemers per vCore. Voor andere maximale vCore-instellingen per data base die minder dan 1 vCore of minder zijn, is het aantal gelijktijdige werk nemers op dezelfde manier opnieuw geschaald.

## <a name="business-critical---provisioned-compute---gen4"></a>Bedrijfs kritieke, ingerichte Compute-Gen4

> [!IMPORTANT]
> Nieuwe Gen4-data bases worden niet meer ondersteund in de Australië-oost-of Brazilië-zuid regio's.

### <a name="business-critical-service-tier-generation-4-compute-platform-part-1"></a>Bedrijfskritische servicelaag: generatie 4 Compute platform (deel 1)

|Berekenings grootte (Service doelstelling)|BC_Gen4_2|BC_Gen4_3|BC_Gen4_4|BC_Gen4_5|BC_Gen4_6|
|:--- | --: |--: |--: |--: |--: |--: |
|Compute genereren|Gen4|Gen4|Gen4|Gen4|Gen4|
|vCores|2|3|4|5|6|
|Geheugen (GB)|14|21|28|35|42|
|Maximum aantal Db's per pool <sup>1</sup>|50|100|100|100|100|
|Column Store-ondersteuning|Ja|Ja|Ja|Ja|Ja|
|OLTP-opslag in het geheugen (GB)|2|3|4|5|6|
|Opslagtype|Lokale SSD|Lokale SSD|Lokale SSD|Lokale SSD|Lokale SSD|
|Maximale gegevens grootte (GB)|1024|1024|1024|1024|1024|
|Maximale logboek grootte (GB)|307|307|307|307|307|
|Maximale gegevens grootte TempDB (GB)|64|96|128|160|192|
|I/o-latentie (bij benadering)|1-2 ms (schrijven)<br>1-2 ms (lezen)|1-2 ms (schrijven)<br>1-2 ms (lezen)|1-2 ms (schrijven)<br>1-2 ms (lezen)|1-2 ms (schrijven)<br>1-2 ms (lezen)|1-2 ms (schrijven)<br>1-2 ms (lezen)|
|Max. aantal gegevens IOPS per pool <sup>2</sup>|9000|13.500|18.000|22.500|27.000|
|Maximale logboek frequentie per pool (MBps)|20|30|40|50|60|
|Maxi maal aantal gelijktijdige werk nemers per pool (aanvragen) <sup>3</sup>|420|630|840|1050|1260|
|Maxi maal aantal gelijktijdige aanmeldingen per groep (aanvragen) <sup>3</sup>|420|630|840|1050|1260|
|Maximaal aantal gelijktijdige sessies|30.000|30.000|30.000|30.000|30.000|
|Min/max vCore keuzen voor elastische pool per data base|0, 0,25, 0,5, 1, 2|0, 0,25, 0,5, 1... 3|0, 0,25, 0,5, 1... 4|0, 0,25, 0,5, 1... 5|0, 0,25, 0,5, 1... 6|
|Aantal replica's|4|4|4|4|4|
|Meerdere AZ|Ja|Ja|Ja|Ja|Ja|
|Uitschalen voor leesbewerking|Ja|Ja|Ja|Ja|Ja|
|Opgenomen back-upopslag|1X-DB-grootte|1X-DB-grootte|1X-DB-grootte|1X-DB-grootte|1X-DB-grootte|

<sup>1</sup> Zie [resource beheer in compacte elastische Pools](elastic-pool-resource-management.md) voor aanvullende overwegingen.

<sup>2</sup> de maximale waarde voor i/o-grootten tussen 8 KB en 64 kB. Werkelijke IOPS zijn werk belasting afhankelijk. Zie [Data io governance](resource-limits-logical-server.md#resource-governance)voor meer informatie.

<sup>3</sup> Zie [enkele database resource limieten](resource-limits-vcore-single-databases.md)voor het maximum aantal gelijktijdige werk rollen (aanvragen) voor elke afzonderlijke data base. Als de elastische pool bijvoorbeeld gebruikmaakt van GEN5 en het maximum aantal vCore per data base is ingesteld op 2, is de waarde voor maximum aantal gelijktijdige werk nemers 200.  Als het maximum aantal vCore per data base is ingesteld op 0,5, is de waarde voor het maximum aantal gelijktijdige werkers 50 sinds op GEN5 een maximum van 100 gelijktijdige werk nemers per vCore. Voor andere maximale vCore-instellingen per data base die minder dan 1 vCore of minder zijn, is het aantal gelijktijdige werk nemers op dezelfde manier opnieuw geschaald.

### <a name="business-critical-service-tier-generation-4-compute-platform-part-2"></a>Bedrijfskritische servicelaag: generatie 4 Compute platform (deel 2)

|Berekenings grootte (Service doelstelling)|BC_Gen4_7|BC_Gen4_8|BC_Gen4_9|BC_Gen4_10|BC_Gen4_16|BC_Gen4_24|
|:--- | --: |--: |--: |--: |--: |--: |
|Compute genereren|Gen4|Gen4|Gen4|Gen4|Gen4|Gen4|
|vCores|7|8|9|10|16|24|
|Geheugen (GB)|49|56|63|70|112|159,5|
|Maximum aantal Db's per pool <sup>1</sup>|100|100|100|100|100|100|
|Column Store-ondersteuning|N.v.t.|N.v.t.|N.v.t.|N.v.t.|N.v.t.|N.v.t.|
|OLTP-opslag in het geheugen (GB)|7|8|9,5|11|20|36|
|Opslagtype|Lokale SSD|Lokale SSD|Lokale SSD|Lokale SSD|Lokale SSD|Lokale SSD|
|Maximale gegevens grootte (GB)|1024|1024|1024|1024|1024|1024|
|Maximale logboek grootte (GB)|307|307|307|307|307|307|
|Maximale gegevens grootte TempDB (GB)|224|256|288|320|512|768|
|I/o-latentie (bij benadering)|1-2 ms (schrijven)<br>1-2 ms (lezen)|1-2 ms (schrijven)<br>1-2 ms (lezen)|1-2 ms (schrijven)<br>1-2 ms (lezen)|1-2 ms (schrijven)<br>1-2 ms (lezen)|1-2 ms (schrijven)<br>1-2 ms (lezen)|1-2 ms (schrijven)<br>1-2 ms (lezen)|
|Max. aantal gegevens IOPS per pool <sup>2</sup>|31.500|36.000|40.500|45.000|72.000|96.000|
|Maximale logboek frequentie per pool (MBps)|70|80|80|80|80|80|
|Maxi maal aantal gelijktijdige werk nemers per pool (aanvragen) <sup>3</sup>|1470|1680|1890|2100|3360|5040|
|Maxi maal aantal gelijktijdige aanmeldingen per groep (aanvragen) <sup>3</sup>|1470|1680|1890|2100|3360|5040|
|Maximaal aantal gelijktijdige sessies|30.000|30.000|30.000|30.000|30.000|30.000|
|Min/max vCore keuzen voor elastische pool per data base|0, 0,25, 0,5, 1... 7|0, 0,25, 0,5, 1... 8|0, 0,25, 0,5, 1... 9|0, 0,25, 0,5, 1... 10|0, 0,25, 0,5, 1... 10, 16|0, 0,25, 0,5, 1... 10, 16, 24|
|Aantal replica's|4|4|4|4|4|4|
|Meerdere AZ|Ja|Ja|Ja|Ja|Ja|Ja|
|Uitschalen voor leesbewerking|Ja|Ja|Ja|Ja|Ja|Ja|
|Opgenomen back-upopslag|1X-DB-grootte|1X-DB-grootte|1X-DB-grootte|1X-DB-grootte|1X-DB-grootte|1X-DB-grootte|

<sup>1</sup> Zie [resource beheer in compacte elastische Pools](elastic-pool-resource-management.md) voor aanvullende overwegingen.

<sup>2</sup> de maximale waarde voor i/o-grootten tussen 8 KB en 64 kB. Werkelijke IOPS zijn werk belasting afhankelijk. Zie [Data io governance](resource-limits-logical-server.md#resource-governance)voor meer informatie.

<sup>3</sup> Zie [enkele database resource limieten](resource-limits-vcore-single-databases.md)voor het maximum aantal gelijktijdige werk rollen (aanvragen) voor elke afzonderlijke data base. Als de elastische pool bijvoorbeeld gebruikmaakt van GEN5 en het maximum aantal vCore per data base is ingesteld op 2, is de waarde voor maximum aantal gelijktijdige werk nemers 200.  Als het maximum aantal vCore per data base is ingesteld op 0,5, is de waarde voor het maximum aantal gelijktijdige werkers 50 sinds op GEN5 een maximum van 100 gelijktijdige werk nemers per vCore. Voor andere maximale vCore-instellingen per data base die minder dan 1 vCore of minder zijn, is het aantal gelijktijdige werk nemers op dezelfde manier opnieuw geschaald.

## <a name="business-critical---provisioned-compute---gen5"></a>Bedrijfs kritieke, ingerichte Compute-GEN5

### <a name="business-critical-service-tier-generation-5-compute-platform-part-1"></a>Bedrijfskritische servicelaag: generatie 5 Compute platform (deel 1)

|Berekenings grootte (Service doelstelling)|BC_Gen5_4|BC_Gen5_6|BC_Gen5_8|BC_Gen5_10|BC_Gen5_12|BC_Gen5_14|
|:--- | --: |--: |--: |--: |---: | --: |--: |
|Compute genereren|GEN5|GEN5|GEN5|GEN5|GEN5|GEN5|
|vCores|4|6|8|10|12|14|
|Geheugen (GB)|20,8|31,1|41,5|51,9|62,3|72,7|
|Maximum aantal Db's per pool <sup>1</sup>|50|100|100|100|100|100|
|Column Store-ondersteuning|Ja|Ja|Ja|Ja|Ja|Ja|
|OLTP-opslag in het geheugen (GB)|3,14|4,71|6,28|8,65|11,02|13,39|
|Maximale gegevens grootte (GB)|1024|1536|1536|1536|3072|3072|
|Maximale logboek grootte (GB)|307|307|461|461|922|922|
|Maximale gegevens grootte TempDB (GB)|128|192|256|320|384|448|
|Opslagtype|Lokale SSD|Lokale SSD|Lokale SSD|Lokale SSD|Lokale SSD|Lokale SSD|
|I/o-latentie (bij benadering)|1-2 ms (schrijven)<br>1-2 ms (lezen)|1-2 ms (schrijven)<br>1-2 ms (lezen)|1-2 ms (schrijven)<br>1-2 ms (lezen)|1-2 ms (schrijven)<br>1-2 ms (lezen)|1-2 ms (schrijven)<br>1-2 ms (lezen)|1-2 ms (schrijven)<br>1-2 ms (lezen)|
|Max. aantal gegevens IOPS per pool <sup>2</sup>|18.000|27.000|36.000|45.000|54.000|63.000|
|Maximale logboek frequentie per pool (MBps)|60|90|120|120|120|120|
|Maxi maal aantal gelijktijdige werk nemers per pool (aanvragen) <sup>3</sup>|420|630|840|1050|1260|1470|
|Maxi maal aantal gelijktijdige aanmeldingen per groep (aanvragen) <sup>3</sup>|420|630|840|1050|1260|1470|
|Maximaal aantal gelijktijdige sessies|30.000|30.000|30.000|30.000|30.000|30.000|
|Min/max vCore keuzen voor elastische pool per data base|0, 0,25, 0,5, 1... 4|0, 0,25, 0,5, 1... 6|0, 0,25, 0,5, 1... 8|0, 0,25, 0,5, 1... 10|0, 0,25, 0,5, 1... 12|0, 0,25, 0,5, 1... 14|
|Aantal replica's|4|4|4|4|4|4|
|Meerdere AZ|Ja|Ja|Ja|Ja|Ja|Ja|
|Uitschalen voor leesbewerking|Ja|Ja|Ja|Ja|Ja|Ja|
|Opgenomen back-upopslag|1X-DB-grootte|1X-DB-grootte|1X-DB-grootte|1X-DB-grootte|1X-DB-grootte|1X-DB-grootte|

<sup>1</sup> Zie [resource beheer in compacte elastische Pools](elastic-pool-resource-management.md) voor aanvullende overwegingen.

<sup>2</sup> de maximale waarde voor i/o-grootten tussen 8 KB en 64 kB. Werkelijke IOPS zijn werk belasting afhankelijk. Zie [Data io governance](resource-limits-logical-server.md#resource-governance)voor meer informatie.

<sup>3</sup> Zie [enkele database resource limieten](resource-limits-vcore-single-databases.md)voor het maximum aantal gelijktijdige werk rollen (aanvragen) voor elke afzonderlijke data base. Als de elastische pool bijvoorbeeld gebruikmaakt van GEN5 en het maximum aantal vCore per data base is ingesteld op 2, is de waarde voor maximum aantal gelijktijdige werk nemers 200.  Als het maximum aantal vCore per data base is ingesteld op 0,5, is de waarde voor het maximum aantal gelijktijdige werkers 50 sinds op GEN5 een maximum van 100 gelijktijdige werk nemers per vCore. Voor andere maximale vCore-instellingen per data base die minder dan 1 vCore of minder zijn, is het aantal gelijktijdige werk nemers op dezelfde manier opnieuw geschaald.

### <a name="business-critical-service-tier-generation-5-compute-platform-part-2"></a>Bedrijfskritische servicelaag: generatie 5 Compute platform (deel 2)

|Berekenings grootte (Service doelstelling)|BC_Gen5_16|BC_Gen5_18|BC_Gen5_20|BC_Gen5_24|BC_Gen5_32|BC_Gen5_40|BC_Gen5_80|
|:--- | --: |--: |--: |--: |---: | --: |--: |
|Compute genereren|GEN5|GEN5|GEN5|GEN5|GEN5|GEN5|GEN5|
|vCores|16|18|20|24|32|40|80|
|Geheugen (GB)|83|93,4|103,8|124,6|166,1|207,6|415,2|
|Maximum aantal Db's per pool <sup>1</sup>|100|100|100|100|100|100|100|
|Column Store-ondersteuning|Ja|Ja|Ja|Ja|Ja|Ja|Ja|
|OLTP-opslag in het geheugen (GB)|15,77|18,14|20,51|25,25|37,94|52,23|131,68|
|Maximale gegevens grootte (GB)|3072|3072|3072|4096|4096|4096|4096|
|Maximale logboek grootte (GB)|922|922|922|1229|1229|1229|1229|
|Maximale gegevens grootte TempDB (GB)|512|576|640|768|1024|1280|2560|
|Opslagtype|Lokale SSD|Lokale SSD|Lokale SSD|Lokale SSD|Lokale SSD|Lokale SSD|Lokale SSD|
|I/o-latentie (bij benadering)|1-2 ms (schrijven)<br>1-2 ms (lezen)|1-2 ms (schrijven)<br>1-2 ms (lezen)|1-2 ms (schrijven)<br>1-2 ms (lezen)|1-2 ms (schrijven)<br>1-2 ms (lezen)|1-2 ms (schrijven)<br>1-2 ms (lezen)|1-2 ms (schrijven)<br>1-2 ms (lezen)|1-2 ms (schrijven)<br>1-2 ms (lezen)|
|Max. aantal gegevens IOPS per pool <sup>2</sup>|72.000|81.000|90,000|108.000|144.000|180.000|256.000|
|Maximale logboek frequentie per pool (MBps)|120|120|120|120|120|120|120|
|Maxi maal aantal gelijktijdige werk nemers per pool (aanvragen) <sup>3</sup>|1680|1890|2100|2520|3360|4200|8400|
|Maxi maal aantal gelijktijdige aanmeldingen per groep (aanvragen) <sup>3</sup>|1680|1890|2100|2520|3360|4200|8400|
|Maximaal aantal gelijktijdige sessies|30.000|30.000|30.000|30.000|30.000|30.000|30.000|
|Min/max vCore keuzen voor elastische pool per data base|0, 0,25, 0,5, 1... 16|0, 0,25, 0,5, 1... 18|0, 0,25, 0,5, 1... 20|0, 0,25, 0,5, 1... 20, 24|0, 0,25, 0,5, 1... 20, 24, 32|0, 0,25, 0,5, 1... 20, 24, 32, 40|0, 0,25, 0,5, 1... 20, 24, 32, 40, 80|
|Aantal replica's|4|4|4|4|4|4|4|
|Meerdere AZ|Ja|Ja|Ja|Ja|Ja|Ja|Ja|
|Uitschalen voor leesbewerking|Ja|Ja|Ja|Ja|Ja|Ja|Ja|
|Opgenomen back-upopslag|1X-DB-grootte|1X-DB-grootte|1X-DB-grootte|1X-DB-grootte|1X-DB-grootte|1X-DB-grootte|1X-DB-grootte|

<sup>1</sup> Zie [resource beheer in compacte elastische Pools](elastic-pool-resource-management.md) voor aanvullende overwegingen.

<sup>2</sup> de maximale waarde voor i/o-grootten tussen 8 KB en 64 kB. Werkelijke IOPS zijn werk belasting afhankelijk. Zie [Data io governance](resource-limits-logical-server.md#resource-governance)voor meer informatie.

<sup>3</sup> Zie [enkele database resource limieten](resource-limits-vcore-single-databases.md)voor het maximum aantal gelijktijdige werk rollen (aanvragen) voor elke afzonderlijke data base. Als de elastische pool bijvoorbeeld gebruikmaakt van GEN5 en het maximum aantal vCore per data base is ingesteld op 2, is de waarde voor maximum aantal gelijktijdige werk nemers 200.  Als het maximum aantal vCore per data base is ingesteld op 0,5, is de waarde voor het maximum aantal gelijktijdige werkers 50 sinds op GEN5 een maximum van 100 gelijktijdige werk nemers per vCore. Voor andere maximale vCore-instellingen per data base die minder dan 1 vCore of minder zijn, is het aantal gelijktijdige werk nemers op dezelfde manier opnieuw geschaald.

## <a name="business-critical---provisioned-compute---m-series"></a>Bedrijfskritische-ingerichte Compute-M-serie

### <a name="m-series-compute-generation-part-1"></a>Generatie van d-Series Compute (deel 1)

|Berekenings grootte (Service doelstelling)|BC_M_8|BC_M_10|BC_M_12|BC_M_14|BC_M_16|BC_M_18|
|:---| ---:|---:|---:|---:|---:|---:|
|Compute genereren|M-serie|M-serie|M-serie|M-serie|M-serie|M-serie|
|vCores|8|10|12|14|16|18|
|Geheugen (GB)|235,4|294,3|353,2|412,0|470,9|529,7|
|Maximum aantal Db's per pool <sup>1</sup>|100|100|100|100|100|100|
|Column Store-ondersteuning|Ja|Ja|Ja|Ja|Ja|Ja|
|OLTP-opslag in het geheugen (GB)|64|80|96|112|128|150|
|Maximale gegevens grootte (GB)|512|640|768|896|1024|1152|
|Maximale logboek grootte (GB)|171|213|256|299|341|384|
|Maximale gegevens grootte TempDB (GB)|256|320|384|448|512|576|
|Opslagtype|Lokale SSD|Lokale SSD|Lokale SSD|Lokale SSD|Lokale SSD|Lokale SSD|
|I/o-latentie (bij benadering)|1-2 ms (schrijven)<br>1-2 ms (lezen)|1-2 ms (schrijven)<br>1-2 ms (lezen)|1-2 ms (schrijven)<br>1-2 ms (lezen)|1-2 ms (schrijven)<br>1-2 ms (lezen)|1-2 ms (schrijven)<br>1-2 ms (lezen)|1-2 ms (schrijven)<br>1-2 ms (lezen)|
|Max. aantal gegevens IOPS per pool <sup>2</sup>|12.499|15.624|18.748|21.873|24.998|28.123|
|Maximale logboek frequentie per pool (MBps)|48|60|72|84|96|108|
|Maxi maal aantal gelijktijdige werk nemers per pool (aanvragen) <sup>3</sup>|800|1000|1200|1400|1600|1800|
|Maxi maal aantal gelijktijdige aanmeldingen per groep (aanvragen) <sup>3</sup>|800|1000|1200|1400|1600|1800|
|Maximaal aantal gelijktijdige sessies|30.000|30.000|30.000|30.000|30.000|30.000|
|Min/max vCore keuzen voor elastische pool per data base|0-8|0-10|0-12|0-14|0-16|0-18|
|Aantal replica's|4|4|4|4|4|4|
|Meerdere AZ|Nee|Nee|Nee|Nee|Nee|Nee|
|Uitschalen voor leesbewerking|Ja|Ja|Ja|Ja|Ja|Ja|
|Opgenomen back-upopslag|1X-DB-grootte|1X-DB-grootte|1X-DB-grootte|1X-DB-grootte|1X-DB-grootte|1X-DB-grootte|

<sup>1</sup> Zie [resource beheer in compacte elastische Pools](elastic-pool-resource-management.md) voor aanvullende overwegingen.

<sup>2</sup> de maximale waarde voor i/o-grootten tussen 8 KB en 64 kB. Werkelijke IOPS zijn werk belasting afhankelijk. Zie [Data io governance](resource-limits-logical-server.md#resource-governance)voor meer informatie.

<sup>3</sup> Zie [enkele database resource limieten](resource-limits-vcore-single-databases.md)voor het maximum aantal gelijktijdige werk rollen (aanvragen) voor elke afzonderlijke data base. Als de elastische pool bijvoorbeeld gebruikmaakt van GEN5 en het maximum aantal vCore per data base is ingesteld op 2, is de waarde voor maximum aantal gelijktijdige werk nemers 200.  Als het maximum aantal vCore per data base is ingesteld op 0,5, is de waarde voor het maximum aantal gelijktijdige werkers 50 sinds op GEN5 een maximum van 100 gelijktijdige werk nemers per vCore. Voor andere maximale vCore-instellingen per data base die minder dan 1 vCore of minder zijn, is het aantal gelijktijdige werk nemers op dezelfde manier opnieuw geschaald.

Als alle vCores van een elastische pool bezet zijn, ontvangt elke data base in de pool een gelijke hoeveelheid reken bronnen om query's te verwerken. Azure SQL Database biedt verdeling voor het delen van resources tussen data bases door gelijke segmenten van reken tijd te garanderen. De verdeling voor het delen van elastische pool bronnen is een aanvulling op alle bronnen, anders wordt elke Data Base gegarandeerd wanneer de vCore min per data base is ingesteld op een andere waarde dan nul.



### <a name="m-series-compute-generation-part-2"></a>Generatie van d-Series Compute (deel 2)

|Berekenings grootte (Service doelstelling)|BC_M_20|BC_M_24|BC_M_32|BC_M_64|BC_M_128|
|:---| ---:|---:|---:|---:|---:|
|Compute genereren|M-serie|M-serie|M-serie|M-serie|M-serie|
|vCores|20|24|32|64|128|
|Geheugen (GB)|588,6|706,3|941,8|1883,5|3767,0|
|Maximum aantal Db's per pool <sup>1</sup>|100|100|100|100|100|100|
|Column Store-ondersteuning|Ja|Ja|Ja|Ja|Ja|
|OLTP-opslag in het geheugen (GB)|172|216|304|704|1768|
|Maximale gegevens grootte (GB)|1280|1536|2048|4096|4096|
|Maximale logboek grootte (GB)|427|512|683|1024|1024|
|Maximale gegevens grootte TempDB (GB)|4096|2048|1024|768|640|
|Opslagtype|Lokale SSD|Lokale SSD|Lokale SSD|Lokale SSD|Lokale SSD|
|I/o-latentie (bij benadering)|1-2 ms (schrijven)<br>1-2 ms (lezen)|1-2 ms (schrijven)<br>1-2 ms (lezen)|1-2 ms (schrijven)<br>1-2 ms (lezen)|1-2 ms (schrijven)<br>1-2 ms (lezen)|1-2 ms (schrijven)<br>1-2 ms (lezen)|
|Max. aantal gegevens IOPS per pool <sup>2</sup>|31.248|37.497|49.996|99.993|160.000|
|Maximale logboek frequentie per pool (MBps)|120|144|192|264|264|
|Maxi maal aantal gelijktijdige werk nemers per pool (aanvragen) <sup>3</sup>|2.000|2.400|3.200|6.400|12.800|
|Maxi maal aantal gelijktijdige aanmeldingen per groep (aanvragen) <sup>3</sup>|2.000|2.400|3.200|6.400|12.800|
|Maximaal aantal gelijktijdige sessies|30.000|30.000|30.000|30.000|30.000|
|Aantal replica's|4|4|4|4|4|
|Meerdere AZ|Nee|Nee|Nee|Nee|Nee|
|Uitschalen voor leesbewerking|Ja|Ja|Ja|Ja|Ja|
|Opgenomen back-upopslag|1X-DB-grootte|1X-DB-grootte|1X-DB-grootte|1X-DB-grootte|1X-DB-grootte|

<sup>1</sup> Zie [resource beheer in compacte elastische Pools](elastic-pool-resource-management.md) voor aanvullende overwegingen.

<sup>2</sup> de maximale waarde voor i/o-grootten tussen 8 KB en 64 kB. Werkelijke IOPS zijn werk belasting afhankelijk. Zie [Data io governance](resource-limits-logical-server.md#resource-governance)voor meer informatie.

<sup>3</sup> Zie [enkele database resource limieten](resource-limits-vcore-single-databases.md)voor het maximum aantal gelijktijdige werk rollen (aanvragen) voor elke afzonderlijke data base. Als de elastische pool bijvoorbeeld gebruikmaakt van GEN5 en het maximum aantal vCore per data base is ingesteld op 2, is de waarde voor maximum aantal gelijktijdige werk nemers 200.  Als het maximum aantal vCore per data base is ingesteld op 0,5, is de waarde voor het maximum aantal gelijktijdige werkers 50 sinds op GEN5 een maximum van 100 gelijktijdige werk nemers per vCore. Voor andere maximale vCore-instellingen per data base die minder dan 1 vCore of minder zijn, is het aantal gelijktijdige werk nemers op dezelfde manier opnieuw geschaald.

Als alle vCores van een elastische pool bezet zijn, ontvangt elke data base in de pool een gelijke hoeveelheid reken bronnen om query's te verwerken. Azure SQL Database biedt verdeling voor het delen van resources tussen data bases door gelijke segmenten van reken tijd te garanderen. De verdeling voor het delen van elastische pool bronnen is een aanvulling op alle bronnen, anders wordt elke Data Base gegarandeerd wanneer de vCore min per data base is ingesteld op een andere waarde dan nul.


## <a name="database-properties-for-pooled-databases"></a>Data base-eigenschappen voor gegroepeerde Data bases

De volgende tabel beschrijft de eigenschappen voor gepoolde data bases.

> [!NOTE]
> De resource limieten van afzonderlijke data bases in elastische Pools zijn in het algemeen hetzelfde als voor afzonderlijke data bases buiten Pools met dezelfde reken grootte (Service doelstelling). Zo is het maximum aantal gelijktijdige werk rollen voor een GP_Gen4_1-data base 200 werk nemers. Daarom is het maximum aantal gelijktijdige werk rollen voor een data base in een GP_Gen4_1 groep ook 200 werk nemers. Opmerking: het totale aantal gelijktijdige werk rollen in GP_Gen4_1 pool is 210.

| Eigenschap | Beschrijving |
|:--- |:--- |
| Maximum aantal vCores per data base |Het maximum aantal vCores dat elke data base in de pool mag gebruiken, indien beschikbaar op basis van het gebruik door andere data bases in de pool. Het maximale aantal vCores per data base is geen resource garantie voor een Data Base. Het is een algemene instelling voor alle databases in de groep. Stel het maximum aantal vCores per data base in dat hoog genoeg is om pieken in het database gebruik te verwerken. Er wordt een zekere mate van het door voeren van de wijzigingen verwacht omdat de groep in het algemeen gaat uitgaan van warme en koude gebruiks patronen voor data bases waarin alle data bases niet tegelijkertijd worden gepiekd.|
| Min vCores per data base |Het minimale aantal vCores dat elke data base in de pool wordt gegarandeerd. Het is een algemene instelling voor alle databases in de groep. Het minimum aantal vCores per data base kan worden ingesteld op 0 en is ook de standaard waarde. Deze eigenschap wordt ingesteld op elke wille keurige locatie tussen 0 en het gemiddelde vCores-gebruik per data base. Het product van het aantal data bases in de pool en de minimale vCores per data base mogen niet groter zijn dan de vCores per pool.|
| Maximale opslag per data base |De maximale database grootte die is ingesteld door de gebruiker voor een data base in een pool. Gegroepeerde Data bases delen toegewezen pool opslag, zodat de grootte van een Data Base beperkt is tot de kleinere opslag ruimte van de resterende pool en de grootte van de data base. De maximale database grootte verwijst naar de maximale grootte van de gegevens bestanden en bevat niet de ruimte die wordt gebruikt door de logboek bestanden. |
|||

## <a name="next-steps"></a>Volgende stappen

- Zie [resource limieten voor afzonderlijke data bases met behulp van het vCore-aankoop model](resource-limits-vcore-single-databases.md) voor vCore resource limieten voor één data base
- Zie [resource limieten voor afzonderlijke data bases met behulp van het DTU-aankoop model](resource-limits-dtu-single-databases.md) voor DTU-resource limieten voor één data base
- Voor DTU-resource limieten voor elastische Pools raadpleegt [u resource limieten voor elastische Pools met behulp van het DTU-aankoop model](resource-limits-dtu-elastic-pools.md)
- Zie [resource limieten voor beheerde](../managed-instance/resource-limits.md)exemplaren voor resource limieten voor beheerde instanties.
- Zie [Azure-abonnement en service limieten, quota's en beperkingen](../../azure-resource-manager/management/azure-subscription-service-limits.md)voor meer informatie over algemene Azure-limieten.
- Zie [overzicht van resource limieten op een logische SQL-Server](resource-limits-logical-server.md) voor informatie over limieten op het niveau van de server en het abonnement voor meer informatie over de limieten voor bronnen op een logische SQL-Server.
