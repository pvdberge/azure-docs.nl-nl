---
title: bestand opnemen
description: bestand opnemen
services: automation
author: mgoedtel
ms.service: automation
ms.topic: include
ms.date: 06/29/2020
ms.author: magoedte
ms.custom: include file
ms.openlocfilehash: aa7b997fe112be5d974d0e82597e786fa219e1f5
ms.sourcegitcommit: 877491bd46921c11dd478bd25fc718ceee2dcc08
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/02/2020
ms.locfileid: "85570177"
---
#### <a name="process-automation"></a>Procesautomatisering

| Resource | Limiet |Notities|
| --- | --- |---|
| Maximum aantal nieuwe taken dat elke 30 seconden per Azure Automation account (niet-geplande taken) kan worden verzonden |100 |Wanneer deze limiet is bereikt, mislukken de volgende aanvragen om een taak te maken. De client ontvangt een fout bericht.|
| Maximum aantal gelijktijdig uitgevoerde taken in hetzelfde exemplaar van de tijd per Automation-account (niet-geplande taken) |200 |Wanneer deze limiet is bereikt, mislukken de volgende aanvragen om een taak te maken. De client ontvangt een fout bericht.|
| Maximale opslag grootte van de meta gegevens van de taak voor een periode van 30 dagen | 10 GB (ongeveer 4.000.000 taken)|Wanneer deze limiet is bereikt, mislukken de volgende aanvragen om een taak te maken. |
| Maximale taak stroom limiet|1 MiB|Eén stroom kan niet groter zijn dan 1 MB.|
| Maxi maal aantal modules dat elke 30 seconden per Automation-account kan worden geïmporteerd |5 ||
| Maximale grootte van een module |100 MB ||
| Uitvoerings tijd van taak, gratis laag |500 minuten per abonnement per kalender maand ||
| Maximale hoeveelheid schijf ruimte die is toegestaan per sandbox<sup>1</sup> |1 GB |Is alleen van toepassing op Azure-sandboxes.|
| Maximale hoeveelheid geheugen die is toegewezen aan een sandbox<sup>1</sup> |400 MB |Is alleen van toepassing op Azure-sandboxes.|
| Maximum aantal netwerk sockets dat is toegestaan per sandbox<sup>1</sup> |1000 |Is alleen van toepassing op Azure-sandboxes.|
| Maxi maal toegestane runtime per runbook<sup>1</sup> |3 uur |Is alleen van toepassing op Azure-sandboxes.|
| Maximum aantal Automation-accounts in een abonnement |Geen limiet ||
| Maximum aantal Hybrid Worker groepen per Automation-account|4000||
|Maximum aantal gelijktijdige taken dat kan worden uitgevoerd op één Hybrid Runbook Worker|50 ||
| Maximale parameter grootte voor runbook-taak   | 512 KB||
| Maximum aantal runbook-para meters   | 50|Als u de limiet van 50-para meter bereikt, kunt u een JSON-of XML-teken reeks door geven aan een para meter en deze parseren met het runbook.|
| Maximale grootte van webhook-nettolading |  512 KB|
| Maximum aantal dagen dat taak gegevens behouden blijven|30 dagen|
| Maximale grootte van Power shell-werk stroom status |5 MB| Is van toepassing op Power shell workflow-runbooks bij het controle punt van een werk stroom.|

<sup>1</sup> Een sandbox is een gedeelde omgeving die kan worden gebruikt door meerdere taken. Taken die gebruikmaken van dezelfde sandbox zijn gebonden aan de resource beperkingen van de sandbox.

#### <a name="change-tracking-and-inventory"></a>Wijzigingen bijhouden en Inventaris

De volgende tabel bevat de limieten voor bijgehouden items per computer voor het bijhouden van wijzigingen.

| **Resource** | **Ondergrens**| **Opmerkingen** |
|---|---|---|
|Bestand|500||
|Register|250||
|Windows-software|250|Bevat geen software-updates.|
|Linux-pakketten|1.250||
|Services|250||
|Daemon|250||

#### <a name="update-management"></a>Updatebeheer

De volgende tabel bevat de limieten voor de Updatebeheer.

| **Resource** | **Ondergrens**| **Opmerkingen** |
|---|---|---|
|Aantal machines per update-implementatie|1000||