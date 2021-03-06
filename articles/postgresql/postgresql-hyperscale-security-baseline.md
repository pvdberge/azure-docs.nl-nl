---
title: Azure-beveiligings basislijn voor Azure Database for PostgreSQL-grootschalige
description: De Azure Database for PostgreSQL-grootschalige beveiligings basislijn biedt procedure richtlijnen en resources voor het implementeren van de beveiligings aanbevelingen die zijn opgegeven in de Azure Security-benchmark test.
author: msmbaldwin
ms.service: postgresql
ms.topic: conceptual
ms.date: 08/04/2020
ms.author: mbaldwin
ms.custom: subject-security-benchmark
ms.openlocfilehash: 37ebd1702ed8ef059b38378b89f5a5cb61748568
ms.sourcegitcommit: d68c72e120bdd610bb6304dad503d3ea89a1f0f7
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/01/2020
ms.locfileid: "89231296"
---
# <a name="azure-security-baseline-for-azure-database-for-postgresql---hyperscale"></a>Azure-beveiligings basislijn voor Azure Database for PostgreSQL-grootschalige

De Azure-beveiligings basislijn voor Azure Database for PostgreSQL-grootschalige bevat aanbevelingen waarmee u de beveiligings-postuur van uw implementatie kunt verbeteren.

