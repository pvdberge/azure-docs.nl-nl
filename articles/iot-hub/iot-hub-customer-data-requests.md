---
title: Aanvragen voor klant gegevens voor Azure IoT Hub-apparaten
description: De meeste apparaten die worden beheerd in azure IoT Hub zijn niet persoonlijk, maar sommige zijn. Dit artikel spreekt over beheerders die persoonlijke gegevens kunnen exporteren of verwijderen van een apparaat.
author: robinsh
ms.author: robinsh
ms.date: 05/16/2018
ms.topic: conceptual
ms.service: iot-hub
services: iot-hub
ms.openlocfilehash: ebc73c75d9a23a53ac94f28208251dcff83e684a
ms.sourcegitcommit: 3fc3457b5a6d5773323237f6a06ccfb6955bfb2d
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/11/2020
ms.locfileid: "90030698"
---
# <a name="customer-data-request-features-for-azure-iot-hub-devices"></a>Functies van klant gegevens aanvragen voor Azure IoT Hub-apparaten

De Azure-IoT Hub is een op REST API gebaseerde Cloud service die is gericht op zakelijke klanten en die beveiligde, bidirectionele communicatie mogelijk maakt tussen miljoenen apparaten en een gepartitioneerde Azure-service.

[!INCLUDE [gdpr-related guidance](../../includes/gdpr-intro-sentence.md)]

Aan afzonderlijke apparaten wordt een apparaat-id (apparaat-ID) toegewezen door een Tenant beheerder. Apparaatgegevens zijn gebaseerd op de toegewezen apparaat-ID. Micro soft onderhoudt geen informatie en heeft geen toegang tot gegevens die apparaat-ID aan gebruikers correlatie toestaan.

Veel van de apparaten die worden beheerd in azure IoT Hub zijn geen persoonlijke apparaten, bijvoorbeeld een Office-Thermo staat of een Factory-robot. Klanten kunnen er echter voor zorgen dat sommige apparaten persoonlijk worden geïdentificeerd en kunnen hun eigen activa of inventaris tracking methoden voor het koppelen van apparaten aan individuen beschouwen. Met Azure IoT Hub worden alle gegevens die zijn gekoppeld aan apparaten, beheerd en opgeslagen alsof deze persoons gegevens zijn.

Tenant beheerders kunnen de Azure Portal of de REST Api's van de service gebruiken om informatie aanvragen uit te voeren door gegevens te exporteren of te verwijderen die zijn gekoppeld aan een apparaat-ID.

Als u de routerings functie van de Azure IoT Hub-service gebruikt om berichten van een apparaat door te sturen naar andere services, moeten gegevens aanvragen door de Tenant beheerder voor elk routerings eindpunt worden uitgevoerd om een volledige aanvraag voor een bepaald apparaat te volt ooien. Zie de referentie documentatie voor elk eind punt voor meer informatie. Zie [referentie-IOT hub-eind punten](iot-hub-devguide-endpoints.md)voor meer informatie over ondersteunde eind punten.

Als u de functie integratie Azure Event Grid van de Azure IoT Hub-service gebruikt, moeten gegevens aanvragen door de Tenant beheerder worden uitgevoerd voor elke abonnee van deze gebeurtenissen. Zie [reageren op IOT hub gebeurtenissen met behulp van Event grid](iot-hub-event-grid.md)voor meer informatie.

Als u de functie voor integratie van Azure Monitor van de Azure IoT Hub-service gebruikt om Diagnostische logboeken te maken, moeten gegevens aanvragen door de Tenant beheerder worden uitgevoerd op basis van de opgeslagen logboeken. Zie [de status van Azure IOT hub controleren](iot-hub-monitor-resource-health.md)voor meer informatie.

## <a name="deleting-customer-data"></a>Klant gegevens verwijderen

Tenant beheerders kunnen de Blade IoT-apparaten van de extensie Azure IoT Hub in de Azure Portal gebruiken om een apparaat te verwijderen, waarmee de gegevens die aan dat apparaat zijn gekoppeld, worden verwijderd.

Het is ook mogelijk om delete-bewerkingen uit te voeren voor apparaten met behulp van REST Api's. Zie voor meer informatie [service-apparaat verwijderen](/azure/iot-hub/iot-c-sdk-ref/iothub-registrymanager-h/iothubregistrymanager-deletedevice).

## <a name="exporting-customer-data"></a>Klant gegevens exporteren

Tenant beheerders kunnen kopiëren en plakken in het deel venster IoT-apparaten van de Azure IoT Hub-extensie in de Azure Portal voor het exporteren van gegevens die zijn gekoppeld aan een apparaat.

Het is ook mogelijk om export bewerkingen uit te voeren voor apparaten met behulp van REST-Api's. Zie [service-apparaat ophalen](/azure/iot-hub/iot-c-sdk-ref/iothub-registrymanager-h/iothubregistrymanager-getdevice)voor meer informatie.

> [!NOTE]
> Wanneer u de Enter prise-services van micro soft gebruikt, genereert micro soft bepaalde informatie, ook wel door het systeem gegenereerde logboeken. Sommige door Azure IoT Hub door het systeem gegenereerde logboeken zijn niet toegankelijk of kunnen niet worden geëxporteerd door Tenant beheerders. Deze logboeken vormen feitelijke acties die zijn uitgevoerd in de service en diagnostische gegevens met betrekking tot afzonderlijke apparaten.

## <a name="links-to-additional-documentation"></a>Koppelingen naar aanvullende documentatie

Volledige documentatie voor Azure IoT Hub service-Api's bevindt zich op [IOT hub service-api's](https://docs.microsoft.com/rest/api/iothub/service/configuration).
