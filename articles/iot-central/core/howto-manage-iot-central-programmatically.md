---
title: IoT Central programmatisch beheren | Microsoft Docs
description: In dit artikel wordt beschreven hoe u IoT Central via een programma maakt en beheert. U kunt de toepassing weer geven, wijzigen en verwijderen met meerdere taal-Sdk's zoals Java script, Python, C#, Ruby en go.
services: iot-central
ms.service: iot-central
author: dominicbetts
ms.author: dobett
ms.date: 05/19/2020
ms.topic: how-to
ms.openlocfilehash: ba0ee0a610299bbe6b7e550f204cd2fd50d6d71a
ms.sourcegitcommit: 877491bd46921c11dd478bd25fc718ceee2dcc08
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/02/2020
ms.locfileid: "83749205"
---
# <a name="manage-iot-central-programmatically"></a>IoT Central programmatisch beheren

[!INCLUDE [iot-central-selector-manage](../../../includes/iot-central-selector-manage.md)]

In plaats van IoT Central-toepassingen te maken en te beheren op de website van [azure IOT Central Application Manager](https://aka.ms/iotcentral) , kunt u uw toepassingen programmatisch beheren met de Azure sdk's. Ondersteunde talen zijn Java script, Python, C#, Ruby en go.

## <a name="install-the-sdk"></a>De SDK installeren

De volgende tabel geeft een lijst van de SDK-opslag plaatsen en pakket installatie opdrachten:

| SDK-opslag plaats | Pakket installeren |
| -------------- | ------------ |
| [Azure IotCentralClient SDK voor Java script](https://github.com/Azure/azure-sdk-for-js/tree/master/sdk/iotcentral/arm-iotcentral) | `npm install @azure/arm-iotcentral` |
| [Microsoft Azure SDK voor python](https://github.com/Azure/azure-sdk-for-python/tree/master/sdk/iothub/azure-mgmt-iotcentral/azure/mgmt/iotcentral) | `pip install azure-mgmt-iotcentral` |
| [Azure-SDK voor .NET](https://github.com/Azure/azure-sdk-for-net/tree/master/sdk/iotcentral/Microsoft.Azure.Management.IotCentral) | `dotnet add package Microsoft.Azure.Management.IotCentral` |
| [Microsoft Azure SDK voor ruby-Resource Management (preview-versie)](https://github.com/Azure/azure-sdk-for-ruby/tree/master/management/azure_mgmt_iot_central/lib/2018-09-01/generated/azure_mgmt_iot_central) | `gem install azure_mgmt_iot_central` |
| [Azure SDK voor Java](https://github.com/Azure/azure-sdk-for-java/tree/master/sdk/iotcentral) | [Maven-pakket](https://search.maven.org/search?q=a:azure-mgmt-iotcentral) |
| [Azure SDK voor Go](https://github.com/Azure/azure-sdk-for-go/tree/master/services/iotcentral/mgmt/2018-09-01/iotcentral) | [Pakket versies](https://github.com/Azure/azure-sdk-for-go/releases) |

## <a name="samples"></a>Voorbeelden

De [azure IOT Central arm-SDK voor beelden](https://docs.microsoft.com/samples/azure-samples/azure-iot-central-arm-sdk-samples/azure-iot-central-arm-sdk-samples/) bevat code voorbeelden voor meerdere programmeer talen die laten zien hoe u Azure IOT Central-toepassingen kunt maken, bijwerken, weer geven en verwijderen.

## <a name="next-steps"></a>Volgende stappen

Nu u hebt geleerd hoe u Azure IoT Central-toepassingen programmatisch kunt beheren, is een voorgestelde volgende stap meer informatie over de [Azure Resource Manager](../../azure-resource-manager/management/overview.md) -service.
