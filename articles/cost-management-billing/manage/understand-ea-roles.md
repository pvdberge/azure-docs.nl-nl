---
title: Inzicht in beheerdersrollen voor Enterprise in Azure
description: Meer informatie over zakelijke beheerdersrollen in Azure. U kunt vijf afzonderlijke beheerdersrollen toewijzen.
author: bandersmsft
ms.reviewer: adwise
ms.service: cost-management-billing
ms.subservice: enterprise
ms.topic: conceptual
ms.date: 09/03/2020
ms.author: banders
ms.openlocfilehash: 564acd6d6072a4308141942666cc0ebcc0ad0136
ms.sourcegitcommit: bf1340bb706cf31bb002128e272b8322f37d53dd
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/03/2020
ms.locfileid: "89433514"
---
# <a name="managing-azure-enterprise-roles"></a>Azure Enterprise-rollen beheren

Voor het beheren van het gebruik en de uitgaven van uw organisatie kunnen Azure-klanten met een Enterprise Agreement (EA) vijf beheerdersrollen toewijzen:

- Zakelijke beheerder
- Zakelijke beheerder (alleen lezen)<sup>1</sup>
- Afdelingsbeheerder
- Afdelingsbeheerder (alleen lezen)
- Eigenaar van account<sup>2</sup>

<sup>1</sup> Deze rol omvat de Factuurcontact van het EA-contract.

<sup>2</sup> Factuurcontact kan niet worden toegevoegd of gewijzigd in de Azure EA-portal, en wordt toegevoegd aan de EA-inschrijving op basis van de gebruiker die op overeenkomstniveau is ingesteld als de Factuurcontact. Als u de Factuurcontact wilt wijzigen, moet u via een partner-/softwareadviseur een aanvraag indienen bij het ROC (Regional Operations Center).

De eerste inschrijvingsbeheerder die wordt ingesteld tijdens het inrichten van de inschrijving, bepaalt het verificatietype van het de factuurcontactaccount. Wanneer de factuurcontact als alleen-lezen-beheerder wordt toegevoegd aan de EA Portal wordt Microsoft-accountverificatie verleend. 

Als het initiële verificatietype bijvoorbeeld is ingesteld op Gemengd, wordt de EA als een Microsoft-account toegevoegd en krijgt de factuurcontact alleen-lezen EA-beheerdersbevoegdheden. Als de EA-beheerder de Microsoft-accountautorisatie voor een bestaand factuurcontact niet goedkeurt, kan de EA-beheerder de betreffende gebruiker verwijderen en de klant vragen de gebruiker weer toe te voegen als een alleen-lezen beheerder met een werk- of schoolaccount dat alleen is ingesteld op inschrijvingsniveau in de EA-portal.

Deze rollen zijn specifiek voor het beheren van Azure Enterprise Agreements en zijn een aanvulling op de ingebouwde rollen waarover Azure beschikt om toegang tot resources te beheren. Zie [Ingebouwde rollen in Azure](../../role-based-access-control/built-in-roles.md) voor meer informatie.

In de volgende secties worden de beperkingen en mogelijkheden van elke rol beschreven.

## <a name="user-limit-for-admin-roles"></a>Gebruikerslimiet voor beheerdersrollen

|Rol| Gebruikerslimiet|
|---|---|
|Zakelijke beheerder|Onbeperkt|
|Zakelijke beheerder (alleen lezen)|Onbeperkt|
|Afdelingsbeheerder|Onbeperkt|
|Afdelingsbeheerder (alleen lezen)|Onbeperkt|
|Accounteigenaar|1 per account<sup>3</sup>|

<sup>3</sup> Voor elk account is een uniek Microsoft-account of werk- of schoolaccount vereist.

## <a name="organization-structure-and-permissions-by-role"></a>De organisatiestructuur en machtigingen per rol

