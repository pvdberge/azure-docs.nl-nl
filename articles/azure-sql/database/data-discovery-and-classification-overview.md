---
title: Gegevensdetectie en -classificatie
description: Gegevens detectie & classificatie voor Azure SQL Database, Azure SQL Managed instance en Azure Synapse Analytics
services: sql-database
ms.service: sql-db-mi
ms.subservice: security
ms.custom: sqldbrb=1
titleSuffix: Azure SQL Database, Azure SQL Managed Instance, and Azure Synapse
ms.devlang: ''
ms.topic: conceptual
author: DavidTrigano
ms.author: datrigan
ms.reviewer: vanto
ms.date: 04/28/2020
tags: azure-synapse
ms.openlocfilehash: 3f1f284255d1c0e77779c175951eaf33d3e56067
ms.sourcegitcommit: 3d79f737ff34708b48dd2ae45100e2516af9ed78
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/23/2020
ms.locfileid: "87004100"
---
# <a name="data-discovery--classification"></a>Gegevensdetectie en -classificatie
[!INCLUDE[appliesto-sqldb-sqlmi-asa](../includes/appliesto-sqldb-sqlmi-asa.md)]

Gegevens detectie & classificatie is ingebouwd in Azure SQL Database, Azure SQL Managed instance en Azure Synapse Analytics. Het biedt geavanceerde mogelijkheden voor het detecteren, classificeren, labelen en rapporteren van gevoelige gegevens in uw data bases.

Uw meest gevoelige gegevens kunnen bedrijfs-, financiële, gezondheids zorg of persoonlijke informatie bevatten. Het detecteren en classificeren van deze gegevens kan een draai functie spelen in de aanpak van de gegevens beveiliging van uw organisatie. Dit kan dienen als infrastructuur om:

- Helpt te voldoen aan normen voor gegevens bescherming en vereisten voor naleving van de regelgeving.
- Diverse beveiligings scenario's, zoals controle (controle) en waarschuwingen over afwijkende toegang tot gevoelige gegevens.
- Het beheren van de toegang tot en het beveiligen van de beveiliging van data bases die uiterst gevoelige gegevens bevatten.

Gegevens detectie & classificatie maakt deel uit van de [geavanceerde gegevens beveiliging](advanced-data-security.md) . Dit is een uniform pakket voor geavanceerde Azure SQL-beveiligings mogelijkheden. U kunt gegevens detectie & classificatie openen en beheren via de sectie **geavanceerde gegevens beveiliging van SQL** van de Azure Portal.

