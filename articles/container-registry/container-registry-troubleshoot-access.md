---
title: Problemen met het netwerk oplossen met het REGI ster
description: Symptomen, oorzaken en oplossingen voor veelvoorkomende problemen bij het openen van een Azure container registry in een virtueel netwerk of achter een firewall
ms.topic: article
ms.date: 08/11/2020
ms.openlocfilehash: 227eeeadb2aef4b4d3feb7923a198b129a6267d3
ms.sourcegitcommit: 152c522bb5ad64e5c020b466b239cdac040b9377
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/14/2020
ms.locfileid: "88227225"
---
# <a name="troubleshoot-network-issues-with-registry"></a>Problemen met het netwerk oplossen met het REGI ster

Dit artikel helpt u bij het oplossen van problemen die zich kunnen voordoen bij het openen van een Azure container registry in een virtueel netwerk of achter een firewall. 

## <a name="symptoms"></a>Symptomen

Dit kan een of meer van de volgende zijn:

* Er kunnen geen installatie kopieën worden gepusht of opgehaald en er wordt een fout bericht weer gegeven `dial tcp: lookup myregistry.azurecr.io`
* Kan geen installatie kopieën pushen of ophalen en u ontvangt een Azure CLI-fout `Could not connect to the registry login server`
* Kan geen installatie kopieën van het REGI ster ophalen naar een Azure Kubernetes-service of een andere Azure-service
* Geen toegang tot een REGI ster achter een HTTPS-proxy en er wordt een fout bericht weer gegeven `Error response from daemon: login attempt failed with status: 403 Forbidden`
* Kan geen toegang krijgen tot of register instellingen weer geven in Azure Portal of het REGI ster niet beheren met de Azure CLI
* Kan de instellingen van het virtuele netwerk of de regels voor open bare toegang niet toevoegen of wijzigen
* ACR-taken kunnen geen push-of pull-installatie kopieën uitvoeren
* Azure Security Center kan afbeeldingen in het REGI ster niet scannen of scan resultaten worden niet weer gegeven in Azure Security Center

## <a name="causes"></a>Oorzaken

