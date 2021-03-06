---
author: vhorne
ms.service: dns
ms.topic: include
ms.date: 11/25/2018
ms.author: victorh
ms.openlocfilehash: 9cc650cea17acb8d89933c819c4ca60e2c459d1c
ms.sourcegitcommit: 877491bd46921c11dd478bd25fc718ceee2dcc08
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/02/2020
ms.locfileid: "67176666"
---
SPF-records (Sender Policy Framework) worden gebruikt om op te geven welke e-mail servers e-mail namens een domein naam kunnen verzenden. De juiste configuratie van SPF-records is belang rijk om te voor komen dat ontvangers uw e-mail berichten als ongewenste e-mail markeren.

De DNS Rfc's heeft oorspronkelijk een nieuw SPF-record type geïntroduceerd ter ondersteuning van dit scenario. Ter ondersteuning van oudere naam servers, hebben ze ook het gebruik van het record type TXT toegestaan om SPF-records op te geven. Deze ambiguïteit heeft geleid tot Verwar ring, die is opgelost door [RFC 7208](http://tools.ietf.org/html/rfc7208#section-3.1). Hiermee wordt aangegeven dat SPF-records moeten worden gemaakt met behulp van het record type TXT. Ook wordt aangegeven dat het SPF-record type is afgeschaft.

**SPF-records worden ondersteund door Azure DNS en moeten worden gemaakt met behulp van het record type TXT.** Het verouderde SPF-record type wordt niet ondersteund. Wanneer u [een DNS-zone bestand importeert](../articles/dns/dns-import-export.md), worden alle SPF-records die gebruikmaken van het SPF-record type geconverteerd naar het TXT-record type.
