---
title: Wat is bewaking van Azure Active Directory? | Microsoft Docs
description: Biedt een algemeen overzicht van Azure Active Directory-bewaking.
services: active-directory
documentationcenter: ''
author: MarkusVi
manager: daveba
editor: ''
ms.assetid: e2b3d8ce-708a-46e4-b474-123792f35526
ms.service: active-directory
ms.devlang: na
ms.topic: overview
ms.tgt_pltfrm: na
ms.workload: identity
ms.subservice: report-monitor
ms.date: 04/18/2019
ms.author: markvi
ms.reviewer: dhanyahk
ms.collection: M365-identity-device-management
ms.openlocfilehash: efa4b625afb641209d3920c8663ed810ee27e1ad
ms.sourcegitcommit: d68c72e120bdd610bb6304dad503d3ea89a1f0f7
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/01/2020
ms.locfileid: "89228644"
---
# <a name="what-is-azure-active-directory-monitoring"></a>Wat is bewaking van Azure Active Directory?

Met bewaking van Azure Active Directory (Azure AD), kunt u nu uw Azure AD-activiteitenlogboeken naar verschillende eindpunten routeren. U kunt deze vervolgens behouden voor later gebruik of integreren met SIEM-hulpprogramma's (Security Information and Event Management) van derden om meer inzicht in uw omgeving te verkrijgen.

Op dit moment kunt u de logboeken routeren naar:

- Een Azure Storage-account.
- Een Azure Event Hub, zodat u deze kunt integreren met uw Splunk en Sumologic-exemplaren.
- Azure Log Analytics-werkruimte, waarin u de gegevens kunt analyseren en een dashboard en waarschuwingen voor specifieke gebeurtenissen kunt maken

**Vereiste rol**: Hoofdbeheerder

> [!VIDEO https://www.youtube.com/embed/syT-9KNfug8]

[!INCLUDE [azure-monitor-log-analytics-rebrand](../../../includes/azure-monitor-log-analytics-rebrand.md)]

## <a name="diagnostic-settings-configuration"></a>Configuratie voor diagnostische instellingen

Om bewakingsinstellingen voor Azure AD-activiteitenlogboeken te configureren, meldt u zich aan bij de [Azure-portal](https://portal.azure.com) en selecteert u **Azure Active Directory**. Vervolgens kunt u de pagina voor het configureren van de diagnostische instellingen op twee manieren openen:

* Selecteer **Diagnostische instellingen** in de sectie **Bewaking**.

    ![Diagnostische instellingen](./media/overview-monitoring/diagnostic-settings.png)
    
* Selecteer **Auditlogboeken** of **Aanmeldingen** en selecteer vervolgens **Exportinstellingen**. 

    ![Exportinstellingen](./media/overview-monitoring/export-settings.png)


## <a name="route-logs-to-storage-account"></a>Logboeken naar opslagaccount doorsturen

Door logboeken te routeren naar een Azure Storage-account, kunt u deze langer bewaren dan de standaardbewaartermijn die wordt beschreven in ons [bewaarbeleid](reference-reports-data-retention.md). Ontdek hoe u [gegevens routeert naar uw opslagaccount](quickstart-azure-monitor-route-logs-to-storage-account.md).

## <a name="stream-logs-to-event-hub"></a>Logboeken naar Event Hub streamen

Het routeren van logboeken naar een Azure Event Hub biedt u de mogelijkheid deze te integreren met SIEM-hulpprogramma's van derden, zoals Sumologic en Splunk. Zo kunt u gegevens van Azure Active Directory-activiteitenlogboeken combineren met andere gegevens die worden beheerd door uw SIEM en meer inzicht krijgen in uw omgeving. Ontdek hoe u [logboeken streamt naar een Event Hub](tutorial-azure-monitor-stream-logs-to-event-hub.md).

## <a name="send-logs-to-azure-monitor-logs"></a>Logboeken verzenden naar logboeken van Azure Monitor

[Logboeken van Azure Monitor](../../azure-monitor/log-query/log-query-overview.md) vormen een oplossing waarin bewakingsgegevens uit verschillende bronnen worden samengevoegd. Met de bijbehorende querytaal en analyse-engine krijgt u meer inzicht in de werking van uw toepassingen en resources. Door Azure AD-activiteitenlogboeken naar logboeken van Azure Monitor te verzenden, kunt u verzamelde gegevens snel ophalen en controleren en eventuele waarschuwingen bekijken. Lees meer over [het verzenden van gegevens naar de logboeken van Azure Monitor](howto-integrate-activity-logs-with-log-analytics.md).

U kunt ook de vooraf gemaakte weergaven voor Azure AD-activiteitenlogboeken installeren om veelvoorkomende scenario's met betrekking tot aanmeldingen en controlegebeurtenissen te bewaken. Ontdek hoe u [Log Analytics-weergaven voor activiteitenlogboeken van Azure AD installeert en gebruikt](howto-install-use-log-analytics-views.md).

## <a name="next-steps"></a>Volgende stappen

* [Activiteitenlogboeken in Azure Monitor](concept-activity-logs-azure-monitor.md)
* [Logboeken naar Event Hub streamen](tutorial-azure-monitor-stream-logs-to-event-hub.md)
* [Logboeken verzenden naar logboeken van Azure Monitor](howto-integrate-activity-logs-with-log-analytics.md)