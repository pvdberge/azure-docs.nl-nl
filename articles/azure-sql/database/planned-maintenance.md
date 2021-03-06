---
title: Plannen voor Azure-onderhouds gebeurtenissen
description: Meer informatie over het voorbereiden van geplande onderhouds gebeurtenissen in Azure SQL Database en Azure SQL Managed instance.
services: sql-database
ms.service: sql-db-mi
ms.subservice: service
ms.custom: sqldbrb=1
ms.devlang: ''
ms.topic: conceptual
author: aamalvea
ms.author: aamalvea
ms.reviewer: carlrab
ms.date: 08/25/2020
ms.openlocfilehash: 4c7b78f14602632068a19d520aeeb940b543be61
ms.sourcegitcommit: e69bb334ea7e81d49530ebd6c2d3a3a8fa9775c9
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/27/2020
ms.locfileid: "88948212"
---
# <a name="plan-for-azure-maintenance-events-in-azure-sql-database-and-azure-sql-managed-instance"></a>Azure-onderhouds gebeurtenissen plannen in Azure SQL Database en Azure SQL Managed instance
[!INCLUDE[appliesto-sqldb-sqlmi](../includes/appliesto-sqldb-sqlmi.md)]

Meer informatie over het voorbereiden van geplande onderhouds gebeurtenissen in uw data base in Azure SQL Database en Azure SQL Managed instance.

## <a name="what-is-a-planned-maintenance-event"></a>Wat is een gepland onderhouds gebeurtenis?

Om ervoor te zorgen dat Azure SQL Database en Azure SQL Managed instance services veilig, compatibel, stabiel en met het uitvoeren van updates worden uitgevoerd via de service onderdelen bijna continu. Dankzij de moderne en robuuste service architectuur en innovatieve technologieën zoals [Hot patching](https://aka.ms/azuresqlhotpatching), zijn de meeste updates volledig transparant en zijn ze niet van invloed op de beschik baarheid van de service. Nog maar weinig typen updates leiden tot korte service interrupts en vereisen een speciale behandeling. 

Voor elke Data Base bewaart Azure SQL Database en Azure SQL Managed instance een quorum van database replica's waarbij één replica het primaire is. Op elk moment moet een primaire replica online onderhoud zijn en moet ten minste één secundaire replica in orde zijn. Tijdens gepland onderhoud gaan leden van het database quorum één keer offline, met de bedoeling dat er één primaire replica is en ten minste één secundaire replica online om ervoor te zorgen dat er geen downtime van de client is. Wanneer de primaire replica offline moet worden gezet, treedt er een herconfiguratie/failover-proces op waarin de ene secundaire replica de nieuwe primair wordt.  

## <a name="what-to-expect-during-a-planned-maintenance-event"></a>Wat u kunt verwachten tijdens een geplande onderhouds gebeurtenis

Onderhouds gebeurtenis kan één of meerdere failovers veroorzaken, afhankelijk van de Constellation van de primaire en secundaire replica's aan het begin van de onderhouds gebeurtenis. Gemiddeld worden er 1,7 failovers uitgevoerd per geplande onderhouds gebeurtenis. Opnieuw configureren/failovers worden over het algemeen binnen 30 seconden voltooid. Het gemiddelde is 8 seconden. Als er al een verbinding is gemaakt, moet uw toepassing opnieuw verbinding maken met de nieuwe primaire replica van uw data base. Als er een nieuwe verbinding tot stand wordt gebracht terwijl de Data Base een herconfiguratie ondergaat voordat de nieuwe primaire replica online is, krijgt u de fout 40613 (Data Base niet beschikbaar): *' data base {DATABASENAME} ' op server ' {servername} ' is momenteel niet beschikbaar. Probeer de verbinding later opnieuw. "* Als uw data base een langlopende query heeft, wordt deze query onderbroken tijdens een herconfiguratie en moet deze opnieuw worden gestart.

## <a name="how-to-simulate-a-planned-maintenance-event"></a>Een geplande onderhouds gebeurtenis simuleren

Om ervoor te zorgen dat uw client toepassing bestand is tegen onderhouds gebeurtenissen voorafgaand aan de implementatie van de productie, helpt het risico op toepassings fouten te verhelpen en helpt de beschik baarheid van toepassingen voor uw eind gebruikers. U kunt het gedrag van uw client toepassing testen tijdens geplande onderhouds gebeurtenissen door [hand matige failover](https://aka.ms/mifailover-techblog) via Power shell, CLI of rest API te initiëren. Het produceert hetzelfde gedrag als onderhouds gebeurtenis die de primaire replica offline brengt.

## <a name="retry-logic"></a>Logica voor opnieuw proberen

Bij elke client productie toepassing die verbinding maakt met een Cloud database service, moet een robuuste logica voor verbinding [opnieuw](troubleshoot-common-connectivity-issues.md#retry-logic-for-transient-errors)worden geïmplementeerd. Dit helpt failovers transparant te maken voor de eind gebruikers of ten minste de negatieve effecten te minimaliseren.

## <a name="resource-health"></a>Status van resources

Als uw data base aanmeldings fouten ondervindt, controleert u het [resource Health](../../service-health/resource-health-overview.md#get-started) venster in het [Azure Portal](https://portal.azure.com) voor de huidige status. De sectie status geschiedenis bevat de downtime-reden voor elke gebeurtenis (indien beschikbaar).

## <a name="next-steps"></a>Volgende stappen

- Meer informatie over [resource Health](resource-health-to-troubleshoot-connectivity.md) voor Azure SQL database en Azure SQL Managed instance.
- Zie voor meer informatie over logica voor opnieuw proberen [logica voor tijdelijke fouten](troubleshoot-common-connectivity-issues.md#retry-logic-for-transient-errors).
