---
title: Op rollen gebaseerd toegangsbeheer in Azure Cosmos DB
description: Meer informatie over hoe Azure Cosmos DB database beveiliging biedt met Active Directory-integratie (RBAC).
author: markjbrown
ms.service: cosmos-db
ms.topic: conceptual
ms.date: 06/03/2020
ms.author: mjbrown
ms.openlocfilehash: 6edf5de852ea836de8be02636dd8a971ccebb86d
ms.sourcegitcommit: 3d56d25d9cf9d3d42600db3e9364a5730e80fa4a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2020
ms.locfileid: "87530568"
---
# <a name="role-based-access-control-in-azure-cosmos-db"></a>Op rollen gebaseerd toegangsbeheer in Azure Cosmos DB

Azure Cosmos DB biedt ingebouwde op rollen gebaseerd toegangs beheer (RBAC) voor algemene beheer scenario's in Azure Cosmos DB. Een persoon die een profiel in Azure Active Directory heeft, kan deze Azure-rollen toewijzen aan gebruikers, groepen, service-principals of beheerde identiteiten voor het verlenen of weigeren van toegang tot resources en bewerkingen op Azure Cosmos DB-resources. Roltoewijzingen zijn alleen gericht op toegangs beheer, waaronder toegang tot Azure Cosmos-accounts, data bases, containers en aanbiedingen (door Voer).

## <a name="built-in-roles"></a>Ingebouwde rollen

Hier volgen de ingebouwde rollen die door Azure Cosmos DB worden ondersteund:

