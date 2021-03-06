---
title: Problemen met gegevens versleuteling oplossen-Azure Database for PostgreSQL-één server
description: Meer informatie over het oplossen van problemen met de gegevens versleuteling op uw Azure Database for PostgreSQL-één server
author: kummanish
ms.author: manishku
ms.service: postgresql
ms.topic: how-to
ms.date: 02/13/2020
ms.openlocfilehash: ee0a1ebe483dd4719fd1a84fec37906329116eba
ms.sourcegitcommit: d7008edadc9993df960817ad4c5521efa69ffa9f
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/08/2020
ms.locfileid: "86117896"
---
# <a name="troubleshoot-data-encryption-in-azure-database-for-postgresql---single-server"></a>Problemen met gegevens versleuteling oplossen in Azure Database for PostgreSQL-één server

Dit artikel helpt u bij het identificeren en oplossen van veelvoorkomende problemen die zich kunnen voordoen in de implementatie met één server van Azure Database for PostgreSQL wanneer deze is geconfigureerd met een door de klant beheerde sleutel.

## <a name="introduction"></a>Introductie

Wanneer u gegevens versleuteling configureert voor het gebruik van een door de klant beheerde sleutel in Azure Key Vault, moet de server voortdurende toegang tot de sleutel hebben. Als de server de toegang tot de door de klant beheerde sleutel in Azure Key Vault kwijtraakt, worden alle verbindingen geweigerd, wordt het juiste fout bericht weer gegeven en wordt de status gewijzigd in niet ***toegankelijk*** in de Azure Portal.

Als u een ontoegankelijke Azure Database for PostgreSQL server niet meer nodig hebt, kunt u deze verwijderen om kosten te besparen. Er zijn geen andere acties op de server toegestaan totdat toegang tot de sleutel kluis is hersteld en de server beschikbaar is. Het is ook niet mogelijk om de gegevens versleutelings optie van (door de `Yes` klant beheerd) te wijzigen in `No` (door service beheerd) op een niet-toegankelijke server wanneer deze is versleuteld met een door de klant beheerde sleutel. U moet de sleutel hand matig opnieuw valideren voordat de server weer toegankelijk is. Deze actie is nodig om de gegevens te beveiligen tegen onbevoegde toegang terwijl machtigingen voor de door de klant beheerde sleutel worden ingetrokken.

## <a name="common-errors-causing-server-to-become-inaccessible"></a>Veelvoorkomende fouten waardoor de server niet meer toegankelijk is

De volgende onjuiste configuraties veroorzaken de meeste problemen met gegevens versleuteling die gebruikmaakt van Azure Key Vault sleutels:

- De sleutel kluis is niet beschikbaar of bestaat niet:
  - De sleutel kluis is per ongeluk verwijderd.
  - Een onregelmatige netwerk fout zorgt ervoor dat de sleutel kluis niet beschikbaar is.

- U hebt geen machtigingen voor toegang tot de sleutel kluis of de sleutel bestaat niet:
  - De sleutel is verlopen of per ongeluk verwijderd of uitgeschakeld.
- De beheerde identiteit van het Azure Database for PostgreSQL exemplaar is per ongeluk verwijderd.
  - De beheerde identiteit van het Azure Database for PostgreSQL-exemplaar heeft onvoldoende sleutel machtigingen. De machtigingen bevatten bijvoorbeeld Get, wrap en Unwrap.
  - De beheerde identiteits machtigingen voor het Azure Database for PostgreSQL-exemplaar zijn ingetrokken of verwijderd.

## <a name="identify-and-resolve-common-errors"></a>Veelvoorkomende fouten identificeren en oplossen

### <a name="errors-on-the-key-vault"></a>Fouten in de sleutel kluis

#### <a name="disabled-key-vault"></a>Uitgeschakelde sleutel kluis

- `AzureKeyVaultKeyDisabledMessage`
- **Uitleg**: de bewerking kan niet worden voltooid op de server omdat de Azure Key Vault sleutel is uitgeschakeld.

#### <a name="missing-key-vault-permissions"></a>Ontbrekende sleutel kluis machtigingen

- `AzureKeyVaultMissingPermissionsMessage`
- **Uitleg**: de vereiste Get-, wrap-en Unwrap-machtigingen voor de server kunnen niet worden Azure Key Vault. Ken de ontbrekende machtigingen toe aan de service-principal met de ID.

### <a name="mitigation"></a>Oplossing

- Controleer of de door de klant beheerde sleutel aanwezig is in de sleutel kluis.
- Zoek de sleutel kluis en ga vervolgens naar de sleutel kluis in de Azure Portal.
- Zorg ervoor dat de sleutel-URI een sleutel identificeert die aanwezig is.

## <a name="next-steps"></a>Volgende stappen

[Gebruik de Azure Portal om gegevens versleuteling in te stellen met een door de klant beheerde sleutel op Azure Database for PostgreSQL](howto-data-encryption-portal.md)
