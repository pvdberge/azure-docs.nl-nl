---
title: Privé-eindpunten gebruiken voor het maken van een Azure Data Factory-pijplijn
description: Deze zelfstudie bevat stapsgewijze instructies voor het maken van een data factory met een pijplijn met behulp van Azure Portal. In dit voorbeeld gebruikt de pijplijn de kopieeractiviteit om gegevens vanuit Azure Blob Storage naar een Azure SQL-database te kopiëren.
services: data-factory
documentationcenter: ''
author: linda33wj
manager: shwang
ms.reviewer: douglasl
ms.service: data-factory
ms.workload: data-services
ms.topic: tutorial
ms.custom: seo-lt-2019
ms.date: 05/15/2020
ms.author: jingwang
ms.openlocfilehash: b2e666419a702832243c69bdb059f4447b02d756
ms.sourcegitcommit: 656c0c38cf550327a9ee10cc936029378bc7b5a2
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/28/2020
ms.locfileid: "89079452"
---
# <a name="copy-data-securely-from-azure-blob-storage-to-a-sql-database-by-using-private-endpoints"></a>Kopieer de gegevens veilig vanuit Azure Blob-opslag naar een SQL-database met privé-eindpunten

[!INCLUDE[appliesto-adf-xxx-md](includes/appliesto-adf-xxx-md.md)]

