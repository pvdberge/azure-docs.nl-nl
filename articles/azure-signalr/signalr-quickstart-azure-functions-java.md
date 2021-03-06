---
title: Java gebruiken om een chatruimte met Azure Functions en SignalR Service te maken
description: Een quickstart waarin u leert hoe u de service Azure SignalR en Azure Functions gebruikt om een chatruimte te maken.
author: sffamily
ms.service: signalr
ms.devlang: java
ms.topic: quickstart
ms.date: 03/04/2019
ms.author: zhshang
ms.custom: devx-track-java
ms.openlocfilehash: 544f200e749b1b125e8077ee65f20a06779fb13d
ms.sourcegitcommit: 8a7b82de18d8cba5c2cec078bc921da783a4710e
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/28/2020
ms.locfileid: "89050570"
---
# <a name="quickstart-use-java-to-create-a-chat-room-with-azure-functions-and-signalr-service"></a>Quickstart: Java gebruiken om een chatruimte met Azure Functions en SignalR Service te maken

Met Azure SignalR Service kunt u eenvoudig realtime functionaliteit toevoegen aan uw toepassing en Azure Functions is een serverloos platform waarmee u uw code kunt uitvoeren zonder een infrastructuur te beheren. In deze quickstart gebruikt u Java om een serverloze, realtime chattoepassing te bouwen die gebruikmaakt van SignalR Service en Functions.

## <a name="prerequisites"></a>Vereisten

- Een code-editor zoals [Visual Studio Code](https://code.visualstudio.com/)
- Een Azure-account met een actief abonnement. [Gratis een account maken](https://azure.microsoft.com/free/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio)
- [Azure Functions Core Tools](https://github.com/Azure/azure-functions-core-tools#installing). Wordt gebruikt om Azure Function-apps lokaal uit te voeren.

   > [!NOTE]
   > De vereiste SignalR Service-bindingen in Java worden alleen ondersteund in Azure Function Core Tools versie 2.4.419 (hostversie 2.0.12332) of hoger.

   > [!NOTE]
   > [.NET Core SDK](https://www.microsoft.com/net/download) moet zijn geïnstalleerd voor Azure Functions Core Tools om de extensies te installeren. Er is echter geen kennis van .NET vereist om JavaScript Azure-functie-apps te bouwen.

- [Java Developer Kit](https://www.azul.com/downloads/zulu/), versie 8
- [Apache Maven](https://maven.apache.org), versie 3.0 of hoger

> [!NOTE]
> Deze quickstart kan worden uitgevoerd op macOS, Windows of Linux.

[Ondervindt u problemen? Laat het ons weten.](https://aka.ms/asrs/qsjava)

## <a name="log-in-to-azure"></a>Meld u aan bij Azure.

Meld u met uw Azure-account aan bij Azure Portal op <https://portal.azure.com/>.

[Ondervindt u problemen? Laat het ons weten.](https://aka.ms/asrs/qsjava)

[!INCLUDE [Create instance](includes/signalr-quickstart-create-instance.md)]

[Ondervindt u problemen? Laat het ons weten.](https://aka.ms/asrs/qsjava)

[!INCLUDE [Clone application](includes/signalr-quickstart-clone-application.md)]

[Ondervindt u problemen? Laat het ons weten.](https://aka.ms/asrs/qsjava)

## <a name="configure-and-run-the-azure-function-app"></a>De Azure-functie-app configureren en uitvoeren

1. Controleer in de browser waarin de Azure-portal is geopend, of het service-exemplaar van SignalR dat u eerder hebt geïmplementeerd, is gemaakt. Hiervoor typt u de naam van het exemplaar in het zoekvak boven in de portal. Selecteer het exemplaar om het te openen.

    ![Het service-exemplaar van SignalR zoeken](media/signalr-quickstart-azure-functions-csharp/signalr-quickstart-search-instance.png)

1. Selecteer **Sleutels** om de verbindingsreeksen voor het service-exemplaar van SignalR weer te geven.

1. Selecteer en kopieer de primaire verbindingsreeks.

    ![De service SignalR maken](media/signalr-quickstart-azure-functions-javascript/signalr-quickstart-keys.png)

1. Open in de code-editor de map *src/chat/java* in de gekloonde opslagplaats.

1. Wijzig de naam *local.settings.sample.json* in *local.settings.json*.

1. Plak in **local.settings.json** de verbindingsreeks in de waarde van de instelling **AzureSignalRConnectionString**. Sla het bestand op.

1. Het hoofdbestand dat de functies bevat, staat in *src/chat/java/src/main/java/com/function/Functions.java*:

    - **negotiate**: gebruikt de invoerbinding *SignalRConnectionInfo* om geldige verbindingsgegevens te genereren en te retourneren.
    - **sendMessage**: ontvangt een chatbericht in de aanvraagbody en gebruikt de uitvoerbinding *SignalR* om het bericht uit te zenden naar alle verbonden clienttoepassingen.

1. Zorg ervoor dat u zich in de terminal in de map *src/chat/java* bevindt. Bouw de functie-app.

    ```bash
    mvn clean package
    ```

1. Voer de functie-app lokaal uit.

    ```bash
    mvn azure-functions:run
    ```
[Ondervindt u problemen? Laat het ons weten.](https://aka.ms/asrs/qsjava)

[!INCLUDE [Run web application](includes/signalr-quickstart-run-web-application.md)]

[Ondervindt u problemen? Laat het ons weten.](https://aka.ms/asrs/qsjava)

[!INCLUDE [Cleanup](includes/signalr-quickstart-cleanup.md)]

[Ondervindt u problemen? Laat het ons weten.](https://aka.ms/asrs/qsjava)

## <a name="next-steps"></a>Volgende stappen

In deze quickstart hebt u een serverloze, realtime toepassing gebouwd en uitgevoerd met behulp van Maven. Hierna leert u hoe u volledig nieuwe Java Azure Functions maakt.

> [!div class="nextstepaction"]
> [Uw eerste functie maken met Java en Maven](../azure-functions/functions-create-first-java-maven.md)

[Ondervindt u problemen? Laat het ons weten.](https://aka.ms/asrs/qsjava)
