---
title: Benoemde waarden gebruiken in azure API Management-beleid
description: Meer informatie over het gebruik van benoemde waarden in azure API Management-beleid. Benoemde waarden kunnen letterlijke teken reeksen en beleids expressies bevatten.
services: api-management
documentationcenter: ''
author: vladvino
manager: erikre
editor: ''
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.topic: article
ms.date: 01/08/2020
ms.author: apimpm
ms.openlocfilehash: 3f317276ae92e6121d519553b7883677dab89705
ms.sourcegitcommit: 7fe8df79526a0067be4651ce6fa96fa9d4f21355
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/06/2020
ms.locfileid: "87852188"
---
# <a name="how-to-use-named-values-in-azure-api-management-policies"></a>Benoemde waarden gebruiken in azure API Management-beleid

API Management-beleid is een krachtige mogelijkheid van het systeem waarmee de Azure Portal het gedrag van de API via configuratie kan wijzigen. Beleidsregels zijn een verzameling instructies die sequentieel worden uitgevoerd op de aanvraag of het antwoord van een API. Beleids instructies kunnen worden samengesteld met behulp van letterlijke tekst waarden, beleids expressies en benoemde waarden.

Elk API Management service-exemplaar heeft een verzameling sleutel-waardeparen, die een benoemde waarde wordt genoemd en die globaal zijn voor het service-exemplaar. Er is geen limiet ingesteld voor het aantal items in de verzameling. Benoemde waarden kunnen worden gebruikt voor het beheren van constante teken reeks waarden voor alle API-configuraties en-beleid. Elke benoemde waarde kan de volgende kenmerken hebben:

| Kenmerk      | Type            | Description                                                                                                                            |
| -------------- | --------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| `Display name` | tekenreeks          | Gebruikt voor het verwijzen naar de benoemde waarde in beleids regels. Een teken reeks van 1 tot 256 tekens. Alleen letters, cijfers, punten en streepjes zijn toegestaan. |
| `Value`        | string          | Werkelijke waarde. Mag niet leeg zijn of alleen uit spaties bestaan. Maxi maal 4096 tekens lang.                                        |
| `Secret`       | boolean         | Hiermee wordt bepaald of de waarde een geheim is en moet worden versleuteld of niet.                                                               |
| `Tags`         | tekenreeksmatrix | Hiermee wordt de lijst met benoemde waarden gefilterd. Maxi maal 32 tags.                                                                                    |

![Benoemde waarden](./media/api-management-howto-properties/named-values.png)

Benoemde waarden kunnen letterlijke teken reeksen en [beleids expressies](./api-management-policy-expressions.md)bevatten. De waarde van `Expression` is bijvoorbeeld een beleids expressie die een teken reeks retourneert met de huidige datum en tijd. De benoemde waarde `Credential` is gemarkeerd als geheim, waardoor de waarde ervan niet standaard wordt weer gegeven.

| Naam       | Waarde                      | Geheim | Tags          |
| ---------- | -------------------------- | ------ | ------------- |
| Waarde      | 42                         | Niet waar  | cruciale cijfers |
| Referentie | ••••••••••••••••••••••     | True   | security      |
| Expression | @ (DateTime. Now. ToString ()) | Niet waar  |               |

