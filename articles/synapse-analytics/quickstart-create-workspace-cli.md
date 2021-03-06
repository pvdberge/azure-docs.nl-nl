---
title: 'Quickstart: Een Synapse-werkruimte maken met Azure CLI'
description: Maak een Azure Synapse-werkruimte met behulp van Azure CLI door de stappen in deze handleiding te volgen.
services: synapse-analytics
author: alehall
ms.service: synapse-analytics
ms.topic: quickstart
ms.subservice: ''
ms.date: 08/25/2020
ms.author: alehall
ms.reviewer: jrasnick, carlrab
ms.openlocfilehash: 7f0bf7d409c5e47abaaa5b59271f55952d8ccff4
ms.sourcegitcommit: 927dd0e3d44d48b413b446384214f4661f33db04
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/26/2020
ms.locfileid: "88871581"
---
# <a name="quickstart-create-an-azure-synapse-workspace-with-azure-cli"></a>Quickstart: Een Azure Synapse-werkruimte maken met Azure CLI

Azure CLI is de nieuwe opdrachtregel van Azure voor het beheren van Azure-resources. U kunt deze gebruiken in uw browser met Azure Cloud Shell. U kunt deze ook installeren op Mac OS, Linux of Windows en uitvoeren vanaf de opdrachtregel.

In deze quickstart leert u hoe u een Synapse-werkruimte maakt met behulp van Azure CLI.

