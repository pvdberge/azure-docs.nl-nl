---
title: Logboek registratie en controle van Azure-beveiliging | Microsoft Docs
description: Meer informatie over de logboeken die beschikbaar zijn in Azure en de beveiligings inzichten die u kunt krijgen.
services: security
documentationcenter: na
author: TerryLanfear
manager: rkarlin
editor: TomSh
ms.assetid: ''
ms.service: security
ms.subservice: security-fundamentals
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/31/2019
ms.author: terrylan
ms.openlocfilehash: bd0f42507e22559690e2682a391c53b9c090aa6c
ms.sourcegitcommit: 877491bd46921c11dd478bd25fc718ceee2dcc08
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/02/2020
ms.locfileid: "75750785"
---
# <a name="azure-security-logging-and-auditing"></a>Azure-logboekregistratie en -controle van beveiligingsgegevens

Azure biedt een breed scala aan Configureer bare opties voor beveiligings controle en logboek registratie waarmee u hiaten in uw beveiligings beleid en-mechanismen kunt identificeren. In dit artikel vindt u informatie over het genereren, verzamelen en analyseren van beveiligings logboeken van services die worden gehost op Azure.

> [!Note]
> Bepaalde aanbevelingen in dit artikel kunnen leiden tot groter gegevens-, netwerk-of COMPUTE-gebruik en uw licentie-of abonnements kosten verhogen.

## <a name="types-of-logs-in-azure"></a>Typen logboeken in azure

Cloud toepassingen zijn complex met veel bewegende onderdelen. Logboek gegevens kunnen inzicht geven in uw toepassingen en u helpen bij het volgende:

- Problemen met eerdere problemen oplossen of mogelijke oorzaken
- Verbeter de prestaties of het onderhoud van toepassingen
- Acties automatiseren waarvoor anders hand matige interventie nodig zou zijn

Azure-logboeken zijn ingedeeld in de volgende typen:
* **Control/Management-logboeken** bevatten informatie over Azure Resource Manager Create-, update-en delete-bewerkingen. Zie [activiteiten logboeken van Azure](../../azure-monitor/platform/platform-logs-overview.md)voor meer informatie.

* **Gegevens vlak logboeken** bevatten informatie over gebeurtenissen die worden gegenereerd als onderdeel van het gebruik van Azure-resources. Voor beelden van dit type logboek zijn het Windows-gebeurtenis systeem, de beveiliging en toepassings Logboeken in een virtuele machine (VM) en de [Diagnostische logboeken](../../azure-monitor/platform/platform-logs-overview.md) die zijn geconfigureerd via Azure monitor.

* **Verwerkte gebeurtenissen** bieden informatie over geanalyseerde gebeurtenissen/waarschuwingen die namens u zijn verwerkt. Voor beelden van dit type zijn [Azure Security Center waarschuwingen](../../security-center/security-center-managing-and-responding-alerts.md) waarbij [Azure Security Center](../../security-center/security-center-intro.md) uw abonnement heeft verwerkt en geanalyseerd en beknopte beveiligings waarschuwingen biedt.

De volgende tabel bevat de belangrijkste typen logboeken die beschikbaar zijn in Azure:

