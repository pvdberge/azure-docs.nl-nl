---
title: Gegevens bronnen verbinden met Azure Sentinel | Microsoft Docs
description: Informatie over het verbinden van gegevens bronnen zoals Microsoft 365 Defender (voorheen micro soft Threat Protection), Microsoft 365 en Office 365, Azure AD, ATP en Cloud App Security aan Azure Sentinel.
services: sentinel
documentationcenter: na
author: yelevin
manager: rkarlin
editor: ''
ms.service: azure-sentinel
ms.subservice: azure-sentinel
ms.devlang: na
ms.topic: how-to
ms.custom: mvc
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/08/2020
ms.author: yelevin
ms.openlocfilehash: 63acffd16fa4374d4f8541a9d3327b29a3641f71
ms.sourcegitcommit: 53acd9895a4a395efa6d7cd41d7f78e392b9cfbe
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/22/2020
ms.locfileid: "90895804"
---
# <a name="connect-data-sources"></a>Verbinding maken met gegevensbronnen

Zodra u Azure Sentinel hebt ingeschakeld, moet u eerst verbinding maken met uw gegevens bronnen. Azure Sentinel wordt geleverd met een aantal connectors voor micro soft-oplossingen, die beschikbaar zijn in de doos en die realtime-integratie bieden, waaronder Microsoft 365 Defender-oplossingen (voorheen micro soft Threat Protection), Microsoft 365 bronnen (waaronder Office 365), Azure AD, micro soft Defender voor identiteit (voorheen Azure ATP), Microsoft Cloud App Security en meer. Daarnaast zijn er ingebouwde connectors voor het bredere beveiligingsecosysteem voor niet-Microsoft-oplossingen. U kunt ook Common Event Format (CEF), Syslog of REST-API gebruiken om uw gegevensbronnen met Azure Sentinel te verbinden.

1. Selecteer in het menu **Data connectors**. Op deze pagina kunt u de volledige lijst met connectors zien die door Azure Sentinel worden geboden en hun status. Selecteer de connector die u wilt verbinden en selecteer de **pagina connector openen**. 

   ![Galerie data connectors](./media/collect-data/collect-data-page.png)

1. Controleer op de pagina specifieke connector of u aan alle vereisten hebt voldaan en volg de instructies voor het verbinden van de gegevens met Azure Sentinel. Het kan enige tijd duren voordat de logboeken worden gesynchroniseerd met Azure Sentinel. Nadat u verbinding hebt gemaakt, ziet u een samen vatting van de gegevens in de grafiek **ontvangen gegevens** en de connectiviteits status van de gegevens typen.

   ![Gegevens connectors configureren](./media/collect-data/opened-connector-page.png)
  
1. Klik op het tabblad **volgende stappen** om een lijst van out-of-the-Box-inhoud weer te geven. Azure Sentinel levert voor het specifieke gegevens type.

   ![Volgende stappen voor connectors](./media/collect-data/data-insights.png)
 

## <a name="data-connection-methods"></a>Gegevensverbindingsmethoden

De volgende gegevens verbindings methoden worden ondersteund door Azure Sentinel:

- **Integratie van service naar service**:<br> Sommige services zijn systeem eigen verbonden, zoals AWS en micro soft-Services, maar deze services maken gebruik van de Azure Foundation voor out-of-the-box Integration, de volgende oplossingen kunnen met een paar klikken worden verbonden:
    - [Amazon Web Services-CloudTrail](connect-aws.md)
    - [Azure-activiteit](connect-azure-activity.md)
    - [Azure Active Directory](connect-azure-active-directory.md) -audit logboeken en aanmeldings logboeken
    - [Azure AD-identiteitsbeveiliging](connect-azure-ad-Identity-protection.md)
    - [Micro soft Defender voor identiteit](connect-azure-atp.md) (voorheen Azure Advanced Threat Protection)
    - [Azure Information Protection](connect-azure-information-protection.md)
    - [Azure Security Center](connect-azure-security-center.md) -waarschuwingen van Azure Defender-oplossingen
    - [Cloud App Security](connect-cloud-app-security.md)
    - [Domeinnaamserver](connect-dns.md)
    - [Office 365](connect-office-365.md)
    - [Micro soft Defender voor eind punt](connect-microsoft-defender-advanced-threat-protection.md) (voorheen micro soft Defender Advanced Threat Protection)
    - [Microsoft Web Application Firewall](connect-microsoft-waf.md)
    - [Windows Firewall](connect-windows-firewall.md)
    - [Windows-beveiligingsgebeurtenissen](connect-windows-security-events.md)

