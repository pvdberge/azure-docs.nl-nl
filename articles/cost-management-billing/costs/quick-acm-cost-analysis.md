---
title: 'Quickstart: Azure-kosten verkennen met kostenanalyse'
description: Deze snelstart helpt u kostenanalyse te gebruiken om de kosten van Azure voor uw bedrijf te verkennen en te analyseren.
author: bandersmsft
ms.author: banders
ms.date: 08/20/2020
ms.topic: quickstart
ms.service: cost-management-billing
ms.subservice: cost-management
ms.reviewer: micflan
ms.custom: seodec18
ms.openlocfilehash: 8ca9eaeeb8d484c9aeae6646e6f4814afbaed577
ms.sourcegitcommit: 6fc156ceedd0fbbb2eec1e9f5e3c6d0915f65b8e
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/21/2020
ms.locfileid: "88718523"
---
# <a name="quickstart-explore-and-analyze-costs-with-cost-analysis"></a>Quickstart: Kosten verkennen en analyseren met kostenanalyse

Voordat u de kosten van Azure goed kunt beheren en optimaliseren, moet u de oorsprong van de kosten in uw bedrijf weten. Het is ook handig om te weten hoeveel uw services kosten en welke omgevingen en systemen erdoor worden ondersteund. Inzicht in de volle breedte van alle kosten is noodzakelijk om nauwkeurig de uitgavenpatronen van uw bedrijf te leren kennen. U kunt uitgavenpatronen gebruiken om kostenbeheersingsmechanismen als budgetten af te dwingen.

In deze snelstart gebruikt u kostenanalyse om de kosten van Azure voor uw bedrijf te verkennen en te analyseren. U kunt de totale kosten per bedrijf weergeven, zodat u begrijpt waar de kosten worden opgebouwd en uitgavenpatronen kunt identificeren. U kunt de totale kosten bekijken om geschatte kostentrends per maand, per kwartaal en zelfs per jaar naast een budget te leggen. Een budget helpt bij het in acht nemen van financiële beperkingen. En een budget wordt gebruikt om dagelijkse en maandelijkse kosten te bekijken om onregelmatigheden in de uitgaven te isoleren. Plus, u kunt de gegevens van het huidige rapport downloaden voor verdere analyse of om in een extern systeem te gebruiken.

In deze snelstart leert u de volgende zaken:

- Kosten in kostenanalyse beoordelen
- Kostenweergaven aanpassen
- Gegevens van kostenanalyse downloaden

## <a name="prerequisites"></a>Vereisten

Kostenanalyse biedt ondersteuning voor verschillende typen Azure-accounts. Zie voor de volledige lijst met ondersteunde accounttypen [Gegevens van Azure Cost Management begrijpen](understand-cost-mgt-data.md). Als u kostengegevens wilt weergeven, hebt u minimaal leestoegang voor uw Azure-account nodig.

Zie [Toegang tot gegevens toewijzen](../../cost-management/assign-access-acm-data.md) voor meer informatie over het toewijzen van toegang tot de gegevens in Azure Cost Management.

Als u een nieuw abonnement hebt, kunt u de Cost Management-functies niet meteen gebruiken. Het kan tot 48 uur duren voordat u alle Cost Management-functies kunt gebruiken.

## <a name="sign-in-to-azure"></a>Aanmelden bij Azure

- Meld u aan bij Azure Portal op https://portal.azure.com.

## <a name="review-costs-in-cost-analysis"></a>Kosten in kostenanalyse beoordelen

Als u de kosten in kostenanalyse wilt controleren, opent u het bereik in de Azure-portal en selecteert u **Kostenanalyse** in het menu. Ga bijvoorbeeld naar **Abonnementen**, selecteer een abonnement in de lijst en selecteer vervolgens **Kostenanalyse** in het menu. Gebruik **Bereik** om over te schakelen naar een ander bereik in kostenanalyse. Zie [Understand and work with scopes](understand-work-scopes.md) (Engelstalig) voor meer informatie over bereiken.

Het bereik dat u selecteert wordt door Cost Management gebruikt om gegevens te bundelen en toegang tot de kostengegevens te beheren. Wanneer u gebruikmaakt van bereiken, moet u geen meervoudige selectie maken. In plaats daarvan selecteert u een groter bereik dat de andere bereiken omvat en filtert u vervolgens zodat alleen de geneste bereiken die u nodig hebt, overblijven. Het is belangrijk dat u deze aanpak begrijpt omdat mogelijk niet iedereen toegang heeft tot één enkel bovenliggend bereik, waarin meerdere bereiken zijn genest.

