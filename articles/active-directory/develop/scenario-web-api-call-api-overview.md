---
title: Een web-API bouwen die web-Api's aanroept-micro soft Identity-platform | Azure
description: Meer informatie over het bouwen van een web-API die downstream Web-Api's (overzicht) aanroept.
services: active-directory
author: jmprieur
manager: CelesteDG
ms.service: active-directory
ms.subservice: develop
ms.topic: conceptual
ms.workload: identity
ms.date: 05/07/2019
ms.author: jmprieur
ms.custom: aaddev, identityplatformtop40
ms.openlocfilehash: 88a0177755fbd913bdaaf0ecf3e12c62dee294c1
ms.sourcegitcommit: 877491bd46921c11dd478bd25fc718ceee2dcc08
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/02/2020
ms.locfileid: "80885069"
---
# <a name="scenario-a-web-api-that-calls-web-apis"></a>Scenario: een web-API die web-Api's aanroept

Meer informatie over wat u moet weten om een web-API te maken die web-Api's aanroept.

## <a name="prerequisites"></a>Vereisten

In dit scenario, waarin een beveiligde web-API Web-Api's aanroept, bouwt u op het scenario ' een web-API beveiligen '. Zie [scenario: Protected Web API](scenario-protected-web-api-overview.md)(Engelstalig) voor meer informatie over dit scenario.

## <a name="overview"></a>Overzicht

- Een web-, Desktop-, mobiele of toepassing met één pagina (niet weer gegeven in het bijbehorende diagram) roept een beveiligde web-API aan en biedt een JSON Web Token (JWT) Bearer-token in de HTTP-header autorisatie.
- De beveiligde web-API valideert het token en maakt gebruik van de methode micro soft Authentication Library (MSAL) `AcquireTokenOnBehalfOf` om een andere token van Azure Active Directory (Azure AD) aan te vragen, zodat de beveiligde web-API een tweede Web-API of downstream Web-API kan aanroepen namens de gebruiker.
- De beveiligde web-API kan later ook aanroepen `AcquireTokenSilent` om tokens voor andere downstream-api's namens dezelfde gebruiker aan te vragen. `AcquireTokenSilent`Hiermee wordt het token vernieuwd wanneer dit nodig is.

![Diagram van een web-API die een web-API aanroept](media/scenarios/web-api.svg)

## <a name="specifics"></a>Opsporingsgegevens

Het app-registratie onderdeel dat is gerelateerd aan API-machtigingen is klassiek. De configuratie van de app omvat het gebruik van de OAuth 2,0-stroom om het JWT Bearer-token uit te wisselen op basis van een token voor een downstream API. Dit token wordt toegevoegd aan de token cache, waar deze beschikbaar is in de controller van de Web-API, en kan vervolgens een token op de achtergrond verkrijgen om downstream-Api's aan te roepen.

## <a name="next-steps"></a>Volgende stappen

> [!div class="nextstepaction"]
> [App-registratie](scenario-web-api-call-api-app-registration.md)