In deze zelfstudie maakt u een data factory met behulp van de Azure Data Factory-gebruikersinterface. *Met de pijplijn in deze data factory worden gegevens veilig gekopieerd van Azure Blob-opslag naar een Azure SQL-database (beide verlenen toegang aan geselecteerde netwerken) met behulp van privé-eindpunten in het door [Azure Data Factory beheerde virtueel netwerk](managed-virtual-network-private-endpoint.md).* Het configuratiepatroon in deze zelfstudie geldt voor het kopiëren van een gegevensarchief op basis van bestanden naar een relationeel gegevensarchief. Zie tabel [Ondersteunde gegevensarchieven en -indelingen](https://docs.microsoft.com/azure/data-factory/copy-activity-overview) voor een lijst met gegevensarchieven die als bron en als sink worden ondersteund.

> [!NOTE]
> Zie [Inleiding tot Azure Data Factory](https://docs.microsoft.com/azure/data-factory/introduction) als u niet bekend bent met Azure Data Factory.

In deze zelfstudie voert u de volgende stappen uit:

* Een data factory maken.
* Een pijplijn met kopieeractiviteit maken.


## <a name="prerequisites"></a>Vereisten
* **Azure-abonnement**. Als u nog geen abonnement op Azure hebt, maak dan een [gratis Azure-account](https://azure.microsoft.com/free/) aan voordat u begint.
* **Azure-opslagaccount**. U gebruikt de blobopslag als *bron*-gegevensopslag. Als u geen opslagaccount hebt, raadpleegt u het artikel [Een opslagaccount maken](https://docs.microsoft.com/azure/storage/common/storage-account-create?tabs=azure-portal) om een account te maken. *Zorg ervoor dat het opslagaccount alleen toegang toestaat vanuit geselecteerde netwerken.* 
* **Azure SQL-database**. U gebruikt de database als *sink*-gegevensopslag. Als u geen Azure SQL-database hebt, raadpleegt u het artikel [Een SQL-database maken](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-portal) om er een te maken. *Zorg ervoor dat het SQL Database-account alleen toegang toestaat vanuit geselecteerde netwerken.* 

### <a name="create-a-blob-and-a-sql-table"></a>Een blob en een SQL-tabel maken

Voer nu de volgende stappen uit om uw blobopslag en SQL-database voor te bereiden voor gebruik in deze zelfstudie.

#### <a name="create-a-source-blob"></a>Een bron-blob maken

1. Open Kladblok. Kopieer de volgende tekst en sla deze op uw schijf op in het bestand **emp.txt**:

    ```
    FirstName,LastName
    John,Doe
    Jane,Doe
    ```

1. Maak in de blobopslag een container met de naam **adftutorial**. Maak een map aan met de naam **invoer** in deze container. Vervolgens kunt u het bestand **emp.txt** uploaden naar de map **invoer**. Gebruik de Azure-portal of hulpprogramma's zoals [Azure Storage Explorer](https://storageexplorer.com/) voor deze taken.

#### <a name="create-a-sink-sql-table"></a>Een SQL-sink-tabel maken

1. Gebruik het volgende SQL-script om de tabel **dbo.emp** te maken in uw SQL database:

    ```sql
    CREATE TABLE dbo.emp
    (
        ID int IDENTITY(1,1) NOT NULL,
        FirstName varchar(50),
        LastName varchar(50)
    )
    GO

    CREATE CLUSTERED INDEX IX_emp_ID ON dbo.emp (ID);
    ```

1. Geef Azure-services toegang tot SQL Server. Zorg ervoor dat **Toegang tot Azure-services toestaan** is **ingeschakeld** voor de SQL-server, zodat Data Factory gegevens naar de SQL-server kan schrijven. Ga naar **Azure SQL Server** > **Overzicht** > **Serverfirewall instellen** als u deze instelling wilt verifiëren en inschakelen. Stel de optie **Toegang tot Azure-services toestaan** in op **AAN**.

## <a name="create-a-data-factory"></a>Een gegevensfactory maken
In deze stap maakt u een data factory en start u de Data Factory-gebruikersinterface om een pijplijn te maken in de data factory.

1. Open Microsoft Edge of Google Chrome. Op dit moment wordt de Data Factory-gebruikersinterface alleen ondersteund in de webbrowsers Microsoft Edge en Google Chrome.

1. Selecteer in het linkermenu **Een resource maken** > **Analyse** > **Data Factory**.

1. Voer op de pagina **Nieuwe data factory** **ADFTutorialDataFactory** in bij **Naam**.

   De naam van de Azure-gegevensfactory moet *wereldwijd uniek* zijn. Als u een foutbericht ontvangt over de naamwaarde, voert u een andere naam in voor de data factory (bijvoorbeeld uwnaamADFTutorialDataFactory). Zie [Data Factory - Naamgevingsregels](https://docs.microsoft.com/azure/data-factory/naming-rules) voor meer informatie over naamgevingsregels voor Data Factory-artefacten.

1. Selecteer het Azure-**abonnement** waarin u de data factory wilt maken.

1. Voer een van de volgende stappen uit voor **Resourcegroep**:

    - Selecteer **Bestaande gebruiken** en selecteer een bestaande resourcegroep in de vervolgkeuzelijst.
    - Selecteer **Nieuwe maken** en voer de naam van een resourcegroep in. 
     
    Zie [Resourcegroepen gebruiken om Azure-resources te beheren](https://docs.microsoft.com/azure/azure-resource-manager/management/overview) voor meer informatie. 

1. Selecteer **V2** onder **Versie**.

1. Selecteer onder **Locatie** een locatie voor de data factory. In de vervolgkeuzelijst worden alleen ondersteunde locaties weergegeven. De gegevensarchieven (bijvoorbeeld Azure Storage en SQL Database) en berekenservices (bijvoorbeeld Azure HDInsight) die door de data factory worden gebruikt, kunnen zich in andere regio's bevinden.

1. Selecteer **Maken**.

1. Als het maken is voltooid, ziet u de melding in het meldingencentrum. Selecteer **Naar de resource gaan** om naar de pagina **Data Factory** te gaan.

1. Selecteer de tegel **Maken en controleren** om de Data Factory-gebruikersinterface te openen op een afzonderlijk tabblad.

## <a name="create-an-azure-integration-runtime-in-data-factory-managed-virtual-network"></a>Een Azure-integratieruntime maken in een door Data Factory beheerd virtueel netwerk
In deze stap maakt u een Azure-integratieruntime en schakelt u het door Data Factory beheerde virtuele netwerk in.

1. Ga in de Data Factory-portal naar **Beheren** en selecteer **Nieuwe** om een nieuwe Azure-integratieruntime te maken.

   ![Schermopname van het maken van een nieuwe Azure-integratieruntime.](./media/tutorial-copy-data-portal-private/create-new-azure-ir.png)
1. Kies ervoor om een **Azure**-integratieruntime te maken.

   ![Schermopname met een nieuwe Azure-integratieruntime.](./media/tutorial-copy-data-portal-private/azure-ir.png)
1. Selecteer onder **Configuratie van virtueel netwerk (preview)** de optie **Inschakelen**.

   ![Schermopname van het inschakelen van een nieuwe Azure-integratieruntime.](./media/tutorial-copy-data-portal-private/enable-managed-vnet.png)
1. Selecteer **Maken**.

## <a name="create-a-pipeline"></a>Een pijplijn maken
In deze stap maakt u een pijplijn met kopieeractiviteit in de data factory. De kopieeractiviteit kopieert gegevens van de blobopslag naar SQL Database. In de [Quickstart](https://docs.microsoft.com/azure/data-factory/quickstart-create-data-factory-portal) hebt u een pijplijn gemaakt met de volgende stappen:

1. Maak een gekoppelde service.
1. Maak invoer- en uitvoergegevenssets.
1. Maak een pijplijn.

In deze zelfstudie begint u met het maken van een pijplijn. Vervolgens maakt u gekoppelde services en gegevenssets wanneer u deze nodig hebt om de pijplijn te configureren.

1. Selecteer op de pagina **Aan de slag** de optie **Pijplijn maken**.

   ![Schermopname waarin het maken van een pijplijn wordt weergegeven.](./media/doc-common-process/get-started-page.png)
1. Voer op het deelvenster Eigenschappen voor de pijplijn **CopyPipeline** in als naam van de pijplijn.

1. Breid in de werkset **Activiteiten** de categorie **Verplaatsen en transformeren** uit. Sleep de activiteit **Gegevens kopiëren** van de werkset en naar het ontwerpoppervlak voor pijplijnen. Geef **CopyFromBlobToSql** als naam op.

    ![Schermopname met de kopieeractiviteit.](./media/tutorial-copy-data-portal-private/drag-drop-copy-activity.png)

### <a name="configure-a-source"></a>Een bron configureren

>[!TIP]
>In deze zelfstudie gebruikt u **Accountsleutel** als verificatietype voor uw brongegevensarchief. U kunt ook andere ondersteunde verificatiemethoden kiezen, zoals **SAS URI**, **service-principal** en **beheerde identiteit**, als dat nodig is. Zie de bijbehorende secties in [Gegevens kopiëren en transformeren in Azure Blob-opslag met behulp van Azure Data Factory](https://docs.microsoft.com/azure/data-factory/connector-azure-blob-storage#linked-service-properties) voor meer informatie.
>
>Het ook raadzaam om Azure Key Vault te gebruiken om geheimen voor gegevensarchieven veilig op te slaan. Zie [Referenties opslaan in Azure Key Vault](https://docs.microsoft.com/azure/data-factory/store-credentials-in-key-vault) voor meer informatie en illustraties.

#### <a name="create-a-source-dataset-and-linked-service"></a>Een brongegevensset en een gekoppelde service maken

1. Ga naar het tabblad **Bron**. Selecteer **+Nieuw** om een brongegevensset te maken.

1. Selecteer in het dialoogvenster **Nieuwe gegevensset** de optie **Azure Blob Storage** en selecteer vervolgens **Doorgaan**. De brongegevens bevinden zich in een blobopslag, daarom selecteert u **Azure Blob-opslag** voor de brongegevensset.

1. Selecteer in het dialoogvenster **Indeling selecteren** het indelingstype van uw gegevens en selecteer vervolgens **Doorgaan**.

1. Voer in het dialoogvenster **Eigenschappen instellen** **SourceBlobDataset** in voor **Naam**. Schakel het selectievakje voor **Eerste rij als header** in. Selecteer onder het tekstvak **Gekoppelde service** de optie **+ Nieuw**.

1. Voer in het dialoogvenster **Nieuwe gekoppelde service (Azure Blob Storage)** **AzureStorageLinkedService** voor **Naam** in en selecteer uw opslagaccount in de lijst **Naam van opslagaccount**. 

1. Zorg ervoor dat u **Interactieve creatie** inschakelt. Het kan ongeveer één minuut duren voordat deze is ingeschakeld.

    ![Schermopname waarin interactieve creatie wordt weergegeven.](./media/tutorial-copy-data-portal-private/interactive-authoring.png)

1. Selecteer **Verbinding testen**. Dit moet mislukken wanneer het opslagaccount alleen toegang toestaat vanuit het **geselecteerde netwerk** en vereist dat Data Factory een privé-eindpunt maakt dat moet worden goedgekeurd voordat het kan worden gebruikt. In het foutbericht wordt een koppeling weergegeven om een privé-eindpunt te maken dat u kunt volgen om een beheerd privé-eindpunt te maken. U kunt ook rechtstreeks naar het tabblad **Beheren** gaan en de instructies in de [volgende sectie](#create-a-managed-private-endpoint) volgen om een beheerd privé-eindpunt te maken.

   > [!NOTE]
   > Het tabblad **Beheren** is mogelijk niet beschikbaar voor alle exemplaren van data factory. Als u het niet ziet, kunt u toegang krijgen tot privé-eindpunten door **Auteur** > **Verbindingen** > **Privé-eindpunt** te selecteren.
1. Houd het dialoogvenster geopend en ga vervolgens naar uw opslagaccount.

1. Volg de instructies in [deze sectie](#approval-of-a-private-link-in-a-storage-account) om de persoonlijke koppeling goed te keuren.

1. Ga terug naar het dialoogvenster. Selecteer **Test de verbinding** opnieuw en selecteer vervolgens **Maken** om de gekoppelde service te implementeren.

1. Nadat de gekoppelde service is gemaakt, gaat u terug naar de pagina **Eigenschappen instellen**. Selecteer naast **Bestandspad** de knop **Bladeren**.

1. Ga naar de map **adftutorial/input**, selecteer het bestand **emp.txt** en klik vervolgens op **Voltooien**.

1. Selecteer **OK**. U wordt automatisch naar de pagina met de pijplijn geleid. Controleer op het tabblad **Bron** of **SourceBlobDataset** is geselecteerd. Selecteer **Gegevens vooraf bekijken** om een voorbeeld van de gegevens op deze pagina te bekijken.

    ![Schermopname met de brongegevensset.](./media/tutorial-copy-data-portal-private/source-dataset-selected.png)

#### <a name="create-a-managed-private-endpoint"></a>Een beheerd privé-eindpunt maken

Als u de hyperlink niet hebt geselecteerd tijdens het testen van de verbinding, volgt u het pad. Nu moet u een beheerd privé-eindpunt maken dat u verbindt met de gekoppelde service die u hebt gemaakt.

1. Ga naar het tabblad **Beheren**.

   > [!NOTE]
   > Het tabblad **Beheren** is mogelijk niet beschikbaar voor alle exemplaren van Data Factory. Als u het niet ziet, kunt u toegang krijgen tot privé-eindpunten door **Auteur** > **Verbindingen** > **Privé-eindpunt** te selecteren.

1. Ga naar het gedeelte **Beheerde privé-eindpunten**.

1. Selecteer **+ Nieuwe** onder **Beheerde privé-eindpunten**.

    ![Schermafbeelding met de knoppen Beheerde privé-eindpunten en Nieuw.](./media/tutorial-copy-data-portal-private/new-managed-private-endpoint.png) 

1. Selecteer de tegel **Azure Blob Storage** in de lijst en selecteer **Doorgaan**.

1. Voer de naam in van het opslagaccount dat u hebt gemaakt.

1. Selecteer **Maken**.

1. Na enkele seconden wordt voor de privékoppeling een goedkeuring vereist.

1. Selecteer het privé-eindpunt dat u hebt gemaakt. U ziet een hyperlink waarmee u het privé-eindpunt kunt goedkeuren op het niveau van het opslagaccount.

    ![Schermafbeelding met het deelvenster Beheerd privé-eindpunt.](./media/tutorial-copy-data-portal-private/manage-private-endpoint.png) 

#### <a name="approval-of-a-private-link-in-a-storage-account"></a>Goedkeuring van een privékoppeling in een opslagaccount
1. Ga in het opslagaccount naar **Privé-eindpuntverbindingen** in het gedeelte **Instellingen**.

1. Selecteer het selectievakje voor het privé-eindpunt dat u hebt gemaakt en selecteer **Goedkeuren**.

    ![Schermopname van de knop Goedkeuren voor het privé-eindpunt.](./media/tutorial-copy-data-portal-private/approve-private-endpoint.png)

1. Voeg een beschrijving toe en selecteer **ja**.
1. Ga terug naar het gedeelte **Beheerde privé-eindpunten** van het tabblad **Beheren** in Data Factory.
1. Na ongeveer een of twee minuten ziet u dat de goedkeuring van uw privé-eindpunt wordt weergegeven in de Data Factory-gebruikersinterface.


### <a name="configure-a-sink"></a>Een sink configureren
>[!TIP]
>In deze zelfstudie gebruikt u **SQL-verificatie** als verificatietype voor uw sink-gegevensarchief. U kunt ook andere ondersteunde verificatiemethoden kiezen, zoals **service-principal** en **beheerde identiteit**, als dat nodig is. Zie de bijbehorende secties in [Gegevens kopiëren en transformeren in Azure SQL Database met behulp van Azure Data Factory](https://docs.microsoft.com/azure/data-factory/connector-azure-sql-database#linked-service-properties) voor meer informatie.
>
>Het ook raadzaam om Azure Key Vault te gebruiken om geheimen voor gegevensarchieven veilig op te slaan. Zie [Referenties opslaan in Azure Key Vault](https://docs.microsoft.com/azure/data-factory/store-credentials-in-key-vault) voor meer informatie en illustraties.

#### <a name="create-a-sink-dataset-and-linked-service"></a>Sink-gegevenssets en gekoppelde service maken
1. Ga naar het tabblad **Sink** en selecteer **+Nieuw** om een sink-gegevensset te maken.

1. Voer in het dialoog venster **Nieuwe gegevensset** **SQL** in het zoekvak in om de connectors te filteren. Selecteer **Azure SQL Database** en vervolgens **Doorgaan**. In deze zelfstudie kopieert u gegevens naar een SQL database.

1. Voer in het dialoogvenster **Eigenschappen instellen** **OutputSqlDataset** in voor **Naam**. Selecteer **+ Nieuw** in de vervolgkeuzelijst **Gekoppelde service**. Een gegevensset moet worden gekoppeld aan een gekoppelde service. De gekoppelde service beschikt over de verbindingsreeks die door Data Factory wordt gebruikt om tijdens runtime een verbinding met de SQL-database tot stand te brengen. De dataset geeft informatie over de container, map en het bestand (optioneel) met de brongegevens.

1. Voer in het dialoogvenster **Nieuwe gekoppelde service (Azure SQL Database)** de volgende stappen uit:

    1. Geef **AzureSqlDatabaseLinkedService** op als **Naam**.
    1. Selecteer bij **Servernaam** uw SQL Server-exemplaar.
    1. Zorg ervoor dat u **Interactieve creatie** inschakelt.
    1. Selecteer uw SQL-database bij **Databasenaam**.
    1. Voer bij **Gebruikersnaam** de naam van de gebruiker in.
    1. Voer bij **Wachtwoord** het wachtwoord voor de gebruiker in.
    1. Selecteer **Verbinding testen**. Dit moet mislukken omdat de SQL-server alleen toegang toestaat vanuit **Geselecteerde netwerken** en vereist dat Data Factory een privé-eindpunt maakt dat moet worden goedgekeurd voordat het kan worden gebruikt. In het foutbericht wordt een koppeling weergegeven om een privé-eindpunt te maken dat u kunt volgen om een beheerd privé-eindpunt te maken. U kunt ook rechtstreeks naar het tabblad **Beheren** gaan en de instructies in de volgende sectie volgen om een beheerd privé-eindpunt te maken.
    1. Houd het dialoogvenster geopend en ga vervolgens naar de geselecteerde SQL-server.
    1. Volg de instructies in [deze sectie](#approval-of-a-private-link-in-sql-server) om de persoonlijke koppeling goed te keuren.
    1. Ga terug naar het dialoogvenster. Selecteer **Test de verbinding** opnieuw en selecteer vervolgens **Maken** om de gekoppelde service te implementeren.

1. Deze gaat automatisch naar het dialoogvenster **Eigenschappen instellen**. Selecteer bij **Tabel** **[dbo].[emp]** . Selecteer vervolgens **OK**.

1. Ga naar het tabblad met de pijplijn en controleer bij **Sink-gegevensset** of **OutputSqlDataset** is geselecteerd.

    ![Schermopname met het tabblad Pijplijn.](./media/tutorial-copy-data-portal-private/pipeline-tab-2.png)

Optioneel kunt u het schema van de bron toewijzen aan het overeenkomstige schema van het doel door [Schematoewijzing in kopieeractiviteit](https://docs.microsoft.com/azure/data-factory/copy-activity-schema-and-type-mapping) te volgen.

#### <a name="create-a-managed-private-endpoint"></a>Een beheerd privé-eindpunt maken

Als u de hyperlink niet hebt geselecteerd tijdens het testen van de verbinding, volgt u het pad. Nu moet u een beheerd privé-eindpunt maken dat u verbindt met de gekoppelde service die u hebt gemaakt.

1. Ga naar het tabblad **Beheren**.
1. Ga naar het gedeelte **Beheerde privé-eindpunten**.
1. Selecteer **+ Nieuwe** onder **Beheerde privé-eindpunten**.

    ![Schermafbeelding met de knoppen Beheerde privé-eindpunten en Nieuw.](./media/tutorial-copy-data-portal-private/new-managed-private-endpoint.png) 

1. Selecteer de tegel **Azure SQL Database** in de lijst en selecteer **Doorgaan**.
1. Voer de naam in van de SQL-Server die u hebt geselecteerd.
1. Selecteer **Maken**.
1. Na enkele seconden wordt voor de privékoppeling een goedkeuring vereist.
1. Selecteer het privé-eindpunt dat u hebt gemaakt. U ziet een hyperlink waarmee u het privé-eindpunt kunt goedkeuren op het niveau van de SQL-server.


#### <a name="approval-of-a-private-link-in-sql-server"></a>Goedkeuring van een privékoppeling in SQL Server
1. Ga in de SQL-server naar **Privé-eindpuntverbindingen** in het gedeelte **Instellingen**.
1. Selecteer het selectievakje voor het privé-eindpunt dat u hebt gemaakt en selecteer **Goedkeuren**.
1. Voeg een beschrijving toe en selecteer **ja**.
1. Ga terug naar het gedeelte **Beheerde privé-eindpunten** van het tabblad **Beheren** in Data Factory.
1. Het duurt een of twee minuten voordat de goedkeuring voor uw privé-eindpunt wordt weergegeven.

#### <a name="debug-and-publish-the-pipeline"></a>Fouten opsporen in de pijplijn en de pijplijn publiceren

U kunt fouten opsporen in een pijplijn voordat u artefacten (gekoppelde services, gegevenssets en pijplijn) publiceert naar Data Factory of uw eigen Azure Repos Git-opslagplaats.

1. Selecteer **Fouten opsporen** om fouten op te sporen in de pijplijn. De status van de pijplijnuitvoering wordt weergegeven op het tabblad **Uitvoer** onder in het venster.
1. Als de pijplijn kan worden uitgevoerd, selecteert u **Alles publiceren** in de bovenste werkbalk. Met deze actie publiceert u entiteiten (gegevenssets en pijplijnen) die u in Data Factory hebt gemaakt.
1. Wacht tot u het bericht **Gepubliceerd** ziet. Als u meldingsberichten wilt zien, selecteert u in de rechter bovenhoek **Meldingen weergeven** (belknop).


#### <a name="summary"></a>Samenvatting
Met de pijplijn in dit voorbeeld worden gegevens gekopieerd van Blob Storage naar SQL Database met behulp van privé-eindpunten in het door Data Factory beheerde virtuele netwerk. U hebt geleerd hoe u:

* Een data factory maken.
* Een pijplijn met kopieeractiviteit maken.

