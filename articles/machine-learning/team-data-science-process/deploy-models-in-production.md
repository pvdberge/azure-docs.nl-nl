---
title: Modellen implementeren in productie-team data Science process
description: Modellen implementeren in productie, zodat ze een actieve rol kunnen spelen bij het nemen van zakelijke beslissingen.
author: marktab
manager: marktab
editor: marktab
ms.service: machine-learning
ms.subservice: team-data-science-process
ms.topic: article
ms.date: 01/10/2020
ms.author: tdsp
ms.custom: seodec18, previous-author=deguhath, previous-ms.author=deguhath
ms.openlocfilehash: e3e2ef3340ca836f56176c21cf3d221f0bf172b9
ms.sourcegitcommit: 877491bd46921c11dd478bd25fc718ceee2dcc08
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/02/2020
ms.locfileid: "76722234"
---
# <a name="deploy-models-to-production-to-play-an-active-role-in-making-business-decisions"></a>Modellen implementeren voor productie om een actieve rol te spelen bij het nemen van zakelijke beslissingen

Bij de productie-implementatie kan een model een actieve rol spelen in een bedrijf. Voor spellingen van een geïmplementeerd model kunnen worden gebruikt voor zakelijke beslissingen.

## <a name="production-platforms"></a>Productie platforms

Er zijn verschillende benaderingen en platformen om modellen in productie te brengen. Hier volgen enkele opties:

- [Het implementeren van modellen met Azure Machine Learning](../how-to-deploy-and-where.md)
- [Implementatie van een model in SQL-Server](https://docs.microsoft.com/sql/advanced-analytics/tutorials/sqldev-py6-operationalize-the-model)
- [Microsoft Machine Learning-server](https://docs.microsoft.com/sql/advanced-analytics/r/r-server-standalone)

>[!NOTE]
>Voorafgaand aan de implementatie moet u er zeker van zijn dat de latentie van de model Score laag genoeg is voor gebruik in de productie omgeving.
>

>[!NOTE]
>Zie [Deploy a Azure machine learning web service](../studio/deploy-a-machine-learning-web-service.md)(Engelstalig) voor implementatie met behulp van Azure machine learning Studio.
>

## <a name="ab-testing"></a>A/B testen

Wanneer er meerdere modellen in productie zijn, kan [een/B-test](https://en.wikipedia.org/wiki/A/B_testing) worden gebruikt om de prestaties van het model te vergelijken. 
 
## <a name="next-steps"></a>Volgende stappen

Er zijn ook instructies voor het leveren van alle stappen in het proces voor **specifieke scenario's** . Ze worden weer gegeven en gekoppeld aan miniatuur beschrijvingen in het artikel [voorbeeld scenario's](walkthroughs.md) . Ze illustreren het combi neren van Cloud, on-premises hulpprogram ma's en services in een werk stroom of pijp lijn om een intelligente toepassing te maken. 
