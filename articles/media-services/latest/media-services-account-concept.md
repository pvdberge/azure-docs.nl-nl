---
title: Azure Media Services v3-accounts beheren | Microsoft Docs
description: Als u media-inhoud in azure wilt beheren, versleutelen, coderen, analyseren en streamen, moet u een Media Services-account maken. In dit artikel wordt uitgelegd hoe u Azure Media Services v3-accounts beheert.
services: media-services
documentationcenter: ''
author: IngridAtMicrosoft
manager: femila
editor: ''
ms.service: media-services
ms.workload: ''
ms.topic: conceptual
ms.date: 08/31/2020
ms.author: inhenkel
ms.openlocfilehash: 7c2cbaaf4866edc20f9745abe6759861db7834c3
ms.sourcegitcommit: 58d3b3314df4ba3cabd4d4a6016b22fa5264f05a
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/02/2020
ms.locfileid: "89291327"
---
# <a name="manage-azure-media-services-v3-accounts"></a>Azure Media Services v3-accounts beheren

[!INCLUDE [media services api v3 logo](./includes/v3-hr.md)]

Als u media-inhoud in azure wilt beheren, versleutelen, coderen, analyseren en streamen, moet u een Media Services-account maken. Als u een Media Services-account gaat maken, moet u de naam van een Azure Storage-accountresource opgeven. Het opgegeven opslagaccount wordt gekoppeld aan uw Media Services-account. Het Media Services-account en alle gekoppelde opslagaccounts moeten zich in hetzelfde Azure-abonnement bevinden. Zie [opslag accounts](storage-account-concept.md)voor meer informatie.

## <a name="moving-a-media-services-account-between-subscriptions"></a>Een Media Services account verplaatsen tussen abonnementen 

Als u een Media Services account naar een nieuw abonnement wilt verplaatsen, moet u eerst de hele resource groep met het Media Services account naar het nieuwe abonnement verplaatsen. U moet alle gekoppelde resources verplaatsen: Azure Storage accounts, Azure CDN profielen, enzovoort. Zie [resources verplaatsen naar een nieuwe resource groep of een nieuw abonnement](../../azure-resource-manager/management/move-resource-group-and-subscription.md)voor meer informatie. Net als bij resources in azure kan het enige tijd duren om de resource groep te verplaatsen.

> [!NOTE]
> Media Services v3 ondersteunt het multi-pacht-model.

### <a name="considerations"></a>Overwegingen

* Maak back-ups van alle gegevens in uw account voordat u migreert naar een ander abonnement.
* U moet alle streaming-eind punten en live streaming-resources stoppen. Uw gebruikers hebben geen toegang tot uw inhoud voor de duur van het verplaatsen van de resource groep. 

> [!IMPORTANT]
> Start het streaming-eind punt niet voordat de verplaatsing is voltooid.

### <a name="troubleshoot"></a>Problemen oplossen 

Als een Media Services account of een gekoppeld Azure Storage account wordt ' losgekoppeld ' nadat de resource groep is verplaatst, roteert u de sleutels van het opslag account. Als door het draaien van de sleutels van het opslag account de status ' verbinding verbroken ' van het Media Services account niet wordt opgelost, wordt er een nieuwe ondersteunings aanvraag in het menu ' ondersteuning en probleem oplossing ' in het Media Services account opgeslagen.  

## <a name="next-steps"></a>Volgende stappen

[Een account maken](./create-account-howto.md)
