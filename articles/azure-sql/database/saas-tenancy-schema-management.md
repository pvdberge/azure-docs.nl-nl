---
title: Schema in een app met één Tenant beheren
description: Schema voor meerdere tenants beheren in een app met één Tenant die gebruikmaakt van Azure SQL Database
services: sql-database
ms.service: sql-database
ms.subservice: scenario
ms.custom: sqldbrb=1
ms.devlang: ''
ms.topic: conceptual
author: stevestein
ms.author: sstein
ms.reviewer: ''
ms.date: 09/19/2018
ms.openlocfilehash: 60c2330578ef4b8e3e40dc3e37a0c8b1eb291e2f
ms.sourcegitcommit: 877491bd46921c11dd478bd25fc718ceee2dcc08
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/02/2020
ms.locfileid: "85255548"
---
# <a name="manage-schema-in-a-saas-application-using-the-database-per-tenant-pattern-with-azure-sql-database"></a>Schema beheren in een SaaS-toepassing met behulp van het data base-per-Tenant patroon met Azure SQL Database
[!INCLUDE[appliesto-sqldb](../includes/appliesto-sqldb.md)]
 
Wanneer een database toepassing wordt ontwikkeld, moeten de wijzigingen onvermijdelijk worden aangebracht in het database schema of de referentie gegevens.  Onderhouds taken voor de Data Base zijn ook regel matig nodig. Als u een toepassing wilt beheren die gebruikmaakt van de data base per Tenant patroon, moet u deze wijzigingen of onderhouds taken Toep assen op een vloot van Tenant databases.

In deze zelf studie wordt gerefereerd met twee scenario's: het implementeren van referentie gegevens updates voor alle tenants en het opnieuw samen stellen van een index voor de tabel die de referentie gegevens bevat. De functie [elastische taken](../../sql-database/elastic-jobs-overview.md) wordt gebruikt om deze acties uit te voeren op alle Tenant databases en op de sjabloon database die wordt gebruikt voor het maken van nieuwe Tenant databases.

In deze zelfstudie leert u het volgende:

> [!div class="checklist"]
> 
> * Een taak agent maken
> * T-SQL-taken worden uitgevoerd op alle Tenant databases
> * Referentie gegevens bijwerken in alle Tenant databases
> * Een index in een tabel maken in alle tenantdatabases


Voor het voltooien van deze zelfstudie moet u ervoor zorgen dat aan de volgende vereisten is voldaan:

* De Wingtip tickets SaaS-data base per Tenant-app wordt geïmplementeerd. Zie [de SaaS-data base van Wingtip tickets implementeren en verkennen per Tenant toepassing](../../sql-database/saas-dbpertenant-get-started-deploy.md) om in minder dan vijf minuten te implementeren
* Azure PowerShell is geïnstalleerd. Zie [Aan de slag met Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps) voor meer informatie.
* De laatste versie van SQL Server Management Studio (SSMS) moet zijn geïnstalleerd. [SSMS downloaden en installeren](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)


## <a name="introduction-to-saas-schema-management-patterns"></a>Inleiding tot SaaS-schema beheer patronen

Met de data base per Tenant patroon worden Tenant gegevens effectief geïsoleerd, maar wordt het aantal data bases dat moet worden beheerd en onderhouden, verhoogd. [Elastische taken](../../sql-database/elastic-jobs-overview.md) vereenvoudigt het beheer en het beheer van meerdere data bases. Met taken kunt u veilig en betrouwbaar taken (T-SQL-scripts) uitvoeren voor een groep data bases. Met taken kunnen schema's en algemene referentie gegevens wijzigingen worden geïmplementeerd in alle Tenant databases in een toepassing. Elastische taken kunnen ook worden gebruikt voor het onderhouden van een *sjabloon* database die wordt gebruikt voor het maken van nieuwe tenants, zodat deze altijd het meest recente schema en referentie gegevens heeft.

![scherm](./media/saas-tenancy-schema-management/schema-management-dpt.png)


## <a name="elastic-jobs-public-preview"></a>Open bare preview van elastische taken

