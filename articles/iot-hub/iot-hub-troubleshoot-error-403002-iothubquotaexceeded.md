---
title: Problemen met Azure IoT Hub-fout 403002 IoTHubQuotaExceeded
description: Meer informatie over het oplossen van fout 403002 IoTHubQuotaExceeded
author: jlian
manager: briz
ms.service: iot-hub
services: iot-hub
ms.topic: troubleshooting
ms.date: 01/30/2020
ms.author: jlian
ms.openlocfilehash: 8312c3267e826088f34b3bffe1520703eec00bdc
ms.sourcegitcommit: 877491bd46921c11dd478bd25fc718ceee2dcc08
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/02/2020
ms.locfileid: "76961112"
---
# <a name="403002-iothubquotaexceeded"></a>403002 IoTHubQuotaExceeded

In dit artikel worden de oorzaken en oplossingen voor **403002 IoTHubQuotaExceeded** -fouten beschreven.

## <a name="symptoms"></a>Symptomen

Alle aanvragen voor IoT Hub mislukken met de fout **403002 IoTHubQuotaExceeded**. In Azure Portal wordt de apparaten lijst van de IoT hub niet geladen.

## <a name="cause"></a>Oorzaak

Het dagelijkse bericht quotum voor de IoT-hub is overschreden. 

## <a name="solution"></a>Oplossing

Voer [een upgrade uit of verg root het aantal eenheden op de IOT-hub](iot-hub-upgrade.md) of wacht op de volgende UTC-dag voor het dagelijks quotum dat moet worden vernieuwd.

## <a name="next-steps"></a>Volgende stappen

* Zie [inzicht IOT hub prijzen](iot-hub-devguide-pricing.md#charges-per-operation) voor meer informatie over hoe bewerkingen worden geteld voor het quotum, zoals dubbele query's en directe methoden.
* Als u bewaking voor dagelijks quotum gebruik wilt instellen, stelt u een waarschuwing in met het metrische *aantal gebruikte berichten*. Zie [metrische gegevens en waarschuwingen instellen met IOT hub](tutorial-use-metrics-and-diags.md#set-up-metrics) voor stapsgewijze instructies