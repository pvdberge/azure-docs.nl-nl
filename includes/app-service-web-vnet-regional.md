---
author: ccompy
ms.service: app-service-web
ms.topic: include
ms.date: 06/08/2020
ms.author: ccompy
ms.openlocfilehash: 926a1867a77b543057fa1de170cdb64ccfefe7cb
ms.sourcegitcommit: ec682dcc0a67eabe4bfe242fce4a7019f0a8c405
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/09/2020
ms.locfileid: "86218073"
---
Door gebruik te maken van regionale VNet-integratie kan uw app toegang tot:

* Resources in een VNet in dezelfde regio als uw app.
* Resources in VNets die zijn gekoppeld aan het VNet waarin uw app is geïntegreerd.
* Beveiligde services voor service-eind punten.
* Bronnen in azure ExpressRoute-verbindingen.
* Resources in het VNet waarmee u bent geïntegreerd.
* Bronnen tussen peered verbindingen, waaronder Azure ExpressRoute-verbindingen.
* Privé-eindpunten 

Wanneer u VNet-integratie met VNets in dezelfde regio gebruikt, kunt u de volgende Azure-netwerk functies gebruiken:

* **Netwerk beveiligings groepen (nsg's)**: u kunt uitgaand verkeer blok keren met een NSG die op uw integratie subnet is geplaatst. De regels voor binnenkomende verbindingen zijn niet van toepassing omdat u VNet-integratie niet kunt gebruiken om inkomende toegang tot uw app te bieden.
* **Route tabellen (udr's)**: u kunt een route tabel plaatsen op het subnet met integratie om uitgaand verkeer te verzenden naar de gewenste locatie.

Standaard stuurt uw app alleen RFC1918-verkeer naar uw VNet. Als u al het uitgaande verkeer wilt door sturen naar uw VNet, past u de app-instelling WEBSITE_VNET_ROUTE_ALL toe op uw app. De app-instelling configureren:

1. Ga naar de **configuratie** gebruikersinterface in de app-Portal. Selecteer **Nieuwe toepassingsinstelling**.
1. Voer **WEBSITE_VNET_ROUTE_ALL** in het vak **naam** in en voer **1** in het vak **waarde** in.

   ![Toepassings instelling opgeven][4]

1. Selecteer **OK**.
1. Selecteer **Opslaan**.

Als u al het uitgaande verkeer naar uw VNet routert, is het onderhevig aan de Nsg's en Udr's die worden toegepast op het integratie subnet. Wanneer u al het uitgaande verkeer naar uw VNet routert, zijn uw uitgaande adressen nog steeds de uitgaande adressen die worden vermeld in de app-eigenschappen, tenzij u routes opgeeft om het verkeer elders te verzenden.

Er zijn enkele beperkingen bij het gebruik van VNet-integratie met VNets in dezelfde regio:

* U kunt geen resources bereiken via globale peering-verbindingen.
* De functie is alleen beschikbaar vanuit nieuwere Azure App Service schaal eenheden die ondersteuning bieden voor PremiumV2 App Service-plannen. Houd er rekening mee dat *uw app niet moet worden uitgevoerd op een PremiumV2 prijs categorie*, alleen dat deze moet worden uitgevoerd op een app service plan waarbij de optie PremiumV2 beschikbaar is (wat impliceert dat het een nieuwere schaal eenheid is waar deze VNet-integratie functie vervolgens ook beschikbaar is).
* Het integratie subnet kan slechts door één App Service schema worden gebruikt.
* De functie kan niet worden gebruikt door toepassingen van het geïsoleerde abonnement in een App Service Environment.
* Voor de functie is een ongebruikt subnet met een/27 met 32-adressen of groter vereist in een Azure Resource Manager VNet.
* De app en het VNet moeten zich in dezelfde regio bevinden.
* U kunt een VNet met een geïntegreerde app niet verwijderen. Verwijder de integratie voordat u het VNet verwijdert.
* U kunt alleen integreren met VNets in hetzelfde abonnement als de app.
* U kunt slechts één regionale VNet-integratie per App Service plan hebben. Meerdere apps in hetzelfde App Service-abonnement kunnen hetzelfde VNet gebruiken.
* U kunt het abonnement van een app of een abonnement niet wijzigen terwijl er een app is die gebruikmaakt van regionale VNet-integratie.
* Uw app kan geen adressen omzetten in Azure DNS Private Zones zonder configuratie wijzigingen

Er wordt één adres gebruikt voor elk exemplaar van het abonnement. Als u uw app schaalt naar vijf instanties, worden er vijf adressen gebruikt. Aangezien de grootte van het subnet niet kan worden gewijzigd na toewijzing, moet u een subnet gebruiken dat groot genoeg is om te kunnen voldoen aan de schaal van uw app. Een/26 met 64-adressen is de aanbevolen grootte. Een/26 met 64-adressen is geschikt voor een Premium-abonnement met 30 exemplaren. Wanneer u een plan omhoog of omlaag schaalt, hebt u twee keer zoveel adressen nodig voor een korte periode.

Als u wilt dat uw apps in een ander abonnement een VNet bereiken dat al is verbonden met apps in een ander abonnement, selecteert u een ander subnet dan het subnetwerk dat wordt gebruikt door de bestaande VNet-integratie.

De functie wordt volledig ondersteund voor Windows-en Linux-web-apps. Alle gedragingen handelen hetzelfde tussen Windows-apps en Linux-apps.

### <a name="service-endpoints"></a>Service-eindpunten

Met regionale VNet-integratie kunt u service-eind punten gebruiken. Als u service-eind punten wilt gebruiken in combi natie met uw app, gebruikt u de regionale VNet-integratie om verbinding te maken met een geselecteerd VNet en configureert u vervolgens service-eind punten met de doel service op het subnet dat u voor de integratie hebt gebruikt. Als u vervolgens een service wilt openen via service-eind punten:

1. regionale VNet-integratie met uw web-app configureren
1. Ga naar de doel service en configureer service-eind punten op het subnet dat wordt gebruikt voor de integratie

### <a name="network-security-groups"></a>Netwerkbeveiligingsgroepen

U kunt netwerk beveiligings groepen gebruiken om binnenkomend en uitgaand verkeer naar resources in een VNet te blok keren. Een app die gebruikmaakt van regionale VNet-integratie kan een [netwerk beveiligings groep][VNETnsg] gebruiken om uitgaand verkeer naar resources in uw VNet of Internet te blok keren. Als u verkeer naar open bare adressen wilt blok keren, moet u de toepassings instelling WEBSITE_VNET_ROUTE_ALL instellen op 1. De binnenkomende regels in een NSG zijn niet van toepassing op uw app, omdat de VNet-integratie alleen van invloed is op uitgaand verkeer van uw app.

Als u inkomend verkeer naar uw app wilt beheren, gebruikt u de functie toegangs beperkingen. Een NSG die wordt toegepast op uw integratie subnet, is van kracht, ongeacht eventuele routes die worden toegepast op het integratie subnet. Als WEBSITE_VNET_ROUTE_ALL is ingesteld op 1 en u geen routes hebt die van invloed zijn op het open bare adres verkeer op het subnet met integratie, is al uw uitgaand verkeer nog steeds afhankelijk van Nsg's die zijn toegewezen aan uw integratie subnet. Als WEBSITE_VNET_ROUTE_ALL niet is ingesteld, worden Nsg's alleen toegepast op RFC1918-verkeer.

### <a name="routes"></a>Routes

U kunt route tabellen gebruiken om uitgaand verkeer van uw app naar de gewenste locatie te routeren. Routerings tabellen zijn standaard alleen van invloed op uw RFC1918-doel verkeer. Als u WEBSITE_VNET_ROUTE_ALL op 1 instelt, worden al uw uitgaande oproepen beïnvloed. Routes die zijn ingesteld op het integratie subnet, zijn niet van invloed op antwoorden op aanvragen voor inkomende apps. Algemene doelen kunnen Firewall apparaten of gateways zijn.

Als u al het uitgaande verkeer on-premises wilt routeren, kunt u een route tabel gebruiken om al het uitgaande verkeer naar uw ExpressRoute-gateway te verzenden. Als u verkeer naar een gateway stuurt, moet u ervoor zorgen dat routes worden ingesteld in het externe netwerk om antwoorden terug te sturen.

Border Gateway Protocol (BGP)-routes hebben ook invloed op uw app-verkeer. Als u BGP-routes van iets zoals een ExpressRoute-gateway hebt, heeft dit gevolgen voor het uitgaande verkeer van uw app. BGP-routes zijn standaard alleen van invloed op uw RFC1918-doel verkeer. Als WEBSITE_VNET_ROUTE_ALL is ingesteld op 1, kan al het uitgaande verkeer worden beïnvloed door de BGP-routes.

### <a name="azure-dns-private-zones"></a>Azure DNS Private Zones 

Nadat uw app met uw VNet is geïntegreerd, maakt deze gebruik van dezelfde DNS-server die is geconfigureerd voor uw VNet. Uw app werkt standaard niet met Azure DNS Private Zones. Als u wilt werken met Azure DNS Private Zones moet u de volgende app-instellingen toevoegen:

1. WEBSITE_DNS_SERVER met waarde 168.63.129.16 
1. WEBSITE_VNET_ROUTE_ALL met waarde 1

Met deze instellingen worden al uw uitgaande oproepen vanuit uw app naar uw VNet verzonden en kan uw app Azure DNS privé zones gebruiken.

### <a name="private-endpoints"></a>Privé-eindpunten

Als u aanroepen naar [persoonlijke eind punten][privateendpoints]wilt maken, moet u de integratie met Azure DNS private zones of het persoonlijke eind punt beheren in de DNS-server die door uw app wordt gebruikt. 

<!--Image references-->
[4]: ../includes/media/web-sites-integrate-with-vnet/vnetint-appsetting.png

<!--Links-->
[VNETnsg]: https://docs.microsoft.com/azure/virtual-network/security-overview/
[privateendpoints]: https://docs.microsoft.com/azure/app-service/networking/private-endpoint