- **Externe oplossingen via API**: sommige gegevens bronnen zijn verbonden via api's die worden meegeleverd met de verbonden gegevens bron. Doorgaans bieden de meeste beveiligings technologieën een set Api's waarmee gebeurtenis logboeken kunnen worden opgehaald. De Api's maken verbinding met Azure Sentinel en verzamelen specifieke gegevens typen en verzenden ze naar Azure Log Analytics. Apparaten verbonden via API zijn:
    
    - [Alcide kAudit](connect-alcide-kaudit.md)
    - [Barracuda WAF](connect-barracuda.md)
    - [Barracuda CloudGen-firewall](connect-barracuda-cloudgen-firewall.md)
    - [Citrix Analytics (Security)](connect-citrix-analytics.md)
    - [F5 BIG-IP](connect-f5-big-ip.md)
    - [Forcepoint DLP](connect-forcepoint-dlp.md)
    - [Perimeter 81 logs](connect-perimeter-81-logs.md)
    - [Squadra Technologies secRMM](connect-squadra-secrmm.md)
    - [Symantec ICDX](connect-symantec.md)
    - [Zimperium](connect-zimperium-mtd.md)


- **Externe oplossingen via agent**: Azure Sentinel kan via een agent worden verbonden met een andere gegevens bron die realtime logboek streaming met het syslog-protocol kan uitvoeren.

    De meeste apparaten gebruiken het syslog-protocol om gebeurtenis berichten te verzenden die het logboek zelf en gegevens over het logboek bevatten. De indeling van de logboeken varieert, maar de meeste apparaten ondersteunen de CEF-opmaak voor logboek gegevens. 

    De Azure Sentinel-agent, die in feite de Log Analytics-agent is, converteert CEF-Logboeken in een indeling die door Log Analytics kan worden opgenomen. Afhankelijk van het type apparaat, wordt de agent rechtstreeks op het apparaat geïnstalleerd of op een speciale, op Linux gebaseerde logboek doorstuur server. De agent voor Linux ontvangt gebeurtenissen van de syslog-daemon via UDP, maar als een Linux-machine verwacht een hoog volume aan syslog-gebeurtenissen te verzamelen, worden ze via TCP van de syslog-daemon naar de agent verzonden en van daaruit naar Log Analytics.

    - **Firewalls, proxy's en eind punten:**
        - [AI Vectra Detect](connect-ai-vectra-detect.md)
        - [Check Point](connect-checkpoint.md)
        - [Cisco ASA](connect-cisco.md)
        - [ExtraHop Reveal(x)](connect-extrahop.md)
        - [F5 ASM](connect-f5.md)
        - [Force Point-producten](connect-forcepoint-casb-ngfw.md)
        - [Fortinet](connect-fortinet.md)
        - [Palo Alto Networks](connect-paloalto.md)
        - [One Identity Safeguard](connect-one-identity.md)
        - [Andere CEF-apparaten](connect-common-event-format.md)
        - [Andere syslog-apparaten](connect-syslog.md)
        - [Deep Security van Trend Micro](connect-trend-micro.md)
        - [Zscaler](connect-zscaler.md)
    - DLP-oplossingen
    - [Threat Intelligence-providers](connect-threat-intelligence.md)
    - [DNS-machines](connect-dns.md) -agent rechtstreeks geïnstalleerd op de DNS-computer
    - Linux-servers
    - Andere Clouds
    
## <a name="agent-connection-options"></a>Verbindingsopties voor agenten<a name="agent-options"></a>

Om uw externe apparaat te verbinden met Azure Sentinel, moet de agent worden geïmplementeerd op een toegewezen machine (VM of on-premises) om de communicatie tussen het apparaat en de Azure-Sentinel te ondersteunen. U kunt de agent automatisch of hand matig implementeren. Automatische implementatie is alleen beschikbaar als uw toegewezen computer een nieuwe VM is die u in azure maakt. 


![CEF in azure](./media/connect-cef/cef-syslog-azure.png)

U kunt de agent ook hand matig implementeren op een bestaande Azure-VM, op een virtuele machine in een andere Cloud of op een on-premises machine.

![CEF on-premises](./media/connect-cef/cef-syslog-onprem.png)

## <a name="map-data-types-with-azure-sentinel-connection-options"></a>Gegevenstypen toewijzen met behulp van Azure Sentinel-verbindingsopties


