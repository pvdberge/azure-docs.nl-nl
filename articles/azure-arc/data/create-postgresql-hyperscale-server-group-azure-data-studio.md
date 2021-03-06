---
title: Azure Arc enabled PostgreSQL grootschalige maken met behulp van Azure Data Studio
description: Azure Arc enabled PostgreSQL grootschalige maken met behulp van Azure Data Studio
services: azure-arc
ms.service: azure-arc
ms.subservice: azure-arc-data
author: TheJY
ms.author: jeanyd
ms.reviewer: mikeray
ms.date: 09/22/2020
ms.topic: how-to
ms.openlocfilehash: af0cdb814433b739b15d79bec9cb399cf0a2fef7
ms.sourcegitcommit: 53acd9895a4a395efa6d7cd41d7f78e392b9cfbe
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/22/2020
ms.locfileid: "90936428"
---
# <a name="create-azure-arc-enabled-postgresql-hyperscale-using-azure-data-studio"></a>Azure Arc enabled PostgreSQL grootschalige maken met behulp van Azure Data Studio

In dit document worden de stappen beschreven voor het gebruik van Azure Data Studio voor het inrichten van Azure Arc ingeschakelde PostgreSQL grootschalige-Server groepen.

[!INCLUDE [azure-arc-common-prerequisites](../../../includes/azure-arc-common-prerequisites.md)]

[!INCLUDE [azure-arc-data-preview](../../../includes/azure-arc-data-preview.md)]

## <a name="connect-to-the-azure-arc-data-controller"></a>Verbinding maken met de Azure-Arc-gegevens controller

Voordat u een exemplaar kunt maken, meldt u zich aan bij de Azure Arc-gegevens controller als u zich nog niet hebt aangemeld.

```console
azdata login
```

Vervolgens wordt u gevraagd om de naam ruimte waarin de gegevens controller is gemaakt, de gebruikers naam en het wacht woord om u aan te melden bij de controller.

> Als u de naam ruimte moet valideren, kunt u uitvoeren ```kubectl get pods -A``` om een lijst met alle naam ruimten op het cluster op te halen.

```console
Username: arcadmin
Password:
Namespace: arc
Logged in successfully to `https://10.0.0.4:30080` in namespace `arc`. Setting active context to `arc`
```

## <a name="create-an-azure-arc-enabled-postgresql-hyperscale-server-group"></a>Een Azure-PostgreSQL grootschalige-Server groep maken

1. Azure Data Studio starten
1. Klik op het tabblad verbindingen op de drie puntjes linksboven en kies nieuwe implementatie
1. Selecteer in de implementatie opties de optie **postgresql grootschalige-Server groep-Azure-boog**
    >[!NOTE]
    > U wordt mogelijk gevraagd om de `azdata` cli hier te installeren als deze nog niet is geïnstalleerd.
1. Accepteer de privacy-en licentie voorwaarden en klik onderaan op **selecteren** .
1. Voer de volgende gegevens in op de Blade PostgreSQL grootschalige-Server groep implementeren-Azure arctangens:
   - Voer een naam in voor de Server groep
   - Voer een wacht woord in en bevestig dit voor de _post gres_ beheerder gebruiker van de Server groep
   - Selecteer de opslag klasse waar dit van toepassing is voor gegevens
   - Selecteer de opslag klasse die geschikt is voor logboeken
   - Selecteer de opslag klasse die geschikt is voor back-ups
   - Het aantal worker-knoop punten selecteren dat moet worden ingericht
1. Klik op de knop **implementeren**

Hiermee wordt het maken van de PostgreSQL grootschalige-Server groep voor Azure-Arc ingeschakeld op de gegevens controller gestart.

Het maken van een paar minuten is voltooid.

## <a name="next-steps"></a>Volgende stappen
- [Uw server groep beheren met Azure Data Studio](manage-postgresql-hyperscale-server-group-with-azure-data-studio.md)
- [Uw server groep controleren](monitor-grafana-kibana.md)
- Lees de concepten en instructies van Azure Database for PostgreSQL grootschalige om uw gegevens te verdelen over meerdere PostgreSQL grootschalige-knoop punten en om te profiteren van alle kracht van Azure data base for post gres grootschalige. :
    * [Knooppunten en tabellen](../../postgresql/concepts-hyperscale-nodes.md)
    * [Toepassingstype bepalen](../../postgresql/concepts-hyperscale-app-type.md)
    * [Een distributiekolom kiezen](../../postgresql/concepts-hyperscale-choose-distribution-column.md)
    * [Tabelcolocatie](../../postgresql/concepts-hyperscale-colocation.md)
    * [Tabellen distribueren en bewerken](../../postgresql/howto-hyperscale-modify-distributed-tables.md)
    * [Een multi tenant-data base ontwerpen](../../postgresql/tutorial-design-database-hyperscale-multi-tenant.md)*
    * [Een real-time analyse dashboard ontwerpen](../../postgresql/tutorial-design-database-hyperscale-realtime.md)*

    > \* In de bovenstaande documenten slaat u de secties **voor het aanmelden bij de Azure Portal**, & **een Azure database for PostgreSQL-grootschalige maken (Citus)**. Implementeer de resterende stappen in de implementatie van Azure Arc. Deze secties zijn specifiek voor de Azure Database for PostgreSQL grootschalige (Citus) die worden aangeboden als een PaaS-service in de Azure-Cloud, maar de andere onderdelen van de documenten zijn rechtstreeks van toepassing op uw PostgreSQL grootschalige van Azure Arc.

- [Uw Azure Database for PostgreSQL grootschalige-Server groep uitschalen](scale-out-postgresql-hyperscale-server-group.md)
- [Opslag configuraties en Kubernetes opslag concepten](storage-configuration.md)
- [Claims voor permanente volumes uitbreiden](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#expanding-persistent-volumes-claims)
- [Kubernetes-resource model](https://github.com/kubernetes/community/blob/master/contributors/design-proposals/scheduling/resources.md#resource-quantities)

