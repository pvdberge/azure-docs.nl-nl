---
title: Sjabloon syntaxis en expressies
description: Beschrijft de declaratieve JSON-syntaxis voor Azure Resource Manager sjablonen.
ms.topic: conceptual
ms.date: 03/17/2020
ms.openlocfilehash: baddedae1b918502e579d2ed230e0779960f45e7
ms.sourcegitcommit: 877491bd46921c11dd478bd25fc718ceee2dcc08
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/02/2020
ms.locfileid: "82203825"
---
# <a name="syntax-and-expressions-in-azure-resource-manager-templates"></a>Syntaxis en expressies in Azure Resource Manager sjablonen

De basis syntaxis van de sjabloon is JSON. U kunt echter expressies gebruiken om de JSON-waarden uit te breiden die beschikbaar zijn in de sjabloon.  Expressies staan respectievelijk tussen de vierkante haken `[` en `]`. De waarde van de expressie wordt geëvalueerd als de sjabloon wordt geïmplementeerd. Een expressie kan een tekenreeks, een geheel getal, een booleaanse waarde of een object retourneren.

Een sjabloon expressie mag niet langer zijn dan 24.576 tekens.

## <a name="use-functions"></a>Functies gebruiken

Azure Resource Manager biedt [functies](template-functions.md) die u in een sjabloon kunt gebruiken. In het volgende voor beeld ziet u een expressie die gebruikmaakt van een functie in de standaard waarde van een para meter:

```json
"parameters": {
  "location": {
    "type": "string",
    "defaultValue": "[resourceGroup().location]"
  }
},
```

Binnen de expressie roept de syntaxis `resourceGroup()` een van de functies aan die Resource Manager biedt voor gebruik in een sjabloon. In dit geval is het de functie [resourceGroup](template-functions-resource.md#resourcegroup) . Net als in Java script worden functie aanroepen opgemaakt als `functionName(arg1,arg2,arg3)` . De syntaxis `.location` haalt één eigenschap op uit het object dat door die functie wordt geretourneerd.

Sjabloon functies en de bijbehorende para meters zijn niet hoofdletter gevoelig. Met Resource Manager worden bijvoorbeeld **variabelen (' var1 ')** en **variabelen (' var1 ')** als hetzelfde omgezet. Als de functie wordt geëvalueerd, wordt de-functie in de gevallen bewaard, tenzij deze expliciet een hoofdletter gebruik wijzigt (zoals toUpper of toLower). Bepaalde resource typen kunnen Case vereisten hebben die gescheiden zijn van de manier waarop functies worden geëvalueerd.

Als u een teken reeks waarde wilt door geven als een para meter voor een functie, gebruikt u enkele aanhalings tekens.

```json
"name": "[concat('storage', uniqueString(resourceGroup().id))]"
```

De meeste functies werken hetzelfde, ongeacht of deze zijn geïmplementeerd in een resource groep, een abonnement, een beheer groep of een Tenant. Voor de volgende functies gelden beperkingen op basis van het bereik:

* [resourceGroup](template-functions-resource.md#resourcegroup) -kan alleen worden gebruikt in implementaties van een resource groep.
* [resourceId](template-functions-resource.md#resourceid) -kan in elk bereik worden gebruikt, maar de geldige para meters veranderen afhankelijk van het bereik.
* [abonnement](template-functions-resource.md#subscription) : kan alleen worden gebruikt in implementaties van een resource groep of abonnement.

## <a name="escape-characters"></a>Escape tekens

Als u een letterlijke teken reeks begint met een haakje `[` en eindigend met een haakje sluiten `]` , maar niet als een expressie, voegt u een extra beugel toe om de teken reeks te starten met `[[` . Bijvoorbeeld de variabele:

```json
"demoVar1": "[[test value]"
```

Wordt omgezet in `[test value]` .

Als de letterlijke teken reeks niet eindigt met een haakje, hoeft u de eerste vier Kante haak niet te sluiten. Bijvoorbeeld de variabele:

```json
"demoVar2": "[test] value"
```

Wordt omgezet in `[test] value` .

Gebruik de back slash om dubbele aanhalings tekens in een expressie te escapen, zoals het toevoegen van een JSON-object in de sjabloon.

```json
"tags": {
    "CostCenter": "{\"Dept\":\"Finance\",\"Environment\":\"Production\"}"
},
```

Wanneer para meter waarden worden door gegeven, is het gebruik van escape tekens afhankelijk van waar de parameter waarde is opgegeven. Als u een standaard waarde in de sjabloon instelt, hebt u de extra accolade nodig.

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "demoParam1":{
            "type": "string",
            "defaultValue": "[[test value]"
        }
    },
    "resources": [],
    "outputs": {
        "exampleOutput": {
            "type": "string",
            "value": "[parameters('demoParam1')]"
        }
    }
}
```

Als u de standaard waarde gebruikt, wordt de sjabloon geretourneerd `[test value]` .

Als u echter een parameter waarde doorgeeft via de opdracht regel, worden de tekens letterlijk geïnterpreteerd. De vorige sjabloon implementeren met:

```azurepowershell
New-AzResourceGroupDeployment -ResourceGroupName demoGroup -TemplateFile azuredeploy.json -demoParam1 "[[test value]"
```

Retourneert `[[test value]` . Gebruik in plaats daarvan:

```azurepowershell
New-AzResourceGroupDeployment -ResourceGroupName demoGroup -TemplateFile azuredeploy.json -demoParam1 "[test value]"
```

Dezelfde opmaak wordt toegepast bij het door geven van waarden in vanuit een parameter bestand. De tekens worden letterlijk geïnterpreteerd. Bij gebruik in combi natie met de voor gaande sjabloon retourneert het volgende parameter bestand `[test value]` :

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "demoParam1": {
            "value": "[test value]"
        }
   }
}
```

## <a name="null-values"></a>Null-waarden

Als u een eigenschap op null wilt instellen, kunt u **Null** of **[JSON (' null ')]** gebruiken. De [json-functie](template-functions-object.md#json) retourneert een leeg object wanneer u `null` de para meter opgeeft. In beide gevallen behandelen Resource Manager-sjablonen dit alsof de eigenschap niet aanwezig is.

```json
"stringValue": null,
"objectValue": "[json('null')]"
```

## <a name="next-steps"></a>Volgende stappen

* Zie [Azure Resource Manager-sjabloon functies](template-functions.md)voor een volledige lijst met sjabloon functies.
* Zie [inzicht krijgen in de structuur en de syntaxis van Azure Resource Manager-sjablonen](template-syntax.md)voor meer informatie over sjabloon bestanden.
