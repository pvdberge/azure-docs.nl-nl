---
title: JSON-inhouds type gebruiken voor sleutel waarden
titleSuffix: Azure App Configuration
description: Meer informatie over het gebruik van JSON-inhouds type voor sleutel waarden
services: azure-app-configuration
author: avanigupta
ms.assetid: ''
ms.service: azure-app-configuration
ms.devlang: azurecli
ms.topic: how-to
ms.date: 08/03/2020
ms.author: avgupta
ms.openlocfilehash: 725beb50e55852e35ee4434539ff158f082059df
ms.sourcegitcommit: b8702065338fc1ed81bfed082650b5b58234a702
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/11/2020
ms.locfileid: "88122008"
---
# <a name="leverage-content-type-to-store-json-key-values-in-app-configuration"></a>Maak gebruik van het inhouds type voor het opslaan van JSON-sleutel waarden in app-configuratie

Gegevens worden in de app-configuratie opgeslagen als sleutel waarden, waarbij waarden standaard worden behandeld als het teken reeks type. U kunt echter een aangepast type opgeven door gebruik te maken van de eigenschap content-type die is gekoppeld aan elke sleutel waarde, zodat u het oorspronkelijke type van uw gegevens kunt behouden of uw toepassing op een andere manier wilt laten werken op basis van het inhouds type.


## <a name="overview"></a>Overzicht

In app-configuratie kunt u het JSON-media type gebruiken als het inhouds type van uw sleutel waarden om te profiteren van voor delen zoals:
- **Eenvoudiger gegevens beheer**: het beheren van sleutel waarden, zoals matrices, is veel eenvoudiger in de Azure Portal.
- **Verbeterde gegevens export**: primitieve typen, matrices en JSON-objecten blijven behouden tijdens het exporteren van gegevens.
- **Systeem eigen ondersteuning met de app-configuratie provider**: sleutel waarden met JSON-inhouds type werken prima wanneer ze worden gebruikt door bibliotheken met app-configuratie providers in uw toepassingen.

#### <a name="valid-json-content-type"></a>Geldig JSON-inhouds type

