---
title: Resources implementeren voor Tenant
description: Hierin wordt beschreven hoe u resources implementeert in het Tenant bereik in een Azure Resource Manager sjabloon.
ms.topic: conceptual
ms.date: 09/04/2020
ms.openlocfilehash: 9b653f3fd4ed66f23521ea3ec8f9972e3b6cc09c
ms.sourcegitcommit: 4feb198becb7a6ff9e6b42be9185e07539022f17
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/04/2020
ms.locfileid: "89468552"
---
# <a name="create-resources-at-the-tenant-level"></a>Resources maken op Tenant niveau

Als uw organisatie is verouderd, moet u mogelijk [beleid](../../governance/policy/overview.md) of Azure [RBAC (op rollen gebaseerd toegangs beheer)](../../role-based-access-control/overview.md) voor uw Azure AD-Tenant definiëren en toewijzen. Met sjablonen op Tenant niveau kunt u declaratief beleid Toep assen en rollen toewijzen op globaal niveau.

## <a name="supported-resources"></a>Ondersteunde resources

Niet alle resource typen kunnen op het Tenant niveau worden geïmplementeerd. In deze sectie wordt een overzicht gegeven van de resource typen die worden ondersteund.

Gebruik voor Azure-beleid:

* [policyAssignments](/azure/templates/microsoft.authorization/policyassignments)
* [policyDefinitions](/azure/templates/microsoft.authorization/policydefinitions)
* [policySetDefinitions](/azure/templates/microsoft.authorization/policysetdefinitions)

Gebruik voor op rollen gebaseerd toegangs beheer:

* [roleAssignments](/azure/templates/microsoft.authorization/roleassignments)

Voor geneste sjablonen die worden geïmplementeerd op beheer groepen,-abonnementen of-resource groepen, gebruikt u:

* [implementaties](/azure/templates/microsoft.resources/deployments)

Voor het maken van beheer groepen gebruikt u:

* [managementGroups](/azure/templates/microsoft.management/managementgroups)

Voor het beheren van kosten gebruikt u:

* [billingProfiles](/azure/templates/microsoft.billing/billingaccounts/billingprofiles)
* [Schriften](/azure/templates/microsoft.billing/billingaccounts/billingprofiles/instructions)
* [invoiceSections](/azure/templates/microsoft.billing/billingaccounts/billingprofiles/invoicesections)

### <a name="schema"></a>Schema

Het schema dat u voor Tenant implementaties gebruikt, wijkt af van het schema voor implementaties van resource groepen.

Voor sjablonen gebruikt u:

```json
https://schema.management.azure.com/schemas/2019-08-01/tenantDeploymentTemplate.json#
```

Het schema voor een parameter bestand is hetzelfde voor alle implementatie bereiken. Gebruik voor parameter bestanden:

```json
https://schema.management.azure.com/schemas/2019-04-01/deploymentParameters.json#
```

## <a name="required-access"></a>Vereiste toegang

De principal-implementatie van de sjabloon moet machtigingen hebben om resources te maken in het Tenant bereik. De principal moet gemachtigd zijn om de implementatie acties ( `Microsoft.Resources/deployments/*` ) uit te voeren en om de resources te maken die in de sjabloon zijn gedefinieerd. Als u bijvoorbeeld een beheer groep wilt maken, moet de principal de machtiging Inzender hebben op het Tenant bereik. Als u roltoewijzingen wilt maken, moet de principal eigenaar toestemming hebben.

De globale beheerder voor de Azure Active Directory is niet automatisch gemachtigd om rollen toe te wijzen. De globale beheerder moet de volgende stappen uitvoeren om sjabloon implementaties in te scha kelen in het Tenant bereik:

1. De toegang tot het account verhogen zodat de globale beheerder rollen kan toewijzen. Zie [toegang verhogen voor het beheer van alle Azure-abonnementen en-beheer groepen](../../role-based-access-control/elevate-access-global-admin.md)voor meer informatie.

1. Wijs eigenaar of bijdrager toe aan de principal die de sjablonen moet implementeren.

   ```azurepowershell-interactive
   New-AzRoleAssignment -SignInName "[userId]" -Scope "/" -RoleDefinitionName "Owner"
   ```

   ```azurecli-interactive
   az role assignment create --assignee "[userId]" --scope "/" --role "Owner"
   ```

De principal heeft nu de vereiste machtigingen voor het implementeren van de sjabloon.

## <a name="deployment-commands"></a>Implementatie opdrachten

De opdrachten voor Tenant implementaties wijken af van de opdrachten voor het implementeren van resource groepen.

