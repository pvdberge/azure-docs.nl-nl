---
title: Uw omgeving instellen voor de operator blauw drukken
description: Meer informatie over het configureren van uw Azure-omgeving voor gebruik met de blauw druk-operator Azure ingebouwde rol.
ms.date: 08/27/2020
ms.topic: how-to
ms.openlocfilehash: ef911553b4985a6497fb397a1ae405387c6539fb
ms.sourcegitcommit: 8a7b82de18d8cba5c2cec078bc921da783a4710e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/28/2020
ms.locfileid: "89051454"
---
# <a name="configure-your-environment-for-a-blueprint-operator"></a>Uw omgeving configureren voor een Blueprint Operator

Het beheer van uw blauw druk-definities en blauw druk-toewijzingen kunnen worden toegewezen aan verschillende teams. Het is gebruikelijk dat een architect of governance-team verantwoordelijk is voor het levenscyclus beheer van uw blauw drukken definities terwijl een operationeel team verantwoordelijk is voor het beheren van toewijzingen van deze centraal beheerde blauw drukken.

Het ingebouwde op rollen gebaseerde toegangs beheer (RBAC) van de **operator blauw** drukken is speciaal ontworpen voor gebruik in dit type scenario. Met deze rol kunnen teams van bewerkingen type de toewijzing van de definities van de blauw druk van de organisaties beheren, maar niet de mogelijkheid om deze te wijzigen. Hiervoor moet u een configuratie in uw Azure-omgeving hebben en in dit artikel worden de stappen beschreven die nodig zijn.

## <a name="grant-permission-to-the-blueprint-operator"></a>Toestemming geven voor de blauw druk-operator

De eerste stap is het verlenen van de rol van de **blauw druk-operator** aan het account of de beveiligings groep (aanbevolen) die aan blauw drukken gaat toewijzen. Deze actie moet worden uitgevoerd op het hoogste niveau in de hiërarchie van de beheer groep, die alle beheer groepen en abonnementen omvat die het operationele team toegang moet geven tot een blauw druk toewijzen. Het is raadzaam om het principe van minimale bevoegdheden te volgen bij het verlenen van deze machtigingen.

1. Aanbevelingen [Een beveiligings groep maken en leden toevoegen](../../../active-directory/fundamentals/active-directory-groups-create-azure-portal.md)

1. [Een roltoewijzing](../../../role-based-access-control/role-assignments-portal.md#add-a-role-assignment) van de **operator voor blauw** drukken toevoegen aan het account of de beveiligings groep

## <a name="user-assign-managed-identity"></a>Door gebruiker beheerde identiteit toewijzen

Een definitie van een blauw druk kan door het systeem toegewezen of door de gebruiker toegewezen beheerde identiteiten gebruiken. Bij gebruik van de functie van de **blauw druk-operator** moet de definitie van de blauw druk echter worden geconfigureerd voor gebruik van een door de gebruiker toegewezen beheerde identiteit. Daarnaast moet aan het account of de beveiligings groep die de functie van de **blauw druk-operator** wordt verleend, de rol **Managed Identity-operator** worden verleend voor de door de gebruiker toegewezen beheerde identiteit. Zonder deze machtiging mislukken de opdrachten voor blauw drukken vanwege onvoldoende machtigingen.

1. [Een door de gebruiker toegewezen beheerde identiteit maken](../../../active-directory/managed-identities-azure-resources/how-to-manage-ua-identity-portal.md#create-a-user-assigned-managed-identity) voor gebruik door een toegewezen blauw druk

1. [Voeg een roltoewijzing](../../../role-based-access-control/role-assignments-portal.md#add-a-role-assignment) van de **operator Managed Identity** toe aan het account of de beveiligings groep. Bereik de roltoewijzing aan de nieuwe door de gebruiker toegewezen beheerde identiteit.

1. Wijs als de **blauw druk-operator** [een blauw druk toe](../create-blueprint-portal.md#assign-a-blueprint) die gebruikmaakt van de nieuwe door de gebruiker toegewezen beheerde identiteit.

## <a name="next-steps"></a>Volgende stappen

- Meer informatie over de [levenscyclus van een blauwdruk](../concepts/lifecycle.md).
- Meer informatie over hoe u [statische en dynamische parameters](../concepts/parameters.md) gebruikt.
- Meer informatie over hoe u de [blauwdrukvolgorde](../concepts/sequencing-order.md) aanpast.
- Meer informatie over hoe u gebruikmaakt van [resourcevergrendeling in blauwdrukken](../concepts/resource-locking.md).
- Problemen oplossen tijdens de toewijzing van een blauwdruk met [algemene probleemoplossing](../troubleshoot/general.md).