---
title: Door Web SDK ondersteunde browsers | Microsoft Azure kaarten
description: Meer informatie over hoe u kunt controleren of de Azure Maps Web-SDK een browser ondersteunt. Bekijk een lijst met ondersteunde browsers. Meer informatie over het gebruik van toewijzings Services met verouderde browsers.
author: rbrundritt
ms.author: richbrun
ms.date: 03/25/2019
ms.topic: conceptual
ms.service: azure-maps
services: azure-maps
manager: cpendle
ms.openlocfilehash: 73d875e32f4fcf22551cf6b0946e49c2f826e523
ms.sourcegitcommit: 07166a1ff8bd23f5e1c49d4fd12badbca5ebd19c
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/15/2020
ms.locfileid: "90085022"
---
# <a name="web-sdk-supported-browsers"></a>Browsers die Web-SDK ondersteunen

De Azure Maps Web-SDK biedt een hulp functie met de naam [Atlas. isSupported](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas#issupported-boolean-). Deze functie detecteert of een webbrowser de minimale set WebGL-functies heeft die vereist is voor het laden en weer geven van het kaart besturings element. Hier volgt een voor beeld van het gebruik van de functie:

```JavaScript
if (!atlas.isSupported()) {
    alert('Your browser is not supported by Azure Maps');
} else if (!atlas.isSupported(true)) {
    alert('Your browser is supported by Azure Maps, but may have major performance caveats.');
} else {
    // Your browser is supported. Add your map code here.
}
```

## <a name="desktop"></a>Bureaublad

De Azure Maps Web-SDK ondersteunt de volgende desktop browsers:

- Micro soft Edge (huidige en vorige versie)
- Google Chrome (huidige en vorige versie)
- Mozilla Firefox (huidige en vorige versie)
- Apple Safari (Mac OS X) (huidige en vorige versie)

Zie ook [verouderde browsers bedoelen](#Target-Legacy-Browsers) verderop in dit artikel.

## <a name="mobile"></a>Mobiele telefoon

De Azure Maps Web-SDK ondersteunt de volgende mobiele browsers:

- Android
  - Huidige versie van Chrome op Android 6,0 en hoger
  - Chrome webweergave op Android 6,0 en hoger
- iOS
  - Mobile Safari met de huidige en vorige primaire versie van iOS
  - UIWebView en WKWebView voor de huidige en vorige primaire versie van iOS
  - Huidige versie van Chrome voor iOS

> [!TIP]
> Als u een kaart in een mobiele toepassing insluit met een besturings element voor webweergave, kunt u het NPM- [pakket van de Azure Maps Web SDK](https://www.npmjs.com/package/azure-maps-control) gebruiken in plaats van te verwijzen naar de versie van de SDK die wordt gehost op Azure Content Delivery Network. Deze aanpak vermindert de laad tijd omdat de SDK zich al op het apparaat van de gebruiker bevindt en niet tijdens runtime hoeft te worden gedownload.

## <a name="nodejs"></a>Node.js

De volgende Web SDK-modules worden ook ondersteund in Node.js:

- Services-module ([documentatie](how-to-use-services-module.md)  |  [NPM module](https://www.npmjs.com/package/azure-maps-rest))

## <a name="target-legacy-browsers"></a><a name="Target-Legacy-Browsers"></a>Doel verouderde browsers

Het is raadzaam om oudere browsers te richten die geen ondersteuning bieden voor WebGL of die alleen beperkte ondersteuning voor het systeem hebben. In dergelijke gevallen kunt u het beste Azure Maps-Services gebruiken in combi natie met een open-source kaart besturings element als een [Folder](https://leafletjs.com/). Hier volgt een voorbeeld:

<br/>

<iframe height="500" style="width: 100%;" scrolling="no" title="Azure Maps en bijsluiter" src="//codepen.io/azuremaps/embed/GeLgyx/?height=500&theme-id=0&default-tab=html,result" frameborder="no" allowtransparency="true" allowfullscreen="true">
Zie de pen <a href='https://codepen.io/azuremaps/pen/GeLgyx/'>Azure Maps + bijsluiter</a> per Azure Maps ( <a href='https://codepen.io/azuremaps'>@azuremaps</a> ) op <a href='https://codepen.io'>CodePen</a>.
</iframe>


## <a name="next-steps"></a>Volgende stappen

Meer informatie over de Azure Maps Web-SDK:

> [!div class="nextstepaction"]
> [Kaartbesturingselement](how-to-use-map-control.md)

> [!div class="nextstepaction"]
> [Services-module](how-to-use-services-module.md)