Als u geen Azure-abonnement hebt, [maakt u een gratis account voordat u begint](https://azure.microsoft.com/free/).

## <a name="prerequisites"></a>Vereisten

- Download en installeer [jq](https://stedolan.github.io/jq/download/), een lichtgewicht en flexibele opdrachtregel-JSON-processor
- [Azure Data Lake Storage Gen2-opslagaccount](../storage/common/storage-account-create.md?toc=/azure/synapse-analytics/toc.json&bc=/azure/synapse-analytics/breadcrumb/toc.json)

    > [!IMPORTANT]
    > De Azure Synapse-werkruimte moet kunnen lezen uit en schrijven naar het geselecteerde ADLS Gen2-account. Daarnaast moet u voor elk opslagaccount dat u als primair opslagaccount koppelt **hiërarchische naamruimte** hebben ingeschakeld bij het maken van het opslagaccount, zoals beschreven op de pagina [Een opslagaccount maken](https://docs.microsoft.com/azure/storage/common/storage-account-create?tabs=azure-portal#create-a-storage-account). 

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="install-the-azure-cli-locally"></a>De Azure CLI lokaal installeren

Zie [Azure CLI installeren](/cli/azure/install-azure-cli) als u Azure CLI liever lokaal installeert en gebruikt.

Als u de Azure CLI lokaal uitvoert, moet u zich aanmelden en verifiëren. Deze stap is niet nodig als u Azure Cloud Shell gebruikt. Als u zich bij Azure CLI wilt aanmelden, voert u `az login` uit en verifieert u zich in het browservenster:

```azurecli
az login
```

Zie [Aanmelden met Azure CLI](/cli/azure/authenticate-azure-cli) voor meer informatie over verificatie met Azure CLI.

## <a name="install-azure-synapse-extension-for-azure-cli"></a>De Azure Synapse-extensie voor Azure CLI installeren

```azurecli
az extension add --name synapse
```

> [!WARNING]
> De Azure Synapse-extensie voor Azure CLI is beschikbaar als preview-versie.

## <a name="create-an-azure-synapse-workspace-using-the-azure-cli"></a>Een Azure Synapse-werkruimte maken met behulp van Azure CLI

1. Definieer de benodigde omgevingsvariabelen om resources voor de Azure Synapse-ruimte te maken.

    | Naam van omgevingsvariabele | Beschrijving |
    |---|---|---|
    |StorageAccountName| Naam van uw bestaande ADLS Gen2-opslagaccount.|
    |StorageAccountResourceGroup| Naam van de resourcegroep van uw bestaande ADLS Gen2-opslagaccount. |
    |FileShareName| Naam van uw bestaande opslagbestandssysteem.|
    |SynapseResourceGroup| Kies een nieuwe naam voor uw Azure Synapse-resourcegroep. |
    |Region| Kies een van de [Azure-regio’s](https://azure.microsoft.com/global-infrastructure/geographies/#overview). |
    |SynapseWorkspaceName| Kies een unieke naam voor uw nieuwe Azure Synapse-werkruimte. |
    |SqlUser| Kies een waarde voor een nieuwe gebruikersnaam.|
    |SqlPassword| Kies een veilig wachtwoord.|
    |||

2. Maak een resourcegroep als container voor uw Azure Synapse-werkruimte:
    ```azurecli
    az group create --name $SynapseResourceGroup --location $Region
    ```
3. Haal de sleutel van het ADLS Gen2-opslagaccount op:
    ```azurecli
    StorageAccountKey=$(az storage account keys list \
      --account-name $StorageAccountName \
      | jq -r '.[0] | .value')
    ```
4. Haal de eindpunt-URL van het ADLS Gen2-opslagaccount op:
    ```azurecli
    StorageEndpointUrl=$(az storage account show \
      --name $StorageAccountName \
      --resource-group $StorageAccountResourceGroup \
      | jq -r '.primaryEndpoints | .dfs')
    ```

5. (Optioneel) U kunt altijd controleren wat de sleutel en eindpunt-URL van uw ADLS Gen2-opslagaccount zijn:
    ```azurecli
    echo "Storage Account Key: $StorageAccountKey"
    echo "Storage Endpoint URL: $StorageEndpointUrl"
    ```

6. Maak een Azure Synapse-werkruimte:
    ```azurecli
    az synapse workspace create \
      --name $SynapseWorkspaceName \
      --resource-group $SynapseResourceGroup \
      --storage-account $StorageAccountName \
      --file-system $FileShareName \
      --sql-admin-login-user $SqlUser \
      --sql-admin-login-password $SqlPassword \
      --location $Region
    ```

7. Haal de Web-URL en Dev-URL van de Azure Synapse-werkruimte op:
    ```azurecli
    WorkspaceWeb=$(az synapse workspace show --name $SynapseWorkspaceName --resource-group $SynapseResourceGroup | jq -r '.connectivityEndpoints | .web')

    WorkspaceDev=$(az synapse workspace show --name $SynapseWorkspaceName --resource-group $SynapseResourceGroup | jq -r '.connectivityEndpoints | .dev')
    ```

8. Maak een firewallregel om vanaf uw computer toegang te krijgen tot de Azure Synapse-werkruimte:

    ```azurecli
    ClientIP=$(curl -sb -H "Accept: application/json" "$WorkspaceDev" | jq -r '.message')
    ClientIP=${ClientIP##'Client Ip address : '}
    echo "Creating a firewall rule to enable access for IP address: $ClientIP"

    az synapse workspace firewall-rule create --end-ip-address $ClientIP --start-ip-address $ClientIP --name "Allow Client IP" --resource-group $SynapseResourceGroup --workspace-name $SynapseWorkspaceName
    ```

9. Open de Web-URL van de Azure Synapse-werkruimte, die in de omgevingsvariabele `WorkspaceWeb` is opgeslagen, om toegang te krijgen tot uw werkruimte:

    ```azurecli
    echo "Open your Azure Synapse Workspace Web URL in the browser: $WorkspaceWeb"
    ```
    
    [ ![Web-URL van Azure Synapse-werkruimte](media/quickstart-create-synapse-workspace-cli/create-workspace-cli-1.png) ](media/quickstart-create-synapse-workspace-cli/create-workspace-cli-1.png#lightbox)


## <a name="clean-up-resources"></a>Resources opschonen

Voer de onderstaande stappen uit om de Azure Synapse-werkruimte te verwijderen.
> [!WARNING]
> Als u een Azure Synapse-werkruimte verwijdert, worden de analyse-engines en de gegevens die zijn opgeslagen in de database van de SQL-pools die het bevat en de metagegevens van de werkruimte verwijderd. Er kan geen verbinding meer worden gemaakt met het SQL- of Apache Spark-eindpunt. Alle codeartefacten worden verwijderd (query's, notebooks, taakdefinities en pijplijnen).
>
> Als u de werkruimte verwijdert, heeft dit **geen** invloed op de gegevens in het Data Lake Storage Gen2-account dat aan de werkruimte is gekoppeld.

Als u de Azure Synapse-werkruimte wilt verwijderen, voert u de volgende opdracht uit:

```azurecli
az synapse workspace delete --name $SynapseWorkspaceName --resource-group $SynapseResourceGroup
```

## <a name="next-steps"></a>Volgende stappen

Vervolgens kunt u [SQL-pools maken](quickstart-create-sql-pool-studio.md) of [Apache Spark-pools maken](quickstart-create-apache-spark-pool-studio.md) zodat u uw gegevens kunt gaan analyseren en verkennen.
