---
title: Het blauwdrukvoorbeeld voor de CAF-migratielandingszone implementeren
description: Implementeer stappen voor het blauwdrukvoorbeeld voor de CAF-migratielandingszone, waaronder details van de parameters voor blauwdrukartefacten.
ms.date: 05/06/2020
ms.topic: sample
ms.openlocfilehash: 109c9a2c4c5670d6f5a676498ae1010a4ab0e418
ms.sourcegitcommit: 62717591c3ab871365a783b7221851758f4ec9a4
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/22/2020
ms.locfileid: "82871177"
---
# <a name="deploy-the-microsoft-cloud-adoption-framework-for-azure-migrate-landing-zone-blueprint-sample"></a>Het Microsoft Cloud Adoption Framework voor het blauwdrukvoorbeeld voor de Azure-migratielandingszone implementeren

Als u het blauwdrukvoorbeeld voor de CAF-migratielandingszone van Azure Blueprints wilt implementeren, moet u de volgende stappen uitvoeren:

> [!div class="checklist1"]
> - Het wordt aanbevolen het [CAF Foundation](../caf-foundation/index.md)-blauwdrukvoorbeeld te implementeren

> [!div class="checklist2"]
> - Een nieuwe blauwdruk maken op basis van het voorbeeld
> - Uw kopie van het voorbeeld markeren als **Gepubliceerd**
> - Uw kopie van de blauwdruk toewijzen aan een bestaand abonnement

