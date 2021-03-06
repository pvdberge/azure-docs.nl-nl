---
title: Verbinding maken met Sqlcmd
description: Gebruik het opdracht regel hulpprogramma Sqlcmd om verbinding te maken met en een query uit te Synapse SQL-groep.
services: synapse-analytics
author: XiaoyuMSFT
manager: craigg
ms.service: synapse-analytics
ms.topic: conceptual
ms.subservice: sql-dw
ms.date: 04/17/2018
ms.author: xiaoyul
ms.reviewer: igorstan
ms.custom: seo-lt-2019
ms.openlocfilehash: 2e76f48466d084d448cceea0490e44041e7d062e
ms.sourcegitcommit: 877491bd46921c11dd478bd25fc718ceee2dcc08
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/02/2020
ms.locfileid: "85212136"
---
# <a name="connect-to-synapse-sql-pool-with-sqlcmd"></a>Verbinding maken met de Synapse SQL-groep met Sqlcmd

> [!div class="op_single_selector"]
>
> * [Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md)
> * [Azure Machine Learning](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md)
> * [Visual Studio](sql-data-warehouse-query-visual-studio.md)
> * [sqlcmd](sql-data-warehouse-get-started-connect-sqlcmd.md)
> * [SSMS](sql-data-warehouse-query-ssms.md)

Gebruik het opdracht regel programma [Sqlcmd] [Sqlcmd] om verbinding te maken met en een query uit te zoeken op een SQL-groep.  

## <a name="1-connect"></a>1. Verbinding maken

Om aan de slag te gaan met [Sqlcmd] [Sqlcmd], opent u de opdracht prompt en voert u **Sqlcmd** in, gevolgd door de Connection String voor de data base van uw SQL-groep. De verbindingstekenreeks moet de volgende parameters bevatten:

* **Server (-S):** Server in de notatie `<`Servernaam`>`.database.windows.net
* **Data Base (-d):** Database naam.
* **Id's van aanhalings tekens inschakelen (-I):** Id's tussen aanhalings tekens moeten zijn ingeschakeld om verbinding te maken met een exemplaar van een SQL-groep.

Als u gebruik wilt maken van SQL Server-verificatie, moet u de gebruikersnaam- en wachtwoordparameters toevoegen:

* **Gebruiker (-U):** Gebruiker van de server in de notatie `<`Gebruiker`>`
* **Wacht woord (-P):** Het wacht woord dat is gekoppeld aan de gebruiker.

Een voorbeeld: uw verbindingstekenreeks kan er als volgt uitzien:

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I
```

Als u geïntegreerde verificatie van Azure Active Directory wilt gebruiken, moet u de Azure Active Directory-parameters toevoegen:

* **Azure Active Directory Authentication (-G):** Azure Active Directory gebruiken voor verificatie

Een voorbeeld: uw verbindingstekenreeks kan er als volgt uitzien:

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -G -I
```

> [!NOTE]
> U moet [Azure Active Directory Authentication inschakelen](sql-data-warehouse-authentication.md) om te verifiëren met Active Directory.

## <a name="2-query"></a>2. Query’s uitvoeren

Wanneer verbinding is gemaakt, kunt u elke ondersteunde Transact-SQL-instructie voor het exemplaar uitvoeren.  In dit voorbeeld worden query's in de interactieve modus verzonden.

```sql
C:\>sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I
1> SELECT name FROM sys.tables;
2> GO
3> QUIT
```

In de volgende voorbeelden ziet u hoe u uw query's in de batchmodus uitvoert met behulp van de optie -Q of door uw SQL naar sqlcmd te sluizen.

```sql
sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I -Q "SELECT name FROM sys.tables;"
```

```sql
"SELECT name FROM sys.tables;" | sqlcmd -S MySqlDw.database.windows.net -d Adventure_Works -U myuser -P myP@ssword -I > .\tables.out
```

## <a name="next-steps"></a>Volgende stappen

Zie [Sqlcmd-documentatie](/sql/tools/sqlcmd-utility?toc=/azure/synapse-analytics/sql-data-warehouse/toc.json&bc=/azure/synapse-analytics/sql-data-warehouse/breadcrumb/toc.json&view=azure-sqldw-latest)voor meer informatie over de beschik bare opties in Sqlcmd.
