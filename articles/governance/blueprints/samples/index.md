---
title: Index van blauwdrukvoorbeelden
description: Index van compatibiliteits- en standaardvoorbeelden voor het implementeren van omgevingen, beleidsregels en grondbeginselen voor Cloud Adoptions Framework met Azure Blueprints.
ms.date: 09/14/2020
ms.topic: sample
ms.openlocfilehash: def5e51a3db7e0733e0d7e1ef5c6895aedb7128d
ms.sourcegitcommit: 03662d76a816e98cfc85462cbe9705f6890ed638
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/15/2020
ms.locfileid: "90530978"
---
# <a name="azure-blueprints-samples"></a>Azure Blueprints-voorbeelden

De volgende tabel bevat links naar voorbeelden voor Azure Blueprints. Elk voorbeeld is van productiekwaliteit en is klaar om vandaag nog te worden geïmplementeerd om uw te helpen bij uw verschillende nalevingsbehoeften.

## <a name="standards-based-blueprint-samples"></a>Op standaarden gebaseerde blauwdrukvoorbeelden

| Voorbeeld | Beschrijving |
|---------|---------|
| [Australian Government ISM PROTECTED](./ism-protected/index.md) | Voorziet in richtlijnen om te voldoen aan Australian Government ISM PROTECTED. |
| [Azure Security-benchmark](./azure-security-benchmark.md) | Biedt richtlijnen voor de naleving van de [Azure Security-benchmark](../../../security/benchmarks/overview.md). |
| [Canada Federal PBMM](./canada-federal-pbmm/index.md) | Voorziet in richtlijnen om te voldoen aan de naleving van PBMM (Canada Federal Protected B, Medium Integrity, Medium Availability). |
| [CIS Microsoft Azure Foundations Benchmark](./cis-azure-1-1-0.md)| Biedt een set beleidsregels om te voldoen aan de aanbevelingen van CIS Microsoft Azure Foundations Benchmark. |
| [DoD Impact Level 4](./dod-impact-level-4/index.md) | Bied een set beleidsregels om te helpen voldoen aan DoD Impact Level 4. |
| [DoD Impact Level 5](./dod-impact-level-5/index.md) | Bied een set beleidsregels om te helpen voldoen aan DoD Impact Level 5. |
| [FedRAMP Moderate](./fedramp-m/index.md) | Bied een set beleidsregels om te helpen voldoen aan FedRAMP Moderate. |
| [FedRAMP High](./fedramp-h/index.md) | Bied een set beleidsregels om te helpen voldoen aan FedRAMP High. |
| [HIPAA HITRUST 9.2](./hipaa-hitrust-9-2.md) | Bied een set beleidsregels om te helpen voldoen aan HIPAA HITRUST. |
| [IRS 1075](./irs-1075/index.md) | Deze blauwdruk biedt richtlijnen voor naleving van IRS 1075.|
| [ISO 27001](./iso27001/index.md) | Deze blauwdruk biedt richtlijnen voor naleving van ISO 27001. |
| [ISO 27001 conforme gedeelde services](./iso27001-shared/index.md) | Deze blauwdruk biedt een set met conforme infrastructuurpatronen en beleidsrichtlijnen die de route naar ISO 27001-attestatie vergemakkelijken. |
| [ISO 27001 conforme App Service Environment-/SQL Database-workloads](./iso27001-ase-sql-workload/index.md) | Deze blauwdruk biedt een aanvullende infrastructuur voor de voorbeeldblauwdruk [ISO 27001 conforme gedeelde services](./iso27001-shared/index.md). |
| [Media](./media/index.md) | Bied een set beleidsregels om te helpen voldoen aan Media MPAA. |
| [NIST SP 800-53 R4](./nist-sp-800-53-r4.md) | Deze blauwdruk biedt richtlijnen voor naleving van NIST SP 800-53 R4. |
| [NIST SP 800-171 R2](./nist-sp-800-171-r2.md) | Deze blauwdruk biedt richtlijnen voor naleving van NIST SP 800-171 R2. |
| [PCI-DSS v3.2.1](./pci-dss-3.2.1/index.md) | Deze blauwdruk biedt een set beleidsregels ter ondersteuning van de naleving van PCI-DSS v3.2.1. |
| [SWIFT CSP-CSCF v2020](./swift-2020/index.md) | Hulpmiddelen voor naleving SWIFT CSP-CSCF v2020. |
| [Governance conform UK OFFICIAL en UK NHS](./ukofficial/index.md) | Deze blauwdruk biedt een set met conforme infrastructuurpatronen en beleidsrichtlijnen die de route naar UK OFFICIAL- en UK NHS-attestatie vergemakkelijken. |
| [CAF Foundation](./caf-foundation/index.md) | Biedt een set met besturingselementen waarmee u uw cloudomgeving kunt beheren in overeenstemming met [Microsoft Cloud Adoption Framework voor Azure (CAF)](/azure/architecture/cloud-adoption/governance/journeys/index). |
| [CAF Migrate-landingszone](./caf-migrate-landing-zone/index.md) | Biedt een set met besturingselementen die u helpen bij de migratie van uw eerste workload, en waarmee u uw cloudomgeving kunt beheren in overeenstemming met [Microsoft Cloud Adoption Framework voor Azure (CAF)](/azure/architecture/cloud-adoption/migrate/index). |

