---
title: Verkeer naar multi tenant-apps beheren via de portal
titleSuffix: Azure Application Gateway
description: Dit artikel bevat richt lijnen voor het configureren van Azure-app service-Web-apps als leden in back-end-pool op een bestaande of nieuwe toepassings gateway.
services: application-gateway
author: abshamsft
ms.service: application-gateway
ms.topic: how-to
ms.date: 06/09/2020
ms.author: absha
ms.openlocfilehash: dbaad0f6639d65d88da6847886d3aa3d39b93e82
ms.sourcegitcommit: 6e1124fc25c3ddb3053b482b0ed33900f46464b3
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/15/2020
ms.locfileid: "90563750"
---
# <a name="configure-app-service-with-application-gateway"></a>App Service configureren met Application Gateway

Omdat app service een multi tenant-service is in plaats van een exclusief gebruik, gebruikt deze host-header in de inkomende aanvraag om de aanvraag om te zetten in het juiste app service-eind punt. Normaal gesp roken is de DNS-naam van de toepassing, die op zijn beurt de DNS-naam die is gekoppeld aan de toepassings gateway voor de app service, afwijkt van de domein naam van de back-end-app service. Daarom is de host-header in de oorspronkelijke aanvraag die wordt ontvangen door de toepassings gateway niet hetzelfde als de hostnaam van de back-end-service. Als gevolg hiervan, tenzij de host-header in de aanvraag van de toepassings gateway naar de back-end is gewijzigd in de hostnaam van de back-end-service, kunnen de back-endservers van meerdere tenants de aanvraag niet omzetten naar het juiste eind punt.

Application Gateway biedt een switch die wordt aangeroepen `Pick host name from backend address` en die de host-header in de aanvraag overschrijft met de hostnaam van de back-end wanneer de aanvraag wordt doorgestuurd van de Application Gateway naar de back-end. Deze mogelijkheid biedt ondersteuning voor back-ends met meerdere tenants, zoals Azure app service en API management. 

In dit artikel leert u het volgende:

- Een back-end-pool maken en hieraan een App Service toevoegen
- HTTP-instellingen en aangepaste test maken met de Schakel opties hostname kiezen ingeschakeld

## <a name="prerequisites"></a>Vereisten

