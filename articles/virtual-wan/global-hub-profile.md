---
title: Azure Virtual WAN Global of hub-based VPN-profielen downloaden | Microsoft Docs
description: Lees meer over geautomatiseerde schaalbare verbindingen tussen filialen, beschikbare regio's en partners via Virtual WAN.
services: virtual-wan
author: kumudD
ms.service: virtual-wan
ms.topic: how-to
ms.date: 4/20/2020
ms.author: alzam
ms.openlocfilehash: d0fc2f608617ca00fea8b9ed5c4b874c65940263
ms.sourcegitcommit: 3d79f737ff34708b48dd2ae45100e2516af9ed78
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/23/2020
ms.locfileid: "87064800"
---
# <a name="download-a-global-or-hub-based-profile-for-user-vpn-clients"></a>Een globaal of op de hub gebaseerd profiel voor VPN-clients van de gebruiker downloaden

Azure Virtual WAN biedt twee soorten connectiviteit voor externe gebruikers: globaal en op basis van de hub. Gebruik de volgende secties voor meer informatie over en het downloaden van een profiel. 

> [!IMPORTANT]
> RADIUS-verificatie ondersteunt alleen het op de hub gebaseerde profiel.

## <a name="global-profile"></a>Algemeen profiel

Het profiel verwijst naar een load balancer dat alle VPN-hubs van de actieve gebruiker bevat. De gebruiker wordt omgeleid naar de hub die zich het dichtst bij de geografische locatie van de gebruiker bevindt. Dit type verbinding is handig wanneer gebruikers regel matig naar verschillende locaties reizen. Het **globale** profiel downloaden:

1. Navigeer naar uw virtuele WAN.
2. Klik op **VPN-gebruikers configuratie**.
3. Markeer de configuratie waarvoor u het profiel wilt downloaden.
4. Klik op **VPN-gebruikers profiel voor virtuele WAN downloaden**.

   ![Algemeen profiel](./media/global-hub-profile/global1.png)

## <a name="hub-based-profile"></a>Op de hub gebaseerd profiel

Het profiel verwijst naar één hub. De gebruiker kan alleen verbinding maken met de betreffende hub met behulp van dit profiel. Het op de **hub gebaseerde** profiel downloaden:

1. Navigeer naar uw virtuele WAN.
2. Klik op **hub** op de pagina overzicht.

    ![Hub-profiel 1](./media/global-hub-profile/hub1.png)
3. Klik op **gebruikers VPN (punt naar site)**.
4. Klik op **VPN-gebruikers profiel voor virtuele hub downloaden**.

   ![Hub-profiel 2](./media/global-hub-profile/hub2.png)
5. Controleer **EAPTLS**.
6. Klik op **profiel genereren en downloaden**.

   ![Hub-profiel 3](./media/global-hub-profile/download.png)

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over Virtual WAN de pagina [Overzicht van Virtual WAN](virtual-wan-about.md).
