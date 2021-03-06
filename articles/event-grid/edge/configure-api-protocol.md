---
title: API-protocollen configureren-Azure Event Grid IoT Edge | Microsoft Docs
description: API-protocollen configureren die worden weer gegeven door Event Grid op IoT Edge.
author: VidyaKukke
manager: rajarv
ms.author: vkukke
ms.reviewer: spelluru
ms.date: 07/08/2020
ms.topic: article
ms.openlocfilehash: 801a320fbd66b4b8a46757ba90881da54b2721de
ms.sourcegitcommit: 1e6c13dc1917f85983772812a3c62c265150d1e7
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/09/2020
ms.locfileid: "86171717"
---
# <a name="configure-event-grid-api-protocols"></a>Event Grid API-protocollen configureren

Deze hand leiding bevat voor beelden van de mogelijke protocol configuraties van een Event Grid module. In de module Event Grid wordt API weer gegeven voor de beheer-en runtime-bewerkingen. In de volgende tabel worden de protocollen en poorten vastgelegd.

| Protocol | Poort | Beschrijving |
| ---------------- | ------------ | ------------ |
| HTTP | 5888 | Standaard uitgeschakeld. Alleen nuttig tijdens het testen. Niet geschikt voor productie werkbelastingen.
| HTTPS | 4438 | Standaard

Zie de hand leiding voor [beveiliging en verificatie](security-authentication.md) voor alle mogelijke configuraties.

## <a name="expose-https-to-iot-modules-on-the-same-edge-network"></a>HTTPS beschikbaar maken voor IoT-modules op hetzelfde Edge-netwerk

```json
 {
  "Env": [
    "inbound__serverAuth__tlsPolicy=strict",
    "inbound__serverAuth__serverCert__source=IoTEdge"
  ]
}
 ```

## <a name="enable-https-to-other-iot-modules-and-non-iot-workloads"></a>HTTPS inschakelen voor andere IoT-modules en niet-IoT-workloads

```json
 {
  "Env": [
    "inbound__serverAuth__tlsPolicy=strict",
    "inbound__serverAuth__serverCert__source=IoTEdge"
  ],
  "HostConfig": {
    "PortBindings": {
      "4438/tcp": [
        {
          "HostPort": "4438"
        }
      ]
    }
  }
}
 ```

>[!NOTE]
> Met de sectie **PortBindings** kunt u interne poorten toewijzen aan poorten van de container host. Met deze functie kunt u de module Event Grid van buiten het netwerk van IoT Edge container bereiken als het IoT edge-apparaat openbaar is.

## <a name="expose-http-and-https-to-iot-modules-on-the-same-edge-network"></a>HTTP en HTTPS beschikbaar maken voor IoT-modules op hetzelfde Edge-netwerk

```json
 {
  "Env": [
    "inbound__serverAuth__tlsPolicy=enabled",
    "inbound__serverAuth__serverCert__source=IoTEdge"
  ]
}
 ```

## <a name="enable-http-and-https-to-other-iot-modules-and-non-iot-workloads"></a>HTTP en HTTPS inschakelen voor andere IoT-modules en niet-IoT-workloads

```json
 {
  "Env": [
    "inbound__serverAuth__tlsPolicy=enabled",
    "inbound__serverAuth__serverCert__source=IoTEdge"
  ],
  "HostConfig": {
    "PortBindings": {
      "4438/tcp": [
        {
          "HostPort": "4438"
        }
      ],
      "5888/tcp": [
        {
          "HostPort": "5888"
        }
      ]
    }
  }
}
 ```

>[!NOTE]
> Elke IoT-module maakt standaard deel uit van de IoT Edge runtime die door het brug netwerk is gemaakt. Hierdoor kunnen verschillende IoT-modules op hetzelfde netwerk communiceren met elkaar. Met **PortBindings** kunt u een interne container poort toewijzen op de hostcomputer, zodat iedereen toegang heeft tot de poort van Event grid module van buiten.

>[!IMPORTANT]
> Hoewel de poorten toegankelijk kunnen worden gemaakt buiten het IoT Edge netwerk, dwingt client verificatie af wie in feite aanroepen naar de module mag worden uitgevoerd.
