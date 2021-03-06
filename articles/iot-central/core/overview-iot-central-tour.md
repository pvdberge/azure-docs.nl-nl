---
title: Kennismaking met de gebruikersinterface van Azure IoT Central | Microsoft Docs
description: Raak vertrouwd met de belangrijkste gebieden van de gebruikersinterface van Azure IoT Central, waarmee u een IoT-oplossing kunt maken, beheren en gebruiken.
author: lmasieri
ms.author: lmasieri
ms.date: 12/09/2019
ms.topic: overview
ms.service: iot-central
services: iot-central
ms.custom: mvc
manager: corywink
ms.openlocfilehash: c07d247358d980152648fdf7f702c8efcb72bab9
ms.sourcegitcommit: 43558caf1f3917f0c535ae0bf7ce7fe4723391f9
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/11/2020
ms.locfileid: "90020070"
---
# <a name="take-a-tour-of-the-azure-iot-central-ui"></a>Kennismaking met de gebruikersinterface van Azure IoT Central

In dit artikel maakt u kennis met de gebruikersinterface van Microsoft Azure IoT Central. U kunt de gebruikersinterface gebruiken om een Azure IoT Central-oplossing te maken en de daarmee verbonden apparaten te beheren en gebruiken.

Als _ontwikkelaar van oplossingen_ gebruikt u de gebruikersinterface van Azure IoT Central om uw Azure IoT Central-oplossing te definiëren. U kunt de gebruikersinterface gebruiken om:

* De typen apparaten te definiëren die met uw oplossing verbinding maken.
* De regels en acties voor uw apparaten te configureren. 
* De gebruikersinterface aan te passen voor een _operator_ die uw oplossing gebruikt.

Als _operator_ gebruikt u de gebruikersinterface van Azure IoT Central om uw Azure IoT Central-oplossing te beheren. U kunt de gebruikersinterface gebruiken om:

* Uw apparaten te controleren.
* Uw apparaten te configureren.
* Problemen met uw apparaten op te lossen.
* Nieuwe apparaten inrichten.

## <a name="iot-central-homepage"></a>Startpagina IoT Central

