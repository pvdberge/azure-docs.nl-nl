---
title: Verbeter de betrouw baarheid van uw toepassing met Advisor
description: Gebruik Azure Advisor om de betrouw baarheid in uw bedrijfs kritieke Azure-implementaties te garanderen en te verbeteren.
ms.topic: article
ms.date: 01/29/2019
ms.openlocfilehash: 0d96974e53f24d5a01eeee8b08eee578177a9ad2
ms.sourcegitcommit: ef055468d1cb0de4433e1403d6617fede7f5d00e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/16/2020
ms.locfileid: "88258498"
---
# <a name="improve-the-reliability-of-your-application-by-using-azure-advisor"></a>Verbeter de betrouw baarheid van uw toepassing met behulp van Azure Advisor

Azure Advisor helpt u de continuïteit van uw bedrijfs kritieke toepassingen te garanderen en te verbeteren. U kunt aanbevelingen voor betrouw baarheid ophalen van Advisor op het tabblad **betrouw baarheid** van het Advisor-dash board.

## <a name="check-the-version-of-your-check-point-network-virtual-appliance-image"></a>Controleer de versie van de installatie kopie van het virtuele netwerk apparaat van Check Point

Advisor kan bepalen of op uw virtuele machine een versie van de Check Point-installatie kopie wordt uitgevoerd waarvan bekend is dat deze de netwerk verbinding verliest tijdens de onderhouds bewerkingen voor het platform. De Advisor-aanbeveling helpt u bij te werken naar een nieuwere versie van de installatie kopie waarmee dit probleem wordt opgelost. Met deze controle wordt de bedrijfs continuïteit gegarandeerd via een betere netwerk verbinding.

## <a name="ensure-application-gateway-fault-tolerance"></a>Fout tolerantie van Application Gateway garanderen

Deze aanbeveling garandeert de bedrijfs continuïteit van essentiële toepassingen die worden aangedreven door toepassings gateways. Advisor identificeert Application Gateway-exemplaren die niet zijn geconfigureerd voor fout tolerantie. Vervolgens worden de herstel acties voorgesteld die u kunt uitvoeren. Advisor identificeert gemiddeld of grote toepassings gateways voor één exemplaar en raadt aan om ten minste één instantie toe te voegen. Ook worden de kleine toepassings gateways met één exemplaar en meerdere instanties geïdentificeerd en wordt aanbevolen om deze te migreren naar een medium of grote Sku's. Advisor raadt deze acties aan om ervoor te zorgen dat de instanties van de toepassings gateway zo zijn geconfigureerd dat ze voldoen aan de huidige SLA-vereisten voor deze resources.

## <a name="protect-your-virtual-machine-data-from-accidental-deletion"></a>Beveilig de gegevens van uw virtuele machine tegen onbedoeld verwijderen

Bij het instellen van de back-up van de virtuele machine wordt de beschik baarheid van uw bedrijfs kritieke gegevens gegarandeerd en wordt bescherming geboden tegen onbedoeld verwijderen of beschadigd. Advisor identificeert virtuele machines waarop back-up niet is ingeschakeld en raadt u aan om back-ups in te scha 

## <a name="ensure-you-have-access-to-azure-experts-when-you-need-it"></a>Zorg ervoor dat u toegang hebt tot Azure-experts wanneer u deze nodig hebt

Wanneer u een bedrijfs kritieke werk belasting uitvoert, is het belang rijk dat u toegang hebt tot technische ondersteuning wanneer u deze nodig hebt. Advisor identificeert potentiële bedrijfs kritieke abonnementen waarvoor geen technische ondersteuning is opgenomen in hun ondersteunings abonnementen. Het wordt aanbevolen een upgrade uit te brengen naar een optie met technische ondersteuning.

## <a name="create-azure-service-health-alerts-to-be-notified-when-azure-problems-affect-you"></a>Azure Service Health waarschuwingen maken om een melding te ontvangen wanneer Azure-problemen van invloed zijn op u