* Een firewall of proxy van de client voor komt toegang tot de [oplossing](#configure-client-firewall-access)
* Toegangs regels voor open bare netwerken in het REGI ster verhinderen toegang tot de [oplossing](#configure-public-access-to-registry)
* De configuratie van het virtuele netwerk voor komt toegang tot de [oplossing](#configure-vnet-access)
* U probeert Azure Security Center te integreren met een REGI ster met een persoonlijk eind punt of service-eind punt- [oplossing](#configure-image-scanning-solution)

## <a name="further-diagnosis"></a>Verdere diagnose 

Voer de opdracht [AZ ACR check-Health](/cli/azure/acr#az-acr-check-health) uit voor meer informatie over de status van de register omgeving en eventueel toegang tot een doel register. U kunt bijvoorbeeld bepaalde problemen met de netwerk verbinding of configuratie vaststellen. 

Zie [de status van een Azure container Registry controleren](container-registry-check-health.md) op opdracht voorbeelden. Als er fouten worden gerapporteerd, raadpleegt u de [fout referentie](container-registry-health-error-reference.md) en de volgende secties voor de aanbevolen oplossingen.

> [!NOTE]
> Sommige problemen met de netwerk verbinding kunnen zich ook voordoen als er problemen zijn met de register verificatie of autorisatie. Zie [problemen met het REGI ster oplossen](container-registry-troubleshoot-login.md).

## <a name="potential-solutions"></a>Mogelijke oplossingen

### <a name="configure-client-firewall-access"></a>Firewall toegang voor clients configureren

Als u toegang wilt krijgen tot een REGI ster van achter een client firewall of proxy server, configureert u firewall regels om toegang te krijgen tot de REST-en data-eind punten van het REGI ster. Als [toegewezen data-eind punten](container-registry-firewall-access-rules.md#enable-dedicated-data-endpoints) zijn ingeschakeld, hebt u regels nodig om toegang te krijgen tot:

* REST-eind punt: `<registryname>.azurecr.io`
* Data-eind punt (en): `<registry-name>.<region>.data.azurecr.io`

Voor een geo-gerepliceerd REGI ster configureert u de toegang tot het gegevens eindpunt voor elke regionale replica.

Controleer achter een HTTPS-proxy of uw docker-client en docker-daemon zijn geconfigureerd voor proxy gedrag.

Register bron Logboeken in de tabel ContainerRegistryLoginEvents kunnen helpen bij het vaststellen van een verbindings poging die is geblokkeerd.

Gerelateerde koppelingen:

* [Regels configureren voor toegang tot een Azure container Registry achter een firewall](container-registry-firewall-access-rules.md)
* [HTTP/HTTPS-proxy configuratie](https://docs.docker.com/config/daemon/systemd/#httphttps-proxy)
* [Geo-replicationin Azure Container Registry](container-registry-geo-replication.md)
* [Azure Container Registry logboeken voor diagnostische evaluatie en controle](container-registry-diagnostics-audit-logs.md)

### <a name="configure-public-access-to-registry"></a>Open bare toegang tot het REGI ster configureren

Als u via internet toegang wilt krijgen tot een REGI ster, controleert u of het REGI ster open bare netwerk toegang tot uw client toestaat. Een Azure container Registry biedt standaard toegang tot de open bare register eindpunten vanuit alle netwerken. Met een REGI ster kunt u de toegang tot geselecteerde netwerken of geselecteerde IP-adressen beperken. 

Als het REGI ster is geconfigureerd voor een virtueel netwerk met een service-eind punt, schakelt het uitschakelen van open bare netwerk toegang ook de toegang via het service-eind punt uit. Als uw REGI ster is geconfigureerd voor een virtueel netwerk met een persoonlijke koppeling, zijn de IP-netwerk regels niet van toepassing op de persoonlijke eind punten van het REGI ster. 

Gerelateerde koppelingen:

* [Open bare IP-netwerk regels configureren](container-registry-access-selected-networks.md)
* [Persoonlijke verbinding maken met een Azure container Registry met behulp van een persoonlijke Azure-koppeling](container-registry-private-link.md)
* [Toegang tot een container register beperken met behulp van een service-eind punt in een virtueel Azure-netwerk](container-registry-vnet.md)


### <a name="configure-vnet-access"></a>VNet-toegang configureren

Controleer of het virtuele netwerk is geconfigureerd met een persoonlijk eind punt voor een persoonlijke koppeling of een service-eind punt (preview). Momenteel wordt er geen Azure Bastion-eind punt ondersteund.

Bekijk de NSG-regels en service tags die worden gebruikt om verkeer van andere bronnen in het netwerk te beperken tot het REGI ster. 

Als een service-eind punt naar het REGI ster is geconfigureerd, controleert u of er een netwerk regel is toegevoegd aan het REGI ster waarmee toegang vanuit dat subnet is toegestaan. Het service-eind punt ondersteunt alleen toegang vanaf virtuele machines en AKS-clusters in het netwerk.

Als Azure Firewall of een vergelijk bare oplossing in het netwerk is geconfigureerd, controleert u of het uitgaande verkeer van andere resources, zoals een AKS-cluster, is ingeschakeld om de register eindpunten te bereiken.

Gerelateerde koppelingen:

* [Persoonlijke verbinding maken met een Azure container Registry met behulp van een persoonlijke Azure-koppeling](container-registry-private-link.md)
* [Toegang tot een container register beperken met behulp van een service-eind punt in een virtueel Azure-netwerk](container-registry-vnet.md)
* [Vereiste uitgaande netwerk regels en FQDN voor AKS-clusters](../aks/limit-egress-traffic.md#required-outbound-network-rules-and-fqdns-for-aks-clusters)
* [Kubernetes: DNS-omzetting oplossen](https://kubernetes.io/docs/tasks/administer-cluster/dns-debugging-resolution/)
* [Service tags van virtueel netwerk](../virtual-network/service-tags-overview.md)

### <a name="configure-image-scanning-solution"></a>Scan oplossing voor afbeeldingen configureren

Als uw REGI ster is geconfigureerd met een privé-eind punt of service-eind punt, kunt u momenteel niet integreren met Azure Security Center voor het scannen van afbeeldingen. U kunt ook andere oplossingen voor het scannen van installatie kopieën configureren die beschikbaar zijn in azure Marketplace, met inbegrip van:

* [Systeem eigen Cloud beveiligings platform met licht blauw](https://azuremarketplace.microsoft.com/marketplace/apps/aqua-security.aqua-security)
* [Twistlock Enter prise Edition](https://azuremarketplace.microsoft.com/marketplace/apps/twistlock.twistlock)

Gerelateerde koppelingen:

* [Azure Container Registry afbeeldingen scannen door Security Center](../security-center/azure-container-registry-integration.md)
* [Feedback](https://feedback.azure.com/forums/347535-azure-security-center/suggestions/41091577-enable-vulnerability-scanning-for-images-that-are) geven


## <a name="advanced-troubleshooting"></a>Geavanceerde probleemoplossing

Als het [verzamelen van bron logboeken](container-registry-diagnostics-audit-logs.md) is ingeschakeld in het REGI ster, raadpleegt u het ContainterRegistryLoginEvents-logboek. In dit logboek worden verificatie gebeurtenissen en status opgeslagen, met inbegrip van de binnenkomende identiteit en het IP-adres. Zoek het logboek op voor [register verificatie fouten](container-registry-diagnostics-audit-logs.md#registry-authentication-failures). 

Gerelateerde koppelingen:

* [Logboeken voor diagnostische evaluaties en controles](container-registry-diagnostics-audit-logs.md)
* [Veelgestelde vragen over container Registry](container-registry-faq.md)
* [Azure-beveiligings basislijn voor Azure Container Registry](security-baseline.md)
* [Aanbevolen procedures voor Azure Container Registry](container-registry-best-practices.md)

## <a name="next-steps"></a>Volgende stappen

Als u uw probleem hier niet kunt oplossen, raadpleegt u de volgende opties.

* Andere onderwerpen over het oplossen van problemen met het REGI ster zijn:
  * [Problemen met register aanmelding oplossen](container-registry-troubleshoot-login.md) 
  * [Problemen met het REGI ster oplossen](container-registry-troubleshoot-performance.md)
* Opties voor [Community-ondersteuning](https://azure.microsoft.com/support/community/)
* [Microsoft Q&A](https://docs.microsoft.com/answers/products/)
* [Een ondersteuningsticket openen](https://azure.microsoft.com/support/create-ticket/)