Als u nog geen abonnement op Azure hebt, maak dan een [gratis account](https://azure.microsoft.com/free) aan voordat u begint.

## <a name="create-blueprint-from-sample"></a>Een blauwdruk maken op basis van een voorbeeld

Implementeer eerst het blauwdrukvoorbeeld door een nieuwe blauwdruk in uw omgeving te maken op basis van het voorbeeld.

1. Selecteer **Alle services** in het linkerdeelvenster. Zoek en selecteer **Blauwdrukken**.

1. Op de pagina **Aan de slag** aan de linkerkant selecteert u de knop **Maken** onder _Een blauwdruk maken_.

1. Zoek onder _Andere voorbeelden_ het blauwdrukvoorbeeld **CAF-migratielandingszone** en selecteer **Dit voorbeeld gebruiken**.

1. Voer de _Basisinstellingen_ van het blauwdrukvoorbeeld in:
   - **Naam blauwdruk** Geef een naam op voor uw exemplaar van het blauwdrukvoorbeeld voor de CAF-migratielandingszone.
   - **Definitielocatie** Gebruik het beletselteken en selecteer de beheergroep waarin u uw exemplaar van het voorbeeld wilt opslaan.

1. Selecteer het tabblad _Artefacten_ boven aan de pagina of kies **Volgende: Artefacten** onder aan de pagina.

1. Controleer de lijst met artefacten die samen het blauwdrukvoorbeeld vormen. Veel van de artefacten bevatten parameters die we later zullen definiëren. Selecteer **Concept opslaan** wanneer u klaar bent met het controleren van het blauwdrukvoorbeeld.

## <a name="publish-the-sample-copy"></a>De voorbeeldkopie publiceren

Uw kopie van het blauwdrukvoorbeeld is nu gemaakt in uw omgeving. De kopie is gemaakt in de **Concept**-modus en moet worden **Gepubliceerd** voordat deze kan worden toegewezen en geïmplementeerd. De kopie van het blauwdrukvoorbeeld kan worden aangepast aan uw omgeving en behoeften, maar door die aanpassing is het mogelijk dat de kopie niet meer is afgestemd op de richtlijnen van de CAF-migratielandingszone.

1. Selecteer **Alle services** in het linkerdeelvenster. Zoek en selecteer **Blauwdrukken**.

1. Selecteer de pagina **Blauwdrukdefinities** aan de linkerkant. Gebruik de filters om uw kopie van het blauwdrukvoorbeeld te zoeken en selecteer vervolgens uw kopie.

1. Selecteer **Blauwdruk publiceren** boven aan de pagina. Op de nieuwe pagina aan de rechterkant geeft u een **Versie** voor uw kopie van het blauwdrukvoorbeeld op. Deze eigenschap is handig als u later een aanpassing wilt maken. Geef **Notities over wijzigingen** op, zoals Eerste gepubliceerde versie op basis van het blauwdrukvoorbeeld voor de CAF-migratielandingszone. Selecteer vervolgens **Publiceren** onder aan de pagina.

## <a name="assign-the-sample-copy"></a>De voorbeeldkopie toewijzen

Zodra de kopie van het blauwdrukvoorbeeld is **Gepubliceerd**, kan het worden toegewezen aan een abonnement binnen de beheergroep waarin de kopie is opgeslagen. Dit is de stap waarin parameters worden opgegeven om elke implementatie van de kopie van het blauwdrukvoorbeeld uniek te maken.

1. Selecteer **Alle services** in het linkerdeelvenster. Zoek en selecteer **Blauwdrukken**.

1. Selecteer de pagina **Blauwdrukdefinities** aan de linkerkant. Gebruik de filters om uw kopie van het blauwdrukvoorbeeld te zoeken en selecteer vervolgens uw kopie.

1. Selecteer **Blauwdruk toewijzen** boven aan de pagina Blauwdrukdefinitie.

1. Geef de parameterwaarden op voor de blauwdruktoewijzing:

   - Basisbeginselen
     - **Abonnementen**: Selecteer een of meer van de abonnementen in de beheergroep waarin u uw kopie van het blauwdrukvoorbeeld hebt opgeslagen. Als u meer dan één abonnement selecteert, wordt een toewijzing gemaakt voor elk abonnement waarvoor de ingevoerde parameters worden gebruikt.
     - **Naam van toewijzing**: De naam wordt vooraf voor u ingevuld op basis van de naam van de blauwdruk.
       Wijzig de naam als dat nodig is of gebruik de opgegeven naam.
     - **Locatie**: Selecteer een regio waarin u de beheerde identiteit wilt maken.
     - Azure Blueprint gebruikt deze beheerde identiteit om alle artefacten in de toegewezen blauwdruk te implementeren.
       Zie [Beheerde identiteiten voor Azure-resources](../../../../active-directory/managed-identities-azure-resources/overview.md) voor meer informatie.
     - **Blauwdrukdefinitieversie**: Kies een **gepubliceerde** versie van uw kopie van het blauwdrukvoorbeeld.
    
   - Toewijzing vergrendelen

     Selecteer de instelling voor het vergrendelen van de blauwdruk voor uw omgeving. Zie voor meer informatie [Vergrendeling van blauwdrukresources](../../concepts/resource-locking.md).

   - Beheerde identiteit

     Kies de standaardoptie voor de _door het systeem toegewezen_ beheerde identiteit of de optie voor de _door de gebruiker toegewezen identiteit_.

   - Blauwdrukparameters

     De parameters die in deze sectie worden gedefinieerd, worden door veel van de artefacten in de definitie van de blauwdruk gebruikt om consistentie te bieden.

       - **Organisatie**: Voer de naam van uw organisatie in, zoals Contoso of Fabrikam. De naam moet uniek zijn.
       - **AzureRegion**: Selecteer één Azure-regio voor implementatie.
       
   - Artefactparameters

     De parameters die in deze sectie worden gedefinieerd, zijn van toepassing op het artefact waaronder de parameter is gedefinieerd. Deze parameters zijn [dynamische parameters](../../concepts/parameters.md#dynamic-parameters), aangezien ze zijn gedefinieerd tijdens de toewijzing van de blauwdruk. Zie de [tabel met artefactparameters](#artifact-parameters-table) voor een volledige lijst met artefactparameters en hun beschrijvingen.

1. Zodra alle parameters zijn ingevoerd, selecteert u **Toewijzen** onder aan de pagina. De blauwdruktoewijzing wordt gemaakt en de implementatie van het artefact begint. De implementatie neemt circa vijf minuten in beslag. Open de blauwdruktoewijzing om de status van de implementatie te controleren.

> [!WARNING]
> De Azure Blueprints-service en de ingebouwde blauwdrukvoorbeelden zijn **gratis**. Azure-resources zijn [geprijsd per product](https://azure.microsoft.com/pricing/). Gebruik de [prijscalculator](https://azure.microsoft.com/pricing/calculator/) om de kosten te schatten voor het uitvoeren van resources die door dit blauwdrukvoorbeeld zijn geïmplementeerd.

## <a name="artifact-parameters-table"></a>Tabel met artefactparameters

In de volgende tabel ziet u een lijst met de blauwdrukartefactparameters:

|Naam van het artefact|Type artefact|Parameternaam|Beschrijving|
|-|-|-|-|
|vNET-landingszone implementeren|Resource Manager-sjabloon|IPAddress_Space|**Vergrendelde**: geef de eerste twee octetten op, bijvoorbeeld 10.0|
|Key Vault implementeren|Resource Manager-sjabloon|KV-AccessPolicy|**Vergrendelde**: groeps-id of gebruikersobject-id om machtigingen te verlenen in Key Vault|
|Log Analytics implementeren|Resource Manager-sjabloon|LogAnalytics_DataRetention|**Vergrendelde**: aantal dagen dat gegevens worden bewaard in Log Analytics|
|Log Analytics implementeren|Resource Manager-sjabloon|LogAnalytics_Location|**Vergrendelde**: regio die wordt gebruikt bij het tot stand brengen van de werkruimte|
|Azure Migrate implementeren|Resource Manager-sjabloon|Azure_Migrate_Location|**Vergrendeld**: selecteer de regio om Azure Migrate te implementeren|

## <a name="next-steps"></a>Volgende stappen

Nu u de stappen voor het implementeren van het blauwdrukvoorbeeld voor de CAF-migratielandingszone hebt doorgenomen, raadpleegt u de volgende artikelen voor informatie over de architectuur:

> [!div class="nextstepaction"]
> [Blauwdruk voor CAF-migratielandingszone - overzicht](./index.md)

Aanvullende artikelen over blauwdrukken en het gebruik hiervan:

- Meer informatie over de [levenscyclus van een blauwdruk](../../concepts/lifecycle.md).
- Meer informatie over hoe u [statische en dynamische parameters](../../concepts/parameters.md) gebruikt.
- Meer informatie over hoe u de [blauwdrukvolgorde](../../concepts/sequencing-order.md) aanpast.
- Meer informatie over hoe u gebruikmaakt van [resourcevergrendeling in blauwdrukken](../../concepts/resource-locking.md).
- Meer informatie over hoe u [bestaande toewijzingen bijwerkt](../../how-to/update-existing-assignments.md).
