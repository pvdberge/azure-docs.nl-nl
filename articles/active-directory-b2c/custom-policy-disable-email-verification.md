---
title: E-mail verificatie uitschakelen tijdens het aanmelden van een klant met een aangepast beleid
titleSuffix: Azure AD B2C
description: Meer informatie over het uitschakelen van e-mail verificatie tijdens het aanmelden van een klant in Azure Active Directory B2C.
services: active-directory-b2c
author: msmimart
manager: celestedg
ms.service: active-directory
ms.workload: identity
ms.topic: how-to
ms.date: 03/11/2020
ms.author: mimart
ms.subservice: B2C
ms.openlocfilehash: 29426f8e3797c89deb712e89e0d972dd1ac8028e
ms.sourcegitcommit: 877491bd46921c11dd478bd25fc718ceee2dcc08
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/02/2020
ms.locfileid: "85389306"
---
# <a name="disable-email-verification-during-customer-sign-up-using-a-custom-policy-in-azure-active-directory-b2c"></a>E-mail verificatie uitschakelen tijdens de aanmelding van een klant met behulp van een aangepast beleid in Azure Active Directory B2C

[!INCLUDE [disable email verification intro](../../includes/active-directory-b2c-disable-email-verification.md)]

## <a name="prerequisites"></a>Vereisten

Voer de stappen in aan de [slag met aangepast beleid](custom-policy-get-started.md). U moet beschikken over een werkend aangepast beleid voor aanmelden en aanmelden met sociale en lokale accounts.

## <a name="add-the-metadata-to-the-self-asserted-technical-profile"></a>De meta gegevens toevoegen aan het zelf-bebevestigde technische profiel

Het technische profiel voor **LocalAccountSignUpWithLogonEmail** is een [zelfbevestigend](self-asserted-technical-profile.md), dat wordt aangeroepen tijdens de registratie stroom. Als u de e-mail verificatie wilt uitschakelen, stelt `EnforceEmailVerification` u de meta gegevens in op ONWAAR. Overschrijf de technische profielen van LocalAccountSignUpWithLogonEmail in het extensie bestand. 

1. Open het bestand extensies van uw beleid. Bijvoorbeeld <em>`SocialAndLocalAccounts/`**`TrustFrameworkExtensions.xml`**</em> .
1. Het `ClaimsProviders` element zoeken. Als het element niet bestaat, voegt u het toe.
1. Voeg de volgende claim provider toe aan het- `ClaimsProviders` element:

```xml
<ClaimsProvider>
  <DisplayName>Local Account</DisplayName>
  <TechnicalProfiles>
    <TechnicalProfile Id="LocalAccountSignUpWithLogonEmail">
      <Metadata>
        <Item Key="EnforceEmailVerification">false</Item>
      </Metadata>
    </TechnicalProfile>
  </TechnicalProfiles>
</ClaimsProvider>
```

## <a name="test-the-custom-policy"></a>Het aangepaste beleid testen

1. Meld u aan bij [Azure Portal](https://portal.azure.com).
2. Zorg ervoor dat u de map met uw Azure AD-Tenant gebruikt door het filter **Directory + abonnement** te selecteren in het bovenste menu en de map te kiezen die uw Azure AD-Tenant bevat.
3. Kies **alle services** in de linkerbovenhoek van de Azure Portal en zoek en selecteer **app-registraties**.
4. Selecteer een **Framework voor identiteits ervaring**.
5. Selecteer **aangepast beleid uploaden**en upload vervolgens de twee beleids bestanden die u hebt gewijzigd.
2. Selecteer het registratie-of aanmeldings beleid dat u hebt geüpload en klik op de knop **nu uitvoeren** .
3. U moet zich kunnen aanmelden met een e-mail adres zonder de validatie.


## <a name="next-steps"></a>Volgende stappen

- Meer informatie over het [zelf-beweringen technische profiel](self-asserted-technical-profile.md) vindt u in de IEF-verwijzing.
