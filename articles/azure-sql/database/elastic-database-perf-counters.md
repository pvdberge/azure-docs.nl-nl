---
title: Prestatie meter items voor het bijhouden van Shard-toewijzings beheer
description: Prestatie meter items ShardMapManager-klasse en gegevens afhankelijke route ring
services: sql-database
ms.service: sql-database
ms.subservice: scale-out
ms.custom: seoapril2019, seo-lt-2019, sqldbrb=1
ms.devlang: ''
ms.topic: conceptual
author: stevestein
ms.author: sstein
ms.reviewer: ''
ms.date: 02/07/2019
ms.openlocfilehash: c4fddcaf786801e13e962c888a154adfdffae9f8
ms.sourcegitcommit: 845a55e6c391c79d2c1585ac1625ea7dc953ea89
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/05/2020
ms.locfileid: "85961826"
---
# <a name="create-performance-counters-to-track-performance-of-shard-map-manager"></a>Prestatie meter items maken om de prestaties van Shard-toewijzings beheer bij te houden
[!INCLUDE[appliesto-sqldb](../includes/appliesto-sqldb.md)]

Prestatie meter items worden gebruikt voor het bijhouden van de prestaties van [gegevens afhankelijke route](elastic-scale-data-dependent-routing.md) bewerkingen. Deze items zijn toegankelijk in de prestatie meter, onder de categorie ' Elastic Database: Shard Management '.

U kunt de prestaties van een [Shard-kaart beheer](elastic-scale-shard-map-management.md)vastleggen, met name bij het gebruik van [gegevens afhankelijke route ring](elastic-scale-data-dependent-routing.md). Tellers worden gemaakt met methoden van de klasse micro soft. Azure. SqlDatabase. ElasticScale. client.  


**Voor de meest recente versie:** Ga naar [micro soft. Azure. SqlDatabase. ElasticScale. client](https://www.nuget.org/packages/Microsoft.Azure.SqlDatabase.ElasticScale.Client/). Zie ook [een app bijwerken voor het gebruik van de meest recente Elastic data base-client bibliotheek](elastic-scale-upgrade-client-library.md).

## <a name="prerequisites"></a>Vereisten

* De gebruiker moet lid zijn van de lokale groep **Administrators** op de computer die als host voor de toepassing fungeert om de prestatie categorie en prestatie meter items te maken.  
* Als u een exemplaar van een prestatie meter item wilt maken en de tellers wilt bijwerken, moet de gebruiker lid zijn van de groep **Administrators** of **prestatie meter gebruikers** .

## <a name="create-performance-category-and-counters"></a>Prestatie categorie en tellers maken

Als u de items wilt maken, roept u de methode CreatePerformanceCategoryAndCounters van de [klasse ShardMapManagementFactory](https://docs.microsoft.com/dotnet/api/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory)aan. Alleen een beheerder kan de volgende methode uitvoeren:

`ShardMapManagerFactory.CreatePerformanceCategoryAndCounters()`

U kunt [Dit](https://gallery.technet.microsoft.com/scriptcenter/Elastic-DB-Tools-for-Azure-17e3d283) Power shell-script ook gebruiken om de-methode uit te voeren.
Met de-methode worden de volgende prestatie meter items gemaakt:  

* **Toewijzingen in de cache**: het aantal toewijzingen in de cache voor de Shard-kaart.
* **DDR-bewerkingen per seconde**: frequentie van gegevens afhankelijke route ring bewerkingen voor de Shard-kaart. Dit item wordt bijgewerkt wanneer een aanroep van [OpenConnectionForKey ()](https://docs.microsoft.com/dotnet/api/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmap.openconnectionforkey) resulteert in een geslaagde verbinding met de doel-Shard.
* **Treffers voor het opzoeken van de opzoek cache per seconde**: frequentie van geslaagde cache opzoek bewerkingen voor toewijzingen in de Shard-toewijzing.
* Missers in de cache voor het opzoeken van de **toewijzingen per seconde**: de frequentie van mislukte opzoek bewerkingen in de cache voor toewijzingen in de Shard-toewijzing.
* **Toewijzingen die zijn toegevoegd of bijgewerkt in de cache per seconde**: de snelheid waarmee toewijzingen worden toegevoegd of bijgewerkt in de cache voor de Shard-toewijzing.
* **Toewijzingen verwijderd uit cache/SEC**: snelheid waarmee toewijzingen worden verwijderd uit de cache voor de Shard-toewijzing.

Prestatie meter items worden gemaakt voor elke Shard-kaart in de cache per proces.  

## <a name="notes"></a>Notities

Met de volgende gebeurtenissen wordt het maken van de prestatie meter items geactiveerd:  

* Initialisatie van de [ShardMapManager](https://docs.microsoft.com/dotnet/api/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanager) met behulp van een te [laden](https://docs.microsoft.com/dotnet/api/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerloadpolicy), als de ShardMapManager een Shard-toewijzing bevat. Dit zijn onder andere de methoden [GetSqlShardMapManager](https://docs.microsoft.com/dotnet/api/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.getsqlshardmapmanager) en [TryGetSqlShardMapManager](https://docs.microsoft.com/dotnet/api/microsoft.azure.sqldatabase.elasticscale.shardmanagement.shardmapmanagerfactory.trygetsqlshardmapmanager) .
* Het opzoeken van een Shard-kaart is geslaagd (met behulp van [GetShardMap ()](https://msdn.microsoft.com/library/azure/dn824215.aspx), [GetListShardMap ()](https://msdn.microsoft.com/library/azure/dn824212.aspx) of [GetRangeShardMap ()](https://msdn.microsoft.com/library/azure/dn824173.aspx)).
* Het maken van een Shard-toewijzing met CreateShardMap () is voltooid.

De prestatie meter items worden bijgewerkt door alle cache bewerkingen die worden uitgevoerd op de Shard-kaart en toewijzingen. Het verwijderen van de Shard-toewijzing met DeleteShardMap () resulteert in het verwijderen van het prestatie meter item-exemplaar.  

## <a name="best-practices"></a>Aanbevolen procedures

* Het maken van de prestatie categorie en prestatie meter items moet slechts één keer worden uitgevoerd voordat het ShardMapManager-object wordt gemaakt. Elke uitvoering van de opdracht CreatePerformanceCategoryAndCounters () wist de vorige prestatie meter items (gegevens verlies van alle instanties) en maakt nieuwe.  
* Instanties voor prestatie meter items worden per proces gemaakt. Het vastlopen van toepassingen of het verwijderen van een Shard-kaart uit de cache leidt ertoe dat de instanties van prestatie meter items worden verwijderd.  

### <a name="see-also"></a>Zie tevens

[Overzicht over functies voor Elastic Database](elastic-scale-introduction.md)  

[!INCLUDE [elastic-scale-include](../../../includes/elastic-scale-include.md)]

<!--Anchors-->
<!--Image references-->