> [!NOTE]
> Zie voor meer informatie over on-premises SQL Server de [classificatie van SQL-gegevens detectie &](https://go.microsoft.com/fwlink/?linkid=866999).

## <a name="what-is-data-discovery--classification"></a><a id="what-is-dc"></a>Wat is de classificatie van gegevens detectie &?

Gegevens detectie & classificatie introduceert een aantal geavanceerde services en nieuwe mogelijkheden in Azure. Er wordt een nieuw model voor gegevens beveiliging voor SQL Database, een beheerd exemplaar van SQL en Azure Synapse, gericht op het beschermen van de gegevens en niet alleen de data base. Het paradigma bevat:

- **Detectie en aanbevelingen:** De classificatie-engine scant uw data base en identificeert kolommen die mogelijk gevoelige gegevens bevatten. Vervolgens krijgt u een eenvoudige manier om de aanbevolen classificatie via de Azure Portal te controleren en toe te passen.

- **Labelen:** U kunt met behulp van nieuwe meta gegevens kenmerken die zijn toegevoegd aan de SQL Server data base-engine, de labels van de gevoeligheids classificatie persistent Toep assen op kolommen. Deze meta gegevens kunnen vervolgens worden gebruikt voor geavanceerde, op gevoeligheid gebaseerde controle-en beveiligings scenario's.

- **Query resultaten-ingestelde gevoeligheid:** De gevoeligheid van een resultatenset van een query wordt in realtime berekend voor controle doeleinden.

- **Zicht baarheid:** U kunt de status van de database classificatie bekijken in een gedetailleerd dash board in de Azure Portal. U kunt ook een rapport in Excel-indeling downloaden om te gebruiken voor compatibiliteit en controle doeleinden en andere behoeften.

## <a name="discover-classify-and-label-sensitive-columns"></a><a id="discover-classify-columns"></a>Gevoelige kolommen detecteren, classificeren en labelen

In deze sectie worden de stappen beschreven voor:

- Het detecteren, classificeren en labelen van kolommen die gevoelige gegevens bevatten in uw data base.
- De huidige classificatie status van uw Data Base weer geven en rapporten exporteren.

De classificatie bevat twee meta gegevens kenmerken:

- **Labels**: de belangrijkste classificatie kenmerken, die worden gebruikt voor het definiëren van het gevoeligheids niveau van de gegevens die zijn opgeslagen in de kolom.  
- **Informatie typen**: kenmerken die meer gedetailleerde informatie geven over het type gegevens dat in de kolom is opgeslagen.

### <a name="define-and-customize-your-classification-taxonomy"></a>Uw classificatie taxonomie definiëren en aanpassen

Gegevens detectie & classificatie wordt geleverd met een ingebouwde set van gevoeligheids labels en een ingebouwde set met gegevens typen en detectie logica. U kunt deze taxonomie zelf aanpassen en een reeks en rangschikking van classificatieconstructies definiëren voor uw omgeving.

U kunt uw classificatie taxonomie op één centrale locatie voor uw hele Azure-organisatie definiëren en aanpassen. Deze locatie bevindt zich in [Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-intro), als onderdeel van uw beveiligings beleid. U kunt deze taak alleen uitvoeren door iemand met beheerders rechten voor de hoofd beheer groep van de organisatie.

Als onderdeel van beleids beheer voor Information Protection kunt u aangepaste labels definiëren, ze rangschikken en koppelen aan een geselecteerde set met gegevens typen. U kunt ook uw eigen aangepaste gegevens typen toevoegen en deze configureren met teken reeks patronen. De patronen worden toegevoegd aan de detectie logica voor het identificeren van dit type gegevens in uw data bases.

Zie [het SQL Information Protection-beleid aanpassen in azure Security Center (preview)](https://go.microsoft.com/fwlink/?linkid=2009845&clcid=0x409)voor meer informatie.

Nadat u het beleid voor de hele organisatie hebt gedefinieerd, kunt u afzonderlijke data bases met behulp van het aangepaste beleid blijven classificeren.

### <a name="classify-your-database"></a>Uw data base classificeren

> [!NOTE]
> In het onderstaande voor beeld wordt Azure SQL Database gebruikt, maar u moet het juiste product selecteren dat u wilt configureren voor de classificatie van gegevens detectie &.

1. Ga naar de [Azure Portal](https://portal.azure.com).

2. Ga naar **geavanceerde gegevens beveiliging** onder de kop **beveiliging** in het deel venster Azure SQL database. Selecteer **geavanceerde gegevens beveiliging**en selecteer vervolgens de kaart **gegevens detectie & classificatie** .

   ![Het deel venster Geavanceerde gegevens beveiliging in Azure Portal](./media/data-discovery-and-classification-overview/data_classification.png)

3. Op de pagina **gegevens detectie & classificatie** bevat het tabblad **overzicht** een samen vatting van de huidige classificatie status van de data base. De samen vatting bevat een gedetailleerde lijst met alle geclassificeerde kolommen, die u ook kunt filteren om alleen specifieke schema onderdelen, informatie typen en labels weer te geven. Als u nog geen kolommen hebt geclassificeerd, [gaat u verder met stap 5](#step-5).

   ![Samen vatting van huidige classificatie status](./media/data-discovery-and-classification-overview/2_data_classification_overview_dashboard.png)

4. Als u een rapport in Excel-indeling wilt downloaden, selecteert u **exporteren** in het bovenste menu van het deel venster.

5. <a id="step-5"></a>Als u uw gegevens wilt classificeren, selecteert u het tabblad **classificatie** op de pagina **gegevens detectie & classificatie** .

    De classificatie-engine scant uw Data Base op kolommen met mogelijk gevoelige gegevens en bevat een lijst met aanbevolen kolom classificaties.

6. Aanbevelingen voor classificatie weer geven en Toep assen:

   - Als u de lijst met aanbevolen kolom classificaties wilt weer geven, selecteert u het deel venster aanbevelingen onder aan het deel venster.

   - Als u een aanbeveling voor een specifieke kolom wilt accepteren, schakelt u het selectie vakje in de linkerkolom van de relevante rij in. Als u alle aanbevelingen als geaccepteerd wilt markeren, selecteert u het meest linkse selectie vakje in de koptekst van de tabel met aanbevelingen.

       ![Controleren en selecteren in de lijst met aanbevelingen voor classificatie](./media/data-discovery-and-classification-overview/6_data_classification_recommendations_list.png)

   - Selecteer **geselecteerde aanbevelingen accepteren**om de geselecteerde aanbevelingen toe te passen.

7. U kunt kolommen ook hand matig classificeren, als een alternatief of naast de classificatie op basis van aanbevelingen:

   1. Selecteer **classificatie toevoegen** in het bovenste menu van het deel venster.

   1. In het context venster dat wordt geopend, selecteert u het schema, de tabel en de kolom die u wilt classificeren, en het gegevens type en gevoeligheids label.

   1. Selecteer **classificatie toevoegen** onder aan het context venster.

      ![Een kolom selecteren die u wilt classificeren](./media/data-discovery-and-classification-overview/9_data_classification_manual_classification.png)

8. Als u de classificatie wilt volt ooien en de database kolommen persistent wilt labelen (labelen) met de nieuwe meta gegevens van de classificatie, selecteert u **Opslaan** in het bovenste menu van het venster.

## <a name="audit-access-to-sensitive-data"></a><a id="audit-sensitive-data"></a>Toegang tot gevoelige gegevens controleren

Een belang rijk aspect van het gegevens beveiligings model is de mogelijkheid om toegang tot gevoelige gegevens te bewaken. [Azure SQL auditing](../../azure-sql/database/auditing-overview.md) is uitgebreid met een nieuw veld in het audit logboek met de naam `data_sensitivity_information` . Dit veld registreert de gevoeligheids classificaties (labels) van de gegevens die door een query zijn geretourneerd. Hier volgt een voorbeeld:

![Auditlogboek](./media/data-discovery-and-classification-overview/11_data_classification_audit_log.png)

## <a name="permissions"></a><a id="permissions"></a>Machtigingen

Deze ingebouwde rollen kunnen de gegevens classificatie van een Data Base lezen:

- Eigenaar
- Lezer
- Inzender
- SQL-beveiligings beheer
- Beheerder van gebruikerstoegang

Deze ingebouwde rollen kunnen de gegevens classificatie van een Data Base wijzigen:

- Eigenaar
- Inzender
- SQL-beveiligings beheer

Meer informatie over op rollen gebaseerde machtigingen in [Azure RBAC](https://docs.microsoft.com/azure/role-based-access-control/overview).

## <a name="manage-classifications"></a><a id="manage-classification"></a>Classificaties beheren

U kunt T-SQL, een REST API of Power shell gebruiken voor het beheren van classificaties.

### <a name="use-t-sql"></a>T-SQL gebruiken

U kunt T-SQL gebruiken om kolom classificaties toe te voegen of te verwijderen en om alle classificaties voor de gehele Data Base op te halen.

> [!NOTE]
> Wanneer u T-SQL gebruikt voor het beheren van labels, is er geen validatie waarbij labels die u toevoegt aan een kolom, aanwezig zijn in het informatie beveiligings beleid van de organisatie (de set labels die wordt weer gegeven in de portal-aanbevelingen). U kunt dit het beste valideren.

Zie de volgende verwijzingen voor meer informatie over het gebruik van T-SQL voor classificaties:

- Om de classificatie van een of meer kolommen toe te voegen of bij te werken: [gevoeligheids classificatie toevoegen](https://docs.microsoft.com/sql/t-sql/statements/add-sensitivity-classification-transact-sql)
- De classificatie verwijderen uit een of meer kolommen: [gevoeligheids classificatie voor neerzetten](https://docs.microsoft.com/sql/t-sql/statements/drop-sensitivity-classification-transact-sql)
- Alle classificaties weer geven op de Data Base: [sys. sensitivity_classifications](https://docs.microsoft.com/sql/relational-databases/system-catalog-views/sys-sensitivity-classifications-transact-sql)

### <a name="use-powershell-cmdlets"></a>PowerShell-cmdlets gebruiken
Beheer classificaties en aanbevelingen voor Azure SQL Database en Azure SQL Managed instance met behulp van Power shell.

#### <a name="powershell-cmdlets-for-azure-sql-database"></a>Power shell-cmdlets voor Azure SQL Database

- [Get-AzSqlDatabaseSensitivityClassification](https://docs.microsoft.com/powershell/module/az.sql/get-azsqldatabasesensitivityclassification)
- [Set-AzSqlDatabaseSensitivityClassification](https://docs.microsoft.com/powershell/module/az.sql/set-azsqldatabasesensitivityclassification)
- [Remove-AzSqlDatabaseSensitivityClassification](https://docs.microsoft.com/powershell/module/az.sql/remove-azsqldatabasesensitivityclassification)
- [Get-AzSqlDatabaseSensitivityRecommendation](https://docs.microsoft.com/powershell/module/az.sql/get-azsqldatabasesensitivityrecommendation)
- [Enable-AzSqlDatabaSesensitivityRecommendation](https://docs.microsoft.com/powershell/module/az.sql/enable-azsqldatabasesensitivityrecommendation)
- [Disable-AzSqlDatabaseSensitivityRecommendation](https://docs.microsoft.com/powershell/module/az.sql/disable-azsqldatabasesensitivityrecommendation)

#### <a name="powershell-cmdlets-for-azure-sql-managed-instance"></a>Power shell-cmdlets voor Azure SQL Managed instance

- [Get-AzSqlInstanceDatabaseSensitivityClassification](https://docs.microsoft.com/powershell/module/az.sql/get-azsqlinstancedatabasesensitivityclassification)
- [Set-AzSqlInstanceDatabaseSensitivityClassification](https://docs.microsoft.com/powershell/module/az.sql/set-azsqlinstancedatabasesensitivityclassification)
- [Remove-AzSqlInstanceDatabaseSensitivityClassification](https://docs.microsoft.com/powershell/module/az.sql/remove-azsqlinstancedatabasesensitivityclassification)
- [Get-AzSqlInstanceDatabaseSensitivityRecommendation](https://docs.microsoft.com/powershell/module/az.sql/get-azsqlinstancedatabasesensitivityrecommendation)
- [Enable-AzSqlInstanceDatabaseSensitivityRecommendation](https://docs.microsoft.com/powershell/module/az.sql/enable-azsqlinstancedatabasesensitivityrecommendation)
- [Disable-AzSqlInstanceDatabaseSensitivityRecommendation](https://docs.microsoft.com/powershell/module/az.sql/disable-azsqlinstancedatabasesensitivityrecommendation)

### <a name="use-the-rest-api"></a>De rest-API gebruiken

U kunt de REST API gebruiken om classificaties en aanbevelingen programmatisch te beheren. De gepubliceerde REST API ondersteunt de volgende bewerkingen:

- [Maken of bijwerken](https://docs.microsoft.com/rest/api/sql/sensitivitylabels/createorupdate): Hiermee wordt het gevoeligheids label van de opgegeven kolom gemaakt of bijgewerkt.
- [Verwijderen](https://docs.microsoft.com/rest/api/sql/sensitivitylabels/delete): Hiermee verwijdert u het gevoeligheids label van de opgegeven kolom.
- [Aanbeveling uitschakelen](https://docs.microsoft.com/rest/api/sql/sensitivitylabels/disablerecommendation): Hiermee worden de gevoeligheids aanbevelingen voor de opgegeven kolom uitgeschakeld.
- [Aanbeveling inschakelen](https://docs.microsoft.com/rest/api/sql/sensitivitylabels/enablerecommendation): Hiermee schakelt u gevoeligheids aanbevelingen in voor de opgegeven kolom. (Aanbevelingen zijn standaard ingeschakeld voor alle kolommen.)
- [Get](https://docs.microsoft.com/rest/api/sql/sensitivitylabels/get): haalt het gevoeligheids label van de opgegeven kolom op.
- [Lijst actueel op data base](https://docs.microsoft.com/rest/api/sql/sensitivitylabels/listcurrentbydatabase): Hiermee wordt de huidige sensitivity-labels van de opgegeven Data Base opgehaald.
- [Lijst aanbevolen door data base](https://docs.microsoft.com/rest/api/sql/sensitivitylabels/listrecommendedbydatabase): Hiermee wordt de aanbevolen gevoeligheids labels van de opgegeven Data Base opgehaald.

## <a name="next-steps"></a><a id="next-steps"></a>Volgende stappen

- Meer informatie over [geavanceerde gegevens beveiliging](advanced-data-security.md).
- U kunt [Azure SQL auditing](../../azure-sql/database/auditing-overview.md) configureren voor het bewaken en controleren van de toegang tot uw geclassificeerde gevoelige gegevens.
- Zie [detecteren, classificeren, labelen & beveiligen van SQL-gegevens voor een presentatie met gegevens detectie & classificatie. Gegevens die worden weer gegeven](https://www.youtube.com/watch?v=itVi9bkJUNc).