Bekijk de video [Cost Management gebruiken in de Azure-portal](https://www.youtube.com/watch?v=mfxysF-kTFA) voor meer informatie over het gebruik van Kostenanalyse. Als u andere video’s wilt bekijken, gaat u naar het [YouTube-kanaal voor Cost Management](https://www.youtube.com/c/AzureCostManagement).

>[!VIDEO https://www.youtube.com/embed/mfxysF-kTFA]

De initiële kostenanalyseweergave omvat de volgende gebieden.

**De weergave Samengevoegde kosten**: hiermee wordt de configuratie van de vooraf gedefinieerde kostenanalyse weergegeven. Elke weergave bevat datumbereik, granulariteit, groeperen op en filterinstellingen. In de standaardweergave worden samengevoegde kosten weergegeven voor de huidige factureringsperiode, maar u kunt deze wijzigen in andere ingebouwde weergaven. Zie [Kostenweergaven aanpassen](#customize-cost-views) voor meer informatie.

**Werkelijke kosten**: hiermee worden de totale verbruiks- en aankoopkosten voor de huidige maand aangeduid. Deze worden samengevoegd en op uw factuur vermeld.

**Prognose**: toont de totale geraamde kosten voor de periode die u kiest.

**Budget**: toont de geplande uitgavenlimiet voor het geselecteerde bereik, indien beschikbaar.

**Geaccumuleerde granulariteit**: toont de totale samengevoegde kosten per dag, vanaf het begin van de factureringsperiode. Nadat u een [budget hebt gemaakt](tutorial-acm-create-budgets.md) voor uw factureringsrekening of abonnement, kunt u snel uw uitgaventrend ten opzichte van het budget bekijken. Beweeg de muisaanwijzer over een datum om de opgebouwde kosten voor die dag te zien.

**Draaigrafieken (ringdiagrammen)** : bieden dynamische draaigrafieken en specificeren de totale kosten, gedetailleerd per algemene standaardeigenschappen. Ze tonen de grootste tot de kleinste kostenposten voor de huidige maand. U kunt draaigrafieken op elk moment wijzigen door een andere pivot te selecteren. Kosten worden standaard weergegeven op: service (metercategorie), locatie (regio) en onderliggend bereik. Inschrijvingsaccounts bevinden zich bijvoorbeeld onder factureringsaccounts, resourcegroepen onder abonnementen en resources onder resourcegroepen.

![Oorspronkelijke weergave van Kostenanalyse in Azure Portal](./media/quick-acm-cost-analysis/cost-analysis-01.png)

### <a name="understand-forecast"></a>Prognose begrijpen

In de kostenprognose wordt een schatting van de kosten voor de geselecteerde periode weergegeven. Het model is gebaseerd op een regressiemodel met tijdreeksen. Er zijn ten minste tien dagen van recente kosten- en gebruiksgegevens nodig om kosten nauwkeurig te kunnen schatten. Voor een bepaalde periode vereist het prognosemodel gelijke delen van trainingsgegevens voor de prognoseperiode. Voor een prognose van drie maanden bijvoorbeeld zijn ten minste drie maanden aan recente kosten- en gebruiksgegevens vereist.

Het model gebruikt een maximum van zes maanden aan trainingsgegevens om kosten voor een heel jaar te schatten. Er zijn minimaal zeven dagen aan trainingsgegevens nodig om de voorspelling te wijzigen. De voorspelling is gebaseerd op opvallende wijzigingen, zoals pieken en dalen, in kosten- en gebruikspatronen. De prognose genereert geen afzonderlijke schattingen voor elk item in **Groeperen op**-eigenschappen. Er wordt alleen een schatting gegeven van het totaal aan samengevoegde kosten. Als u meerdere valuta's gebruikt, geeft het model prognoses voor de kosten alleen in Amerikaanse dollars.

## <a name="customize-cost-views"></a>Kostenweergaven aanpassen

Kostenanalyse heeft vier ingebouwde weergaven die zijn geoptimaliseerd voor de meest voorkomende doelstellingen:

Weergave | Geven antwoord op vragen als
--- | ---
Samengevoegde kosten | Hoeveel heb ik tot dusverre besteed deze maand? Blijf ik binnen mijn budget?
Dagelijkse kosten | Zijn de kosten per dag de afgelopen 30 dagen toegenomen?
Kosten per service | Hoe varieert mijn maandelijkse gebruik op de laatste drie facturen?
Kosten per resource | Welke resources hebben tot dusverre het meest gekost deze maand?

![Weergaveselector met een voorbeeldselectie voor deze maand](./media/quick-acm-cost-analysis/view-selector.png)

Er zijn echter veel gevallen waar u een meer gedetailleerde analyse nodig hebt. Het aanpassen begint bovenaan de pagina, met de selectie van de datum.

Kostenanalyse toont standaard de gegevens voor de huidige maand. Gebruik de datumselector om snel naar veelgebruikte datumbereiken over te schakelen. Voorbeelden hiervan zijn de laatste zeven dagen, de afgelopen maand, het huidige jaar of een aangepast datumbereik. Betalen per gebruik-abonnementen omvatten ook datumbereiken op basis van uw factureringsperiode, die niet is gekoppeld aan de kalendermaand, zoals de huidige factureringsperiode of de laatste factuur. Gebruik de koppelingen **< VORIGE** en **VOLGENDE >** boven aan het menu om naar respectievelijk de vorige of volgende periode te gaan. Met **< VORIGE** gaat u bijvoorbeeld van de **Afgelopen 7 dagen** naar **8-14 dagen geleden** of **15-21 dagen geleden**.

![Datumselector met een voorbeeldselectie voor deze maand](./media/quick-acm-cost-analysis/date-selector.png)

Kostenanalyse toont standaard **opgebouwde** kosten. Samengevoegde kosten zijn inclusief alle kosten voor elke dag plus de afgelopen dagen, voor een continu groeiend zicht op uw dagelijks cumulatieve kosten. Deze weergave is geoptimaliseerd om u te laten zien hoe u het doet in verhouding met het budget voor het geselecteerde tijdsbereik.

Gebruik de prognosediagramweergave om mogelijke budgetoverschrijdingen te identificeren. Wanneer er sprake is van een mogelijke budgetoverschrijding, wordt de geschatte overschrijding in het rood weergegeven. Er wordt ook een indicatiesymbool weergegeven in het diagram. Als u de muisaanwijzer boven het symbool houdt, wordt de geschatte datum van de budgetoverschrijding weergegeven.

![Voorbeeld van mogelijke budgetoverschrijding](./media/quick-acm-cost-analysis/budget-breach.png)

Er is ook de **dagelijkse** weergave die de kosten voor elke dag toont. De dagelijkse weergave toont geen groeitrend. De weergave is ontworpen om u onregelmatigheden als pieken of dalen in de kosten per dag te laten zien. Als u een budget hebt geselecteerd, toont de dagelijkse weergave ook een schatting van hoe uw dagelijkse budget eruitziet.

Als uw dagelijkse kosten stelselmatig boven het geschatte dagelijkse budget uitkomen, kunt u ervan uitgaan dat u uw maandelijkse budget overschrijdt. Het geschatte dagelijkse budget is een manier om u te helpen uw budget op een lager niveau te visualiseren. Wanneer u schommelingen hebt in uw dagelijkse kosten dan is de vergelijking tussen het geschatte dagelijkse budget en uw maandelijkse budget minder nauwkeurig.

Hier volgt een dagelijkse weergave van recente uitgaven waarvoor bestedingsprognose is ingeschakeld.
![Voorbeeld van een dagelijkse weergave waarin te zien is wat de dagelijkse kosten zijn in de huidige maand](./media/quick-acm-cost-analysis/daily-view.png)

Als u bestedingsprognose uitschakelt, ziet u geen geschatte uitgaven voor datums in de toekomst. En als u naar de kosten voor perioden in het verleden kijkt, bevatten de kostenprognoses geen kosten.

Over het algemeen zijn binnen acht tot twaalf uur gegevens of meldingen te zien over de verbruikte resources.

**Groeperen op** algemene eigenschappen om de kosten te specificeren en de belangrijkste kostenfactoren te identificeren. Als u bijvoorbeeld op resourcetag wilt groeperen, selecteert u de tagcode waarop u wilt groeperen. De kosten worden per tagwaarde weergegeven, met een extra segment voor resources waarop die tag niet is toegepast.  Zie [Groeps- en filteropties](https://docs.microsoft.com/azure/cost-management-billing/costs/group-filter) voor meer informatie over opties voor groeperen en filteren.

De meeste [Azure-resources bieden ondersteuning voor het gebruik van tags](../../azure-resource-manager/management/tag-support.md). Maar sommige tags zijn niet beschikbaar in Cost Management en facturering. Bovendien worden resourcegroeptags niet ondersteund. Ondersteuning voor labels is van toepassing op het gebruik dat is gerapporteerd *nadat* de tag is toegepast op de resource. Tags worden niet met terugwerkende kracht toegepast voor samengetelde kosten.

Bekijk de video [How to review tag policies with Azure Cost Management](https://www.youtube.com/watch?v=nHQYcYGKuyw) (Engelstalig) voor meer informatie over het gebruik van tagbeleid in Azure om de zichtbaarheid van kostengegevens te verbeteren.

Dit is een weergave van Azure-servicekosten voor de afgelopen maand.

![Gegroepeerde, dagelijks samengevoegde weergave met een voorbeeld van Azure-servicekosten van de afgelopen maand](./media/quick-acm-cost-analysis/grouped-daily-accum-view.png)

Standaard worden in een kostenanalyse alle gebruiks- en aankoopkosten weergegeven, terwijl ze worden samengevoegd. Deze worden weergegeven op uw factuur en worden ook wel **werkelijke kosten** genoemd. De mogelijkheid om de werkelijke kosten weer te geven, is ideaal als u uw factuur wilt afstemmen. Pieken in aankoopkosten kunnen alarmerend zijn als u afwijkingen in uitgaven en andere kostenfluctuaties onder controle wilt houden. Als u pieken wilt afvlakken die worden veroorzaakt door de aankoopkosten van een reservering, schakelt u over naar **Afgeschreven kosten**.

![Schakel van de werkelijke kosten over naar de afgeschreven kosten als u de reserveringsaankopen die zijn toegewezen aan de resources die van de reservering gebruik hebben gemaakt, verspreid over de hele periode wilt bekijken.](./media/quick-acm-cost-analysis/metric-picker.png)

Afgeschreven kosten worden weergegeven als reserveringsaankopen die zijn uitgesplitst in dagelijkse segmenten en verspreid over de duur van de reserveringsperiode. Zo ziet u in bijvoorbeeld in plaats van een aankoop van € 365 op 1 januari, een aankoop van € 1,00 voor elke dag van 1 januari tot en met 31 december. Naast de basisafschrijving ervan, worden deze kosten ook opnieuw toegewezen en gekoppeld met behulp van de specifieke resources die van de reservering gebruik hebben gemaakt. Als bijvoorbeeld de dagelijkse kosten van € 1,00 zijn uitgesplitst over twee virtuele machines, ziet u twee kostenposten van € 0,50 per dag. Als een deel van de reservering voor een bepaalde dag niet wordt gebruikt, ziet u één kostenpost van € 0,50 die is gekoppeld aan de desbetreffende virtuele machine en een extra kostenpost van € 0,50 met een kostentype `UnusedReservation`. Houd er rekening mee dat ongebruikte reserveringskosten alleen kunnen worden weergegeven als afgeschreven kosten worden weergegeven.

Omdat er een andere manier wordt gebruikt om kosten weer te geven, is het belangrijk om er rekening mee te houden dat de weergave van werkelijke kosten en de weergave van afgeschreven kosten andere totaalbedragen laten zien. Over het algemeen nemen de totale kosten voor maanden met een reserveringsaankoop af als deze in de weergave van afgeschreven kosten worden bekeken, en nemen deze in de maanden na een reserveringsaankoop toe. Afschrijving is alleen beschikbaar voor reserveringsaankopen en is op dit moment niet van toepassing op aankopen via Azure Marketplace.

De volgende afbeelding toont de resourcegroepnamen. U kunt op tag groeperen om de totale kosten per tag weer te geven of door de weergave **Kosten per resource** te gebruiken om alle labels voor een bepaalde resource te bekijken.

![Volledige gegevens van de huidige weergave, waarbij de resourcegroepnamen worden weergegeven](./media/quick-acm-cost-analysis/full-data-set.png)

Als u kosten groepeert op een specifiek kenmerk, worden de bovenste tien kostenposten van hoog naar laag weergegeven. Als er meer dan tien groepen zijn, worden de negen grootste kostenposten weergegeven, evenals een groep **Overige**, die alle overige groepen omvat. Wanneer u op tags groepeert, wordt een groep **Zonder tag** weergegeven voor kosten waarop de tagcode niet is toegepast. **Zonder tag** staat altijd onderaan, zelfs als de kosten zonder tag hoger zijn dan die met tag. Kosten zonder tags maken deel uit van **Overige** als er 10 of meer tagwaarden zijn. Schakel over naar de tabelweergave en wijzig de granulariteit in **Geen** om alle waarden gerangschikt van hoogste naar de laagste kosten weer te geven.

Klassieke virtuele machines, netwerken en opslagresources delen geen gedetailleerde factureringsgegevens. Ze worden samengevoegd als **Klassieke services** wanneer kosten worden gegroepeerd.

Draaigrafieken onder de hoofdgrafiek tonen verschillende groeperingen om u een breder beeld te geven van de totale kosten voor de geselecteerde periode en filters. Selecteer een eigenschap of tag om geaggregeerde kosten voor een dimensie weer te geven.

![Voorbeeld van draaigrafieken](./media/quick-acm-cost-analysis/pivot-charts.png)

U kunt de volledige gegevensset voor elke weergave bekijken. Selecties of filters die u toepast, zijn van invloed op de getoonde gegevens. Als u de volledige gegevensset wilt zien, selecteert u de lijst **grafiektype** en selecteert u vervolgens de **tabel**weergave.

![Gegevens voor de huidige weergave in tabelvorm](./media/quick-acm-cost-analysis/chart-type-table-view.png)

## <a name="saving-and-sharing-customized-views"></a>Aangepaste weergaven opslaan en delen

Sla aangepaste weergaven op en deel ze met anderen door een kostenanalyses vast te maken aan het dashboard in de Azure-portal of door een koppeling naar een kostenanalyse te kopiëren.

Bekijk de video [Sharing and saving views in Azure Cost Management](https://www.youtube.com/watch?v=kQkXXj-SmvQ) (Weergaven delen en opslaan in Azure Cost Management) voor meer informatie over het gebruik van de portal om kennis over kosten te delen in uw organisatie. Als u andere video’s wilt bekijken, gaat u naar het [YouTube-kanaal voor Cost Management](https://www.youtube.com/c/AzureCostManagement).

>[!VIDEO https://www.youtube.com/embed/kQkXXj-SmvQ]

Als u de kostenanalyse wilt vastmaken, selecteert u de speld in de rechterbovenhoek. Als u de kostenanalyse vastmaakt, wordt alleen de hoofdgrafiek of de tabelweergave opgeslagen. Deel het dashboard zodat anderen toegang tot de tegel hebben. Houd er wel rekening mee dat hiermee alleen de dashboardconfiguratie wordt gedeeld en dat andere gebruikers geen toegang tot de onderliggende gegevens krijgen. Als u geen toegang hebt tot kosten maar wel toegang hebt tot een gedeeld dashboard, wordt een bericht weergegeven met de strekking dat toegang is geweigerd.

Als u een koppeling naar de kostenanalyse wilt delen, selecteert u **Delen** boven aan de blade. Er wordt een aangepaste URL weergegeven, waarmee deze specifieke weergave voor dit specifieke bereik kan worden geopend. Als u geen toegang tot de kosten hebt en deze URL ontvangt, wordt er een bericht weergegeven dat aangeeft dat toegang is geweigerd.

Als u meer wilt weten over het verlenen van toegang tot kosten voor elk ondersteund bereik, raadpleegt u [Understand and work with scopes](understand-work-scopes.md) (Engelstalig).

## <a name="download-usage-data"></a>Gebruiksgegevens downloaden

Er zijn momenten waarop u de gegevens wilt downloaden voor verdere analyse, deze wilt samenvoegen met uw eigen gegevens of deze integreert in uw eigen systemen. Cost Management biedt een aantal verschillende opties. Als u behoefte hebt aan een tijdelijk kostenoverzicht dat de grote lijnen bevat, zoals het overzicht dat in een kostenanalyse beschikbaar is, moet u om te beginnen de weergave bouwen die u nodig hebt. Download deze vervolgens door **Exporteren** en **Gegevens naar CSV downloaden** of **Gegevens naar Excel downloaden** te selecteren. Het gedownloade Excel-bestand biedt aanvullende context voor de weergave die u hebt gebruikt om de download te genereren, zoals het bereik, de configuratie van de query, de totalen en de datum waarop de download is gegenereerd.

Als u de volledige, niet-geaggregeerde gegevensset nodig hebt, kunt u deze downloaden vanuit het factureringsaccount. Ga vervolgens in de lijst met services in het linkerdeelvenster in de portal naar **Kostenbeheer en facturering**. Selecteer uw factureringsaccount, indien van toepassing. Ga naar **Gebruik + kosten** en selecteer vervolgens het pictogram **Downloaden** voor de gewenste factureringsperiode.

## <a name="clean-up-resources"></a>Resources opschonen

- Als u een aangepaste weergave voor kostenanalyse hebt vastgemaakt en deze niet meer nodig hebt, gaat u naar het dashboard waar u deze hebt vastgemaakt en verwijdert u deze.
- Als u bestanden met gebruiksgegevens hebt gedownload en deze niet meer nodig hebt, zorg er dan voor dat u ze verwijdert.

## <a name="next-steps"></a>Volgende stappen

Ga door naar de eerste zelfstudie voor informatie over het maken en beheren van een budget.

> [!div class="nextstepaction"]
> [Budgetten maken en beheren](tutorial-acm-create-budgets.md)