De basis lijn voor deze service wordt opgehaald uit de [Azure Security Bench Mark-versie 1,0](https://docs.microsoft.com/azure/security/benchmarks/overview), die aanbevelingen biedt over hoe u uw cloud oplossingen kunt beveiligen in azure met onze richt lijnen voor best practices.

Zie [overzicht van Azure Security-basis lijnen](https://docs.microsoft.com/azure/security/benchmarks/security-baselines-overview)voor meer informatie.

## <a name="network-security"></a>Netwerkbeveiliging

*Zie [beveiligings beheer: netwerk beveiliging](/azure/security/benchmarks/security-control-network-security)voor meer informatie.*

### <a name="11-protect-azure-resources-within-virtual-networks"></a>1,1: Azure-resources in virtuele netwerken beveiligen

**Richt lijnen**: Azure database for PostgreSQL Server firewall voor komt dat u toegang hebt tot uw grootschalige (Citus)-coördinator knooppunt totdat u opgeeft welke computers zijn gemachtigd. De firewall verleent toegang tot de server op basis van het oorspronkelijke IP-adres van elke aanvraag. U configureert de firewall door firewallregels te maken die bereiken opgeven van acceptabele IP-adressen. U kunt Firewall regels maken op server niveau.

- [Firewall regels configureren in Azure Database for PostgreSQL-grootschalige (Citus)](https://docs.microsoft.com/azure/postgresql/concepts-hyperscale-firewall-rules)

**Azure Security Center bewaking**: momenteel niet beschikbaar

**Verantwoordelijkheid**: klant

### <a name="19-maintain-standard-security-configurations-for-network-devices"></a>1,9: standaard beveiligings configuraties voor netwerk apparaten onderhouden

**Hulp**: Definieer en implementeer standaard beveiligings configuraties voor netwerk instellingen en netwerk resources die zijn gekoppeld aan uw Azure database for PostgreSQL-instanties met Azure Policy. Gebruik Azure Policy aliassen in de naam ruimte ' micro soft. netwerk ' om aangepaste beleids regels te maken om de netwerk configuratie van uw Azure Database for PostgreSQL instanties te controleren of af te dwingen.

- [Azure Policy configureren en beheren](https://docs.microsoft.com/azure/governance/policy/tutorials/create-and-manage)

- [Voor beelden Azure Policy voor netwerken](https://docs.microsoft.com/azure/governance/policy/samples/#network)

- [Een Azure Blueprint maken](https://docs.microsoft.com/azure/governance/blueprints/create-blueprint-portal)

**Azure Security Center bewaking**: niet van toepassing

**Verantwoordelijkheid**: klant

## <a name="logging-and-monitoring"></a>Logboekregistratie en bewaking

*Zie voor meer informatie [beveiligings beheer: logboek registratie en controle](/azure/security/benchmarks/security-control-logging-monitoring).*

### <a name="22-configure-central-security-log-management"></a>2,2: Centraal beveiligings logboek beheer configureren

**Richt lijnen**: voor het bijhouden van de controle op vliegtuig controles, schakelt u Diagnostische instellingen voor Azure-activiteiten logboek in en verzendt u de logboeken naar een log Analytics-werk ruimte, Azure Event hub of Azure Storage-account voor archivering. Met Azure-activiteiten logboek gegevens kunt u de ' What, wie en wanneer ' bepalen voor schrijf bewerkingen (PUT, POST, DELETE) die zijn uitgevoerd op het niveau van het controle vlak voor uw Azure-resources.

Neem ook opname logboeken via Azure Monitor op voor het verzamelen van beveiligings gegevens die zijn gegenereerd door grootschalige (Citus). In de Azure Monitor gebruikt u Log Analytics werk ruimte (n) om een query uit te voeren en een analyse te verrichten en opslag accounts te gebruiken voor lange termijn/archiverings opslag. U kunt ook gegevens naar Azure Sentinel of een beveiligings incident en gebeurtenis beheer van derden (SIEM) inschakelen en op de trein zetten. 

- [Diagnostische instellingen voor Azure-activiteiten logboek inschakelen](https://docs.microsoft.com/azure/azure-monitor/platform/diagnostic-settings-legacy)

- [Metrische gegevens in grootschalige (Citus)](https://docs.microsoft.com/azure/postgresql/concepts-hyperscale-monitoring)

- [Azure-Sentinel onboarden](https://docs.microsoft.com/azure/sentinel/quickstart-onboard)

**Azure Security Center bewaking**: momenteel niet beschikbaar

**Verantwoordelijkheid**: klant

### <a name="23-enable-audit-logging-for-azure-resources"></a>2,3: controle logboek registratie inschakelen voor Azure-resources

**Hulp**: grootschalige (Citus) geeft metrische gegevens voor elk knoop punt in een server groep. De metrische gegevens bieden inzicht in het gedrag van ondersteunende resources. Elke metriek wordt verzonden met een frequentie van één minuut en heeft tot wel 30 dagen aan geschiedenis.

Schakel de diagnostische instellingen voor het Azure-activiteiten logboek in voor de controle van het controle vlak en verzend de logboeken naar een Log Analytics-werk ruimte, een Azure Event Hub of een Azure-opslag account voor archivering. Met Azure-activiteiten logboek gegevens kunt u de ' What, wie en wanneer ' bepalen voor schrijf bewerkingen (PUT, POST, DELETE) die zijn uitgevoerd op het niveau van het controle vlak voor uw Azure-resources.

Neem ook opname logboeken via Azure Monitor op voor het verzamelen van beveiligings gegevens die zijn gegenereerd door grootschalige (Citus). In de Azure Monitor gebruikt u Log Analytics werk ruimte (n) om een query uit te voeren en een analyse te verrichten en opslag accounts te gebruiken voor lange termijn/archiverings opslag. U kunt ook gegevens naar Azure Sentinel of een beveiligings incident en gebeurtenis beheer van derden (SIEM) inschakelen en op de trein zetten. 

- [Metrische gegevens in grootschalige (Citus)](https://docs.microsoft.com/azure/postgresql/concepts-hyperscale-monitoring)

- [Diagnostische instellingen voor Azure-activiteiten logboek inschakelen](https://docs.microsoft.com/azure/azure-monitor/platform/diagnostic-settings-legacy)

- [Azure-Sentinel onboarden](https://docs.microsoft.com/azure/sentinel/quickstart-onboard)

**Azure Security Center bewaking**: momenteel niet beschikbaar

**Verantwoordelijkheid**: klant

### <a name="25-configure-security-log-storage-retention"></a>2,5: Bewaar beveiliging van het beveiligings logboek configureren

**Richt lijnen**: in azure monitor voor de log Analytics-werk ruimte die wordt gebruikt om uw grootschalige (Citus)-logboeken te bewaren, stelt u de Bewaar periode in volgens de nalevings voorschriften van uw organisatie. Gebruik Azure Storage-accounts voor lange termijn/archiverings opslag.

- [Para meters voor het bewaren van Logboeken instellen voor Log Analytics-werk ruimten](https://docs.microsoft.com/azure/azure-monitor/platform/manage-cost-storage#change-the-data-retention-period)

- [Bron logboeken opslaan in een Azure Storage-account](https://docs.microsoft.com/azure/azure-monitor/platform/resource-logs-collect-storage)

**Azure Security Center bewaking**: niet van toepassing

**Verantwoordelijkheid**: klant

### <a name="26-monitor-and-review-logs"></a>2,6: Logboeken bewaken en controleren

**Richt lijnen**: Logboeken analyseren en bewaken vanuit uw grootschalige (Citus)-instanties voor afwijkend gedrag. Gebruik de Log Analytics van Azure Monitor om logboeken te controleren en query's uit te voeren op logboek gegevens. U kunt ook gegevens in-of uitschakelen voor Azure Sentinel of een SIEM van derden.

- [Azure-Sentinel onboarden](https://docs.microsoft.com/azure/sentinel/quickstart-onboard)

- [Voor meer informatie over de Log Analytics](https://docs.microsoft.com/azure/azure-monitor/log-query/get-started-portal)

- [Aangepaste query's uitvoeren in Azure Monitor](https://docs.microsoft.com/azure/azure-monitor/log-query/get-started-queries)

**Azure Security Center bewaking**: niet van toepassing

**Verantwoordelijkheid**: klant

### <a name="27-enable-alerts-for-anomalous-activities"></a>2,7: waarschuwingen inschakelen voor afwijkende activiteiten

**Richt lijnen**: u kunt Diagnostische instellingen voor grootschalige (Citus) inschakelen en logboeken naar een log Analytics-werk ruimte verzenden. U kunt een waarschuwing configureren en ontvangen op basis van metrische bewakings gegevens voor uw Azure-Services. Gebruik de Log Analytics van Azure Monitor om logboeken te controleren en query's uit te voeren op logboek gegevens. U kunt ook gegevens in-of uitschakelen voor Azure Sentinel of een SIEM van derden.

Onboarding van uw Log Analytics-werk ruimte naar Azure-Sentinel, omdat dit een via-oplossing (Security Orchestration Automated Response) biedt. Hiermee kunnen playbooks (geautomatiseerde oplossingen) worden gemaakt en gebruikt om beveiligings problemen op te lossen.

- [Metrische gegevens in grootschalige (Citus)](https://docs.microsoft.com/azure/postgresql/howto-hyperscale-alert-on-metric)

- [Diagnostische instellingen configureren voor het Azure-activiteiten logboek](https://docs.microsoft.com/azure/azure-monitor/platform/diagnostic-settings-legacy)

- [Azure-Sentinel onboarden](https://docs.microsoft.com/azure/sentinel/quickstart-onboard)

**Azure Security Center bewaking**: momenteel niet beschikbaar

**Verantwoordelijkheid**: klant

## <a name="identity-and-access-control"></a>Identiteits- en toegangsbeheer

*Zie [beveiligings beheer: identiteits-en toegangs beheer](/azure/security/benchmarks/security-control-identity-access-control)voor meer informatie.*

### <a name="31-maintain-an-inventory-of-administrative-accounts"></a>3,1: een inventaris van beheerders accounts onderhouden

**Richt lijnen**: behoud een inventaris van de gebruikers accounts met beheerders toegang tot het besturings vlak (bijvoorbeeld Azure Portal) van uw grootschalige-exemplaren (Citus). Daarnaast houdt u een inventarisatie bij van de beheerders accounts die toegang hebben tot het gegevens vlak (binnen de data base zelf) van uw grootschalige-exemplaren (Citus).

Grootschalige (Citus) biedt geen ondersteuning voor ingebouwde op rollen gebaseerd toegangs beheer, maar u kunt aangepaste rollen maken op basis van specifieke bewerkingen van de resource provider.

Daarnaast gebruikt de PostgreSQL-engine rollen om de toegang tot database objecten te beheren en een nieuw gemaakte grootschalige (Citus)-Server groep wordt geleverd met verschillende rollen vooraf gedefinieerd. Als u gebruikers bevoegdheden wilt wijzigen, gebruikt u de standaard PostgreSQL-opdrachten met een hulp programma zoals PgAdmin of psql.

- [Informatie over aangepaste rollen voor het Azure-abonnement](https://docs.microsoft.com/azure/role-based-access-control/custom-roles) 

- [Meer informatie over de bewerkingen van Azure Database for PostgreSQL resource provider](https://docs.microsoft.com/azure/role-based-access-control/resource-provider-operations#microsoftdbforpostgresql) 

- [Toegangs beheer voor Azure Database for PostgreSQL](https://docs.microsoft.com/azure/postgresql/concepts-security#access-management])

- [Gebruikers maken in Azure Database for PostgreSQL-grootschalige (Citus)](https://docs.microsoft.com/azure/postgresql/howto-hyperscale-create-users)

- [Verbinding maken met PostgreSQL-grootschalige (Citus) met behulp van psql](https://docs.microsoft.com/azure/postgresql/quickstart-create-hyperscale-portal#connect-to-the-database-using-psql)


**Azure Security Center bewaking**: niet van toepassing

**Verantwoordelijkheid**: klant

### <a name="32-change-default-passwords-where-applicable"></a>3,2: standaard wachtwoorden wijzigen indien van toepassing

**Hulp**: Azure AD heeft niet het concept van standaard wachtwoorden. Andere Azure-resources die een wacht woord vereisen, moeten een wacht woord afdwingen voor het maken van complexiteits vereisten en een minimale wachtwoord lengte, die afhankelijk is van de service. U bent verantwoordelijk voor toepassingen van derden en Marketplace-services die standaard wachtwoorden kunnen gebruiken.

**Azure Security Center bewaking**: niet van toepassing

**Verantwoordelijkheid**: klant

### <a name="33-use-dedicated-administrative-accounts"></a>3,3: speciale beheerders accounts gebruiken

**Richt lijnen**: Maak standaard procedures voor het gebruik van specifieke beheerders accounts die worden gebruikt voor toegang tot uw grootschalige-exemplaren (Citus). De beheerders accounts voor het beheren van de Azure-resource zijn gekoppeld aan Azure Active Directory. er zijn ook lokale server beheerders accounts die zich in de grootschalige-Server groep (Citus) bevinden voor het beheren van toegangs machtigingen voor de data base. Gebruik Azure Security Center identiteits-en toegangs beheer om het aantal beheerders accounts in Azure Active Directory te bewaken.

- [Inzicht in Azure Security Center identiteit en toegang](https://docs.microsoft.com/azure/security-center/security-center-identity-access) 

- [Gebruikers maken in Azure Database for PostgreSQL-grootschalige (Citus)](https://docs.microsoft.com/azure/postgresql/howto-hyperscale-create-users)

**Azure Security Center bewaking**: niet van toepassing

**Verantwoordelijkheid**: klant

### <a name="35-use-multi-factor-authentication-for-all-azure-active-directory-based-access"></a>3,5: multi-factor Authentication gebruiken voor alle op Azure Active Directory gebaseerde toegang

**Hulp**: voor toegang tot de Azure Portal Azure Active Directory multi-factor Authentication (MFA) in te scha kelen en Azure Security Center aanbevelingen voor identiteits-en toegangs beheer te volgen.

- [MFA inschakelen in azure](https://docs.microsoft.com/azure/active-directory/authentication/howto-mfa-getstarted)

- [Identiteit en toegang bewaken in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-identity-access)


**Azure Security Center bewaking**: Ja

**Verantwoordelijkheid**: klant

### <a name="36-use-dedicated-machines-privileged-access-workstations-for-all-administrative-tasks"></a>3,6: gebruik speciale machines (privileged Access workstations) voor alle beheer taken

**Hulp**: gebruik Paw's (privileged Access workstations) met multi-factor Authentication (MFA) die zijn geconfigureerd voor aanmelding bij en configureren van Azure-resources.

- [Meer informatie over privileged Access workstations](https://docs.microsoft.com/windows-server/identity/securing-privileged-access/privileged-access-workstations)

- [MFA inschakelen in azure](https://docs.microsoft.com/azure/active-directory/authentication/howto-mfa-getstarted)


**Azure Security Center bewaking**: niet van toepassing

**Verantwoordelijkheid**: klant

### <a name="37-alert-on-account-login-behavior-deviation"></a>3,7: waarschuwing voor de afwijking van het aanmeldings gedrag van accounts

**Hulp**: gebruik Azure Active Directory (AD) PRIVILEGED Identity Management (PIM) voor het genereren van Logboeken en waarschuwingen wanneer verdachte of onveilige activiteiten in de omgeving worden uitgevoerd.

Gebruik Azure AD-risico detecties om waarschuwingen en rapporten weer te geven over Risk ante gebruikers gedrag.

- [Privileged Identity Management implementeren (PIM)](https://docs.microsoft.com/azure/active-directory/privileged-identity-management/pim-deployment-plan)

- [Meer informatie over Azure AD-risico detectie](https://docs.microsoft.com/azure/active-directory/reports-monitoring/concept-risk-events)


**Azure Security Center bewaking**: niet van toepassing

**Verantwoordelijkheid**: klant

### <a name="38-manage-azure-resources-from-only-approved-locations"></a>3,8: Azure-resources alleen beheren vanaf goedgekeurde locaties

**Richt lijnen**: Gebruik voorwaardelijke toegang met de naam locaties om portal en Azure Resource Manager toegang alleen te bieden vanuit specifieke logische groepen met IP-adresbereiken of landen/regio's.

- [Benoemde locaties configureren in azure](https://docs.microsoft.com/azure/active-directory/reports-monitoring/quickstart-configure-named-locations)

**Azure Security Center bewaking**: niet van toepassing

**Verantwoordelijkheid**: klant

### <a name="39-use-azure-active-directory"></a>3,9: Azure Active Directory gebruiken

**Hulp**: gebruik Azure Active Directory (AD) als centrale verificatie-en autorisatie systeem voor het beheren van postgresql-resources. Azure AD beveiligt gegevens door gebruik te maken van sterke versleuteling voor gegevens in rust en onderweg. Azure AD bevat ook zouten, hashes en veilige gebruikers referenties.

Gebruikers binnen een grootschalige-Server groep (Citus) kunnen niet rechtstreeks aan Azure Active Directory accounts worden gekoppeld. Als u de gebruikers bevoegdheden voor database object toegang wilt wijzigen, gebruikt u de standaard PostgreSQL-opdrachten met hulpprogram ma's als PgAdmin of psql.

- [Bevoegdheden voor gebruikers rollen wijzigen](https://docs.microsoft.com/azure/postgresql/howto-hyperscale-create-users#how-to-modify-privileges-for-user-role)

- [Een AAD-exemplaar maken en configureren](https://docs.microsoft.com/azure/active-directory/fundamentals/active-directory-access-create-new-tenant)



**Azure Security Center bewaking**: niet van toepassing

**Verantwoordelijkheid**: klant

### <a name="310-regularly-review-and-reconcile-user-access"></a>3,10: regel matig gebruikers toegang controleren en afstemmen

**Richt lijnen**: de toegang controleren en afstemmen voor zowel gebruikers die toegang hebben tot de lokale Data Base als via Azure Active Directory voor het beheren van postgresql-resources.

Raadpleeg de logboeken van de Azure Active Directory (AD) voor gebruikers met toegang tot het beheren van data base Azure-resources om verouderde accounts te detecteren. Daarnaast kunt u Azure Identity Access revisies gebruiken om groepslid maatschappen efficiënt te beheren, toegang te krijgen tot bedrijfs toepassingen die kunnen worden gebruikt voor toegang tot grootschalige (Citus) en roltoewijzingen. Gebruikers toegang moet regel matig worden gecontroleerd, bijvoorbeeld elke 90 dagen, om ervoor te zorgen dat alleen de juiste gebruikers toegang hebben.

- [PostgreSQL-gebruikers en toegewezen rollen controleren](https://www.postgresql.org/docs/current/database-roles.html)

- [Meer informatie over Azure AD-rapportage](https://docs.microsoft.com/azure/active-directory/reports-monitoring/)

- [Beoordelingen over Azure Identity Access gebruiken](https://docs.microsoft.com/azure/active-directory/governance/access-reviews-overview)

**Azure Security Center bewaking**: Ja

**Verantwoordelijkheid**: klant

### <a name="311-monitor-attempts-to-access-deactivated-credentials"></a>3,11: controle pogingen om toegang te krijgen tot gedeactiveerde referenties

**Hulp**: in azure Active Directory (AD) hebt u toegang tot de logboeken van Azure AD-aanmeldings activiteiten, controle en risico gebeurtenissen, waarmee u kunt integreren met elk Siem/bewakings programma. 

U kunt dit proces stroom lijnen door Diagnostische instellingen voor Azure Active Directory gebruikers accounts te maken en de audit logboeken en aanmeldings logboeken te verzenden naar een Log Analytics-werk ruimte. U kunt de gewenste waarschuwingen configureren in Log Analytics werk ruimte. 

- [Azure-activiteiten logboeken integreren in Azure Monitor](https://docs.microsoft.com/azure/active-directory/reports-monitoring/howto-integrate-activity-logs-with-log-analytics)


**Azure Security Center bewaking**: niet van toepassing

**Verantwoordelijkheid**: klant

### <a name="312-alert-on-account-sign-in-behavior-deviation"></a>3,12: waarschuwing voor de afwijking van het aanmeldings gedrag van het account

**Hulp**: gebruik de functies voor identiteits beveiliging en risico detectie van Azure Active Directory om automatische antwoorden te configureren op gedetecteerde verdachte acties op het niveau van de Azure Active Directory (AD). U kunt automatische antwoorden via Azure Sentinel inschakelen voor het implementeren van de beveiligings reacties van uw organisatie.

U kunt ook logboeken opnemen in azure Sentinel voor verder onderzoek.

- [Overzicht van Azure AD Identity Protection](https://docs.microsoft.com/azure/active-directory/identity-protection/overview-identity-protection)

- [Risk ante aanmeldingen voor Azure AD weer geven](https://docs.microsoft.com/azure/active-directory/reports-monitoring/concept-risk-events)

- [Azure-Sentinel onboarden](https://docs.microsoft.com/azure/sentinel/quickstart-onboard)

**Azure Security Center bewaking**: niet van toepassing

**Verantwoordelijkheid**: klant

### <a name="313-provide-microsoft-with-access-to-relevant-customer-data-during-support-scenarios"></a>3,13: micro soft biedt toegang tot relevante klant gegevens tijdens ondersteunings scenario's

**Hulp**: momenteel niet beschikbaar; Klanten-lockbox wordt nog niet ondersteund voor grootschalige (Citus).

- [Lijst met door Klanten-lockbox ondersteunde services](https://docs.microsoft.com/azure/security/fundamentals/customer-lockbox-overview#supported-services-and-scenarios-in-general-availability)

**Azure Security Center bewaking**: momenteel niet beschikbaar

**Verantwoordelijkheid**: momenteel niet beschikbaar

## <a name="data-protection"></a>Gegevensbeveiliging

*Zie [beveiligings beheer: gegevens beveiliging](/azure/security/benchmarks/security-control-data-protection)voor meer informatie.*

### <a name="41-maintain-an-inventory-of-sensitive-information"></a>4,1: een inventaris van gevoelige informatie onderhouden

**Hulp**: Labels gebruiken bij het traceren van grootschalige-exemplaren (Citus) of gerelateerde resources die gevoelige informatie opslaan of verwerken.

- [Tags maken en gebruiken](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags)

**Azure Security Center bewaking**: niet van toepassing

**Verantwoordelijkheid**: klant

### <a name="42-isolate-systems-storing-or-processing-sensitive-information"></a>4,2: systemen isoleren die gevoelige informatie opslaan of verwerken

**Richt lijnen**: afzonderlijke abonnementen en/of beheer groepen implementeren voor ontwikkeling, testen en productie. Gebruik een combi natie van beheerders rollen en firewall regels om netwerk toegang tot uw Azure Database for PostgreSQL-instanties te isoleren en te beperken.

- [Aanvullende Azure-abonnementen maken](https://docs.microsoft.com/azure/billing/billing-create-subscription)

- [Beheergroepen maken](https://docs.microsoft.com/azure/governance/management-groups/create)

- [Informatie over Firewall regels in Azure Database for PostgreSQL-grootschalige (Citus)](https://docs.microsoft.com/azure/postgresql/concepts-hyperscale-firewall-rules)

- [Rollen begrijpen in grootschalige (Citus)](https://docs.microsoft.com/azure/postgresql/howto-hyperscale-create-users)

**Azure Security Center bewaking**: niet van toepassing

**Verantwoordelijkheid**: klant

### <a name="44-encrypt-all-sensitive-information-in-transit"></a>4,4: alle gevoelige gegevens in de overdracht versleutelen

**Richt lijnen**: voor client toepassings verbindingen met het grootschalige (Citus)-knoop punt is Transport Layer Security (TLS) 1,2 vereist. Het afdwingen van TLS-verbindingen tussen uw database server en uw client toepassingen helpt bij het beveiligen van ' man-in-the-middle '-aanvallen door de gegevens stroom tussen de server en uw toepassing te versleutelen.

Voor alle Azure Database for PostgreSQL servers die via de Azure Portal worden ingericht, wordt het afdwingen van TLS-verbindingen standaard ingeschakeld.

In sommige gevallen vereist toepassingen van derden een lokaal certificaat bestand dat is gegenereerd op basis van een certificaat bestand van een vertrouwde certificerings instantie (. CER) om veilig verbinding te kunnen maken.

- [TLS configureren in Azure Database for PostgreSQL-grootschalige (Citus)](https://docs.microsoft.com/azure/postgresql/concepts-hyperscale-ssl-connection-security)

- [Toepassingen waarvoor certificaat verificatie voor TLS-connectiviteit is vereist](https://docs.microsoft.com/azure/postgresql/concepts-hyperscale-ssl-connection-security)



**Azure Security Center bewaking**: Ja

**Verantwoordelijkheid**: gedeeld

### <a name="46-use-azure-rbac-to-control-access-to-resources"></a>4,6: Azure RBAC gebruiken om de toegang tot resources te beheren

**Richt lijnen**: gebruik Azure RBAC (op rollen gebaseerd toegangs beheer) om de toegang tot het besturings element grootschalige (Citus) (bijvoorbeeld Azure Portal) te beheren. Azure RBAC heeft geen invloed op de gebruikers machtigingen binnen de data base.

Als u de gebruikers bevoegdheden op database niveau wilt wijzigen, gebruikt u de standaard PostgreSQL-opdrachten met een hulp programma zoals PgAdmin of psql.

- [Azure RBAC configureren](https://docs.microsoft.com/azure/role-based-access-control/role-assignments-portal)

- [Gebruikers toegang configureren met SQL voor Azure Database for PostgreSQL](https://docs.microsoft.com/azure/postgresql/howto-hyperscale-create-users)


**Azure Security Center bewaking**: Ja

**Verantwoordelijkheid**: klant

### <a name="48-encrypt-sensitive-information-at-rest"></a>4,8: gevoelige informatie op rest versleutelen

**Hulp**:  
Azure Database for PostgreSQL grootschalige (Citus) heeft ten minste één keer per dag een moment opname van gegevens bestanden en het transactie logboek van de data base. Met de back-ups kunt u een server herstellen naar elk gewenst moment binnen de Bewaar periode. (De Bewaar periode is momenteel 35 dagen voor alle clusters.) Alle back-ups worden versleuteld met AES 256-bits versleuteling. De PostgreSQL grootschalige (Citus)-aanbieding maakt gebruik van door micro soft beheerde sleutels voor versleuteling.

- [Informatie over versleuteling voor Azure PostgreSQL-grootschalige (Citus)-back-ups](https://docs.microsoft.com/azure/postgresql/concepts-hyperscale-backup)



**Azure Security Center bewaking**: niet van toepassing

**Verantwoordelijkheid**: gedeeld

### <a name="49-log-and-alert-on-changes-to-critical-azure-resources"></a>4,9: wijzigingen in essentiële Azure-resources vastleggen en waarschuwen

**Hulp**: gebruik Azure monitor met het Azure-activiteiten logboek om waarschuwingen te maken wanneer wijzigingen worden aangebracht in productie-exemplaren van grootschalige (Citus) en andere essentiële of verwante resources.

- [Waarschuwingen maken voor gebeurtenissen in het Azure-activiteiten logboek](https://docs.microsoft.com/azure/azure-monitor/platform/alerts-activity-log)

**Azure Security Center bewaking**: Ja

**Verantwoordelijkheid**: klant

## <a name="vulnerability-management"></a>Beheer van beveiligingsproblemen

*Zie [beveiligings beheer: beveiligingslek beheer](/azure/security/benchmarks/security-control-vulnerability-management)voor meer informatie.*

### <a name="51-run-automated-vulnerability-scanning-tools"></a>5,1: automatische hulpprogram ma's voor het scannen van beveiligings problemen uitvoeren

**Hulp**: momenteel niet beschikbaar; Azure Security Center biedt nog geen ondersteuning voor de evaluatie van beveiligings problemen voor Azure Database for PostgreSQL-grootschalige (Citus).

- [Functie dekking voor Azure PaaS Services in Azure Security Center](https://docs.microsoft.com/azure/security-center/features-paas)

**Azure Security Center bewaking**: momenteel niet beschikbaar

**Verantwoordelijkheid**: momenteel niet beschikbaar

## <a name="inventory-and-asset-management"></a>Inventarisatie en asset-management

*Zie voor meer informatie [beveiligings beheer: inventarisatie en activa beheer](/azure/security/benchmarks/security-control-inventory-asset-management).*

### <a name="61-use-automated-asset-discovery-solution"></a>6,1: automatische Asset-detectie oplossing gebruiken

**Hulp**: Azure resource Graph gebruiken om alle resources (inclusief grootschalige (Citus)-instanties) binnen uw abonnement (en) te doorzoeken en te detecteren. Zorg ervoor dat u de juiste machtigingen (lezen) hebt in uw Tenant en dat u alle Azure-abonnementen kunt inventariseren, evenals de resources in uw abonnementen.

- [Query's maken met Azure Graph](https://docs.microsoft.com/azure/governance/resource-graph/first-query-portal)

- [Uw Azure-abonnementen weer geven](https://docs.microsoft.com/powershell/module/az.accounts/get-azsubscription?view=azps-3.0.0)

- [Meer informatie over Azure RBAC](https://docs.microsoft.com/azure/role-based-access-control/overview)

**Azure Security Center bewaking**: niet van toepassing

**Verantwoordelijkheid**: klant

### <a name="62-maintain-asset-metadata"></a>6,2: meta gegevens van activa onderhouden

**Richt lijnen**: Tags Toep assen op grootschalige (Citus) en andere gerelateerde resources die meta gegevens geven om ze logisch in een taxonomie te organiseren.

- [Tags maken en gebruiken](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags)

**Azure Security Center bewaking**: niet van toepassing

**Verantwoordelijkheid**: klant

### <a name="63-delete-unauthorized-azure-resources"></a>6,3: niet-geautoriseerde Azure-resources verwijderen

**Richt lijnen**: Gebruik labels, beheer groepen en afzonderlijke abonnementen, indien van toepassing, om grootschalige-exemplaren (Citus) en gerelateerde resources te organiseren en bij te houden. Sluit de inventaris regel matig af en zorg ervoor dat niet-geautoriseerde resources tijdig worden verwijderd uit het abonnement.

- [Aanvullende Azure-abonnementen maken](https://docs.microsoft.com/azure/billing/billing-create-subscription)

- [Beheergroepen maken](https://docs.microsoft.com/azure/governance/management-groups/create)

- [Tags maken en gebruiken](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags)

**Azure Security Center bewaking**: niet van toepassing

**Verantwoordelijkheid**: klant

### <a name="64-define-and-maintain-inventory-of-approved-azure-resources"></a>6,4: de inventaris van goedgekeurde Azure-resources definiëren en onderhouden

**Hulp: Azure**Policy gebruiken om beperkingen te geven aan het type resources dat kan worden gemaakt in klant abonnement (en) met de volgende ingebouwde beleids definities:

- Niet toegestane resourcetypen

- Toegestane brontypen

Daarnaast gebruikt u de resource grafiek van Azure voor het opvragen/detecteren van resources binnen een of meer abonnementen.

- [Azure Policy configureren en beheren](https://docs.microsoft.com/azure/governance/policy/tutorials/create-and-manage)

- [Query's maken met Azure Graph](https://docs.microsoft.com/azure/governance/resource-graph/first-query-portal)


**Azure Security Center bewaking**: niet van toepassing

**Verantwoordelijkheid**: klant

### <a name="65-monitor-for-unapproved-azure-resources"></a>6,5: monitor voor niet-goedgekeurde Azure-resources

**Hulp: Azure**Policy gebruiken om beperkingen te geven aan het type resources dat kan worden gemaakt in klant abonnement (en) met de volgende ingebouwde beleids definities:

- Niet toegestane resourcetypen
- Toegestane brontypen

Daarnaast gebruikt u de resource grafiek van Azure voor het opvragen/detecteren van resources binnen een of meer abonnementen.

- [Azure Policy configureren en beheren](https://docs.microsoft.com/azure/governance/policy/tutorials/create-and-manage)

- [Query's maken met Azure Graph](https://docs.microsoft.com/azure/governance/resource-graph/first-query-portal)

**Azure Security Center bewaking**: niet van toepassing

**Verantwoordelijkheid**: klant

### <a name="69-use-only-approved-azure-services"></a>6,9: alleen goedgekeurde Azure-Services gebruiken

**Hulp: Azure**Policy gebruiken om beperkingen te geven aan het type resources dat kan worden gemaakt in klant abonnement (en) met de volgende ingebouwde beleids definities:

- Niet toegestane resourcetypen
- Toegestane brontypen

- [Azure Policy configureren en beheren](https://docs.microsoft.com/azure/governance/policy/tutorials/create-and-manage)

- [Een specifiek resource type weigeren met Azure Policy](https://docs.microsoft.com/azure/governance/policy/samples/not-allowed-resource-types)

**Azure Security Center bewaking**: niet van toepassing

**Verantwoordelijkheid**: klant

### <a name="611-limit-users-ability-to-interact-with-azure-resource-manager"></a>6,11: de mogelijkheid van gebruikers om te communiceren met Azure Resource Manager beperken

**Richt lijnen**: gebruik de voorwaardelijke toegang van Azure om gebruikers de mogelijkheid te bieden om te communiceren met Azure Resource Manager door ' blok toegang ' te configureren voor de app Microsoft Azure management. Dit kan ertoe leiden dat het maken en wijzigen van bronnen binnen een omgeving met hoge beveiliging, zoals instanties van grootschalige (Citus) die gevoelige informatie bevatten, wordt voor komen.

- [Voorwaardelijke toegang configureren om de toegang tot Azure Resource Manager te blok keren](https://docs.microsoft.com/azure/role-based-access-control/conditional-access-azure-management)

**Azure Security Center bewaking**: niet van toepassing

**Verantwoordelijkheid**: klant

## <a name="secure-configuration"></a>Veilige configuratie

*Zie [beveiligings beheer: beveiligde configuratie](/azure/security/benchmarks/security-control-secure-configuration)voor meer informatie.*

### <a name="71-establish-secure-configurations-for-all-azure-resources"></a>7,1: veilige configuraties instellen voor alle Azure-resources

**Hulp**: Definieer en implementeer standaard beveiligings configuraties voor uw grootschalige-exemplaren (Citus) met Azure Policy. Gebruik Azure Policy om aangepaste beleids regels te maken om de netwerk configuratie van uw Azure Database for PostgreSQL instanties te controleren of af te dwingen.

Azure Resource Manager heeft ook de mogelijkheid om de sjabloon in JavaScript Object Notation (JSON) te exporteren, die moet worden gecontroleerd om ervoor te zorgen dat de configuraties voldoen aan de beveiligings vereisten voor uw organisatie of deze overschrijden. 

- [Beschik bare Azure Policy aliassen weer geven](https://docs.microsoft.com/powershell/module/az.resources/get-azpolicyalias?view=azps-3.3.0)

- [Azure Policy configureren en beheren](https://docs.microsoft.com/azure/governance/policy/tutorials/create-and-manage)

- [Eén en meerdere resources exporteren naar een sjabloon in Azure Portal](https://docs.microsoft.com/azure/azure-resource-manager/templates/export-template-portal) 



**Azure Security Center bewaking**: niet van toepassing

**Verantwoordelijkheid**: klant

### <a name="73-maintain-secure-azure-resource-configurations"></a>7,3: Beveilig Azure-resource configuraties onderhouden

**Richt lijnen**: gebruik Azure Policy [deny] en [implementeren indien niet aanwezig] voor het afdwingen van beveiligde instellingen voor uw Azure-resources.  Daarnaast kunt u Azure Resource Manager sjablonen gebruiken om de beveiligings configuratie van uw Azure-resources te onderhouden die uw organisatie nodig heeft. 

- [Azure Policy effecten begrijpen](https://docs.microsoft.com/azure/governance/policy/concepts/effects)

- [Beleidsregels voor het afdwingen van naleving maken en beheren](https://docs.microsoft.com/azure/governance/policy/tutorials/create-and-manage)

- [Overzicht van Azure Resource Manager sjablonen](https://docs.microsoft.com/azure/azure-resource-manager/templates/overview)



**Azure Security Center bewaking**: niet van toepassing

**Verantwoordelijkheid**: klant

### <a name="75-securely-store-configuration-of-azure-resources"></a>7,5: de configuratie van Azure-resources veilig opslaan

**Richt lijnen**: als u aangepaste Azure-beleids definities gebruikt voor uw grootschalige-exemplaren (Citus) en gerelateerde resources, gebruikt u Azure opslag plaatsen om uw code veilig op te slaan en te beheren.

- [Code opslaan in azure DevOps](https://docs.microsoft.com/azure/devops/repos/git/gitworkflow?view=azure-devops)

- [Documentatie voor Azure opslag plaatsen](https://docs.microsoft.com/azure/devops/repos/index?view=azure-devops)

**Azure Security Center bewaking**: niet van toepassing

**Verantwoordelijkheid**: klant

### <a name="77-deploy-configuration-management-tools-for-azure-resources"></a>7,7: hulpprogram ma's voor configuratie beheer voor Azure-resources implementeren

**Richt lijnen**: gebruik Azure Policy [deny] en [implementeren indien niet aanwezig] voor het afdwingen van beveiligde instellingen voor uw Azure-resources.  Daarnaast kunt u Azure Resource Manager sjablonen gebruiken om de beveiligings configuratie van uw Azure-resources te onderhouden die uw organisatie nodig heeft. 

- [Azure Policy effecten begrijpen](https://docs.microsoft.com/azure/governance/policy/concepts/effects)

- [Beleidsregels voor het afdwingen van naleving maken en beheren](https://docs.microsoft.com/azure/governance/policy/tutorials/create-and-manage)

- [Overzicht van Azure Resource Manager sjablonen](https://docs.microsoft.com/azure/azure-resource-manager/templates/overview)



**Azure Security Center bewaking**: niet van toepassing

**Verantwoordelijkheid**: klant

### <a name="79-implement-automated-configuration-monitoring-for-azure-resources"></a>7,9: geautomatiseerde configuratie bewaking voor Azure-resources implementeren

**Hulp**: gebruik Azure Policy aliassen in de naam ruimte ' micro soft. DBforPostgreSQL ' om aangepaste beleids regels te maken om systeem configuraties te Signa lering, te controleren en af te dwingen. Gebruik Azure Policy [audit], [deny] en [implementeren indien niet aanwezig] om automatisch configuraties af te dwingen voor uw Azure Database for PostgreSQL instanties en gerelateerde resources.

- [Azure Policy configureren en beheren](https://docs.microsoft.com/azure/governance/policy/tutorials/create-and-manage)

**Azure Security Center bewaking**: niet van toepassing

**Verantwoordelijkheid**: klant

### <a name="712-manage-identities-securely-and-automatically"></a>7,12: identiteiten veilig en automatisch beheren

**Hulp**: Azure database for PostgreSQL-grootschalige (Citus) biedt momenteel geen rechtstreekse ondersteuning voor beheerde identiteiten. Tijdens het maken van de Azure Database for PostgreSQL-server moet u referenties opgeven voor een beheerders gebruiker. U kunt aanvullende gebruikers rollen maken in de Azure Portal-interface.

- [Een Azure Database for PostgreSQL-grootschalige maken (Citus)](https://docs.microsoft.com/azure/postgresql/quickstart-create-hyperscale-portal#create-an-azure-database-for-postgresql---hyperscale-citus)

- [Aanvullende gebruikers rollen maken](https://docs.microsoft.com/azure/postgresql/howto-hyperscale-create-users#how-to-create-additional-user-roles)


**Azure Security Center bewaking**: momenteel niet beschikbaar

**Verantwoordelijkheid**: momenteel niet beschikbaar

### <a name="713-eliminate-unintended-credential-exposure"></a>7,13: onbedoelde referentie blootstelling elimineren

**Richt lijnen**: referentie scanner implementeren om referenties in code te identificeren. Referentie scanner stimuleert ook het verplaatsen van gedetecteerde referenties naar veiliger locaties, zoals Azure Key Vault.

- [Referentie scanner instellen](https://secdevtools.azurewebsites.net/helpcredscan.html)

**Azure Security Center bewaking**: niet van toepassing

**Verantwoordelijkheid**: klant

## <a name="malware-defense"></a>Beveiliging tegen malware

*Zie [beveiligings beheer: verdediging tegen malware](/azure/security/benchmarks/security-control-malware-defense)voor meer informatie.*

### <a name="82-pre-scan-files-to-be-uploaded-to-non-compute-azure-resources"></a>8,2: scan bestanden die moeten worden geüpload naar niet-reken resources van Azure

**Hulp**: micro soft anti-malware is ingeschakeld op de onderliggende host die ondersteuning biedt voor Azure-Services, bijvoorbeeld grootschalige (Citus), maar wordt niet uitgevoerd op de inhoud van de klant.

Scan vooraf op inhoud die wordt geüpload naar niet-reken resources van Azure, zoals App Service, Data Lake Storage, Blob Storage, Azure Database for PostgreSQL, enzovoort. Micro soft heeft geen toegang tot uw gegevens in deze instanties.

**Azure Security Center bewaking**: niet van toepassing

**Verantwoordelijkheid**: klant

## <a name="data-recovery"></a>Gegevensherstel

*Zie [beveiligings beheer: gegevens herstel](/azure/security/benchmarks/security-control-data-recovery)voor meer informatie.*

### <a name="91-ensure-regular-automated-back-ups"></a>9,1: controleren op regel matige automatische back-ups

**Hulp**: met Azure database for PostgreSQL – grootschalige (Citus) worden automatisch back-ups gemaakt van elk knoop punt en opgeslagen in lokaal redundante opslag. Back-ups kunnen worden gebruikt om uw grootschalige-cluster (Citus) naar een opgegeven tijd te herstellen.

- [Back-up en herstel in Azure Database for PostgreSQL-grootschalige (Citus)](https://docs.microsoft.com/azure/postgresql/concepts-hyperscale-backup)

**Azure Security Center bewaking**: Ja

**Verantwoordelijkheid**: klant

### <a name="92-perform-complete-system-backups-and-backup-any-customer-managed-keys"></a>9,2: volledige back-ups van het systeem uitvoeren en een back-up maken van door de klant beheerde sleutels

**Richt lijnen**: ten minste één keer per dag Azure database for PostgreSQL moment opname back-ups van gegevens bestanden en het transactie logboek van de data base. Met de back-ups kunt u een server herstellen naar elk gewenst moment binnen de Bewaar periode. De retentie periode is momenteel 35 dagen voor alle clusters. Alle back-ups worden versleuteld met AES 256-bits versleuteling.

In azure-regio's die beschikbaarheids zones ondersteunen, worden back-upmomentopnamen opgeslagen in drie beschikbaarheids zones. Zolang er ten minste één beschikbaarheids zone online is, is het grootschalige-cluster (Citus) te herstorbaar.

- [Back-up en herstel in Azure Database for PostgreSQL-grootschalige (Citus)](https://docs.microsoft.com/azure/postgresql/concepts-hyperscale-backup)


**Azure Security Center bewaking**: Ja

**Verantwoordelijkheid**: klant

### <a name="93-validate-all-backups-including-customer-managed-keys"></a>9,3: alle back-ups valideren, inclusief door de klant beheerde sleutels

**Richt lijnen**: bij het herstellen van een grootschalige-cluster (Citus) wordt in azure database for PostgreSQL een nieuw cluster gemaakt op basis van de back-ups van de oorspronkelijke knoop punten. U kunt in de afgelopen 35 dagen een cluster herstellen naar elk gewenst moment. Het herstel proces maakt een nieuw cluster in dezelfde Azure-regio, hetzelfde abonnement en dezelfde resource groep als het origineel. De nieuwe cluster configuratie is hetzelfde als de oorspronkelijke cluster configuratie: hetzelfde aantal knoop punten, aantal vCores, opslag grootte en gebruikers rollen.

Firewall-instellingen en PostgreSQL-server parameters blijven niet behouden van de oorspronkelijke server groep. ze worden opnieuw ingesteld op de standaard waarden. De firewall voor komt dat alle verbindingen. U moet deze instellingen na het herstellen hand matig aanpassen.

- [Back-up en herstel in Azure Database for PostgreSQL-grootschalige (Citus)](https://docs.microsoft.com/azure/postgresql/concepts-hyperscale-backup)

**Azure Security Center bewaking**: Ja

**Verantwoordelijkheid**: klant

### <a name="94-ensure-protection-of-backups-and-customer-managed-keys"></a>9,4: zorg voor de bescherming van back-ups en door de klant beheerde sleutels

**Hulp**: verwijderde grootschalige-clusters (Citus) kunnen niet worden hersteld. Als u het cluster verwijdert, worden alle knoop punten die deel uitmaken van het cluster, verwijderd en kunnen ze niet worden hersteld. Voor het beveiligen van cluster bronnen na de implementatie van onopzettelijk verwijderen of onverwachte wijzigingen, kunnen beheerders gebruikmaken van beheer vergrendelingen.

- [Back-up en herstel in Azure Database for PostgreSQL-grootschalige (Citus)](https://docs.microsoft.com/azure/postgresql/concepts-hyperscale-backup)

**Azure Security Center bewaking**: momenteel niet beschikbaar

**Verantwoordelijkheid**: klant

## <a name="incident-response"></a>Reageren op incidenten

*Zie voor meer informatie [beveiligings beheer: reactie op incidenten](/azure/security/benchmarks/security-control-incident-response).*

### <a name="101-create-an-incident-response-guide"></a>10,1: een hand leiding voor reactie op incidenten maken

**Hulp**: een antwoord gids voor incidenten maken voor uw organisatie. Zorg ervoor dat er schriftelijke incidenten abonnementen zijn die alle werk rollen definiëren, evenals fasen van incident handling/management van detectie tot een beoordeling van het incident. 

- [Werk stroom automatisering configureren in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-planning-and-operations-guide) 

- [Richt lijnen voor het bouwen van uw eigen beveiligings incident antwoord proces](https://msrc-blog.microsoft.com/2019/07/01/inside-the-msrc-building-your-own-security-incident-response-process/) 

- [Micro soft Security Response Center anatomie van een incident](https://msrc-blog.microsoft.com/2019/07/01/inside-the-msrc-building-your-own-security-incident-response-process/) 

- [Klant kan ook gebruikmaken van de hand leiding voor de verwerking van het computer beveiligings incident van het NIST om hulp te bieden bij het maken van een eigen incident respons plan](https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-61r2.pdf)

**Azure Security Center bewaking**: niet van toepassing

**Verantwoordelijkheid**: klant

### <a name="102-create-an-incident-scoring-and-prioritization-procedure"></a>10,2: een beoordelings procedure voor incidenten en prioriteits procedures maken

**Hulp**: Security Center wijst aan elke waarschuwing een Ernst toe om u te helpen bepalen welke waarschuwingen het eerst moeten worden onderzocht. De ernst is gebaseerd op de manier waarop vertrouwen Security Center is in de zoek actie of het analyse programma dat wordt gebruikt om de waarschuwing te geven, evenals het betrouwbaarheids niveau dat er schadelijke bedoelingen zijn achter de activiteit die tot de waarschuwing heeft geleid. 

Daarnaast kunt u ook duidelijk abonnementen markeren (voor bijvoorbeeld productie, niet-productie) en maak een naamgevings systeem om Azure-resources duidelijk te identificeren en te categoriseren.

**Azure Security Center bewaking**: niet van toepassing

**Verantwoordelijkheid**: klant

### <a name="103-test-security-response-procedures"></a>10,3: procedures voor beveiligings antwoorden testen

**Richt lijnen**: oefent oefeningen uit om de respons mogelijkheden van uw systeem op een gewone uitgebracht te testen. Identificeer zwakke punten en tussen ruimten en wijzig zo nodig het schema. 

- [Raadpleeg de publicatie van het NIST: hand leiding voor het testen, trainen en uitoefenen van Program Ma's voor IT-plannen en-mogelijkheden](https://nvlpubs.nist.gov/nistpubs/Legacy/SP/nistspecialpublication800-84.pdf)

**Azure Security Center bewaking**: niet van toepassing

**Verantwoordelijkheid**: klant

### <a name="104-provide-security-incident-contact-details-and-configure-alert-notifications-for-security-incidents"></a>10,4: contact gegevens van het beveiligings incident opgeven en waarschuwings meldingen configureren voor beveiligings incidenten

**Hulp**: contact gegevens van beveiligings incidenten worden door micro soft gebruikt om contact met u op te nemen als het micro soft Security Response Center (MSRC) detecteert dat de gegevens van de klant zijn geopend door een onrecht matige of niet-gemachtigde partij.  Bekijk incidenten na het feit om te controleren of de problemen zijn opgelost. 

- [De Azure Security Center Security-contact persoon instellen](https://docs.microsoft.com/azure/security-center/security-center-provide-security-contact-details)

**Azure Security Center bewaking**: Ja

**Verantwoordelijkheid**: klant

### <a name="105-incorporate-security-alerts-into-your-incident-response-system"></a>10,5: beveiligings waarschuwingen opnemen in uw reactie systeem van uw incident

**Richt lijnen**: uw Azure Security Center waarschuwingen en aanbevelingen exporteren met de functie continue export. Met doorlopend exporteren kunt u waarschuwingen en aanbevelingen hand matig of op een doorlopende manier exporteren. U kunt de Azure Security Center Data Connector gebruiken om de Sentinel van waarschuwingen te streamen. 

- [Continue export configureren](https://docs.microsoft.com/azure/security-center/continuous-export) 

- [Waarschuwingen streamen naar Azure Sentinel](https://docs.microsoft.com/azure/sentinel/connect-azure-security-center)

**Azure Security Center bewaking**: niet van toepassing

**Verantwoordelijkheid**: klant

### <a name="106-automate-the-response-to-security-alerts"></a>10,6: de reactie op beveiligings waarschuwingen automatiseren

**Hulp**: gebruik de functie werk stroom automatisering in azure Security Center om automatisch reacties te activeren via ' Logic apps ' in beveiligings waarschuwingen en aanbevelingen. 

- [Werk stroom automatisering en Logic Apps configureren](https://docs.microsoft.com/azure/security-center/workflow-automation)

**Azure Security Center bewaking**: niet van toepassing

**Verantwoordelijkheid**: klant

## <a name="penetration-tests-and-red-team-exercises"></a>Penetratietests en Red Team-oefeningen

*Zie voor meer informatie [Security Control: Indringings tests en Red team-oefeningen](/azure/security/benchmarks/security-control-penetration-tests-red-team-exercises).*

### <a name="111-conduct-regular-penetration-testing-of-your-azure-resources-and-ensure-remediation-of-all-critical-security-findings"></a>11,1: voert regel matig indringings tests van uw Azure-resources uit en zorgt voor herbemiddeling van alle essentiële beveiligings resultaten

**Richt lijnen**: Volg de micro soft-regels om ervoor te zorgen dat de indringings tests niet worden geschonden door het micro soft-beleid: https://www.microsoft.com/msrc/pentest-rules-of-engagement?rtc=1 

- [U vindt hier meer informatie over de strategie van micro soft en de uitvoering van Red Teaming en live site indringings tests met door micro soft beheerde Cloud infrastructuur,-services en-toepassingen.](https://gallery.technet.microsoft.com/Cloud-Red-Teaming-b837392e)

**Azure Security Center bewaking**: niet van toepassing

**Verantwoordelijkheid**: gedeeld

## <a name="next-steps"></a>Volgende stappen

- Zie de [Azure Security-Bench Mark](/azure/security/benchmarks/overview)
- Meer informatie over [Azure-beveiligings basislijnen](/azure/security/benchmarks/security-baselines-overview)
