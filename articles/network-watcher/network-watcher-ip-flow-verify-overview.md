---
title: Inleiding tot IP-stroom controleren in azure Network Watcher | Microsoft Docs
description: Op deze pagina vindt u een overzicht van de mogelijkheden van de Network Watcher IP-stroom controle
services: network-watcher
documentationcenter: na
author: damendo
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/30/2017
ms.author: damendo
ms.openlocfilehash: 69aca5e0901a0da8aa98fe310ac220898bf650b2
ms.sourcegitcommit: 877491bd46921c11dd478bd25fc718ceee2dcc08
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/02/2020
ms.locfileid: "76845003"
---
# <a name="introduction-to-ip-flow-verify-in-azure-network-watcher"></a>Inleiding tot IP-stroom controleren in azure Network Watcher

IP-stroom controleert of een pakket wordt toegestaan of geweigerd op een virtuele machine. De informatie bestaat uit richting, protocol, lokaal IP, extern IP-adres, lokale poort en externe poort. Als het pakket wordt geweigerd door een beveiligings groep, wordt de naam van de regel die het pakket heeft geweigerd, geretourneerd. Terwijl elke bron-of doel-IP kan worden gekozen, kunnen beheerders met IP-stroom controleren snel verbindings problemen vaststellen vanuit of naar Internet en van of naar de on-premises omgeving.

De IP-stroom controleert de regels voor alle netwerk beveiligings groepen (Nsg's) die worden toegepast op de netwerk interface, zoals een subnet of virtuele-machine-NIC. De verkeers stroom wordt vervolgens geverifieerd op basis van de geconfigureerde instellingen van of naar die netwerk interface. Verificatie van de IP-stroom is handig om te controleren of een regel in een netwerk beveiligings groep binnenkomend of uitgaand verkeer naar of van een virtuele machine blokkeert.

Er moet een exemplaar van Network Watcher worden gemaakt in alle regio's die u wilt gebruiken om de IP-stroom te controleren. Network Watcher is een regionale service en kan alleen worden uitgevoerd op resources in dezelfde regio. Het gebruikte exemplaar heeft geen invloed op de resultaten van de IP-stroom controle, omdat er nog steeds een route wordt geretourneerd die is gekoppeld aan de NIC of het subnet.

![1][1]

## <a name="next-steps"></a>Volgende stappen

Ga naar het volgende artikel voor meer informatie over het toestaan of weigeren van een pakket voor een specifieke virtuele machine via de portal. [Controleren of verkeer is toegestaan op een virtuele machine met IP-stroom controleren met behulp van de portal](diagnose-vm-network-traffic-filtering-problem.md)

[1]: ./media/network-watcher-ip-flow-verify-overview/figure1.png

