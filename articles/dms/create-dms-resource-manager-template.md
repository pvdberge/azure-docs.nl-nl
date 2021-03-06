---
title: Een instantie van DMS maken (Azure Resource Manager-sjabloon)
description: Lees hoe u een instantie van Database Migration Service maakt met behulp van een Azure Resource Manager-sjabloon (ARM-sjabloon).
author: MashaMSFT
ms.topic: quickstart
ms.custom: subject-armqs
ms.author: mathoma
ms.date: 06/29/2020
ms.service: dms
ms.openlocfilehash: 24a0d16a6ff052df4b7a9bcdd078542987b4fd50
ms.sourcegitcommit: d18a59b2efff67934650f6ad3a2e1fe9f8269f21
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88661177"
---
# <a name="quickstart-create-instance-of-azure-database-migration-service-using-arm-template"></a>Quickstart: Een instantie van Azure Database Migration Service maken met behulp van een ARM-sjabloon

Gebruik deze Azure Resource Manager-sjabloon (ARM-sjabloon) om een instantie van de Azure Database Migration Service te implementeren. 

[!INCLUDE [About Azure Resource Manager](../../includes/resource-manager-quickstart-introduction.md)]

Als uw omgeving voldoet aan de vereisten en u benkend bent met het gebruik van ARM-sjablonen, selecteert u de knop **Implementeren naar Azure**. De sjabloon wordt in Azure Portal geopend.

[![Implementeren in Azure](../media/template-deployments/deploy-to-azure.svg)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3a%2f%2fraw.githubusercontent.com%2fAzure%2fazure-quickstart-templates%2fmaster%2f101-azure-database-migration-simple-deploy%2fazuredeploy.json)

## <a name="prerequisites"></a>Vereisten

Voor de ARM-sjabloon voor Azure Database Migration Service is het volgende vereist: 

- De nieuwste versie van de [Azure CLI](/cli/azure/install-azure-cli) en/of [PowerShell](/powershell/scripting/install/installing-powershell). 
- Een Azure-abonnement. Als u nog geen abonnement hebt, maakt u een [gratis account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) voordat u begint.

## <a name="review-the-template"></a>De sjabloon controleren

De sjabloon die in deze quickstart wordt gebruikt, komt uit [Azure-quickstartsjablonen](https://azure.microsoft.com/resources/templates/101-azure-database-migration-simple-deploy/).

:::code language="json" source="~/quickstart-templates/101-azure-database-migration-simple-deploy/azuredeploy.json":::

Er worden drie Azure-resources gedefinieerd in de sjabloon: 

- [Microsoft.Network/virtualNetworks](/azure/templates/microsoft.network/virtualnetworks): Hiermee wordt het virtuele netwerk gemaakt. 
- [Microsoft.Network/virtualNetworks/subnets](/azure/templates/microsoft.network/virtualnetworks/subnets): Hiermee wordt het subnet gemaakt. 
- [Microsoft.DataMigration/services](/azure/templates/microsoft.datamigration/services): Hiermee wordt een instantie van de Azure Database Migration Service geïmplementeerd. 

Meer sjablonen voor Azure Database Migration Service zijn te vinden in de [galerie met quickstart-sjablonen](https://azure.microsoft.com/resources/templates/?resourceType=Microsoft.Datamigration&pageNumber=1&sort=Popular).


## <a name="deploy-the-template"></a>De sjabloon implementeren

1. Selecteer de volgende afbeelding om u aan te melden bij Azure en een sjabloon te openen. Met de sjabloon wordt een instantie van de Azure Database Migration Service gemaakt. 

   [![Implementeren in Azure](../media/template-deployments/deploy-to-azure.svg)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3a%2f%2fraw.githubusercontent.com%2fAzure%2fazure-quickstart-templates%2fmaster%2f101-azure-database-migration-simple-deploy%2fazuredeploy.json)

2. Typ of selecteer de volgende waarden.

    * **Abonnement**: Selecteer een Azure-abonnement.
    * **Resourcegroep**: Selecteer een bestaande resourcegroep in de vervolgkeuzelijst of selecteer **Nieuwe maken** om een nieuwe resourcegroep te maken. 
    * **Regio**: De locatie waar de resources worden geïmplementeerd.
    * **Servicenaam**: De naam van de nieuwe migratieservice.
    * **Locatie**: De locatie van de resourcegroep. Laat de standaardwaarde `[resourceGroup().location]` staan.
    * **VNet-naam**: Naam van het nieuwe virtuele netwerk.
    * **Subnetnaam**: Naam van het nieuwe subnet dat is gekoppeld aan het virtuele netwerk.



3. Selecteer **Controleren + maken**. Nadat de instantie van Azure Database Migration Service is geïmplementeerd, ontvangt u een melding. 


Voor het implementeren van de sjabloon wordt de Azure-portal gebruikt. Naast Azure Portal kunt u ook de Azure PowerShell, Azure CLI en REST API gebruiken. Zie [Sjablonen implementeren](../azure-resource-manager/templates/deploy-powershell.md) voor meer informatie over andere implementatiemethoden.

## <a name="review-deployed-resources"></a>Geïmplementeerde resources bekijken

U kunt de Azure CLI gebruiken om geïmplementeerde resources te controleren. 


```azurecli-interactive
echo "Enter the resource group where your SQL Server VM exists:" &&
read resourcegroupName &&
az resource list --resource-group $resourcegroupName 
```


## <a name="clean-up-resources"></a>Resources opschonen

Wanneer u deze niet meer nodig hebt, verwijdert u de resourcegroep met Azure CLI of Azure PowerShell:

# <a name="cli"></a>[CLI](#tab/CLI)

```azurecli-interactive
echo "Enter the Resource Group name:" &&
read resourceGroupName &&
az group delete --name $resourceGroupName &&
echo "Press [ENTER] to continue ..."
```

# <a name="powershell"></a>[PowerShell](#tab/PowerShell)

```azurepowershell-interactive
$resourceGroupName = Read-Host -Prompt "Enter the Resource Group name"
Remove-AzResourceGroup -Name $resourceGroupName
Write-Host "Press [ENTER] to continue..."
```

---

## <a name="next-steps"></a>Volgende stappen

Zie voor een stapsgewijze zelfstudie die u door het proces van het maken van een sjabloon leidt:

> [!div class="nextstepaction"]
> [Zelfstudie: Uw eerste ARM-sjabloon maken en implementeren](/azure/azure-resource-manager/templates/template-tutorial-create-first-template)

Zie voor andere manieren om Azure Database Migration Service te implementeren: 
- [Azure-portal](quickstart-create-data-migration-service-portal.md)

Zie voor meer informatie [een overzicht van Azure Database Migration Service](dms-overview.md)