Media typen, zoals [hier](https://www.iana.org/assignments/media-types/media-types.xhtml)gedefinieerd, kunnen worden toegewezen aan het type inhoud dat is gekoppeld aan elke sleutel waarde.
Een media type bestaat uit een type en een subtype. Als het type is `application` en het subtype (of achtervoegsel) is `json` , wordt het media type beschouwd als een geldig JSON-inhouds type.
Enkele voor beelden van geldige JSON-inhouds typen zijn:

- application/json
- toepassing/activiteit + JSON
- application/vnd. foobar + JSON; charset = UTF-8

#### <a name="valid-json-values"></a>Geldige JSON-waarden

Wanneer een sleutel waarde een JSON-inhouds type heeft, moet de waarde ervan een geldige JSON-indeling hebben zodat clients deze correct kunnen verwerken. Anders kunnen clients mislukken of terugvallen en deze als teken reeks indeling behandelen.
Enkele voor beelden van geldige JSON-waarden zijn:

- "John Doe"
- 723
- false
- null
- "2020-01-01T12:34:56.789 Z"
- [1, 2, 3, 4]
- {"ObjectSetting": {"doel gericht": {"default": True, "level": "Information"}}}

> [!NOTE]
> Voor de rest van dit artikel wordt een sleutel waarde in de app-configuratie met een geldig JSON-inhouds type en een geldige JSON-waarde aangeduid als **JSON-sleutel waarde**. 

In deze zelfstudie leert u het volgende:
> [!div class="checklist"]
> * JSON-sleutel waarden maken in app-configuratie.
> * JSON-sleutel waarden uit een JSON-bestand importeren.
> * JSON-sleutel waarden exporteren naar een JSON-bestand.
> * JSON-sleutel waarden gebruiken in uw toepassingen.


## <a name="prerequisites"></a>Vereisten

- Azure-abonnement: [Maak een gratis versie](https://azure.microsoft.com/free/).
- Nieuwste versie van Azure CLI (2.10.0 of hoger). Voer `az --version` uit om de versie te bekijken. Zie [Azure CLI installeren](/cli/azure/install-azure-cli) als u de CLI wilt installeren of een upgrade wilt uitvoeren. Als u Azure CLI gebruikt, moet u zich eerst aanmelden met `az login` . U kunt eventueel de Azure Cloud Shell gebruiken.

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]


## <a name="create-an-app-configuration-store"></a>Een App Configuration-archief maken

[!INCLUDE [azure-app-configuration-create](../../includes/azure-app-configuration-create.md)]


## <a name="create-json-key-values-in-app-configuration"></a>JSON-sleutel waarden maken in app-configuratie

JSON-sleutel waarden kunnen worden gemaakt met behulp van Azure Portal, Azure CLI of door importeren vanuit een JSON-bestand. In deze sectie vindt u instructies voor het maken van dezelfde JSON-sleutel waarden met behulp van alle drie de methoden.

### <a name="create-json-key-values-using-azure-portal"></a>JSON-sleutel waarden maken met behulp van Azure Portal

Blader naar uw app-configuratie archief en selecteer **Configuration Explorer**  >  **Create**  >  **sleutel-waarde** maken om de volgende sleutel-waardeparen toe te voegen:

| Sleutel | Waarde | Type inhoud |
|---|---|---|
| Instellingen: BackgroundColor | Dag | application/json |
| Instellingen: FontSize | 24 | application/json |
| Instellingen: UseDefaultRouting | false | application/json |
| Instellingen: BlockedUsers | null | application/json |
| Instellingen: ReleaseDate | "2020-08-04T12:34:56.789 Z" | application/json |
| Instellingen: RolloutPercentage | [25, 50, 75100] | application/json |
| Instellingen: logboek registratie | {"Test": {"niveau": "debug"}, "Prod": {"level": "Warning"}} | application/json |

Laat het **Label** leeg en selecteer **Toep assen**.

### <a name="create-json-key-values-using-azure-cli"></a>JSON-sleutel waarden maken met behulp van Azure CLI

Met de volgende opdrachten worden JSON-sleutel waarden in uw app-configuratie archief gemaakt. Vervang door `<appconfig_name>` de naam van uw app-configuratie archief.

```azurecli-interactive
appConfigName=<appconfig_name>
az appconfig kv set -n $appConfigName --content-type application/json --key Settings:BackgroundColor --value \"Green\"
az appconfig kv set -n $appConfigName --content-type application/json --key Settings:FontSize --value 24
az appconfig kv set -n $appConfigName --content-type application/json --key Settings:UseDefaultRouting --value false
az appconfig kv set -n $appConfigName --content-type application/json --key Settings:BlockedUsers --value null
az appconfig kv set -n $appConfigName --content-type application/json --key Settings:ReleaseDate --value \"2020-08-04T12:34:56.789Z\"
az appconfig kv set -n $appConfigName --content-type application/json --key Settings:RolloutPercentage --value [25,50,75,100]
az appconfig kv set -n $appConfigName --content-type application/json --key Settings:Logging --value {\"Test\":{\"Level\":\"Debug\"},\"Prod\":{\"Level\":\"Warning\"}}
```

> [!IMPORTANT]
> Als u gebruikmaakt van Azure CLI of Azure Cloud Shell om JSON-sleutel waarden te maken, moet de gegeven waarde een JSON-teken reeks zonder Escape zijn.

### <a name="import-json-key-values-from-a-file"></a>JSON-sleutel waarden uit een bestand importeren

Maak een JSON-bestand `Import.json` met de naam met de volgende inhoud en importeer als sleutel waarden in de app-configuratie:

```json
{
  "Settings": {
    "BackgroundColor": "Green",
    "BlockedUsers": null,
    "FontSize": 24,
    "Logging": {"Test":{"Level":"Debug"},"Prod":{"Level":"Warning"}},
    "ReleaseDate": "2020-08-04T12:34:56.789Z",
    "RolloutPercentage": [25,50,75,100],
    "UseDefaultRouting": false
  }
}
```

```azurecli-interactive
az appconfig kv import -s file --format json --path "~/Import.json" --content-type "application/json" --separator : --depth 2
```

> [!Note]
> Het `--depth` argument wordt gebruikt voor het afvlakken van hiërarchische gegevens uit een bestand in sleutel-waardeparen. In deze zelf studie is depth opgegeven om aan te tonen dat u ook JSON-objecten als waarden in de app-configuratie kunt opslaan. Als depth niet is opgegeven, worden JSON-objecten standaard afgevlakt op het hoogste niveau.

De JSON-sleutel waarden die u hebt gemaakt, moeten er als volgt uitzien in app-configuratie:

![Configuratie archief met JSON-sleutel waarden](./media/create-json-settings.png)


## <a name="export-json-key-values-to-a-file"></a>JSON-sleutel waarden exporteren naar een bestand

Een van de grote voor delen van het gebruik van JSON-sleutel waarden is de mogelijkheid om het oorspronkelijke gegevens type van uw waarden te behouden tijdens het exporteren. Als een sleutel waarde in de app-configuratie geen JSON-inhouds type heeft, wordt de waarde ervan beschouwd als teken reeks. 

Houd rekening met deze sleutel waarden zonder JSON-inhouds type:

| Sleutel | Waarde | Type inhoud |
|---|---|---|
| Instellingen: FontSize | 24 | |
| Instellingen: UseDefaultRouting | false | |

Wanneer u deze sleutel waarden naar een JSON-bestand exporteert, worden de waarden geëxporteerd als teken reeksen:
```json
{
  "Settings": {
    "FontSize": "24",
    "UseDefaultRouting": "false"
  }
}
```

Wanneer u JSON-sleutel waarden naar een bestand exporteert, behouden alle waarden echter het oorspronkelijke gegevens type. U kunt dit controleren door sleutel waarden van de app-configuratie te exporteren naar een JSON-bestand. U ziet dat het geëxporteerde bestand dezelfde inhoud heeft als het `Import.json` bestand dat u eerder hebt geïmporteerd.

```azurecli-interactive
az appconfig kv export -d file --format json --path "~/Export.json" --separator :
```

> [!NOTE]
> Als uw app-configuratie archief bepaalde sleutel waarden bevat zonder JSON-inhouds type, worden ze ook geëxporteerd naar hetzelfde bestand in de teken reeks indeling. Als u alleen de JSON-sleutel waarden wilt exporteren, wijst u een uniek label of voor voegsel toe aan uw JSON-sleutel waarden en gebruikt u label-of voorvoegsel filtering tijdens het exporteren.


## <a name="consuming-json-key-values-in-applications"></a>JSON-sleutel waarden gebruiken in toepassingen

De eenvoudigste manier om JSON-sleutel waarden in uw toepassing te gebruiken, is door de bibliotheek van de app-configuratie provider. Met de provider bibliotheken hoeft u geen speciale verwerking van JSON-sleutel waarden in uw toepassing te implementeren. Ze worden altijd op dezelfde manier gedeserialiseerd voor uw toepassing als andere bibliotheken met de JSON-configuratie provider. 

> [!Important]
> Systeem eigen ondersteuning voor JSON-sleutel waarden is beschikbaar in .NET Configuration provider versie 4.0.0 (of hoger). Zie de sectie [*volgende stappen*](#next-steps) voor meer informatie.

Als u de SDK of REST API gebruikt voor het lezen van sleutel waarden van de app-configuratie, op basis van het type inhoud, is uw toepassing verantwoordelijk voor het deserialiseren van de waarde van een JSON-sleutel waarde met behulp van een standaard-JSON-deserializer.


## <a name="clean-up-resources"></a>Resources opschonen

[!INCLUDE [azure-app-configuration-cleanup](../../includes/azure-app-configuration-cleanup.md)]

## <a name="next-steps"></a>Volgende stappen

Nu u weet hoe u met JSON-sleutel waarden in uw app-configuratie archief kunt werken, maakt u een toepassing voor het gebruik van deze sleutel waarden:

* [Snelstartgids ASP.NET Core](./quickstart-aspnet-core-app.md)
    * Vereiste: [micro soft. Azure. AppConfiguration. AspNetCore](https://www.nuget.org/packages/Microsoft.Azure.AppConfiguration.AspNetCore) package v 4.0.0 of hoger.

* [Snelstartgids voor .NET core](./quickstart-dotnet-core-app.md)
    * Vereiste: [Microsoft.Extensions.Configuratie. AzureAppConfiguration](https://www.nuget.org/packages/Microsoft.Extensions.Configuration.AzureAppConfiguration) package v 4.0.0 of hoger.