| **Gegevenstype** | **Verbinding maken** | **Data Connector?** | **Opmerkingen** |
|------|---------|-------------|------|
| AWSCloudTrail | [Verbinding maken met AWS](connect-aws.md) | &#10003; | |
| AzureActivity | Overzicht van [Azure activiteit](connect-azure-activity.md) en [activiteiten logboeken](../azure-monitor/platform/platform-logs-overview.md) verbinden| &#10003; | |
| Audit logs bevat | [Verbinding maken met Azure AD](connect-azure-active-directory.md)  | &#10003; | |
| SigninLogs | [Verbinding maken met Azure AD](connect-azure-active-directory.md)  | &#10003; | |
| AzureFirewall |[Azure Diagnostics](../firewall/tutorial-diagnostics.md) | &#10003; | |
| InformationProtectionLogs_CL  | [Azure Information Protection rapporten](https://docs.microsoft.com/azure/information-protection/reports-aip)<br>[Verbinding maken met Azure Information Protection](connect-azure-information-protection.md)  | &#10003; | Dit maakt gewoonlijk gebruik van de functie **InformationProtectionEvents** naast het gegevens type. Zie [de rapporten wijzigen en aangepaste query's maken](https://docs.microsoft.com/azure/information-protection/reports-aip#how-to-modify-the-reports-and-create-custom-queries) voor meer informatie|
| AzureNetworkAnalytics_CL  | Verkeers [analyse](../network-watcher/traffic-analytics.md) van [Traffic analytic-schema](../network-watcher/traffic-analytics.md)  | | |
| CommonSecurityLog  | [Verbinding maken met CEF](connect-common-event-format.md)  | &#10003; | |
| OfficeActivity | [Verbinding maken met Office 365](connect-office-365.md) | &#10003; | |
| SecurityEvents | [Verbinding maken met Windows-beveiligingsgebeurtenissen](connect-windows-security-events.md)  | &#10003; | Zie voor de werkmappen met Inveilige protocollen [onveilige protocollen werkmap instellen](/azure/sentinel/quickstart-get-visibility#use-built-in-workbooks)  |
| Syslog | [Verbinding maken met Syslog](connect-syslog.md) | &#10003; | |
| Micro soft Web Application firewall (WAF)-(AzureDiagnostics) |[Verbinding maken met micro soft Web Application firewall](connect-microsoft-waf.md) | &#10003; | |
| SymantecICDx_CL | [Symantec verbinden](connect-symantec.md) | &#10003; | |
| ThreatIntelligenceIndicator  | [Verbinding maken met bedreigingsinformatie](connect-threat-intelligence.md)  | &#10003; | |
| VMConnection <br> ServiceMapComputer_CL<br> ServiceMapProcess_CL|  [Toewijzing van Azure Monitor-service](../azure-monitor/insights/service-map.md)<br>[Voor bereiding op Azure Monitor VM Insights](../azure-monitor/insights/vminsights-onboard.md) <br> [Azure Monitor VM Insights inschakelen](../azure-monitor/insights/vminsights-enable-overview.md) <br> [Eén virtuele machine on-boarding gebruiken](../azure-monitor/insights/vminsights-enable-single-vm.md)<br>  [On-boarding gebruiken via het beleid](../azure-monitor/insights/vminsights-enable-at-scale-policy.md)| &#10007; | VM Insights-werkmap  |
| DnsEvents | [DNS verbinden](connect-dns.md) | &#10003; | |
| W3CIISLog | [IIS-logboeken verbinden](../azure-monitor/platform/data-sources-iis-logs.md)  | &#10007; | |
| WireData | [Bedradings gegevens verbinden](../azure-monitor/insights/wire-data.md) | &#10007; | |
| WindowsFirewall | [Windows Firewall verbinden](connect-windows-firewall.md) | &#10003; | |
| AADIP SecurityAlert  | [Verbinding maken met Azure AD Identity Protection](connect-azure-ad-identity-protection.md)  | &#10003; | |
| AATP SecurityAlert  | [Verbinding maken met micro soft Defender voor identiteit](connect-azure-atp.md) (voorheen Azure ATP) | &#10003; | |
| ASC SecurityAlert  | [Azure Defender-waarschuwingen verbinden](connect-azure-security-center.md) vanuit Azure Security Center  | &#10003; | |
| MCAS SecurityAlert  | [Microsoft Cloud App Security verbinden](connect-cloud-app-security.md)  | &#10003; | |
| SecurityAlert | | | |
| Voor-en naactiviteit (gebeurtenis) | [Verbinding maken](https://azure.microsoft.com/blog/detecting-in-memory-attacks-with-sysmon-and-azure-security-center)<br> [Windows-gebeurtenissen verbinden](../azure-monitor/platform/data-sources-windows-events.md) <br> [De ophaal-parser ophalen](https://github.com/Azure/Azure-Sentinel/blob/master/Parsers/Sysmon/Sysmon-v10.42-Parser.txt)| &#10007; | De garbagecollection-verzameling wordt niet standaard op virtuele machines geïnstalleerd. [Zie voor](https://docs.microsoft.com/sysinternals/downloads/sysmon)meer informatie over het installeren van de opschoon agent. |
| ConfigurationData  | [VM-inventarisatie automatiseren](../automation/automation-vm-inventory.md)| &#10007; | |
| ConfigurationChange  | [VM-tracking automatiseren](../automation/change-tracking.md) | &#10007; | |
| F5 BIG-IP | [Verbinding maken met F5 BIG-IP](https://devcentral.f5.com/s/articles/Integrating-the-F5-BIGIP-with-Azure-Sentinel)  | &#10007; | |
| McasShadowItReporting  |  | &#10007; | |
| Barracuda_CL | [Verbinding maken met Barracuda](connect-barracuda.md) | &#10003; | |


## <a name="next-steps"></a>Volgende stappen

- U moet een Microsoft Azure-abonnement hebben om met Azure Sentinel aan de slag te gaan. Als u geen abonnement hebt, kunt u zich aanmelden voor een [gratis proefversie](https://azure.microsoft.com/free/).
- Leer hoe u [uw gegevens kunt onboarden in Azure Sentinel](quickstart-onboard.md) en [krijg inzicht in uw gegevens en mogelijke bedreigingen](quickstart-get-visibility.md).
