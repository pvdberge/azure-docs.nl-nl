---
title: Client verificatie van binnenkomende oproepen configureren-Azure Event Grid IoT Edge | Microsoft Docs
description: API-protocollen configureren die worden weer gegeven door Event Grid op IoT Edge.
author: VidyaKukke
manager: rajarv
ms.author: vkukke
ms.reviewer: spelluru
ms.date: 07/08/2020
ms.topic: article
ms.openlocfilehash: a0bba9559c2a0b4ff6c8a4e5f2287692e27f8a1a
ms.sourcegitcommit: 1e6c13dc1917f85983772812a3c62c265150d1e7
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/09/2020
ms.locfileid: "86171700"
---
# <a name="configure-client-authentication-of-incoming-calls"></a>Client verificatie van binnenkomende oproepen configureren

Deze hand leiding bevat voor beelden van de mogelijke configuraties voor client verificatie voor de module Event Grid. De module Event Grid ondersteunt twee typen client verificatie:

* Shared Access Signature (SAS) op basis van sleutels
* Op basis van certificaten

Zie de hand leiding voor [beveiliging en verificatie](security-authentication.md) voor alle mogelijke configuraties.

## <a name="enable-certificate-based-client-authentication-no-self-signed-certificates"></a>Client authenticatie op basis van certificaten inschakelen, geen zelfondertekende certificaten

```json
 {
  "Env": [
    "inbound__clientAuth__sasKeys__enabled=false",
    "inbound__clientAuth__clientCert__enabled=true",
    "inbound__clientAuth__clientCert__source=IoTEdge",
    "inbound__clientAuth__clientCert__allowUnknownCA=false"
  ]
}
 ```

## <a name="enable-certificate-based-client-authentication-allow-self-signed-certificates"></a>Client authenticatie op basis van certificaten inschakelen, zelfondertekende certificaten toestaan

```json
 {
  "Env": [
    "inbound__clientAuth__sasKeys__enabled=false",
    "inbound__clientAuth__clientCert__enabled=true",
    "inbound__clientAuth__clientCert__source=IoTEdge",
    "inbound__clientAuth__clientCert__allowUnknownCA=true"
  ]
}
```

>[!NOTE]
>Stel de eigenschap **inbound__clientAuth__clientCert__allowUnknownCA** in op **waar** alleen in test omgevingen, omdat u meestal zelfondertekende certificaten kunt gebruiken. Voor werk belastingen wordt u aangeraden deze eigenschap in te stellen op **False** en certificaten van een certificerings instantie (CA).

## <a name="enable-certificate-based-and-sas-key-based-client-authentication"></a>Op certificaten gebaseerde en SAS-sleutel gebaseerde client verificatie inschakelen

```json
 {
  "Env": [
    "inbound__clientAuth__sasKeys__enabled=true",
    "inbound__clientAuth__sasKeys__key1=<some-secret1-here>",
    "inbound__clientAuth__sasKeys__key2=<some-secret2-here>",
    "inbound__clientAuth__clientCert__enabled=true",
    "inbound__clientAuth__clientCert__source=IoTEdge",
    "inbound__clientAuth__clientCert__allowUnknownCA=true"
  ]
}
 ```

>[!NOTE]
>Met SAS-client authenticatie op basis van sleutels kan een niet-IoT Edge-module beheer-en runtime-bewerkingen uitvoeren, uitgaande van de API-poorten die buiten het IoT Edge netwerk toegankelijk zijn.