|Taken| Zakelijke beheerder|Zakelijke beheerder (alleen lezen)|Afdelingsbeheerder|Afdelingsbeheerder (alleen lezen)|Accounteigenaar| Partner|
|---|---|---|---|---|---|---|
|Zakelijke beheerders weergeven|✔|✔|✘|✘|✘|✔|
|Zakelijke beheerders toevoegen of verwijderen|✔|✘|✘|✘|✘|✘|
|Contactpersonen voor meldingen weergeven<sup>4</sup> |✔|✔|✘|✘|✘|✔|
|Contactpersonen voor meldingen toevoegen of verwijderen<sup>4</sup> |✔|✘|✘|✘|✘|✘|
|Afdelingen maken en beheren |✔|✘|✘|✘|✘|✘|
|Afdelingsbeheerders weergeven|✔|✔|✔|✔|✘|✔|
|Afdelingsbeheerders toevoegen of verwijderen|✔|✘|✔|✘|✘|✘|
|Accounts in de inschrijving weergeven |✔|✔|✔<sup>5</sup>|✔<sup>5</sup>|✘|✔|
|Accounts aan de inschrijving toevoegen en de accounteigenaar wijzigen|✔|✘|✔<sup>5</sup>|✘|✘|✘|
|Abonnementen en abonnementsmachtigingen maken en beheren|✘|✘|✘|✘|✔|✘|

- <sup>4</sup> Contactpersonen voor meldingen ontvangen e-mailberichten over de Azure Enterprise Agreement.
- <sup>5</sup> Taak is beperkt tot accounts in uw afdeling.

## <a name="add-a-new-enterprise-administrator"></a>Een nieuwe ondernemingsbeheerder toevoegen