|**Ingebouwde rol**  |**Beschrijving**  |
|---------|---------|
|[Inzender voor DocumentDB-accounts](../role-based-access-control/built-in-roles.md#documentdb-account-contributor)|Kan Azure Cosmos DB accounts beheren.|
|[Lezer van Cosmos DB-account](../role-based-access-control/built-in-roles.md#cosmos-db-account-reader-role)|Kan gegevens van Azure Cosmos DB-account lezen.|
|[Cosmos-back-upoperator](../role-based-access-control/built-in-roles.md#cosmosbackupoperator)|Kan een herstel aanvraag indienen voor een Azure Cosmos-data base of een container.|
|[Cosmos DB-operator](../role-based-access-control/built-in-roles.md#cosmos-db-operator)|Kan Azure Cosmos-accounts,-data bases en-containers inrichten, maar heeft geen toegang tot de sleutels die nodig zijn voor toegang tot de gegevens.|

> [!IMPORTANT]
> RBAC-ondersteuning in Azure Cosmos DB is alleen van toepassing op beheer vlak bewerkingen. Gegevensvlak bewerkingen worden beveiligd met behulp van hoofd sleutels of bron tokens. Zie [beveiligde toegang tot gegevens in azure Cosmos DB](secure-access-to-data.md) voor meer informatie.

## <a name="identity-and-access-management-iam"></a>Identiteits-en toegangs beheer (IAM)

Het deel venster **toegangs beheer (IAM)** in de Azure portal wordt gebruikt voor het configureren van toegangs beheer op basis van rollen op Azure Cosmos-resources. De rollen worden toegepast op gebruikers, groepen, service-principals en beheerde identiteiten in Active Directory. U kunt ingebouwde rollen of aangepaste rollen gebruiken voor individuen en groepen. De volgende scherm afbeelding toont Active Directory Integration (RBAC) met behulp van toegangs beheer (IAM) in de Azure Portal:

:::image type="content" source="./media/role-based-access-control/database-security-identity-access-management-rbac.png" alt-text="Toegangs beheer (IAM) in de Azure Portal-demonstrerende database beveiliging":::

## <a name="custom-roles"></a>Aangepaste rollen

Naast de ingebouwde rollen kunnen gebruikers ook [aangepaste rollen](../role-based-access-control/custom-roles.md) maken in Azure en deze rollen Toep assen op service-principals in alle abonnementen binnen hun Active Directory Tenant. Aangepaste rollen bieden gebruikers de mogelijkheid om Azure-roldefinities te maken met een aangepaste set van de bewerkingen van de resource provider. Als u wilt weten welke bewerkingen beschikbaar zijn voor het maken van aangepaste rollen voor Azure Cosmos DB raadpleegt u [Azure Cosmos DB resource provider bewerkingen](../role-based-access-control/resource-provider-operations.md#microsoftdocumentdb)

## <a name="preventing-changes-from-the-azure-cosmos-db-sdks"></a><a id="prevent-sdk-changes"></a>Wijzigingen van de Azure Cosmos DB Sdk's voor komen

De resource provider van Azure Cosmos DB kan worden vergrendeld om te voor komen dat er wijzigingen worden aangebracht in resources van een client die verbinding maken met behulp van de account sleutels (dat wil zeggen toepassingen die verbinding maken via de Azure Cosmos SDK). Dit omvat ook wijzigingen die zijn aangebracht vanuit het Azure Portal. Deze functie kan wenselijk zijn voor gebruikers die een hogere mate van controle en governance voor productie omgevingen willen. Door wijzigingen van de SDK te voor komen, kunt u ook functies als resource vergrendelingen en Diagnostische logboeken voor bewerkingen in het vlak van het besturings element. De clients die verbinding maken vanaf Azure Cosmos DB SDK, kunnen geen eigenschappen wijzigen voor de Azure Cosmos-accounts,-data bases,-containers en-door voer. De bewerkingen met betrekking tot het lezen en schrijven van gegevens naar Cosmos-containers zelf worden niet beïnvloed.

Als deze functie is ingeschakeld, kunnen wijzigingen aan resources alleen worden aangebracht van een gebruiker met de juiste Azure-rol en Azure Active Directory referenties, inclusief beheerde service-identiteiten.

> [!WARNING]
> Het inschakelen van deze functie kan gevolgen hebben voor uw toepassing. Zorg ervoor dat u bekend bent met de gevolgen voordat u deze functie inschakelt.

### <a name="check-list-before-enabling"></a>Lijst controleren voordat deze wordt ingeschakeld

Met deze instelling wordt voor komen dat alle Cosmos-bronnen worden gewijzigd vanuit elke client die verbinding maakt met behulp van account sleutels, inclusief een Cosmos DB SDK, alle hulpprogram ma's die verbinding maken via account sleutels of via de Azure Portal. Als u problemen of fouten van toepassingen na het inschakelen van deze functie wilt voor komen, controleert u of toepassingen of Azure Portal gebruikers een van de volgende acties uitvoeren voordat u deze functie inschakelt, waaronder:

- Elke wijziging van het Cosmos-account met alle eigenschappen of het toevoegen of verwijderen van regio's.

- Maken, verwijderen van onderliggende resources, zoals data bases en containers. Dit omvat resources voor andere Api's, zoals Cassandra-, MongoDB-, Gremlin-en Table-resources.

- De door Voer van resources op Data Base-of container niveau bijwerken.

- Container eigenschappen wijzigen, inclusief het index beleid, de TTL en de unieke sleutels.

- Opgeslagen procedures, triggers of door de gebruiker gedefinieerde functies wijzigen.

Als uw toepassingen (of gebruikers via Azure Portal) een van deze acties uitvoeren, moeten ze worden gemigreerd om te worden uitgevoerd via [arm-sjablonen](manage-sql-with-resource-manager.md), [Power shell](manage-with-powershell.md), [Azure cli](manage-with-cli.md), rest of [Azure Management Library](https://github.com/Azure-Samples/cosmos-management-net). Houd er rekening mee dat Azure Management beschikbaar is in [meerdere talen](https://docs.microsoft.com/azure/?product=featured#languages-and-tools).

### <a name="set-via-arm-template"></a>Instellen via ARM-sjabloon

Als u deze eigenschap wilt instellen met behulp van een ARM-sjabloon, werkt u uw bestaande sjabloon bij of exporteert u een nieuwe sjabloon voor uw huidige implementatie. vervolgens voegt `"disableKeyBasedMetadataWriteAccess": true` u de aan de eigenschappen voor de `databaseAccounts` resources toe. Hieronder volgt een eenvoudig voor beeld van een Azure Resource Manager sjabloon met deze eigenschaps instelling.

```json
{
    {
      "type": "Microsoft.DocumentDB/databaseAccounts",
      "name": "[variables('accountName')]",
      "apiVersion": "2020-04-01",
      "location": "[parameters('location')]",
      "kind": "GlobalDocumentDB",
      "properties": {
        "consistencyPolicy": "[variables('consistencyPolicy')[parameters('defaultConsistencyLevel')]]",
        "locations": "[variables('locations')]",
        "databaseAccountOfferType": "Standard",
        "disableKeyBasedMetadataWriteAccess": true
        }
    }
}
```

> [!IMPORTANT]
> Zorg ervoor dat u de andere eigenschappen voor uw account en onderliggende resources opneemt wanneer redploying met deze eigenschap. Implementeer deze sjabloon niet als zodanig, of Hiermee worden al uw account eigenschappen opnieuw ingesteld.

### <a name="set-via-azure-cli"></a>Instellen via Azure CLI

Gebruik de onderstaande opdracht om in te scha kelen met behulp van Azure CLI:

```azurecli-interactive
az cosmosdb update  --name [CosmosDBAccountName] --resource-group [ResourceGroupName]  --disable-key-based-metadata-write-access true

```

### <a name="set-via-powershell"></a>Instellen via Power shell

Als u het gebruik van Azure PowerShell wilt inschakelen, gebruikt u de onderstaande opdracht:

```azurepowershell-interactive
Update-AzCosmosDBAccount -ResourceGroupName [ResourceGroupName] -Name [CosmosDBAccountName] -DisableKeyBasedMetadataWriteAccess true
```

## <a name="next-steps"></a>Volgende stappen

- [Wat is Azure Role-based Access Control (Azure RBAC)](../role-based-access-control/overview.md)
- [Aangepaste Azure-rollen](../role-based-access-control/custom-roles.md)
- [Bewerkingen voor de resource provider Azure Cosmos DB](../role-based-access-control/resource-provider-operations.md#microsoftdocumentdb)
