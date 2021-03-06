---
title: Uw resource hiërarchie beveiligen-Azure governance
description: Meer informatie over het beveiligen van uw resource hiërarchie met hiërarchie-instellingen, zoals het instellen van de standaard beheer groep.
ms.date: 09/02/2020
ms.topic: conceptual
ms.openlocfilehash: 19d699b54a9979df1030c0f6e294d5a4492f2853
ms.sourcegitcommit: 4feb198becb7a6ff9e6b42be9185e07539022f17
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/04/2020
ms.locfileid: "89469776"
---
# <a name="how-to-protect-your-resource-hierarchy"></a>Uw resource hiërarchie beveiligen

Uw resources, resource groepen, abonnementen, beheer groepen en Tenant vormen samen de resource hiërarchie. Instellingen in de hoofd beheer groep, zoals aangepaste Azure-rollen of Azure Policy-beleids toewijzingen, kunnen van invloed zijn op elke resource in de resource hiërarchie. Het is belang rijk om de resource hiërarchie te beschermen tegen wijzigingen die een negatieve invloed kunnen hebben op alle resources.

Beheer groepen hebben nu hiërarchie-instellingen waarmee de Tenant beheerder dit gedrag kan beheren. In dit artikel worden alle beschik bare hiërarchie-instellingen beschreven en wordt uitgelegd hoe u deze kunt instellen.

## <a name="rbac-permissions-for-hierarchy-settings"></a>RBAC-machtigingen voor hiërarchie-instellingen

Voor het configureren van een van de hiërarchie-instellingen zijn de volgende twee RBAC-bewerkingen vereist voor de hoofd beheer groep:

- `Microsoft.Management/managementgroups/settings/write`
- `Microsoft.Management/managementgroups/settings/read`

Met deze bewerkingen kan een gebruiker de hiërarchie-instellingen niet lezen en bijwerken. De bewerkingen bieden geen andere toegang tot de hiërarchie van de beheer groep of resources in de hiërarchie. Beide bewerkingen zijn beschikbaar in de beheerder van de ingebouwde rol hiërarchie- **instellingen**van Azure.

## <a name="setting---default-management-group"></a>Instelling: standaard beheer groep

Een nieuw abonnement dat in een Tenant wordt toegevoegd, wordt standaard toegevoegd als lid van de hoofd beheer groep. Als beleids toewijzingen, op rollen gebaseerd toegangs beheer (RBAC) en andere governance-constructies zijn toegewezen aan de hoofd beheer groep, hebben ze direct invloed op deze nieuwe abonnementen. Daarom passen veel organisaties deze constructs niet toe aan de hoofd beheer groep, zelfs als dat wel de gewenste plaats is om ze toe te wijzen. In andere gevallen is een meer beperkende set besturings elementen gewenst voor nieuwe abonnementen, maar niet aan alle abonnementen. Deze instelling ondersteunt beide use-cases.

Door toe te staan dat de standaard beheer groep voor nieuwe abonnementen kan worden gedefinieerd, kunnen bedrijfsbrede governance-constructies worden toegepast in de hoofd beheer groep en een afzonderlijke beheer groep met beleids toewijzingen of Azure-roltoewijzingen die geschikter zijn voor een nieuw abonnement, kan worden gedefinieerd.

### <a name="set-default-management-group-in-portal"></a>Standaard beheer groep instellen in Portal

Voer de volgende stappen uit om deze instelling te configureren in Azure Portal:

1. Gebruik de zoek balk om beheer groepen te zoeken en te selecteren.

1. Selecteer in de hoofd beheer groep de optie **Details** naast de naam van de beheer groep.

1. Selecteer onder **instellingen**de optie **hiërarchie-instellingen**.

1. Selecteer de knop **standaard beheer groep wijzigen** .

   > [!NOTE]
   > Als de knop **standaard beheer groep wijzigen** is uitgeschakeld, is de beheer groep die wordt weer gegeven, niet de hoofd beheer groep of uw beveiligingsprincipal heeft niet de benodigde machtigingen om de hiërarchie-instellingen te wijzigen.

