---
title: Persoonlijke Dash boards voor Azure IoT Central maken | Microsoft Docs
description: Als gebruiker leert u hoe u uw persoonlijke Dash boards kunt maken en beheren.
author: mavoge
ms.author: mavoge
ms.date: 10/17/2019
ms.topic: how-to
ms.service: iot-central
services: iot-central
manager: philmea
ms.openlocfilehash: f7dca7352a49e668231f64632371a445985e4de3
ms.sourcegitcommit: 877491bd46921c11dd478bd25fc718ceee2dcc08
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/02/2020
ms.locfileid: "83634552"
---
# <a name="create-and-manage-multiple-dashboards"></a>Meerdere Dash boards maken en beheren

Het **dash board** is de pagina die wordt geladen wanneer u voor het eerst naar uw toepassing navigeert. Een **opbouw functie** in uw toepassing definieert het standaard toepassings dashboard voor alle gebruikers. U kunt ook uw eigen, gepersonaliseerde toepassings dashboard maken. U kunt verschillende Dash boards hebben die verschillende gegevens weer geven en hiertussen scha kelen.

Als u een **beheerder** van de toepassing bent, kunt u Maxi maal 10 Dash boards op toepassings niveau maken om te delen met andere gebruikers van de toepassing. Alleen **beheerders** kunnen Dash boards op toepassings niveau maken, bewerken en verwijderen.  

## <a name="create-dashboard"></a>Dash board maken

In de volgende scherm afbeelding ziet u het dash board in een toepassing die is gemaakt op basis van de sjabloon voor **aangepaste toepassingen** . U kunt het standaard toepassings dashboard vervangen door een persoonlijk dash board of als u een beheerder bent, een dash board op toepassings niveau. Als u dit wilt doen, selecteert u **+ Nieuw** in de linkerbovenhoek van de pagina.

> [!div class="mx-imgBorder"]
> ![Dash board voor toepassingen op basis van de sjabloon ' aangepaste toepassing '](media/howto-create-personal-dashboards/dashboard-custom-app.png)

Als u **+ Nieuw** selecteert, wordt de dash board-editor geopend. In de editor kunt u uw dash board een naam geven en items uit de bibliotheek kiezen. De bibliotheek bevat de tegels en dashboard primitieven die u kunt gebruiken om het dash board aan te passen.

> [!div class="mx-imgBorder"]
> ![Dashboard bibliotheek](media/howto-create-personal-dashboards/dashboard-library.png)

Als u een **beheerder** van de toepassing bent, krijgt u de optie om een dash board op persoonlijk niveau of een dash board op toepassings niveau te maken. Als u een dash board op persoonlijk niveau maakt, kunt u dit alleen bekijken. Als u een dash board op toepassings niveau maakt, kan elke gebruiker van de toepassing dit bekijken. Nadat u een titel hebt ingevoerd en het type dash board hebt geselecteerd dat u wilt maken, kunt u later tegels opslaan en toevoegen. Of als u nu klaar bent en u een sjabloon en apparaatinstantie hebt toegevoegd, kunt u uw eerste tegel gaan maken.  

> [!div class="mx-imgBorder"]
> ![Formulier Details van apparaat configureren met Details voor de Tempe ratuur](media/howto-create-personal-dashboards/device-details.png)

U kunt bijvoorbeeld een **telemetrie** -tegel toevoegen voor de huidige Tempe ratuur van het apparaat. Dit doet u als volgt:

1. Een sjabloon voor een **apparaat** selecteren
1. Selecteer een apparaat in **apparaten** voor het apparaat dat u wilt weer geven op een dashboard tegel. Vervolgens ziet u een lijst met de eigenschappen van het apparaat die kunnen worden gebruikt op de tegel.
1. Als u de tegel op het dash board wilt maken, klikt u op **Tempe ratuur** en sleept u deze naar het dashboard gebied. U kunt ook op het selectie vakje naast **Tempe ratuur** klikken en vervolgens op **tegel toevoegen**klikken. Op de volgende scherm afbeelding ziet u hoe u een sjabloon en apparaat selecteert en vervolgens een temperatuur telemetrie-tegel op het dash board maakt.
1. Selecteer in de linkerbovenhoek op **Opslaan** om uw wijzigingen in het dash board op te slaan.

> [!div class="mx-imgBorder"]
> ![Het tabblad dash board met Details voor de temperatuur tegel](media/howto-create-personal-dashboards/temperature-tile-edit.png)

Wanneer u nu uw persoonlijke dash board bekijkt, ziet u de nieuwe tegel met de instelling voor de **Tempe ratuur** van het apparaat:

> [!div class="mx-imgBorder"]
> ![Het tabblad dash board met Details voor de temperatuur tegel](media/howto-create-personal-dashboards/temperature-tile-complete.png)

U kunt andere tegel typen in de bibliotheek verkennen om te ontdekken hoe u uw persoonlijke Dash boards verder moet aanpassen.

Zie [tegels toevoegen aan uw dash board](howto-add-tiles-to-your-dashboard.md)voor meer informatie over het gebruik van tegels in azure IOT Central.

## <a name="manage-dashboards"></a>Dash boards beheren

U kunt verschillende persoonlijke Dash boards hebben en hiertussen scha kelen of kiezen uit een van de standaard toepassings dashboards:

> [!div class="mx-imgBorder"]
> ![Scha kelen tussen Dash boards](media/howto-create-personal-dashboards/switch-dashboards.png)

U kunt uw persoonlijke Dash boards bewerken en alle Dash boards verwijderen die u niet meer nodig hebt. Als u een **beheerder**bent, kunt u ook Dash boards op toepassings niveau bewerken of verwijderen.

> [!div class="mx-imgBorder"]
> ![Dash boards verwijderen](media/howto-create-personal-dashboards/delete-dashboards.png)

## <a name="next-steps"></a>Volgende stappen

Nu u hebt geleerd hoe u persoonlijke Dash boards maakt en beheert, kunt u [meer informatie krijgen over het beheren van de voor keuren van uw toepassing](howto-manage-preferences.md).
