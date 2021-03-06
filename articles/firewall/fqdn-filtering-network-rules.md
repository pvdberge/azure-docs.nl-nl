---
title: Azure Firewall FQDN-filtering in netwerk regels (preview-versie)
description: Azure Firewall FQDN-filtering gebruiken in netwerk regels
services: firewall
author: vhorne
ms.service: firewall
ms.topic: article
ms.date: 08/25/2020
ms.author: victorh
ms.openlocfilehash: 1a35d9c48dd46d5d220699589f4ed758d21feca8
ms.sourcegitcommit: b33c9ad17598d7e4d66fe11d511daa78b4b8b330
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/25/2020
ms.locfileid: "88854282"
---
# <a name="use-fqdn-filtering-in-network-rules-preview"></a>FQDN-filtering in netwerk regels gebruiken (preview-versie)

> [!IMPORTANT]
> FQDN-filtering in netwerk regels is momenteel beschikbaar als open bare preview.
> Deze preview-versie wordt aangeboden zonder service level agreement en wordt niet aanbevolen voor productieworkloads. Misschien worden bepaalde functies niet ondersteund of zijn de mogelijkheden ervan beperkt. Zie [Supplemental Terms of Use for Microsoft Azure Previews (Aanvullende gebruiksvoorwaarden voor Microsoft Azure-previews)](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) voor meer informatie.

Een Fully Qualified Domain Name (FQDN) vertegenwoordigt een domein naam van een host of IP-adres (sen). U kunt FQDN-namen gebruiken in netwerk regels op basis van DNS-omzetting in Azure Firewall en firewall-beleid. Met deze mogelijkheid kunt u uitgaand verkeer filteren met elk TCP/UDP-protocol (met inbegrip van NTP, SSH, RDP en meer). U moet DNS-proxy inschakelen om FQDN-namen in uw netwerk regels te gebruiken. Zie [Azure firewall DNS-instellingen (preview-versie)](dns-settings.md)voor meer informatie.

> [!NOTE]
> Daarom biedt FQDN-filtering geen ondersteuning voor joker tekens.

## <a name="how-it-works"></a>Hoe het werkt

Wanneer u eenmaal hebt gedefinieerd welke DNS-server uw organisatie nodig heeft (Azure DNS of uw eigen aangepaste DNS), Azure Firewall de FQDN-naam naar een IP-adres (sen) vertaald op basis van de geselecteerde DNS-server. Deze vertaling gebeurt voor de verwerking van toepassingen en netwerk regels.

Wat is het verschil tussen het gebruik van domein namen in toepassings regels vergeleken met die van netwerk regels? 

- FQDN-filtering in toepassings regels voor HTTP/S en MSSQL is gebaseerd op een transparentproxy op toepassings niveau en de SNI-header. Zo kan het onderscheid worden tussen twee FQDN-adressen die worden omgezet naar hetzelfde IP-adres. Dit is niet het geval met FQDN-filtering in netwerk regels. Altijd toepassings regels gebruiken wanneer dit mogelijk is.
- In toepassings regels kunt u HTTP/S en MSSQL als uw geselecteerde protocollen gebruiken. In netwerk regels kunt u elk TCP/UDP-protocol gebruiken met uw doel-FQDN-namen.

## <a name="next-steps"></a>Volgende stappen

[DNS-instellingen Azure Firewall](dns-settings.md)