Gebruik [AZ Deployment Tenant Create](/cli/azure/deployment/tenant?view=azure-cli-latest#az-deployment-tenant-create)voor Azure cli:

```azurecli-interactive
az deployment tenant create \
  --name demoTenantDeployment \
  --location WestUS \
  --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/tenant-deployments/new-mg/azuredeploy.json"
```

Voor Azure PowerShell gebruikt u [New-AzTenantDeployment](/powershell/module/az.resources/new-aztenantdeployment).

```azurepowershell-interactive
New-AzTenantDeployment `
  -Name demoTenantDeployment `
  -Location "West US" `
  -TemplateUri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/tenant-deployments/new-mg/azuredeploy.json"
```

Gebruik voor REST API [implementaties-maken of bijwerken in het Tenant bereik](/rest/api/resources/deployments/createorupdateattenantscope).

## <a name="deployment-location-and-name"></a>Locatie en naam van de implementatie

Voor implementaties op Tenant niveau moet u een locatie opgeven voor de implementatie. De locatie van de implementatie is gescheiden van de locatie van de resources die u implementeert. De implementatie locatie geeft aan waar de implementatie gegevens moeten worden opgeslagen.

U kunt een naam opgeven voor de implementatie of de naam van de standaard implementatie gebruiken. De standaard naam is de naam van het sjabloon bestand. Als u bijvoorbeeld een sjabloon met de naam **azuredeploy.jsop** implementeert, maakt de standaard implementatie naam **azuredeploy**.

Voor elke implementatie naam is de locatie onveranderbaar. U kunt geen implementatie op één locatie maken wanneer er een bestaande implementatie met dezelfde naam op een andere locatie is. Als u de fout code krijgt `InvalidDeploymentLocation` , moet u een andere naam of dezelfde locatie gebruiken als de vorige implementatie voor die naam.

## <a name="deployment-scopes"></a>Implementatie bereiken

Wanneer u implementeert naar een Tenant, kunt u de Tenant-of beheer groepen, abonnementen en resource groepen in de Tenant richten. De gebruiker die de sjabloon implementeert, moet toegang hebben tot het opgegeven bereik.

Resources die zijn gedefinieerd in de sectie resources van de sjabloon worden toegepast op de Tenant.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2019-08-01/tenantDeploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
        tenant-level-resources
    ],
    "outputs": {}
}
```

Als u een beheer groep in de Tenant wilt richten, voegt u een geneste implementatie toe en geeft u de `scope` eigenschap op.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2019-08-01/tenantDeploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "mgName": {
            "type": "string"
        }
    },
    "variables": {
        "mgId": "[concat('Microsoft.Management/managementGroups/', parameters('mgName'))]"
    },
    "resources": [
        {
            "type": "Microsoft.Resources/deployments",
            "apiVersion": "2020-06-01",
            "name": "nestedMG",
            "scope": "[variables('mgId')]",
            "location": "eastus",
            "properties": {
                "mode": "Incremental",
                "template": {
                    nested-template-with-resources-in-mg
                }
            }
        }
    ],
    "outputs": {}
}
```

## <a name="use-template-functions"></a>Sjabloon functies gebruiken

Voor Tenant implementaties gelden enkele belang rijke aandachtspunten bij het gebruik van sjabloon functies:

* De functie [resourceGroup ()](template-functions-resource.md#resourcegroup) wordt **niet** ondersteund.
* De functie [Subscription ()](template-functions-resource.md#subscription) wordt **niet** ondersteund.
* De functies [Reference ()](template-functions-resource.md#reference) en [List ()](template-functions-resource.md#list) worden ondersteund.
* Gebruik [resourceId ()](template-functions-resource.md#resourceid) niet om de resource-id op te halen voor resources die worden geïmplementeerd op Tenant niveau.

  Gebruik in plaats daarvan de functie [tenantResourceId ()](template-functions-resource.md#tenantresourceid) .

  Als u bijvoorbeeld de bron-ID voor een ingebouwde beleids definitie wilt ophalen, gebruikt u:

  ```json
  tenantResourceId('Microsoft.Authorization/policyDefinitions/', parameters('policyDefinition'))
  ```

  De geretourneerde Resource-ID heeft de volgende indeling:

  ```json
  /providers/{resourceProviderNamespace}/{resourceType}/{resourceName}
  ```

## <a name="create-management-group"></a>Beheergroep maken

Met de [volgende sjabloon](https://github.com/Azure/azure-quickstart-templates/tree/master/tenant-deployments/new-mg) maakt u een beheer groep.

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2019-08-01/tenantDeploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "mgName": {
      "type": "string",
      "defaultValue": "[concat('mg-', uniqueString(newGuid()))]"
    }
  },
  "resources": [
    {
      "type": "Microsoft.Management/managementGroups",
      "apiVersion": "2019-11-01",
      "name": "[parameters('mgName')]",
      "properties": {
      }
    }
  ]
}
```

## <a name="assign-role"></a>Rol toewijzen

De [volgende sjabloon](https://github.com/Azure/azure-quickstart-templates/tree/master/tenant-deployments/tenant-role-assignment) wijst een rol toe aan het Tenant bereik.

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2019-08-01/tenantDeploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "principalId": {
      "type": "string",
      "metadata": {
        "description": "principalId if the user that will be given contributor access to the resourceGroup"
      }
    },
    "roleDefinitionId": {
      "type": "string",
      "defaultValue": "8e3af657-a8ff-443c-a75c-2fe8c4bcb635",
      "metadata": {
        "description": "roleDefinition for the assignment - default is owner"
      }
    }
  },
  "variables": {
    // This creates an idempotent guid for the role assignment
    "roleAssignmentName": "[guid('/', parameters('principalId'), parameters('roleDefinitionId'))]"
  },
  "resources": [
    {
      "name": "[variables('roleAssignmentName')]",
      "type": "Microsoft.Authorization/roleAssignments",
      "apiVersion": "2019-04-01-preview",
      "properties": {
        "roleDefinitionId": "[tenantResourceId('Microsoft.Authorization/roleDefinitions', parameters('roleDefinitionId'))]",
        "principalId": "[parameters('principalId')]",
        "scope": "/"
      }
    }
  ]
}
```

## <a name="next-steps"></a>Volgende stappen

* Zie [Azure-roltoewijzingen toevoegen met Azure Resource Manager sjablonen](../../role-based-access-control/role-assignments-template.md)voor meer informatie over het toewijzen van rollen.
* U kunt ook sjablonen implementeren op [abonnements niveau](deploy-to-subscription.md) of op het niveau van de [beheer groep](deploy-to-management-group.md).