1. Selecteer een beheer groep in uw hiërarchie en gebruik de knop **selecteren** .

### <a name="set-default-management-group-with-rest-api"></a>Standaard beheer groep instellen met REST API

Als u deze instelling wilt configureren met REST API, wordt het eind punt van de [hiërarchie-instellingen](/rest/api/resources/hierarchysettings) aangeroepen. Gebruik hiervoor de volgende REST API URI en de indeling van de hoofd tekst. Vervang door `{rootMgID}` de id van uw hoofd beheer groep en `{defaultGroupID}` met de id van de beheer groep om de standaard beheer groep te worden:

- REST API-URI

  ```http
  PUT https://management.azure.com/providers/Microsoft.Management/managementGroups/{rootMgID}/settings/default?api-version=2020-02-01
  ```

- Aanvraagtekst

  ```json
  {
      "properties": {
          "defaultManagementGroup": "/providers/Microsoft.Management/managementGroups/{defaultGroupID}"
      }
  }
  ```

Gebruik hetzelfde eind punt en stel **defaultManagementGroup** in op een waarde van om de standaard beheer groep weer in te stellen op de hoofd beheer groep `/providers/Microsoft.Management/managementGroups/{rootMgID}` .

## <a name="setting---require-authorization"></a>Instelling: autorisatie vereisen

Elke gebruiker kan standaard nieuwe beheer groepen maken binnen een Tenant. Beheerders van een Tenant kunnen deze machtigingen alleen aanbieden aan specifieke gebruikers om consistentie en overeenstemming in de beheer groeps hiërarchie te behouden. Als deze functie is ingeschakeld, moet de gebruiker de `Microsoft.Management/managementGroups/write` bewerking in de hoofd beheer groep uitvoeren om nieuwe onderliggende beheer groepen te maken.

### <a name="set-require-authorization-in-portal"></a>Instellen dat autorisatie is vereist in de portal

Voer de volgende stappen uit om deze instelling te configureren in Azure Portal:

1. Gebruik de zoek balk om beheer groepen te zoeken en te selecteren.

1. Selecteer in de hoofd beheer groep de optie **Details** naast de naam van de beheer groep.

1. Selecteer onder **instellingen**de optie **hiërarchie-instellingen**.

1. Scha kelen tussen **machtigingen vereisen voor het maken van nieuwe beheer groepen.** optie aan aan.

   > [!NOTE]
   > Als de **machtigingen vereisen voor het maken van nieuwe beheer groepen.** Wissel knop is uitgeschakeld. de beheer groep die wordt weer gegeven, is niet de hoofd beheer groep of uw beveiligingsprincipal beschikt niet over de benodigde machtigingen om de hiërarchie-instellingen te wijzigen.

### <a name="set-require-authorization-with-rest-api"></a>Instellen vereisen autorisatie met REST API

Als u deze instelling wilt configureren met REST API, wordt het eind punt van de [hiërarchie-instellingen](/rest/api/resources/hierarchysettings) aangeroepen. Gebruik hiervoor de volgende REST API URI en de indeling van de hoofd tekst. Deze waarde is een _Boolean_, dus geef **waar** of **Onwaar** op voor de waarde. Met de waarde **True** wordt deze methode voor het beveiligen van uw beheer groeps hiërarchie ingeschakeld:

- REST API-URI

  ```http
  PUT https://management.azure.com/providers/Microsoft.Management/managementGroups/{rootMgID}/settings/default?api-version=2020-02-01
  ```

- Aanvraagtekst

  ```json
  {
      "properties": {
          "requireAuthorizationForGroupCreation": true
      }
  }
  ```

Als u de instelling wilt uitschakelen, gebruikt u hetzelfde eind punt en stelt u **requireAuthorizationForGroupCreation** in op de waarde **False**.

## <a name="next-steps"></a>Volgende stappen

Voor meer informatie over beheergroepen gaat u naar:

- [Beheergroepen maken om Azure-resources te ordenen](../create.md)
- [Uw beheergroepen wijzigen, verwijderen of beheren](../manage.md)
