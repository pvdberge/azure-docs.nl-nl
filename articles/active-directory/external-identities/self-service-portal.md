---
title: Self-service-aanmeldings portal voor B2B-samen werking-Azure AD
description: Azure Active Directory B2B-samenwerking ondersteunt uw externe bedrijfsrelaties door zakelijke partners selectief toegang te verlenen tot uw zakelijke toepassingen
services: active-directory
ms.service: active-directory
ms.subservice: B2B
ms.topic: conceptual
ms.date: 02/12/2020
ms.author: mimart
author: msmimart
manager: celestedg
ms.reviewer: mal
ms.collection: M365-identity-device-management
ms.openlocfilehash: ff18d3d9cae6e887abbd9fb1845de62386062b2b
ms.sourcegitcommit: 4e5560887b8f10539d7564eedaff4316adb27e2c
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/06/2020
ms.locfileid: "87908517"
---
# <a name="self-service-for-azure-ad-b2b-collaboration-sign-up"></a>Self-service voor Azure AD B2B-samenwerkings aanmelding

Klanten kunnen veel doen met de ingebouwde functies die via de [Azure-portal](https://portal.azure.com) en het [Toepassingstoegangsvenster](https://myapps.microsoft.com) beschikbaar worden gesteld voor eindgebruikers. Het kan echter nodig zijn om de onboarding-workflow voor B2B-gebruikers aan te passen aan de behoeften van uw organisatie.

## <a name="azure-ad-entitlement-management-for-b2b-guest-user-sign-up"></a>Azure AD-rechts beheer voor B2B gast gebruikers registratie

Als uitnodigende organisatie weet u mogelijk niet vooraf dat de afzonderlijke externe deel nemers toegang tot uw resources nodig hebben. U hebt een manier nodig waarmee gebruikers van partner bedrijven zich kunnen aanmelden met beleids regels die u beheert. Als u gebruikers van andere organisaties in staat wilt stellen om toegang aan te vragen, en op basis van de goed keuring is ingericht met gast accounts en toegewezen aan groepen, apps en share point online-sites, kunt u het [beheer van rechten van Azure AD](https://docs.microsoft.com/azure/active-directory/governance/entitlement-management-overview) gebruiken voor het configureren van beleids regels waarmee de [toegang voor externe gebruikers wordt beheerd](https://docs.microsoft.com/azure/active-directory/governance/entitlement-management-external-users#how-access-works-for-external-users).

## <a name="azure-active-directory-b2b-invitation-api"></a>Azure Active Directory-API voor B2B-uitnodiging

Organisaties kunnen de [API voor Microsoft Graph uitnodigingen](https://docs.microsoft.com/graph/api/resources/invitation?view=graph-rest-1.0) gebruiken om hun eigen voorbereidings ervaring te bouwen voor B2B-gast gebruikers. Wanneer u de aanmelding van selfservice voor B2B-gast gebruikers wilt aanbieden, kunt u het beste [Azure AD-beheer](https://docs.microsoft.com/azure/active-directory/governance/entitlement-management-overview)gebruiken. Maar als u uw eigen ervaring wilt maken, kunt u de API voor het maken van een [uitnodiging](https://docs.microsoft.com/graph/api/invitation-post?view=graph-rest-1.0&tabs=http) gebruiken om uw aangepaste uitnodigings-e-mail automatisch rechtstreeks naar de B2B-gebruiker te verzenden. Of uw app kan gebruikmaken van de inviteRedeemUrl die is geretourneerd in de reactie van het maken van uw eigen uitnodiging (via uw communicatie mechanisme) voor de uitgenodigde gebruiker.

## <a name="next-steps"></a>Volgende stappen

* [Wat is Azure AD B2B-samenwerking?](what-is-b2b.md)
* [Licentie voor Azure AD B2B-samenwerking](licensing-guidance.md)
* [Veelgestelde vragen over Azure Active Directory B2B-samenwerking](faq.md)
