---
title: Gebeurtenis tellers in Application Insights | Microsoft Docs
description: Bewaak systeem-en aangepaste .NET/.NET core-EventCounters in Application Insights.
ms.topic: conceptual
ms.date: 09/20/2019
ms.custom: devx-track-csharp
ms.openlocfilehash: f8ae36545eecbbad2a6695ca979fb7da8380e8cc
ms.sourcegitcommit: f8d2ae6f91be1ab0bc91ee45c379811905185d07
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/10/2020
ms.locfileid: "89657011"
---
# <a name="eventcounters-introduction"></a>EventCounters-Inleiding

`EventCounter` is .NET/.NET core-mechanisme voor het publiceren en gebruiken van tellers of statistieken. [Dit](https://github.com/dotnet/runtime/blob/master/src/libraries/System.Diagnostics.Tracing/documentation/EventCounterTutorial.md) document bevat een overzicht van `EventCounters` en voor beelden voor het publiceren en gebruiken van deze. EventCounters worden ondersteund in alle OS-platformen-Windows, Linux en macOS. Het kan worden beschouwd als een platform dat gelijkwaardig is aan de [Performance Counters](/dotnet/api/system.diagnostics.performancecounter) die alleen wordt ondersteund in Windows-systemen.

Hoewel gebruikers aangepaste kunnen publiceren `EventCounters` om aan hun behoeften te voldoen, publiceert .net Core 3,0 en hogere runtime standaard een set van deze prestatie meter items. In dit document worden de stappen beschreven die nodig zijn voor het verzamelen en weer geven (door het `EventCounters` systeem gedefinieerde of door de gebruiker gedefinieerde definitie) in azure-toepassing Insights.

## <a name="using-application-insights-to-collect-eventcounters"></a>EventCounters verzamelen met behulp van Application Insights

Application Insights ondersteunt `EventCounters` het verzamelen met de `EventCounterCollectionModule` , die deel uitmaakt van het zojuist gepubliceerde NuGet-pakket [micro soft. ApplicationInsights. EventCounterCollector](https://www.nuget.org/packages/Microsoft.ApplicationInsights.EventCounterCollector). `EventCounterCollectionModule` wordt automatisch ingeschakeld wanneer [AspNetCore](asp-net-core.md) of [WorkerService](worker-service.md)wordt gebruikt. `EventCounterCollectionModule` verzamelt tellers met een niet-Configureer bare verzamelings frequentie van 60 seconden. Er zijn geen speciale machtigingen vereist voor het verzamelen van EventCounters.

## <a name="default-counters-collected"></a>Verzamelde standaard items

Voor apps die worden uitgevoerd in .NET Core 3,0 of hoger, worden de volgende prestatie meter items automatisch verzameld door de SDK. De naam van de prestatie meter items heeft de indeling ' Category | Teller ".

|Categorie | Prestatiemeteritem|
|---------------|-------|
|`System.Runtime` | `cpu-usage` |
|`System.Runtime` | `working-set` |
|`System.Runtime` | `gc-heap-size` |
|`System.Runtime` | `gen-0-gc-count` |
|`System.Runtime` | `gen-1-gc-count` |
|`System.Runtime` | `gen-2-gc-count` |
|`System.Runtime` | `time-in-gc` |
|`System.Runtime` | `gen-0-size` |
|`System.Runtime` | `gen-1-size` |
|`System.Runtime` | `gen-2-size` |
|`System.Runtime` | `loh-size` |
|`System.Runtime` | `alloc-rate` |
|`System.Runtime` | `assembly-count` |
|`System.Runtime` | `exception-count` |
|`System.Runtime` | `threadpool-thread-count` |
|`System.Runtime` | `monitor-lock-contention-count` |
|`System.Runtime` | `threadpool-queue-length` |
|`System.Runtime` | `threadpool-completed-items-count` |
|`System.Runtime` | `active-timer-count` |

> [!NOTE]
> Vanaf de 2.15.0-beta3-versie van de [ASPNETCORE SDK](asp-net-core.md) of [WorkerService SDK](worker-service.md)worden standaard geen tellers verzameld. De module zelf is ingeschakeld, zodat gebruikers eenvoudigweg de gewenste items kunnen toevoegen om ze te verzamelen.

## <a name="customizing-counters-to-be-collected"></a>Te verzamelen items aanpassen

In het volgende voor beeld ziet u hoe u tellers kunt toevoegen/verwijderen. Deze aanpassing wordt uitgevoerd in de `ConfigureServices` methode van uw toepassing nadat Application Insights telemetrie-verzameling is ingeschakeld met ofwel `AddApplicationInsightsTelemetry()` of `AddApplicationInsightsWorkerService()` . Hieronder volgt een voorbeeld code van een ASP.NET Core-toepassing. Raadpleeg [Dit](worker-service.md#configuring-or-removing-default-telemetrymodules) document voor een ander type toepassingen.

```csharp
    using Microsoft.ApplicationInsights.Extensibility.EventCounterCollector;
    using Microsoft.Extensions.DependencyInjection;

    public void ConfigureServices(IServiceCollection services)
    {
        //... other code...

        // The following code shows how to configure the module to collect
        // additional counters.
        services.ConfigureTelemetryModule<EventCounterCollectionModule>(
            (module, o) =>
            {
                // This removes all default counters.
                module.Counters.Clear();

                // This adds a user defined counter "MyCounter" from EventSource named "MyEventSource"
                module.Counters.Add(new EventCounterCollectionRequest("MyEventSource", "MyCounter"));

                // This adds the system counter "gen-0-size" from "System.Runtime"
                module.Counters.Add(new EventCounterCollectionRequest("System.Runtime", "gen-0-size"));
            }
        );
    }
```

## <a name="disabling-eventcounter-collection-module"></a>Module Event Counter-verzameling uitschakelen

`EventCounterCollectionModule` kan worden uitgeschakeld met behulp van `ApplicationInsightsServiceOptions` . Hieronder wordt een voor beeld weer gegeven wanneer u ASP.NET Core SDK gebruikt.

```csharp
    using Microsoft.ApplicationInsights.AspNetCore.Extensions;
    using Microsoft.Extensions.DependencyInjection;

    public void ConfigureServices(IServiceCollection services)
    {
        //... other code...

        var applicationInsightsServiceOptions = new ApplicationInsightsServiceOptions();
        applicationInsightsServiceOptions.EnableEventCounterCollectionModule = false;
        services.AddApplicationInsightsTelemetry(applicationInsightsServiceOptions);
    }
```

Er kan ook een soort gelijke benadering worden gebruikt voor de WorkerService-SDK, maar de naam ruimte moet worden gewijzigd, zoals wordt weer gegeven in het onderstaande voor beeld.

```csharp
    using Microsoft.ApplicationInsights.WorkerService;
    using Microsoft.Extensions.DependencyInjection;

    var applicationInsightsServiceOptions = new ApplicationInsightsServiceOptions();
    applicationInsightsServiceOptions.EnableEventCounterCollectionModule = false;
    services.AddApplicationInsightsTelemetryWorkerService(applicationInsightsServiceOptions);
```

## <a name="event-counters-in-metric-explorer"></a>Gebeurtenis tellers in metrische Explorer

Als u metrische gegevens van Event Counter wilt weer geven in de [metrische Explorer](../platform/metrics-charts.md), selecteert u Application Insights resource en kiest u metrische gegevens op basis van een logboek als metrische naam ruimte. Vervolgens worden event Counter-metrische gegevens weer gegeven onder aangepaste categorie.

> [!div class="mx-imgBorder"]
> ![Gebeurtenis tellers die zijn gerapporteerd in Application Insights metrische gegevens Verkenner](./media/event-counters/metrics-explorer-counter-list.png)

## <a name="event-counters-in-analytics"></a>Gebeurtenis tellers in Analytics

U kunt ook rapporten over gebeurtenis tellers in [Analytics](../log-query/log-query-overview.md)zoeken en weer geven in de tabel **customMetrics** .

Voer bijvoorbeeld de volgende query uit om te zien welke tellers worden verzameld en beschikbaar zijn voor het uitvoeren van query's:

```Kusto
customMetrics | summarize avg(value) by name
```

> [!div class="mx-imgBorder"]
> ![Gebeurtenis tellers die zijn gerapporteerd in Application Insights Analytics](./media/event-counters/analytics-event-counters.png)

Voer de volgende query uit om een grafiek van een specifieke teller te verkrijgen (bijvoorbeeld: `ThreadPool Completed Work Item Count` ) in de recente periode.

```Kusto
customMetrics 
| where name contains "System.Runtime|ThreadPool Completed Work Item Count"
| where timestamp >= ago(1h)
| summarize  avg(value) by cloud_RoleInstance, bin(timestamp, 1m)
| render timechart
```
> [!div class="mx-imgBorder"]
> ![Chatten van een enkele teller in Application Insights](./media/event-counters/analytics-completeditems-counters.png)

Net als bij andere telemetrie heeft **customMetrics** ook een kolom `cloud_RoleInstance` die de identiteit aangeeft van het exemplaar van de hostserver waarop uw app wordt uitgevoerd. De bovenstaande query toont de item waarde per exemplaar en kan worden gebruikt om de prestaties van verschillende server instanties te vergelijken.

## <a name="alerts"></a>Waarschuwingen
Net als bij andere metrische gegevens kunt u [een waarschuwing instellen](../platform/alerts-log.md) om u te waarschuwen als een gebeurtenis teller buiten een limiet valt die u opgeeft. Open het deel venster waarschuwingen en klik op waarschuwing toevoegen.

## <a name="frequently-asked-questions"></a>Veelgestelde vragen

### <a name="can-i-see-eventcounters-in-live-metrics"></a>Kan ik EventCounters in Live Metrics zien?

Met Live metrische gegevens wordt EventCounters vanaf vandaag niet weer gegeven. Gebruik metrische Explorer of Analytics om de telemetrie weer te geven.

### <a name="i-have-enabled-application-insights-from-azure-web-app-portal-but-i-cant-see-eventcounters"></a>Ik heb Application Insights ingeschakeld vanuit de Azure web app-Portal. Maar ik zie EventCounters niet.?

 Deze functie wordt nog niet ondersteund door de [Application Insights extensie](./azure-web-apps.md) voor ASP.net core. Dit document wordt bijgewerkt wanneer deze functie wordt ondersteund.

## <a name="next-steps"></a><a name="next"></a>Volgende stappen

* [Afhankelijkheden bijhouden](./asp-net-dependencies.md)