## <a name="samples-strategy"></a>Voorbeeldstrategie

:::image type="complex" source="../media/blueprint-samples-strategy.png" alt-text="Diagram van waar de blauwdrukvoorbeelden passen voor architecturale complexiteit versus nalevingsvereisten." border="false":::
   Beschrijft een coördinatensysteem waarbij de architecturale complexiteit op de X-as en de nalevingsvereisten op de Y-as liggen.  Naarmate de architecturale complexiteit en nalevingsvereisten toenemen, gebruikt u standaard blauwdrukvoorbeelden van de portal in regio E. Klanten die aan de slag gaan met Azure gebruiken het Cloud Adoption Framework (C A F) gebaseerd op Foundation- en landingszoneblauwdrukken uit regio A en B. De resterende ruimte is gereserveerd voor aangepaste blauwdrukken die zijn gemaakt door klanten die partners voor de regio's C, D en F zijn. :::image-end:::

Bij de CAF Foundation- en CAF Migrate- blauwdrukken voor landingszones wordt ervan uitgegaan dat de klant één bestaand leeg abonnement voorbereidt voor het migreren van on-premises activa en workloads naar Azure.
(Regio A en B in de afbeelding).  

U kunt de voorbeeldblauwdrukken herhalen en zoeken naar patronen in aanpassingen die een klant toepast. Er bestaat ook een mogelijkheid om proactief te werken met branchespecifieke blauwdrukken, zoals financiële services en e-commerce (boven aan Regio B). Op dezelfde manier willen we graag blauwdrukken gaan samenstellen voor architecturen met complexe onderdelen, zoals meerdere abonnementen, hoge beschikbaarheid, resources in verschillende regio’s, en klanten die besturingselementen implementeren in bestaande abonnementen en resources (Regio C en D).

Er zijn voorbeeldblauwdrukken voor klantscenario’s waarbij de compliancevereisten hoog zijn en de architectuur zeer complex is (Regio E in de afbeelding). Regio F in de afbeelding hierboven is de regio voor klanten en partners die de voorbeeldblauwdrukken gebruiken en deze aanpassen aan hun eigen unieke behoeften.

## <a name="next-steps"></a>Volgende stappen

- Meer informatie over de [levenscyclus van een blauwdruk](../concepts/lifecycle.md).
- Meer informatie over hoe u [statische en dynamische parameters](../concepts/parameters.md) gebruikt.
- Meer informatie over hoe u de [blauwdrukvolgorde](../concepts/sequencing-order.md) aanpast.
- Meer informatie over hoe u gebruikmaakt van [resourcevergrendeling in blauwdrukken](../concepts/resource-locking.md).
- Meer informatie over hoe u [bestaande toewijzingen bijwerkt](../how-to/update-existing-assignments.md).
- Problemen oplossen tijdens de toewijzing van een blauwdruk met [algemene probleemoplossing](../troubleshoot/general.md).