| Logboekcategorie | Logboek type | Gebruik | Integratie |
| ------------ | -------- | ------ | ----------- |
|[Activiteiten logboeken](../../azure-monitor/platform/platform-logs-overview.md)|Gebeurtenissen op het vlak van het besturings element op Azure Resource Manager resources|  Biedt inzicht in de bewerkingen die zijn uitgevoerd voor de resources in uw abonnement.|    Rest API, [Azure monitor](../../azure-monitor/platform/platform-logs-overview.md)|
|[Azure-resource logboeken](../../azure-monitor/platform/platform-logs-overview.md)|Frequente gegevens over de werking van Azure Resource Manager resources in het abonnement|   Biedt inzicht in de bewerkingen die uw resource zelf heeft uitgevoerd.| Azure Monitor|
|[Azure Active Directory-rapportage](../../active-directory/reports-monitoring/overview-reports.md)|Logboeken en rapporten | Rapporteert aanmeldings activiteiten van gebruikers en informatie over systeem activiteiten over gebruikers en groeps beheer.|[Graph API](../../active-directory/develop/active-directory-graph-api-quickstart.md)|
|[Virtuele machines en Cloud Services](../../azure-monitor/learn/quick-collect-azurevm.md)|Windows Event Log-service en Linux syslog|  Legt systeem gegevens vast en registreert gegevens op de virtuele machines en brengt deze gegevens over naar een opslag account van uw keuze.|   Windows (met behulp van Windows Azure Diagnostics [[wad](../../monitoring-and-diagnostics/azure-diagnostics.md)]-opslag) en Linux in azure monitor|
|[Azure Opslaganalyse](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics)|Met opslag logboek registratie kunt u metrische gegevens voor een opslag account|Biedt inzicht in Trace-aanvragen, analyse van gebruiks trends en het vaststellen van problemen met uw opslag account.|   REST API of de [client bibliotheek](https://msdn.microsoft.com/library/azure/mt347887.aspx)|
|[Stroom logboeken voor netwerk beveiligings groepen (NSG)](../../network-watcher/network-watcher-nsg-flow-logging-overview.md)|JSON-indeling, geeft uitgaande en inkomende stromen per regel weer|Geeft informatie weer over binnenkomend en uitgaand IP-verkeer via een netwerk beveiligings groep.|[Azure Network Watcher](../../network-watcher/network-watcher-monitoring-overview.md)|
|[Toepassings inzicht](../../azure-monitor/app/app-insights-overview.md)|Logboeken, uitzonde ringen en aangepaste diagnostische gegevens|  Biedt een service voor het controleren van de prestaties van toepassingen (APM) voor webontwikkelaars op meerdere platforms.| REST API, [Power bi](https://powerbi.microsoft.com/documentation/powerbi-azure-and-power-bi/)|
|[Gegevens/beveiligings waarschuwingen verwerken](../../security-center/security-center-intro.md)|  Waarschuwingen voor Azure Security Center, Azure Monitor logboeken|    Geeft beveiligings informatie en waarschuwingen.|  REST Api's, JSON|

## <a name="log-integration-with-on-premises-siem-systems"></a>Integratie met on-premises SIEM-systemen vastleggen
Bij het [integreren van Security Center waarschuwingen](../../security-center/security-center-export-data-to-siem.md) wordt beschreven hoe u Security Center waarschuwingen, beveiligings gebeurtenissen voor virtuele machines die worden verzameld door Azure Diagnostics-logboeken en Azure-controle Logboeken kunt synchroniseren met uw Azure monitor Logboeken of Siem-oplossing.

## <a name="next-steps"></a>Volgende stappen

- [Controle en logboek registratie](management-monitoring-overview.md): Beveilig gegevens door zicht baarheid te behouden en snel te reageren op tijdige beveiligings waarschuwingen.

- [Beveiligings logboeken en audit-logboek verzameling in azure](https://azure.microsoft.com/resources/videos/security-logging-and-audit-log-collection/): afdwingen deze instellingen om ervoor te zorgen dat uw Azure-instanties de juiste beveiligings-en audit logboeken verzamelen.

- [Controle-instellingen voor een site verzameling configureren](https://support.office.com/article/Configure-audit-settings-for-a-site-collection-A9920C97-38C0-44F2-8BCB-4CF1E2AE22D2?ui=&rs=&ad=US): als u beheerder van een site verzameling bent, haalt u de geschiedenis op van de acties van afzonderlijke gebruikers en de geschiedenis van de acties die zijn uitgevoerd tijdens een bepaald datum bereik.

- [Zoek in het controle logboek in het office 365 security & compliance Center](https://support.office.com/article/Search-the-audit-log-in-the-Office-365-Security-Compliance-Center-0d4d0f35-390b-4518-800e-0c7ec95e946c?ui=&rs=&ad=US): gebruik het Office 365 Security & compliance Center om in het uniforme controle logboek te zoeken en gebruikers-en beheerders activiteiten in uw Office 365-organisatie te bekijken.