We raden u aan Azure Service Health waarschuwingen in te stellen, zodat u wordt gewaarschuwd wanneer er problemen met de Azure-service zijn. [Azure service Health](https://azure.microsoft.com/features/service-health/) is een gratis service die persoonlijke begeleiding en ondersteuning biedt wanneer u het probleem van een Azure-service ondervindt. Advisor identificeert abonnementen waarvoor geen waarschuwingen zijn geconfigureerd en raadt u aan om deze te configureren.

## <a name="configure-traffic-manager-endpoints-for-resiliency"></a>Traffic Manager-eind punten voor tolerantie configureren

Azure Traffic Manager profielen met meer dan één eindpunt ervaring hogere Beschik baarheid als een bepaald eind punt mislukt. Het plaatsen van eind punten in verschillende regio's verbetert de betrouw baarheid van de service. Advisor identificeert Traffic Manager-profielen waarbij er slechts één eind punt is en raadt aan ten minste één eind punt toe te voegen in een andere regio.

Als alle eind punten in een Traffic Manager profiel dat is geconfigureerd voor proximity-route ring zich in dezelfde regio bevinden, kunnen gebruikers uit andere regio's verbindings vertragingen ondervinden. Als u een eind punt toevoegt of verplaatst naar een andere regio, worden de algehele prestaties verbeterd en wordt er een betere Beschik baarheid geboden als alle eind punten in één regio mislukken. Advisor identificeert Traffic Manager profielen die zijn geconfigureerd voor proximity route ring waarbij alle eind punten zich in dezelfde regio bevinden. Het wordt aanbevolen een eind punt toe te voegen aan of te verplaatsen naar een andere Azure-regio.

Als een Traffic Manager profiel is geconfigureerd voor geografische route ring, wordt verkeer doorgestuurd naar eind punten op basis van gedefinieerde regio's. Als er een fout optreedt in een regio, is er geen vooraf gedefinieerde failover. Als u een eind punt hebt waarop de regionale groepering is geconfigureerd voor **alle (wereld)**, kunt u voor komen dat verkeer wordt geblokkeerd en de beschik baarheid van de service wordt verbeterd. Advisor identificeert Traffic Manager profielen die zijn geconfigureerd voor geografische route ring waarbij er geen eind punt is geconfigureerd voor de regionale groepering als **Alles (wereld)**. Het wordt aanbevolen de configuratie te wijzigen om een eind punt **(wereld)** te maken.

## <a name="use-soft-delete-on-your-azure-storage-account-to-save-and-recover-data-after-accidental-overwrite-or-deletion"></a>Gebruik zacht verwijderen in uw Azure Storage-account om gegevens op te slaan en te herstellen nadat het per ongeluk is overschreven of verwijderd

Schakel de optie [voorlopig verwijderen](../storage/blobs/soft-delete-overview.md) in uw opslag account in, zodat verwijderde blobs overstappen naar een voorlopig verwijderde status in plaats van permanent worden verwijderd. Als gegevens worden overschreven, wordt er een voorlopig verwijderde momentopname gegenereerd waarin de status van de overschreven gegevens wordt opgeslagen. Met de functie voor het gebruik van zacht verwijderen kunt u herstellen van onbedoeld verwijderen of overschrijvingen. Advisor identificeert Azure Storage-accounts waarvoor geen tijdelijke verwijdering is ingeschakeld en raadt u aan om deze in te scha kelen.

## <a name="configure-your-vpn-gateway-to-active-active-for-connection-resiliency"></a>Configureer uw VPN-gateway naar actief-actief voor verbindings tolerantie

In de configuratie actief-actief maken beide exemplaren van een VPN-gateway S2S VPN-tunnels naar uw on-premises VPN-apparaat. Wanneer een geplande onderhouds gebeurtenis of een niet-geplande gebeurtenis plaatsvindt in één gateway-exemplaar, wordt verkeer automatisch overgeschakeld naar de andere actieve IPsec-tunnel. Azure Advisor identificeert VPN-gateways die niet zijn geconfigureerd als actief-actief en raadt u aan deze te configureren voor hoge Beschik baarheid.

## <a name="use-production-vpn-gateways-to-run-your-production-workloads"></a>Productie-VPN-gateways gebruiken voor het uitvoeren van uw productie-workloads

Azure Advisor controleert op alle VPN-gateways die gebruikmaken van een basis-SKU en raadt u aan om in plaats daarvan een productie-SKU te gebruiken. De basis-SKU is ontworpen voor ontwikkeling en testen. Aanbod productie-Sku's:
- Meer tunnels. 
- BGP-ondersteuning. 
- Opties voor actief/actief-configuratie. 
- Aangepast IPSec/IKE-beleid. 
- Hogere stabiliteit en beschik baarheid.

## <a name="ensure-virtual-machine-fault-tolerance-temporarily-disabled"></a>Fout tolerantie voor virtuele machines garanderen (tijdelijk uitgeschakeld)

Om redundantie voor uw toepassing te bieden, raden we u aan om twee of meer virtuele machines in een beschikbaarheidsset te groeperen. Advisor identificeert virtuele machines die geen deel uitmaken van een beschikbaarheidsset en raadt u aan deze te verplaatsen naar één. Deze configuratie zorgt ervoor dat tijdens gepland of niet-gepland onderhoud ten minste één virtuele machine beschikbaar is en voldoet aan de SLA van de virtuele Azure-machine. U kunt ervoor kiezen een beschikbaarheidsset voor de virtuele machine te maken of de virtuele machine toe te voegen aan een bestaande beschikbaarheidsset.

> [!NOTE]
> Als u een beschikbaarheidsset maakt, moet u er ten minste één virtuele machine aan toevoegen. We raden u aan twee of meer virtuele machines in een beschikbaarheidsset te groeperen om ervoor te zorgen dat er ten minste één computer beschikbaar is tijdens een storing.

## <a name="ensure-availability-set-fault-tolerance-temporarily-disabled"></a>Fout tolerantie voor beschikbaarheidsset garanderen (tijdelijk uitgeschakeld)

Om redundantie voor uw toepassing te bieden, raden we u aan om twee of meer virtuele machines in een beschikbaarheidsset te groeperen. Advisor identificeert beschikbaarheids sets die één virtuele machine bevatten en raadt u aan om een of meer virtuele machines toe te voegen.Deze configuratie zorgt ervoor dat tijdens gepland of niet-gepland onderhoud ten minste één virtuele machine beschikbaar is en voldoet aan de SLA van de virtuele Azure-machine.U kunt ervoor kiezen om een virtuele machine te maken of een bestaande virtuele machine toe te voegen aan de beschikbaarheidsset.  

## <a name="use-managed-disks-to-improve-data-reliability-temporarily-disabled"></a>Beheerde schijven gebruiken om de betrouw baarheid van gegevens te verbeteren (tijdelijk uitgeschakeld)

Virtuele machines die deel uitmaken van een beschikbaarheidsset met schijven die opslag accounts of opslag schaal eenheden delen, zijn niet van kracht voor storingen in één opslag schaal eenheden tijdens storingen. Advisor identificeert deze beschikbaarheids sets en raadt u aan om te migreren naar Azure Managed disks. Deze migratie zorgt ervoor dat de schijven van de virtuele machines in de beschikbaarheidsset voldoende geïsoleerd zijn om een Single Point of Failure te voor komen. 

## <a name="repair-invalid-log-alert-rules"></a>Ongeldige regels voor logboek waarschuwingen herstellen

Azure Advisor detecteert waarschuwings regels waarvoor ongeldige query's zijn opgegeven in de sectie voor waarde. U kunt waarschuwings regels voor logboeken maken in Azure Monitor en ze gebruiken om analyse query's uit te voeren op basis van opgegeven intervallen. De resultaten van een query bepalen of een waarschuwing moet worden geactiveerd. Analytische query's kunnen na verloop van tijd ongeldig worden vanwege wijzigingen in resources, tabellen of opdrachten waarnaar wordt verwezen. Advisor raadt u aan de query in de waarschuwings regel te corrigeren om te voor komen dat deze automatisch wordt uitgeschakeld en de bewakings dekking van uw resources in azure te controleren. [Meer informatie over het oplossen van waarschuwings regels.](https://aka.ms/aa_logalerts_queryrepair)

## <a name="configure-consistent-indexing-mode-on-your-azure-cosmos-db-collection"></a>Consistente indexerings modus configureren voor uw Azure Cosmos DB verzameling

Het configureren van Azure Cosmos DB-containers met de vertraagde indexerings modus kan van invloed zijn op de versheid van de query resultaten. Advisor detecteert containers die op deze manier zijn geconfigureerd en raadt aan om over te scha kelen naar de consistente modus. [Meer informatie over het indexeren van beleid in Azure Cosmos DB.](https://aka.ms/cosmosdb/how-to-manage-indexing-policy)

## <a name="configure-your-azure-cosmos-db-containers-with-a-partition-key"></a>Uw Azure Cosmos DB-containers met een partitiesleutel configureren

Azure Advisor identificeert Azure Cosmos DB niet-gepartitioneerde verzamelingen die de ingerichte opslag limiet nadert. U wordt aangeraden deze verzamelingen te migreren naar nieuwe verzamelingen met een partitie sleutel definitie zodat deze automatisch kan worden uitgeschaald door de service. [Meer informatie over het kiezen van een partitie sleutel.](https://aka.ms/cosmosdb/choose-partitionkey)

## <a name="upgrade-your-azure-cosmos-db-net-sdk-to-the-latest-version-from-nuget"></a>Upgrade uw Azure Cosmos DB .NET SDK naar de nieuwste versie van NuGet

Azure Advisor identificeert Azure Cosmos DB accounts die gebruikmaken van oude versies van de .NET SDK. Het wordt aanbevolen dat u een upgrade uitvoert naar de meest recente versie van NuGet voor de nieuwste oplossingen, prestatie verbeteringen en functie mogelijkheden. [Meer informatie over Azure Cosmos DB .NET SDK.](https://aka.ms/cosmosdb/sql-api-sdk-dotnet)

## <a name="upgrade-your-azure-cosmos-db-java-sdk-to-the-latest-version-from-maven"></a>Uw Azure Cosmos DB Java SDK bijwerken naar de nieuwste versie van Maven

Azure Advisor identificeert Azure Cosmos DB accounts die gebruikmaken van oude versies van de Java-SDK. Het wordt aanbevolen dat u een upgrade uitvoert naar de meest recente versie van Maven voor de nieuwste oplossingen, prestatie verbeteringen en functie mogelijkheden. [Meer informatie over Azure Cosmos DB Java SDK.](https://aka.ms/cosmosdb/sql-api-sdk-async-java)

## <a name="upgrade-your-azure-cosmos-db-spark-connector-to-the-latest-version-from-maven"></a>Voer een upgrade uit van uw Azure Cosmos DB Spark-connector naar de nieuwste versie van Maven

Azure Advisor identificeert Azure Cosmos DB accounts die gebruikmaken van oude versies van de Azure Cosmos DB Spark-connector. Het wordt aanbevolen dat u een upgrade uitvoert naar de meest recente versie van Maven voor de nieuwste oplossingen, prestatie verbeteringen en functie mogelijkheden. [Meer informatie over Azure Cosmos DB Spark-connector.](https://aka.ms/cosmosdb/spark-connector)

## <a name="consider-moving-to-kafka-21-on-hdinsight-40"></a>Overweeg om over te stappen op Kafka 2,1 in HDInsight 4,0

Vanaf 1 juli 2020 kunt u geen nieuwe Kafka-clusters maken met behulp van Kafka 1,1 op Azure HDInsight 4,0. Bestaande clusters worden zonder ondersteuning van Microsoft uitgevoerd zoals ze zijn. Overweeg om op 30 juni 2020 over te stappen op Kafka 2,1 op HDInsight 4,0 om mogelijke onderbreking van systeem/ondersteuning te voor komen.

## <a name="consider-upgrading-older-spark-versions-in-hdinsight-spark-clusters"></a>Overwegen oudere Spark-versies in HDInsight Spark-clusters te upgraden

Vanaf 1 juli 2020 kunt u geen nieuwe Spark-clusters maken met behulp van Spark 2,1 of 2,2 op HDInsight 3,6. U kunt geen nieuwe Spark-clusters maken met behulp van Spark 2,3 op HDInsight 4,0. Bestaande clusters worden zonder ondersteuning van Microsoft uitgevoerd zoals ze zijn. 

## <a name="enable-virtual-machine-replication"></a>Replicatie van virtuele machines inschakelen
Virtuele machines waarvoor geen replicatie is ingeschakeld voor een andere regio, zijn niet flexibel voor regionale storingen. Het repliceren van virtuele machines vermindert nadelige gevolgen voor het bedrijf tijdens de uitval van Azure-regio's. Advisor detecteert Vm's waarop replicatie niet is ingeschakeld en raadt aan om deze functie in te scha kelen. Wanneer u replicatie inschakelt en er zich een storing voordoet, kunt u uw virtuele machines snel weer geven in een externe Azure-regio. [Meer informatie over replicatie van virtuele machines.](../site-recovery/azure-to-azure-quickstart.md)

## <a name="how-to-access-high-availability-recommendations-in-advisor"></a>Toegang tot aanbevelingen voor hoge Beschik baarheid in Advisor

1. Meld u aan bij de [Azure Portal](https://portal.azure.com)en open vervolgens [Advisor](https://aka.ms/azureadvisordashboard).

2.  Op het Advisor-dash board selecteert u het tabblad **maximale Beschik baarheid** .

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over Advisor-aanbevelingen:
* [Inleiding tot Advisor](advisor-overview.md)
* [Aan de slag met Advisor](advisor-get-started.md)
* [Aanbevelingen van Advisor met betrekking tot kosten](advisor-cost-recommendations.md)
* [Aanbevelingen voor Advisor-prestaties](advisor-performance-recommendations.md)
* [Aanbevelingen voor de beveiliging van Advisor](advisor-security-recommendations.md)
* [Aanbevelingen voor operationele uitmuntendheid van Advisor](advisor-operational-excellence-recommendations.md)