Ondernemingsbeheerders beschikken over de meeste bevoegdheden voor het beheren van een Azure EA-inschrijving. De eerste Azure EA-beheerder is gemaakt toen de EA-overeenkomst is gesloten. U kunt echter op elk moment nieuwe beheerders toevoegen of verwijderen. Nieuwe beheerders kunnen alleen worden toegevoegd door bestaande beheerders. Zie [Een andere ondernemingsbeheerder maken](ea-portal-get-started.md#create-another-enterprise-administrator) voor meer informatie over het toevoegen van ondernemingsbeheerders. Zie [Rollen en taken voor factureringsprofiel ](understand-mca-roles.md#billing-profile-roles-and-tasks) voor meer informatie over de rollen en taken voor het factureringsprofiel.

## <a name="update-account-owner-state-from-pending-to-active"></a>De status van een accounteigenaar bijwerken van in behandeling naar actief

Wanneer nieuwe accounteigenaren (AO) voor de eerste keer worden toegevoegd aan een Azure EA-inschrijving, krijgen ze de status _In behandeling_. Zodra een nieuwe accounteigenaar de welkomstmail voor de activering ontvangt, kan deze zich aanmelden om het account te activeren. Zodra het account wordt geactiveerd, wordt de accountstatus bijgewerkt van _In behandeling_ naar _Actief_. De accounteigenaar moet het waarschuwingsbericht lezen en **Doorgaan** selecteren. Nieuwe gebruikers worden mogelijk gevraagd hun voor- en achternaam op te geven om een Commerce-account te maken. Als dat het geval is, moeten ze de vereiste informatie toevoegen om door te gaan, waarna het account wordt geactiveerd.

## <a name="add-a-department-admin"></a>Een afdelingsbeheerder toevoegen

Nadat een Azure EA-beheerder een afdeling heeft gemaakt, kan de Azure Enterprise-beheerder afdelingsbeheerders toevoegen en deze koppelen aan een afdeling. Een afdelingsbeheerder kan nieuwe accounts maken. Nieuwe accounts zijn nodig om nieuwe Azure EA-abonnementen te maken.

Raadpleeg [Een Azure EA-afdelingsbeheerder](ea-portal-get-started.md#add-a-department-administrator) maken voor meer informatie over het toevoegen van een afdelingsbeheerder.

## <a name="usage-and-costs-access-by-role"></a>Toegang tot gebruik en kosten per rol

|Taken| Zakelijke beheerder|Zakelijke beheerder (alleen lezen)|Afdelingsbeheerder|Afdelingsbeheerder (alleen lezen) |Accounteigenaar| Partner|
|---|---|---|---|---|---|---|
|Tegoedsaldo weergeven, inclusief Azure-vooruitbetaling|✔|✔|✘|✘|✘|✔|
|Bestedingsquotum van afdeling weergeven|✔|✔|✘|✘|✘|✔|
|Bestedingsquotum van afdeling instellen|✔|✘|✘|✘|✘|✘|
|Het EA-prijzenoverzicht van de organisatie weergeven|✔|✔|✘|✘|✘|✔|
|Details over gebruik en kosten weergeven|✔|✔|✔<sup>6</sup>|✔<sup>6</sup>|✔<sup>7</sup>|✔|
|Resources beheren in Azure Portal|✘|✘|✘|✘|✔|✘|

- <sup>6</sup> Hiervoor is vereist dat de ondernemingsbeheerder het beleid **DA-weergavekosten** inschakelt in de Enterprise Portal. De afdelingsbeheerder kan vervolgens gedetailleerde kosten voor de afdeling bekijken.
- <sup>7</sup> Hiervoor is vereist dat de ondernemingsbeheerder het beleid **AO-weergavekosten** inschakelt in de Enterprise Portal. De accounteigenaar kan vervolgens gedetailleerde kosten voor het account zien.

## <a name="see-pricing-for-different-user-roles"></a>Prijzen voor verschillende gebruikersrollen bekijken

Mogelijk ziet u verschillende prijzen in Azure Portal, afhankelijk van uw beheerdersrol en de manier waarop de beleidsregels voor weergavekosten zijn ingesteld door de zakelijke beheerder. De twee beleidsregels in de zakelijke portal die invloed hebben op de prijzen die u in Azure Portal ziet, zijn:

- DA-weergavekosten
- AO-weergavekosten

Zie [Toegang tot factureringsgegevens beheren voor Azure](manage-billing-access.md) voor informatie over de manier waarop u deze beleidsregels instelt.

In de volgende tabel ziet u de relatie tussen de Enterprise Agreement-beheerdersrollen, het weergavekostenbeleid, de Azure-rol in de Azure-portal en de prijzen die u ziet in de Azure-portal. De zakelijke beheerder ziet altijd gebruiksgegevens op basis van de EA-prijzen van de organisatie. De afdelingsbeheerder en de accounteigenaar zien echter verschillende prijsweergaven op basis van het weergavekostenbeleid en hun Azure-rol. De afdelingsbeheerdersrol die in de volgende tabel wordt vermeld, verwijst naar zowel de rol van afdelingsbeheerder als de rol van afdelingsbeheerder (alleen lezen).

|Enterprise Agreement-beheerdersrol|Weergavekostenbeleid voor rol|Azure-rol|Prijsweergave|
|---|---|---|---|
|Accounteigenaar of afdelingsbeheerder|✔ Ingeschakeld|Eigenaar|EA-prijzen van de organisatie|
|Accounteigenaar of afdelingsbeheerder|✘ Uitgeschakeld|Eigenaar|Retailprijzen|
|Accounteigenaar of afdelingsbeheerder|✔ Ingeschakeld |geen|Geen prijzen|
|Accounteigenaar of afdelingsbeheerder|✘ Uitgeschakeld |geen|Geen prijzen|
|Geen|Niet van toepassing |Eigenaar|Retailprijzen|

U stelt de zakelijke beheerdersrol en beleidsregels voor weergavekosten in via de zakelijke portal. De Azure-rol kan worden bijgewerkt in de Azure-portal. Zie [Toegang beheren met op rollen gebaseerd toegangsbeheer en Azure Portal](../../role-based-access-control/role-assignments-portal.md) voor meer informatie.



## <a name="next-steps"></a>Volgende stappen

- [Toegang tot factureringsgegevens beheren voor Azure](manage-billing-access.md)
- [Toegang beheren met op rollen gebaseerd toegangsbeheer en Azure Portal](../../role-based-access-control/role-assignments-portal.md)
- [Ingebouwde Azure-rollen](../../role-based-access-control/built-in-roles.md)