- Application Gateway: als u geen bestaande toepassings gateway hebt, raadpleegt u [een toepassings gateway maken](https://docs.microsoft.com/azure/application-gateway/quick-create-portal)
- App service: als u geen bestaande app service hebt, raadpleegt u [app service-documentatie](https://docs.microsoft.com/azure/app-service/).

## <a name="add-app-service-as-backend-pool"></a>App service toevoegen als back-end-groep

1. Open in de Azure Portal de configuratie weergave van de Application Gateway.

2. Klik onder **back-end-Pools**op **toevoegen** om een nieuwe back-end-groep te maken.

3. Geef een geschikte naam op voor de back-end-groep. 

4. Klik onder **doelen**op de vervolg keuzelijst en kies **app Services** als optie.

5. Een vervolg keuzelijst direct onder de vervolg keuzelijst **doel**  wordt weer gegeven, die een lijst met uw app Services bevat. Kies in deze vervolg keuzelijst de App Service die u wilt toevoegen als lid van een back-end-groep en klik op toevoegen.

   ![App service-back-end](./media/configure-web-app-portal/backendpool.png)
   
   > [!NOTE]
   > In de vervolg keuzelijst worden alleen de app-Services ingevuld die zich in hetzelfde abonnement bevinden als uw Application Gateway. Als u een app-service wilt gebruiken die zich in een ander abonnement bevindt dan de versie waarin de Application Gateway is, kiest u in plaats van **app Services** in de vervolg keuzelijst **doel** de optie **IP-adres of hostnaam** en voert u de hostnaam (voor beeld in. azurewebsites.net) van de app service.

## <a name="create-http-settings-for-app-service"></a>HTTP-instellingen voor app service maken

1. Klik onder **http-instellingen**op **toevoegen** om een nieuwe http-instelling te maken.

2. Voer een naam in voor de HTTP-instelling en u kunt op cookie gebaseerd affiniteit op basis van uw vereisten in-of uitschakelen.

3. Kies het protocol als HTTP of HTTPS volgens uw use-case. 

   > [!NOTE]
   > Als u HTTPS selecteert, hoeft u geen verificatie certificaat of vertrouwd basis certificaat te uploaden om de app service-back-end toe te staan omdat de app service een vertrouwde Azure-service is.

4. Schakel het selectie vakje in voor het **gebruik van app service** . Houd er rekening mee dat de switches  `Create a probe with pick host name from backend address` `Pick host name from backend address` automatisch worden ingeschakeld.`Pick host name from backend address` overschrijft de host-header in de aanvraag met de hostnaam van de back-end wanneer de aanvraag wordt doorgestuurd van de Application Gateway naar de back-end.  

   `Create a probe with pick host name from backend address` maakt automatisch een status test en koppelt deze aan deze HTTP-instelling. U hoeft geen andere Health probe voor deze HTTP-instelling te maken. U kunt controleren of er een nieuwe test met de naam <HTTP Setting name> <Unique GUID> is toegevoegd aan de lijst met status controles en dat deze al de switch heeft `Pick host name from backend http settings enabled` .

   Als u al een of meer HTTP-instellingen hebt die worden gebruikt voor app service en als deze HTTP-instellingen hetzelfde protocol gebruiken als de protocollen die u maakt, wordt in plaats van de `Create a probe with pick host name from backend address` Switch een vervolg keuzelijst weer geven om een van de aangepaste tests te selecteren. Dit komt doordat er al een HTTP-instelling met app service bestaat, dus er zou ook een status test met de switch bestaan `Pick host name from backend http settings enabled` . Kies die aangepaste test in de vervolg keuzelijst.

5. Klik op **OK** om de http-instelling te maken.

   ![Scherm afbeelding toont het instellingen deel venster H T/m P toevoegen met gebruik voor app service en OK geselecteerd.](./media/configure-web-app-portal/http-setting1.png)

   ![Scherm afbeelding toont een status test met de naam van de back-endserver voor het kiezen van een host http-instellingen.](./media/configure-web-app-portal/http-setting2.png)



## <a name="create-rule-to-tie-the-listener-backend-pool-and-http-setting"></a>Regel maken om de listener, back-end-pool en HTTP-instelling te koppelen

1. Klik onder **regels**op **Basic** om een nieuwe basis regel te maken.

2. Geef een geschikte naam op en selecteer de listener waarmee de binnenkomende aanvragen voor de app service worden geaccepteerd.

3. Kies in de vervolg keuzelijst **back-endadresgroep** de back-end-groep die u hierboven hebt gemaakt.

4. Kies in de vervolg keuzelijst **http-instelling** de http-instelling die u hierboven hebt gemaakt.

5. Klik op **OK** om deze regel op te slaan.

   ![Scherm afbeelding toont het deel venster basis regel toevoegen met listener, back-end-pool en H T T P-instelling gemarkeerd.](./media/configure-web-app-portal/rule.png)

## <a name="additional-configuration-in-case-of-redirection-to-app-services-relative-path"></a>Aanvullende configuratie in het geval van omleiding naar het relatieve pad van de app service

Wanneer de app service een omleidings reactie naar de client verzendt om om te leiden naar het relatieve pad (bijvoorbeeld een omleiding van contoso.azurewebsites.net/path1 naar contoso.azurewebsites.net/path2), wordt dezelfde hostnaam gebruikt in de locatie header van de reactie van de toepassing in de aanvraag die is ontvangen van de toepassings gateway. De client gaat de aanvraag dus rechtstreeks naar contoso.azurewebsites.net/path2 in plaats van de Application Gateway (contoso.com/path2). Het overs laan van de toepassings gateway is niet gewenst.

Als u in uw gebruiks voorbeeld scenario's hebt waarbij de app service een omleidings antwoord naar de client moet verzenden, voert [u de extra stappen uit om de locatie header te herschrijven](https://docs.microsoft.com/azure/application-gateway/troubleshoot-app-service-redirection-app-service-url#sample-configuration).

## <a name="restrict-access"></a>Toegang beperken

In de web-apps die in deze voor beelden zijn geïmplementeerd, worden open bare IP-adressen gebruikt die rechtstreeks via internet toegankelijk zijn. Dit helpt bij het oplossen van problemen met een nieuwe functie en nieuwe dingen. Maar als u van plan bent een functie in productie te implementeren, wilt u meer beperkingen toevoegen.

Een manier om de toegang tot uw web-apps te beperken, is door [Azure app service statische IP-beperkingen](../app-service/app-service-ip-restrictions.md)te gebruiken. Zo kunt u de Web-App zodanig beperken dat alleen verkeer van de toepassings gateway wordt ontvangen. Gebruik de functie IP-beperking van app service om de Application Gateway-VIP weer te geven als het enige adres met Access.

## <a name="next-steps"></a>Volgende stappen

Zie [ondersteuning voor multi tenant-Services met toepassings gateway](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-app-overview)voor meer informatie over de app service en andere ondersteuning voor meerdere tenants met Application Gateway.
