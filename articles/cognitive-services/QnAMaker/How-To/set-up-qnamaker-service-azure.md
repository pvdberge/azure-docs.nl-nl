---
title: Een QnA Maker-service instellen-QnA Maker
description: Voordat u QnA Maker Knowledge bases kunt maken, moet u eerst een QnA Maker service in azure instellen. Iedereen met een machtiging voor het maken van nieuwe resources in een abonnement kan een QnA Maker-service instellen.
ms.topic: conceptual
ms.date: 07/13/2020
ms.openlocfilehash: 7ba8134f58a4f0e4e26a3246a44574df295e3c20
ms.sourcegitcommit: 3d79f737ff34708b48dd2ae45100e2516af9ed78
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/23/2020
ms.locfileid: "87040389"
---
# <a name="manage-qna-maker-resources"></a>QnA Maker-resources beheren

Voordat u QnA Maker Knowledge bases kunt maken, moet u eerst een QnA Maker service in azure instellen. Iedereen met een machtiging voor het maken van nieuwe resources in een abonnement kan een QnA Maker-service instellen.

Een uitgevulde uitleg van de volgende concepten is handig voordat u de resource maakt:

* [QnA Maker resources](../Concepts/azure-resources.md)
* [Sleutels ontwerpen en publiceren](../Concepts/azure-resources.md#keys-in-qna-maker)

## <a name="create-a-new-qna-maker-service"></a>Een nieuwe QnA Maker-service maken

Met deze procedure maakt u de Azure-resources die nodig zijn voor het beheren van de inhoud van de Knowledge Base. Nadat u deze stappen hebt voltooid, vindt u de _abonnements_ sleutels op de pagina **sleutels** voor de resource in de Azure Portal.

1. Meld u aan bij de Azure Portal en [Maak een QnA Maker](https://ms.portal.azure.com/#create/Microsoft.CognitiveServicesQnAMaker) -resource.

1. Selecteer **maken** nadat u de voor waarden hebt gelezen:

    ![Een nieuwe QnA Maker-service maken](../media/qnamaker-how-to-setup-service/create-new-resource-button.png)

1. Selecteer in **QnA Maker**de juiste lagen en regio's:

    ![Een nieuwe QnA Maker prijs categorie en regio's voor services maken](../media/qnamaker-how-to-setup-service/enter-qnamaker-info.png)

    * Voer in het veld **naam** een unieke naam in om deze QnA Maker service aan te duiden. Deze naam duidt ook het QnA Maker-eind punt aan waaraan uw kennis grondslagen worden gekoppeld.
    * Kies het **abonnement** waarmee de QnA Maker resource wordt geïmplementeerd.
    * Selecteer de **prijs categorie** voor de QnA Maker-beheer Services (Portal-en beheer-api's). Bekijk [meer informatie over de prijzen van de SKU](https://aka.ms/qnamaker-pricing).
    * Een nieuwe **resource groep** maken (aanbevolen) of een bestaande gebruiken om deze QnA Maker-resource te implementeren. QnA Maker maakt verschillende Azure-resources. Wanneer u een resource groep maakt om deze resources te bevatten, kunt u deze resources eenvoudig vinden, beheren en verwijderen op basis van de naam van de resource groep.
    * Selecteer een **locatie voor de resource groep**.
    * Kies de **prijs categorie voor zoeken** in de Azure Cognitive Search-service. Als de optie gratis laag niet beschikbaar is (grijs weer gegeven), betekent dit dat u al een gratis service hebt geïmplementeerd via uw abonnement. In dat geval moet u beginnen met de laag basis. Zie de [prijs informatie voor Azure Cognitive Search](https://azure.microsoft.com/pricing/details/search/).
    * Kies de **Zoek locatie** waar u Azure Cognitive Search-indexen wilt implementeren. Beperkingen voor het opslaan van klant gegevens kunnen helpen bij het bepalen van de locatie die u kiest voor Azure Cognitive Search.
    * Voer in het veld **app-naam** een naam in voor uw Azure app service-exemplaar.
    * Standaard App Service standaard ingesteld op de standaard laag (S1). U kunt het abonnement wijzigen nadat u het hebt gemaakt. Meer informatie over [app service prijzen](https://azure.microsoft.com/pricing/details/app-service/).
    * Kies de **locatie** van de Website waar app service worden geïmplementeerd.

        > [!NOTE]
        > De **Zoek locatie** kan afwijken van de **locatie**van de website.

    * Kies of u **Application Insights**wilt inschakelen. Als **Application Insights** is ingeschakeld, verzamelt QnA Maker telemetrie in verkeer, chat logboeken en fouten.
    * Kies de **app Insights-locatie** waar de Application Insights resource wordt geïmplementeerd.
    * Voor kosten besparingen kunt u enkele, maar niet alle Azure-resources die zijn gemaakt voor QnA Maker [delen](#configure-qna-maker-to-use-different-cognitive-search-resource) .

1. Nadat alle velden zijn gevalideerd, selecteert u **maken**. Het proces kan een paar minuten duren.

1. Nadat de implementatie is voltooid, ziet u de volgende resources die zijn gemaakt in uw abonnement:

   ![Resource heeft een nieuwe QnA Maker service gemaakt](../media/qnamaker-how-to-setup-service/resources-created.png)

    De resource met het _Cognitive Services_ type heeft uw _abonnements_ sleutels.


## <a name="find-authoring-keys-in-the-azure-portal"></a>Zoek sleutels zoeken in de Azure Portal

U kunt uw ontwerp sleutels bekijken en opnieuw instellen in de Azure Portal, waar u de QnA Maker resource hebt gemaakt. Deze sleutels kunnen worden aangeduid als abonnements sleutels.

1. Ga naar de QnA Maker resource in de Azure Portal en selecteer de resource met het _Cognitive Services_ type:

    ![QnA Maker Resource lijst](../media/qnamaker-how-to-key-management/qnamaker-resource-list.png)

2. Ga naar **sleutels**:

    ![Abonnementssleutel](../media/qnamaker-how-to-key-management/subscription-key.PNG)

## <a name="find-query-endpoint-keys-in-the-qna-maker-portal"></a>Zoek eindpunt sleutels zoeken in de QnA Maker Portal

Het eind punt bevindt zich in dezelfde regio als de resource omdat de eindpunt sleutels worden gebruikt voor het aanroepen van de Knowledge Base.

Eindpunt sleutels kunnen worden beheerd vanuit de [QnA Maker Portal](https://qnamaker.ai).

1. Meld u aan bij de [QnA Maker-Portal](https://qnamaker.ai), ga naar uw profiel en selecteer vervolgens service- **instellingen**:

    ![Eindpunt sleutel](../media/qnamaker-how-to-key-management/Endpoint-keys.png)

2. Uw sleutels weer geven of herstellen:

    > [!div class="mx-imgBorder"]
    > ![Eindpunt sleutel beheer](../media/qnamaker-how-to-key-management/Endpoint-keys1.png)

    >[!NOTE]
    >Vernieuw uw sleutels als u denkt dat ze zijn aangetast. Hiervoor kunnen eventueel bijbehorende wijzigingen in de client toepassing of bot code worden vereist.

### <a name="update-the-resources"></a>De resources bijwerken

Meer informatie over het bijwerken van de resources die worden gebruikt door uw Knowledge Base.

### <a name="upgrade-qna-maker-sku"></a>QnA Maker SKU bijwerken

Als u meer vragen en antwoorden in uw Knowledge Base wilt hebben, moet u de prijs categorie van QnA Maker service upgraden naar uw huidige laag.

Een upgrade uitvoeren van de QnA Maker Management SKU:

1. Ga in de Azure Portal naar uw QnA Maker-resource en selecteer **prijs categorie**.

    ![QnA Maker resource](../media/qnamaker-how-to-upgrade-qnamaker/qnamaker-resource.png)

1. Kies de juiste SKU en druk op **selecteren**.

    ![QnA Maker prijzen](../media/qnamaker-how-to-upgrade-qnamaker/qnamaker-pricing-page.png)

### <a name="upgrade-app-service"></a>App Service bijwerken

 Als uw Knowledge Base meer aanvragen van uw client-app wil leveren, moet u uw App Service prijs categorie bijwerken.

U kunt App Service [schalen](https://docs.microsoft.com/azure/app-service/manage-scale-up) of uitschalen.

Ga naar de App Service resource in de Azure Portal en selecteer de optie **Omhoog schalen** of **uitschalen** .

![QnA Maker App Service schaal](../media/qnamaker-how-to-upgrade-qnamaker/qnamaker-appservice-scale.png)

### <a name="upgrade-the-azure-cognitive-search-service"></a>De Azure Cognitive Search-service upgraden

Als u van plan bent een groot aantal Knowledge bases te hebben, moet u de prijs categorie van uw Azure Cognitive Search-service bijwerken.

Op dit moment kunt u geen in-place upgrade van de SKU voor Azure Search uitvoeren. U kunt echter een nieuwe Azure Search-resource met de gewenste SKU maken, de gegevens herstellen naar de nieuwe resource en deze vervolgens koppelen aan de QnA Maker-stack. Voer hiervoor de volgende stappen uit:

1. Maak een nieuwe Azure-Zoek resource in het Azure Portal en selecteer de gewenste SKU.

    ![QnA Maker Azure Search-resource](../media/qnamaker-how-to-upgrade-qnamaker/qnamaker-azuresearch-new.png)

1. Herstel de indexen van de oorspronkelijke Azure Search-resource naar de nieuwe. Zie de [voorbeeld code voor het terugzetten van back-ups](https://github.com/pchoudhari/QnAMakerBackupRestore).

1. Nadat de gegevens zijn hersteld, gaat u naar uw nieuwe Azure Search-resource, selecteert u **sleutels**en noteert u de **naam** en de **beheerders sleutel**:

    ![QnA Maker Azure-Zoek sleutels](../media/qnamaker-how-to-upgrade-qnamaker/qnamaker-azuresearch-keys.png)

1. Als u de nieuwe Azure Search-resource wilt koppelen aan de QnA Maker stack, gaat u naar het QnA Maker App Service-exemplaar.

    ![App Service instantie QnA Maker](../media/qnamaker-how-to-upgrade-qnamaker/qnamaker-resource-list-appservice.png)

1. Selecteer **Toepassings instellingen** en wijzig de instellingen in de velden **AzureSearchName** en **AzureSearchAdminKey** uit stap 3.

    ![Instelling voor QnA Maker App Service](../media/qnamaker-how-to-upgrade-qnamaker/qnamaker-appservice-settings.png)

1. Start het App Service-exemplaar opnieuw.

    ![Het QnA Maker App Service-exemplaar opnieuw starten](../media/qnamaker-how-to-upgrade-qnamaker/qnamaker-appservice-restart.png)

## <a name="get-the-latest-runtime-updates"></a>Down load de meest recente runtime-updates

De QnAMaker-runtime maakt deel uit van het Azure App Service-exemplaar dat wordt geïmplementeerd wanneer u [een QnAMaker-service](./set-up-qnamaker-service-azure.md) in de Azure Portal maakt. Er worden regel matig updates uitgevoerd voor de runtime. Het QnA Maker App Service-exemplaar bevindt zich in de modus automatisch bijwerken na de site-extensie release van april 2019 (versie 5 +). Deze update is ontworpen om te zorgen dat er geen downtime is tijdens de upgrade.

U kunt uw huidige versie controleren op https://www.qnamaker.ai/UserSettings . Als uw versie ouder is dan versie 5. x, moet u App Service opnieuw opstarten om de meest recente updates toe te passen:

1. Ga naar de QnAMaker-service (resource groep) in het [Azure Portal](https://portal.azure.com).

    > [!div class="mx-imgBorder"]
    > ![Azure-resource groep QnAMaker](../media/qnamaker-how-to-troubleshoot/qnamaker-azure-resourcegroup.png)

1. Selecteer de App Service instantie en open de sectie **overzicht** .

    > [!div class="mx-imgBorder"]
    > ![QnAMaker App Service-instantie](../media/qnamaker-how-to-troubleshoot/qnamaker-azure-appservice.png)


1. Start App Service opnieuw. Het update proces moet binnen een paar seconden worden voltooid. Alle afhankelijke toepassingen of botsingen die gebruikmaken van deze QnAMaker-service, zijn niet beschikbaar voor eind gebruikers tijdens de herstart periode.

    ![Het QnAMaker App Service-exemplaar opnieuw starten](../media/qnamaker-how-to-upgrade-qnamaker/qnamaker-appservice-restart.png)

## <a name="cognitive-search-consideration"></a>Cognitive Searche overweging

Cognitive Search, als afzonderlijke resource, hebben een aantal verschillende configuraties waar u rekening mee moet houden.

### <a name="configure-qna-maker-to-use-different-cognitive-search-resource"></a>QnA Maker configureren voor het gebruik van verschillende Cognitive Search resource

Als u een QnA-service en de bijbehorende afhankelijkheden (zoals zoeken) maakt via de portal, wordt er een zoek service voor u gemaakt en gekoppeld aan de QnA Maker-service. Nadat deze resources zijn gemaakt, kunt u de App Service-instelling bijwerken om een eerder bestaande zoek service te gebruiken en de toepassing verwijderen die u zojuist hebt gemaakt.

De **app service** resource van QnA Maker maakt gebruik van de Cognitive Search resource. Als u de Cognitive Search resource wilt wijzigen die door QnA Maker wordt gebruikt, moet u de instelling wijzigen in de Azure Portal.

1. Haal de **beheerders sleutel** en de **naam** op van de Cognitive Search resource die u QnA Maker wilt gebruiken.

1. Meld u aan bij de [Azure Portal](https://portal.azure.com) en zoek de **app service** die aan uw QnA Maker-resource zijn gekoppeld. Beide met dezelfde naam hebben.

1. Selecteer **instellingen**en vervolgens **configuratie**. Hiermee worden alle bestaande instellingen voor de App Service van de QnA Maker weer gegeven.

    > [!div class="mx-imgBorder"]
    > ![Scherm opname van Azure Portal App Service configuratie-instellingen worden weer gegeven](../media/qnamaker-how-to-upgrade-qnamaker/change-search-service-app-service-configuration.png)

1. Wijzig de waarden voor de volgende sleutels:

    * **AzureSearchAdminKey**
    * **AzureSearchName**

1. Als u de nieuwe instellingen wilt gebruiken, moet u de app service opnieuw starten. Selecteer **overzicht**en selecteer **opnieuw opstarten**.

    > [!div class="mx-imgBorder"]
    > ![Scherm opname van Azure Portal App Service opnieuw opstarten nadat de configuratie-instellingen zijn gewijzigd](../media/qnamaker-how-to-upgrade-qnamaker/screenshot-azure-portal-restart-app-service.png)

Als u een QnA-service maakt via Azure Resource Manager sjablonen, kunt u alle resources maken en de App Service maken om een bestaande zoek service te gebruiken.

Meer informatie over het configureren van de App Service [Toepassings instellingen](../../../app-service/configure-common.md#configure-app-settings).

### <a name="configuring-cognitive-search-as-a-private-endpoint-inside-a-vnet"></a>Cognitive Search configureren als een persoonlijk eind punt in een VNET

Wanneer een zoek instantie wordt gemaakt tijdens het maken van een QnA Maker bron, kunt u Cognitive Search voor het ondersteunen van een persoonlijke eindpunt configuratie die volledig is gemaakt in het VNet van de klant.

Alle resources moeten in dezelfde regio worden gemaakt om een persoonlijk eind punt te kunnen gebruiken.

* QnA Maker resource
* nieuwe Cognitive Search resource
* nieuwe Virtual Network resource

Voer de volgende stappen uit in de [Azure Portal](https://portal.azure.com):

1. Maak een [QnA Maker resource](https://ms.portal.azure.com/#create/Microsoft.CognitiveServicesQnAMaker).
1. Maak een nieuwe Cognitive Search resource waarvan de eindpunt verbinding (gegevens) is ingesteld op _privé_. Maak de resource in dezelfde regio als de QnA Maker resource die u in stap 1 hebt gemaakt. Meer informatie over het [maken van een Cognitive Search resource](../../../search/search-create-service-portal.md)en vervolgens met behulp van deze koppeling rechtstreeks naar de [pagina maken van de resource](https://ms.portal.azure.com/#create/Microsoft.Search)gaan.
1. Maak een nieuwe [Virtual Network resource](https://ms.portal.azure.com/#create/Microsoft.VirtualNetwork-ARM).
1. Configureer het VNET op de app service-resource die u hebt gemaakt in stap 1 van deze procedure.
    1. Maak een nieuwe DNS-vermelding in het VNET voor een nieuwe Cognitive Search resource die u in stap 2 hebt gemaakt. naar het IP-adres van de Cognitive Search.
1. [Koppel de app service aan de nieuwe Cognitive Search resource die u](#configure-qna-maker-to-use-different-cognitive-search-resource) in stap 2 hebt gemaakt. Vervolgens kunt u de oorspronkelijke Cognitive Search resource verwijderen die u in stap 1 hebt gemaakt.

Maak uw eerste Knowledge Base in de [QnA Maker Portal](https://www.qnamaker.ai/).


### <a name="inactivity-policy-for-free-search-resources"></a>Inactiviteits beleid voor gratis Zoek bronnen

Als u geen QnA Maker-resource gebruikt, moet u alle resources verwijderen. Als u geen ongebruikte resources verwijdert, zal uw kennis basis niet meer werken als u een gratis Zoek resource hebt gemaakt.

Gratis Zoek bronnen worden na 90 dagen verwijderd zonder dat er een API-aanroep wordt ontvangen.

## <a name="configure-app-service-idle-setting-to-avoid-timeout"></a>De instelling niet-actieve app service configureren om een time-out te voor komen

De app service, die de QnA Maker Voorspellings runtime voor een gepubliceerde kennis database gebruikt, heeft een time-outconfiguratie voor inactiviteit, die standaard automatisch een time-out krijgt als de service niet actief is. In het geval van QnA Maker betekent dit dat uw prediction runtime generateAnswer-API af en toe na Peri Oden van geen verkeer kan worden uitgevoerd.

Als u de app voor Voorspellings eindpunt wilt laden, zelfs wanneer er geen verkeer is, stelt u de niet-actief in op altijd aan.

1. Meld u aan bij [Azure Portal](https://portal.azure.com).
1. Zoek en selecteer de app service van uw QnA Maker-resource. Deze heeft dezelfde naam als de QnA Maker resource, maar heeft een ander **type** app service.
1. Zoek **instellingen** en selecteer **configuratie**.
1. In het deel venster configuratie selecteert u **algemene instellingen**, vervolgens **altijd zoeken in** **en selecteert u** als waarde.

    > [!div class="mx-imgBorder"]
    > ![Selecteer in het deel venster configuratie de optie * * algemene instellingen * *, zoek * * always on * * en selecteer * * op * * als waarde.](../media/qnamaker-how-to-upgrade-qnamaker/configure-app-service-idle-timeout.png)

1. Selecteer **Opslaan** om de configuratie op te slaan.
1. U wordt gevraagd of u de app opnieuw wilt starten voor het gebruik van de nieuwe instelling. Selecteer **Doorgaan**.

Meer informatie over het configureren van de App Service [algemene instellingen](../../../app-service/configure-common.md#configure-general-settings).

## <a name="configure-app-service-environment-to-host-qna-maker-app-service"></a>App Service Environment voor het hosten van QnA Maker configureren App Service
De App Service Environment kan worden gebruikt om QnA Maker app service te hosten. Als de App Service Environment intern is, moet u deze stappen volgen:
1. Maak een app service en een Azure Search-service.
2. Maak de app-service beschikbaar en sta QnA Maker Beschik baarheid toe als:
    * Openbaar beschikbaar-standaard
    * Label voor de DNS-service:
        * `CognitiveServicesManagement`
    * IP-adressen die zijn gekoppeld aan QnA Maker zijn:
        * 13.91.138.229
        * 40.88.22.25
        * 13.86.184.142
        * 20.185.105.28
        * 13.86.178.10
1. Maak een QnA Maker cognitieve service-exemplaar (micro soft. CognitiveServices/accounts) met behulp van Azure Resource Manager, waarbij QnA Maker eind punt moet worden ingesteld op App Service Environment.

## <a name="business-continuity-with-traffic-manager"></a>Bedrijfs continuïteit met Traffic Manager

Het hoofd doel van het plan voor bedrijfs continuïteit is het maken van een robuust eind punt van de Knowledge Base, waardoor er geen verdere tijd is voor de bot of de toepassing die deze gebruikt.

> [!div class="mx-imgBorder"]
> ![QnA Maker BCP-abonnement](../media/qnamaker-how-to-bcp-plan/qnamaker-bcp-plan.png)

Het idee op hoog niveau zoals hierboven wordt weer gegeven, is als volgt:

1. Stel twee parallelle [QnA Maker Services](set-up-qnamaker-service-azure.md) in in [Azure gekoppelde regio's](https://docs.microsoft.com/azure/best-practices-availability-paired-regions).

1. [Back-up maken](../../../app-service/manage-backup.md) van uw primaire QnA Maker app-service en deze [herstellen](../../../app-service/web-sites-restore.md) in de secundaire installatie. Dit zorgt ervoor dat beide instellingen werken met dezelfde hostnaam en sleutels.

1. Zorg ervoor dat de primaire en secundaire Azure Search-indexen synchroon blijven. Gebruik het GitHub-voor beeld [hier](https://github.com/pchoudhari/QnAMakerBackupRestore) om te zien hoe u een back-up maakt van Azure-indexen.

1. Maak een back-up van de Application Insights met [doorlopend exporteren](../../../application-insights/app-insights-export-telemetry.md).

1. Zodra de primaire en secundaire Stacks zijn ingesteld, gebruikt u [Traffic Manager](../../../traffic-manager/traffic-manager-overview.md) om de twee eind punten te configureren en een routerings methode in te stellen.

1. U moet een Transport Layer Security (TLS), voorheen bekend als Secure Sockets Layer (SSL), maken van het certificaat voor uw Traffic Manager-eind punt. [BIND het TLS/SSL-certificaat](../../../app-service/configure-ssl-bindings.md) in uw app-Services.

1. Ten slotte gebruikt u het Traffic Manager-eind punt in uw bot of app.

## <a name="delete-azure-resources"></a>Azure-resources verwijderen

Als u een van de Azure-resources verwijdert die voor uw QnA Maker Knowledge bases worden gebruikt, werken de kennis bases niet meer. Voordat u een resource verwijdert, moet u de kennis bases exporteren vanaf de pagina **instellingen** .

## <a name="next-steps"></a>Volgende stappen

Meer informatie over de [app service](../../../app-service/index.yml) en de [Zoek service](../../../search/index.yml).

> [!div class="nextstepaction"]
> [Meer informatie over hoe u met anderen kunt ontwerpen](../how-to/collaborate-knowledge-base.md)