Op de startpagina van [IoT Central](https://aka.ms/iotcentral-get-started) vindt u meer informatie over het laatste nieuws en de beschikbare functies op IoT Central, kunt u nieuwe toepassingen maken en uw bestaande toepassing weergeven en starten.

> [!div class="mx-imgBorder"]
> ![Startpagina IoT Central](media/overview-iot-central-tour/iot-central-homepage-pnp.png)

### <a name="create-an-application"></a>Een app maken

In de sectie Build kunt u bladeren door de lijst met branchespecifieke IoT Central-sjablonen om snel aan de slag te gaan, of met een volledig nieuwe aangepaste app-sjabloon gebruiken.  
> [!div class="mx-imgBorder"]
> ![Ontwikkelpagina IoT Central](media/overview-iot-central-tour/iot-central-build-pnp.png)

Raadpleeg het artikel [Een Azure IoT Central-toepassing maken](quick-deploy-iot-central.md) voor meer informatie.

### <a name="launch-your-application"></a>Uw toepassing starten

U kunt uw IoT Central-toepassing starten door naar de URL te gaan die u of de opbouwfunctie voor uw oplossing hebt/heeft gekozen tijdens het maken van de app. U kunt ook een lijst weergeven met alle toepassingen waartoe u toegang hebt tot het [IoT Central-app-beheer](https://aka.ms/iotcentral-apps).

> [!div class="mx-imgBorder"]
> ![App-beheer IoT Central](media/overview-iot-central-tour/app-manager-pnp.png)

## <a name="navigate-your-application"></a>Door uw toepassing bladeren

Als u zich in uw IoT-toepassing bevindt, gebruikt u het linkerdeelvenster voor toegang tot de verschillende gebieden. U kunt het linkerdeelvenster uitvouwen of samenvouwen door het pictogram met drie lijnen boven aan het deelvenster te selecteren:

> [!NOTE]
> De items die u in het linkerdeelvenster ziet, zijn afhankelijk van uw gebruikersrol. Meer informatie over het [beheren van gebruikers en rollen](howto-manage-users-roles.md). 

:::row:::
  :::column span="":::
      > [!div class="mx-imgBorder"]
      > ![linkerdeelvenster](media/overview-iot-central-tour/navigationbar-pnp.png)
  :::column-end:::
  :::column span="2":::
     Het **dashboard** geeft uw toepassingsdashboard weer. Als *ontwikkelaar van oplossingen* kunt u het globale dashboard aanpassen voor uw operators. Afhankelijk van hun gebruikersrol kunnen operators ook hun eigen persoonlijke dashboards maken.
     
     Met **Apparaten** kunt u uw - echte en gesimuleerde - verbonden apparaten beheren.

     Met **Apparaatgroepen** kunt u logische verzamelingen apparaten weergeven en maken die door een query zijn opgegeven. U kunt deze query opslaan en apparaatgroepen via de toepassing gebruiken om bulkbewerkingen uit te voeren.

     Met **Regels** kunt u regels maken en bewerken om uw apparaten te bewaken. Regels worden geëvalueerd op basis van de telemetrie van het apparaat en het activeren van aanpasbare acties.

     Met **Analyse** kunt u uw apparaatgegevens aangepast weergeven voor meer inzicht in uw toepassing.

     Met **Taken** kunt u uw apparaten op schaal beheren door bulkbewerkingen uit te voeren.

     In **Apparaatsjablonen** kunt u de kenmerken van de apparaten die verbinding maken met uw toepassing beheren.

     Met **Gegevensexport** kunt u een continue export naar externe services configureren, zoals opslag en wachtrijen.

     In **Beheer** kunt u de instellingen, aanpassing, facturering, gebruikers en rollen van uw toepassing beheren.

     Met **IoT Central** kunnen *beheerders* teruggaan naar het app-beheer van IoT Central.
     
   :::column-end:::
:::row-end:::

### <a name="search-help-theme-and-support"></a>Zoeken, hulp, thema en ondersteuning

Het bovenste menu wordt op elke pagina weergegeven:

> [!div class="mx-imgBorder"]
> ![Werkbalk](media/overview-iot-central-tour/toolbar-pnp.png)

* Als u wilt zoeken naar apparaatsjablonen en apparaten, geeft u een **Zoek**-waarde op.
* Als u de taal of het thema van de gebruikersinterface wilt wijzigen, kiest u het pictogram **Instellingen**. Meer informatie over [het beheren van de voorkeuren van uw toepassing](howto-manage-preferences.md)
* Als u zich wilt afmelden bij de toepassing, kiest u het pictogram **Account**.
* Als u hulp en ondersteuning nodig hebt, kiest u het keuzemenu **Help** voor een lijst met bronnen. U kunt [informatie over uw toepassing](./howto-get-app-info.md) ophalen uit de koppeling **Over uw app**. In een toepassing met een gratis abonnement bevatten de ondersteuningsresources toegang tot [live chat](howto-show-hide-chat.md).

Voor de gebruikersinterface kunt u kiezen tussen een licht thema of een donker thema:

> [!NOTE]
> De optie om te kiezen tussen lichte en donkere thema's is niet beschikbaar als uw beheerder een aangepast thema voor de toepassing heeft geconfigureerd.

> [!div class="mx-imgBorder"]
> ![Een thema voor de gebruikersinterface kiezen](media/overview-iot-central-tour/themes-pnp.png)

### <a name="dashboard"></a>Dashboard
> [!div class="mx-imgBorder"]
> ![Dashboard](media/overview-iot-central-tour/dashboard-pnp.png)

* Het dashboard is de eerste pagina die u ziet als u zich aanmeldt bij uw Azure IoT Central-toepassing. Als *ontwikkelaar van oplossingen* kunt u meerdere algemene toepassingsdashboards voor andere gebruikers maken en aanpassen. Meer informatie over [tegels toevoegen aan uw dashboard](howto-add-tiles-to-your-dashboard.md)

* Als *operator* kunt u, als uw gebruikersrol dit toestaat, persoonlijke dashboards maken om te controleren wat u belangrijk vindt. Zie het artikel met instructies [Create Azure IoT Central personal dashboards](howto-create-personal-dashboards.md) (Azure IoT Central persoonlijke dashboards maken) voor meer informatie.

### <a name="devices"></a>Apparaten

> [!div class="mx-imgBorder"]
> ![De pagina Apparaten](media/overview-iot-central-tour/devices-pnp.png)

Op de Device Explorer-pagina worden de _apparaten_ in uw Azure IoT Central-toepassing gegroepeerd weergegeven op _apparaatsjabloon_. 

* Met een apparaatsjabloon wordt een type apparaat gedefinieerd dat met uw toepassing verbinding kan maken.
* Een apparaat vertegenwoordigt een echt of een gesimuleerd apparaat in uw toepassing.

Zie de quickstart [Uw apparaten bewaken](./quick-monitor-devices.md) voor meer informatie. 

### <a name="device-groups"></a>Apparaatgroepen

> [!div class="mx-imgBorder"]
> ![De pagina Apparaatgroepen](media/overview-iot-central-tour/device-groups-pnp.png)

Apparaatgroepen zijn verzamelingen verwante apparaten. Een *ontwikkelaar van oplossingen* definieert een query om de apparaten te identificeren die in een apparaatgroep zijn opgenomen. U gebruikt apparaatgroepen om bulkbewerkingen uit te voeren in uw toepassing. Raadpleeg het artikel [Apparaatgroepen gebruiken in uw Azure IoT Central-toepassing](tutorial-use-device-groups.md) voor meer informatie.

### <a name="rules"></a>Regels
> [!div class="mx-imgBorder"]
> ![De pagina Regels](media/overview-iot-central-tour/rules-pnp.png)

Op de pagina Regels kunt u regels definiëren op basis van de telemetrie, status of gebeurtenissen van apparaten. Wanneer een regel wordt geactiveerd, kunnen hierdoor een of meer acties worden geactiveerd, zoals het verzenden van een e-mail bericht, het melden van een extern systeem via webhook-waarschuwingen, enzovoort. Zie de zelfstudie [Regels configureren](tutorial-create-telemetry-rules.md) voor meer informatie. 

### <a name="analytics"></a>Analyse

> [!div class="mx-imgBorder"]
> ![De pagina Analyse](media/overview-iot-central-tour/analytics-pnp.png)

Met Analyse kunt u uw apparaatgegevens aangepast weergeven voor meer inzicht in uw toepassing. Raadpleeg het artikel [Analyses maken voor uw Azure IoT Central-toepassing](howto-create-analytics.md) voor meer informatie.

### <a name="jobs"></a>Taken

> [!div class="mx-imgBorder"]
> ![De pagina Taken](media/overview-iot-central-tour/jobs-pnp.png)

Met de pagina Taken kunt u bulksgewijze beheerbewerkingen op uw apparaten uitvoeren. U kunt eigenschappen en instellingen van apparaten bijwerken en opdrachten uitvoeren ten aanzien van apparaatgroepen. Zie voor meer informatie, het artikel [Een taak uitvoeren](howto-run-a-job.md).

### <a name="device-templates"></a>Apparaatsjablonen

> [!div class="mx-imgBorder"]
> ![De pagina Apparaatsjablonen](media/overview-iot-central-tour/templates-pnp.png)

De opbouwfunctie gebruikt de pagina Apparaatsjablonen om de apparaatsjablonen in de toepassing te maken en beheren. Met een apparaatsjabloon worden de kenmerken van apparaten opgegeven, zoals:

* Telemetrie-, status- en gebeurtenismetingen
* Eigenschappen
* Opdrachten
* Weergaven

De *ontwikkelaar van oplossingen* kan ook formulieren en dashboards maken die operators kunnen gebruiken om apparaten te beheren.

Raadpleeg voor meer informatie de zelfstudie [Define a new device type in your Azure IoT Central application](howto-set-up-template.md) (Een nieuw apparaattype definiëren in uw Azure IoT Central-toepassing). 

### <a name="data-export"></a>Gegevensexport
> [!div class="mx-imgBorder"]
> ![De pagina Gegevensexport](media/overview-iot-central-tour/export-pnp.png)

Met Gegevensexport kunt u gegevensstromen, zoals telemetrie, van de toepassing naar externe systemen instellen. Zie het artikel [Exporteren van gegevens in Azure IoT Central](./howto-export-data.md) voor meer informatie.

### <a name="administration"></a>Beheer
> [!div class="mx-imgBorder"]
> ![De pagina Beheer](media/overview-iot-central-tour/administration-pnp.png)

Op de pagina Beheer kunt u uw IoT Central-toepassing configureren en aanpassen. Hier kunt u de naam, de URL, de thema's van uw toepassing wijzigen, de gebruikers en rollen beheren, API-tokens maken en uw toepassing exporteren. Raadpleeg voor meer informatie het artikel [Administer your Azure IoT Central application](howto-administer.md) (Uw Azure IoT Central-toepassing beheren).

## <a name="next-steps"></a>Volgende stappen

Nu u een overzicht hebt van Azure IoT Central en bekend bent met de indeling van de gebruikersinterface, is de voorgestelde vervolgstap om de snelstart [Create an Azure IoT Central application](quick-deploy-iot-central.md) (Een Azure IoT Central-toepassing maken) te voltooien.
