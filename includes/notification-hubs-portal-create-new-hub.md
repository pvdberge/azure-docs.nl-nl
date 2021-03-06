---
title: bestand opnemen
description: bestand opnemen
services: notification-hubs
author: jwargo
ms.service: notification-hubs
ms.topic: include
ms.date: 01/17/2019
ms.author: jowargo
ms.custom: include file
ms.openlocfilehash: 5afcc8e4524a0e8353766ba239d5ab9161b29d86
ms.sourcegitcommit: 62717591c3ab871365a783b7221851758f4ec9a4
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/22/2020
ms.locfileid: "67509081"
---
1. Meld u aan bij de [Azure-portal](https://portal.azure.com).

1. Selecteer **Alle services** in het menu aan de linkerkant en selecteer **Notification Hubs** in de sectie **Mobiel**. Selecteer het sterpictogram naast de servicenaam om de service toe te voegen aan de sectie **FAVORIETEN** in het menu aan de linkerkant. Nadat u **Notification Hubs** hebt toegevoegd aan **FAVORIETEN**, selecteert u dit in het linkermenu.

      ![Azure Portal - Notification Hubs selecteren](./media/notification-hubs-portal-create-new-hub/all-services-select-notification-hubs.png)

1. Op de **Notification Hubs**-pagina selecteert u **Toevoegen** op de werkbalk.

      ![Toevoegen van Notification Hubs - knop op de werkbalk](./media/notification-hubs-portal-create-new-hub/add-toolbar-button.png)

1. Voer op de pagina **Notification Hub** de volgende stappen uit:

    1. Voer een naam in **Notification Hub** in.  

    1. Voer een naam in **Een nieuwe naamruimte maken** in. Een naamruimte bevat een of meer hubs.

    1. Selecteer een waarde in de vervolgkeuzelijst **Locatie**. Deze waarde specificeert de locatie waar u de hub wilt maken.

    1. Selecteer een bestaande resourcegroep in **Resourcegroep** of maak een naam voor een nieuwe resourcegroep.

    1. Selecteer **Maken**.

        ![Azure Portal - eigenschappen van de Notification Hub instellen](./media/notification-hubs-portal-create-new-hub/notification-hubs-azure-portal-settings.png)

1. Selecteer **Meldingen** (het belpictogram) en selecteer vervolgens **Ga naar resource**. U kunt ook de lijst op de pagina **Notification Hubs** vernieuwen en uw hub selecteren.

      ![Azure Portal - Meldingen -> Naar de resource gaan](./media/notification-hubs-portal-create-new-hub/go-to-notification-hub.png)

1. Selecteer **Toegangsbeleid** in de lijst. U ziet dat de twee verbindingsreeksen voor u beschikbaar zijn. Later moet u er pushmeldingen mee afhandelen.

      >[!IMPORTANT]
      >Gebruik *niet* het beleid **DefaultFullSharedAccessSignature** in uw toepassing. Deze mag alleen in uw back-end worden gebruikt.
      >

      ![Azure Portal - verbindingsreeksen voor de Notification Hub](./media/notification-hubs-portal-create-new-hub/notification-hubs-connection-strings-portal.png)