> [!NOTE]
> In plaats van benoemde waarden die zijn opgeslagen in een API Management-service, kunt u waarden gebruiken die zijn opgeslagen in de [Azure Key Vault](https://azure.microsoft.com/services/key-vault/) -service, zoals wordt geïllustreerd door dit [voor beeld](https://github.com/Azure/api-management-policy-snippets/blob/master/examples/Look%20up%20Key%20Vault%20secret%20using%20Managed%20Service%20Identity.policy.xml).

## <a name="to-add-and-edit-a-named-value"></a>Een benoemde waarde toevoegen en bewerken

![Een benoemde waarde toevoegen](./media/api-management-howto-properties/add-property.png)

1. Selecteer **API's** bij **API MANAGEMENT**.
2. Selecteer **benoemde waarden**.
3. Druk op **+ toevoegen**.

    Naam en waarde zijn vereiste waarden. Als de waarde een geheim is, schakelt u het selectie vakje _Dit is een geheim_ in. Voer een of meer optionele Tags in om u te helpen bij het ordenen van uw benoemde waarden en klik op opslaan.

4. Klik op **Maken**.

Zodra de benoemde waarde is gemaakt, kunt u deze bewerken door erop te klikken. Als u de naam van de benoemde waarde wijzigt, worden alle beleids regels die verwijzen naar deze benoemde waarde, automatisch bijgewerkt voor gebruik van de nieuwe naam.

## <a name="to-delete-a-named-value"></a>Een benoemde waarde verwijderen

Als u een benoemde waarde wilt verwijderen, klikt u op **verwijderen** naast de naam waarde die u wilt verwijderen.

> [!IMPORTANT]
> Als er wordt verwezen naar de genoemde waarde, kunt u deze pas verwijderen als u de genoemde waarde verwijdert uit alle beleids regels die deze gebruiken.

## <a name="to-search-and-filter-named-values"></a>Benoemde waarden zoeken en filteren

Het tabblad **benoemde waarden** bevat Zoek-en filter functies waarmee u uw benoemde waarden kunt beheren. Als u de lijst met benoemde waarden op naam wilt filteren, voert u een zoek term in het tekstvak **Zoek eigenschap** in. Als u alle benoemde waarden wilt weer geven, schakelt u het tekstvak **Zoek eigenschap** uit en drukt u op ENTER.

Als u de lijst op label wilt filteren, voert u een of meer tags in het tekstvak **filteren op labels** in. Als u alle benoemde waarden wilt weer geven, schakelt u het tekstvak **filteren op labels** uit en drukt u op ENTER.

## <a name="to-use-a-named-value"></a>Een benoemde waarde gebruiken

Als u een benoemde waarde in een beleid wilt gebruiken, plaatst u de naam ervan in een dubbel paar accolades `{{ContosoHeader}}` , zoals in het volgende voor beeld wordt weer gegeven:

```xml
<set-header name="{{ContosoHeader}}" exists-action="override">
  <value>{{ContosoHeaderValue}}</value>
</set-header>
```

In dit voor beeld `ContosoHeader` wordt gebruikt als de naam van een koptekst in een `set-header` beleid en `ContosoHeaderValue` wordt gebruikt als de waarde van die koptekst. Wanneer dit beleid wordt geëvalueerd tijdens een aanvraag of reactie op de API Management Gateway, `{{ContosoHeader}}` en `{{ContosoHeaderValue}}` worden vervangen door hun respectievelijke waarden.

Benoemde waarden kunnen worden gebruikt als volledige kenmerk-of element waarden, zoals wordt weer gegeven in het vorige voor beeld, maar ze kunnen ook worden ingevoegd in of gecombineerd met een letterlijke tekst expressie, zoals wordt weer gegeven in het volgende voor beeld:`<set-header name = "CustomHeader{{ContosoHeader}}" ...>`

Benoemde waarden kunnen ook beleids expressies bevatten. In het volgende voor beeld `ExpressionProperty` wordt de gebruikt.

```xml
<set-header name="CustomHeader" exists-action="override">
    <value>{{ExpressionProperty}}</value>
</set-header>
```

Wanneer dit beleid wordt geëvalueerd, `{{ExpressionProperty}}` wordt vervangen door de waarde: `@(DateTime.Now.ToString())` . Omdat de waarde een beleids expressie is, wordt de expressie geëvalueerd en wordt het beleid voortgezet met de uitvoering ervan.

U kunt dit testen in de ontwikkelaars portal door een bewerking aan te roepen die een beleid bevat met benoemde waarden binnen het bereik. In het volgende voor beeld wordt een bewerking aangeroepen met de twee voor gaande voorbeeld `set-header` beleidsregels met benoemde waarden. Houd er rekening mee dat het antwoord twee aangepaste kopteksten bevat die zijn geconfigureerd met behulp van beleids regels met benoemde waarden.

![ontwikkelaarsportal][api-management-send-results]

Als u de [API Inspector-tracering](api-management-howto-api-inspector.md) voor een aanroep met de twee voor gaande voorbeeld beleidsregels met benoemde waarden bekijkt, ziet u de twee `set-header` beleids regels met de naam waarden ingevoegd en de evaluatie van de beleids expressie voor de naam waarde die de beleids expressie bevat.

![API Inspector-tracering][api-management-api-inspector-trace]

Hoewel benoemde waarden beleids expressies kunnen bevatten, kunnen ze geen andere benoemde waarden bevatten. Als tekst met een verwijzing naar een benoemde waarde wordt gebruikt voor een waarde, zoals `Text: {{MyProperty}}` , wordt die verwijzing niet opgelost en vervangen.

## <a name="next-steps"></a>Volgende stappen

-   Meer informatie over het werken met beleids regels
    -   [Beleid in API Management](api-management-howto-policies.md)
    -   [Naslaginformatie over beleidsregels](./api-management-policies.md)
    -   [Beleidsexpressies](./api-management-policy-expressions.md)

[api-management-send-results]: ./media/api-management-howto-properties/api-management-send-results.png
[api-management-properties-filter]: ./media/api-management-howto-properties/api-management-properties-filter.png
[api-management-api-inspector-trace]: ./media/api-management-howto-properties/api-management-api-inspector-trace.png
