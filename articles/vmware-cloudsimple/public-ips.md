---
title: 'Azure VMware-oplossing op CloudSimple: open bare IP-adressen toewijzen'
description: Hierin wordt beschreven hoe u open bare IP-adressen toewijst voor virtuele machines in de Privécloud.
author: sharaths-cs
ms.author: b-shsury
ms.date: 08/15/2019
ms.topic: article
ms.service: azure-vmware-cloudsimple
ms.reviewer: cynthn
manager: dikamath
ms.openlocfilehash: 565c9ad0fbd37b026a1ba555d83b9032d2efcba4
ms.sourcegitcommit: 877491bd46921c11dd478bd25fc718ceee2dcc08
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/02/2020
ms.locfileid: "77024293"
---
# <a name="allocate-public-ip-addresses-for-private-cloud-environment"></a>Open bare IP-adressen toewijzen voor een privé-cloud omgeving

Open het tabblad open bare Ip's op de pagina netwerk om open bare IP-adressen toe te wijzen voor virtuele machines in uw Privécloud.

1. [Open de CloudSimple-Portal](access-cloudsimple-portal.md) en selecteer **netwerk** in het menu aan de zijkant.
2. Selecteer **open bare ip's**.
3. Klik op **nieuw openbaar IP-adres**.

    ![Open bare IPs-pagina](media/public-ips-page.png)

4. Voer een naam in om de IP-adres vermelding te identificeren.
5. Behoud de standaard locatie.
6. Gebruik de schuif regelaar om, indien nodig, de time-out voor inactiviteit te wijzigen.
7. Voer het lokale IP-adres in waarvoor u een openbaar IP-adres wilt toewijzen.
8. Voer een bijbehorende DNS-naam in.
9. Klik op **Submit**

![Open bare IP-adressen toewijzen](media/network-public-ip-allocate.png)

De taak voor het toewijzen van het open bare IP-adres begint. U kunt de status van de taak controleren op de pagina **activiteit > taken** . Wanneer de toewijzing is voltooid, wordt de nieuwe vermelding op de open bare IPs-pagina weer gegeven.