Er is een nieuwe versie van elastische taken die nu een geïntegreerde functie van Azure SQL Database zijn. Deze nieuwe versie van elastische taken is momenteel beschikbaar als open bare preview. Deze open bare preview ondersteunt momenteel het gebruik van Power shell om een taak agent te maken en T-SQL om taken te maken en te beheren.
Zie het artikel over [Elastic database taken](https://docs.microsoft.com/azure/azure-sql/database/elastic-jobs-overview) voor meer informatie.

## <a name="get-the-wingtip-tickets-saas-database-per-tenant-application-scripts"></a>De Wingtip tickets SaaS-data base ophalen per Tenant toepassings scripts

De bron code-en beheer scripts van de toepassing zijn beschikbaar in de [WingtipTicketsSaaS-DbPerTenant](https://github.com/Microsoft/WingtipTicketsSaaS-DbPerTenant) github opslag plaats. Bekijk de [algemene richt lijnen](saas-tenancy-wingtip-app-guidance-tips.md) voor de stappen voor het downloaden en blok keren van de Wingtip tickets SaaS-scripts.

## <a name="create-a-job-agent-database-and-new-job-agent"></a>Een taak agent-data base en nieuwe taak agent maken

Voor deze zelf studie moet u Power shell gebruiken om een taak agent en de data base van de back-uptaak van de-agent te maken. De data base van de taak agent bevat taak definities, taak status en geschiedenis. Zodra de taak agent en de bijbehorende data base zijn gemaakt, kunt u taken direct maken en bewaken.

1. Open **in Power shell ISE**.. \\ .Demo-SchemaManagement.ps1voor het schema beheer van learning modules \\ \\ * *.
1. Druk op **F5** om het script uit te voeren.

Het *Demo-SchemaManagement.ps1* script roept het *Deploy-SchemaManagement.ps1* script aan om een Data Base met de naam *osagent* te maken op de catalogus server. Vervolgens wordt de taak agent gemaakt met behulp van de-Data Base als een para meter.

## <a name="create-a-job-to-deploy-new-reference-data-to-all-tenants"></a>Een taak maken om nieuwe referentiegegevens te implementeren voor alle tenants

In de Wingtip tickets-app bevat elke Tenant database een set ondersteunde typen locaties. Elke locatie is van een specifiek type locatie, dat het soort gebeurtenissen definieert dat kan worden gehost, en bepaalt de achtergrond afbeelding die in de app wordt gebruikt. Deze referentie gegevens moeten worden bijgewerkt en nieuwe locatie typen worden toegevoegd, zodat de toepassing nieuwe soorten gebeurtenissen kan ondersteunen.  In deze oefening implementeert u een update voor alle tenantdatabases waarbij twee nieuwe locatietypen worden toegevoegd: *Motorcycle Racing* en *Swimming Club*.

Controleer eerst de locatie typen die zijn opgenomen in elke Tenant database. Verbinding maken met een van de Tenant-data bases in SQL Server Management Studio (SSMS) en de VenueTypes-tabel controleren.  U kunt ook een query uitvoeren op deze tabel in de query-editor in het Azure Portal, toegankelijk via de pagina Data Base. 

1. Open SSMS en maak verbinding met de Tenant server: *tenants1-dpt- &lt; user &gt; . database.Windows.net*
1. Als u wilt controleren of de motor met de *race* en de *zwem Club* op dit moment **niet is** opgenomen, bladert u naar de _contosoconcerthall_ -Data Base op de *tenants1-dpt- &lt; gebruikers &gt; * server en zoekt u de tabel *VenueTypes* .

Nu gaan we een taak maken om de *VenueTypes* -tabel in alle Tenant databases bij te werken om de nieuwe typen locaties toe te voegen.

Als u een nieuwe taak wilt maken, gebruikt u een set taken opgeslagen systeem procedures die in de _jobagent_ -Data Base zijn gemaakt toen de taak agent werd gemaakt.

1. Maak in SSMS verbinding met de catalogus server: *Catalog-dpt- &lt; user &gt; . database.Windows.net-* server 
1. Open het bestand in SSMS... \\ Learning modules \\ schema beheer \\ DeployReferenceData. SQL
1. Wijzig de instructie: SET @wtpUser = &lt; User &gt; en substitueer de gebruikers waarde die wordt gebruikt bij het implementeren van de SaaS-data base van de Wingtip tickets per Tenant-app
1. Zorg ervoor dat u bent verbonden met de _jobagent_ -data base en druk op **F5** om het script uit te voeren

Bekijk de volgende elementen in het script *DeployReferenceData. SQL* :
* **SP \_ add- \_ doel \_ groep** maakt de naam van de doel groep DemoServerGroup.
* **SP \_ toevoegen \_ doel \_ groepslid \_ ** wordt gebruikt voor het definiëren van de set doel databases.  Eerst wordt de _tenants1-dpt &lt; - &gt; gebruikers_ server toegevoegd.  Als u de server als doel toevoegt, worden de data bases op die server op het moment van de taak uitvoering in de taak opgenomen. Vervolgens worden de _basetenantdb_ -data base en de *adhocreporting* -data base (gebruikt in een latere zelf studie) als doelen toegevoegd.
* met **SP \_ add \_ Job** maakt u een taak met de naam _referentie gegevens implementatie_.
* **SP \_ add \_ jobstep** maakt de taak stap die de T-SQL-opdracht tekst bevat voor het bijwerken van de referentie tabel, VenueTypes.
* De resterende weergaven in het script tonen het bestaan van de objecten en controleren de taakuitvoering. Gebruik deze query's om de status waarde in de kolom **levens duur** te controleren om te bepalen wanneer de taak is voltooid voor alle doel databases.

Nadat het script is voltooid, kunt u controleren of de referentie gegevens zijn bijgewerkt.  Blader in SSMS naar de *contosoconcerthall* -Data Base op de *tenants1-dpt &lt; - &gt; gebruikers* server en zoek de tabel *VenueTypes* op.  Controleer of de race en *zwem Club* van *motor rijwiel* nu aanwezig **zijn** .


## <a name="create-a-job-to-manage-the-reference-table-index"></a>Een taak maken voor het beheren van de referentietabelindex

In deze oefening wordt een taak gebruikt voor het opnieuw samen stellen van de index op de primaire sleutel van de verwijzings tabel.  Dit is een normale onderhouds bewerking voor de data base die kan worden uitgevoerd na het laden van grote hoeveel heden gegevens.

Maak een taak met dezelfde in het systeem opgeslagen procedures.

1. Open SSMS en maak verbinding met de _catalogus-dpt- &lt; user &gt; . database.Windows.net-_ server
1. Het bestand openen _... \\ Learning modules \\ schema beheer \\ OnlineReindex. SQL_
1. Klik met de rechter muisknop, Selecteer verbinding en maak verbinding met de _catalogus-dpt- &lt; user &gt; . database.Windows.net-_ server, als deze nog niet is verbonden
1. Zorg ervoor dat u bent verbonden met de _jobagent_ -data base en druk op **F5** om het script uit te voeren

Bekijk de volgende elementen in het script _OnlineReindex. SQL_ :
* met de ** \_ \_ opdracht SP add** wordt een nieuwe taak gemaakt met de naam ' online REINDEX PK \_ \_ VenueTyp \_ \_ 265E44FD7FD4C885 '
* **SP \_ add \_ jobstep** maakt de taak stap die de T-SQL-opdracht tekst bevat om de index bij te werken
* De resterende weer gaven van de script controle taak worden uitgevoerd. Gebruik deze query's om de status waarde in de kolom **levens cyclus** te controleren om te bepalen wanneer de taak is voltooid voor alle leden van de doel groep.



## <a name="next-steps"></a>Volgende stappen

In deze zelfstudie hebt u het volgende geleerd:

> [!div class="checklist"]
> 
> * Een taak agent maken voor het uitvoeren van meerdere data bases in T-SQL-taken
> * Referentie gegevens bijwerken in alle Tenant databases
> * Een index in een tabel maken in alle tenantdatabases

Probeer vervolgens de [zelf studie ad hoc Reporting](../../sql-database/saas-tenancy-cross-tenant-reporting.md) uit te voeren om gedistribueerde query's te verkennen in Tenant databases.


## <a name="additional-resources"></a>Aanvullende bronnen

* [Aanvullende zelf studies die voortbouwen op de Wingtip tickets SaaS data base per Tenant toepassings implementatie](../../sql-database/saas-dbpertenant-wingtip-app-overview.md#sql-database-wingtip-saas-tutorials)
* [Uitgeschaalde clouddatabases beheren](../../sql-database/elastic-jobs-overview.md)
