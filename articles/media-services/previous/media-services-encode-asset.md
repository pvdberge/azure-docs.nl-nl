---
title: Overzicht van media encoders van Azure on-demand | Microsoft Docs
description: Azure Media Services biedt meerdere opties voor het coderen van media in de Cloud. In dit artikel vindt u een overzicht van Azure-media encoders op aanvraag.
services: media-services
documentationcenter: ''
author: juliako
manager: femila
editor: ''
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/25/2019
ms.author: juliako
ms.openlocfilehash: c98d265f2d21c1e16ca787d4055eb4c2b1a89133
ms.sourcegitcommit: bcda98171d6e81795e723e525f81e6235f044e52
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/01/2020
ms.locfileid: "89269077"
---
# <a name="overview-of-azure-on-demand-media-encoders"></a>Overzicht van media encoders op aanvraag van Azure

[!INCLUDE [media services api v2 logo](./includes/v2-hr.md)]

> [!NOTE]
> Er worden geen nieuwe functies of functionaliteit meer aan Media Services v2. toegevoegd. <br/>Bekijk de nieuwste versie [Media Services v3](../latest/index.yml). Zie ook [migratie richtlijnen van v2 naar v3](../latest/migrate-from-v2-to-v3.md)

Azure Media Services biedt meerdere opties voor het coderen van media in de Cloud.

Wanneer u met Media Services begint, is het belang rijk dat u begrijpt wat het verschil is tussen codecs en bestands indelingen.
Codecs zijn de software waarmee de algoritmen voor compressie/decompressie worden geïmplementeerd. bestands indelingen zijn containers die de gecomprimeerde video bevatten.

Media Services biedt dynamische pakketten waarmee u uw Adaptive bitrate MP4 of Smooth Streaming gecodeerde inhoud kunt leveren in streaming-indelingen die worden ondersteund door Media Services (MPEG DASH, HLS, Smooth Streaming) zonder dat u opnieuw moet inpakken in deze streaming-indelingen.

Wanneer uw Media Services-account is gemaakt, wordt er een **standaard** streaming-eind punt aan uw account toegevoegd met de status **gestopt** . Als u inhoud wilt streamen en gebruik wilt maken van dynamische pakketten en dynamische versleuteling, moet het streaming-eindpunt van waar u inhoud wilt streamen, de status **Wordt uitgevoerd** hebben. Facturering voor streaming-eind punten treedt op wanneer het eind punt **actief** is.

Media Services ondersteunt de volgende op aanvraag encoders die in dit artikel worden beschreven:

* [Media Encoder Standard](media-services-encode-asset.md#media-encoder-standard)
* [Media Encoder Premium Workflow](media-services-encode-asset.md#media-encoder-premium-workflow)

Dit artikel bevat een kort overzicht van de media encoders op aanvraag en bevat koppelingen naar artikelen met meer gedetailleerde informatie. Het onderwerp bevat ook een vergelijking van de encoders.

Elke Media Services-account kan standaard één actieve coderings taak tegelijk hebben. U kunt coderings eenheden reserveren waarmee meerdere versleutelings taken gelijktijdig kunnen worden uitgevoerd, één voor elke gereserveerde encoding-eenheid die u koopt. Zie [coderings eenheden schalen](media-services-scale-media-processing-overview.md)voor meer informatie.

## <a name="media-encoder-standard"></a>Media Encoder Standard

### <a name="how-to-use"></a>Gebruik
[Coderen met Media Encoder Standard](media-services-dotnet-encode-with-media-encoder-standard.md)

### <a name="formats"></a>Indelingen
[Indelingen en codecs](media-services-media-encoder-standard-formats.md)

### <a name="presets"></a>Stations
Media Encoder Standard is geconfigureerd met behulp van een van de [hier](https://go.microsoft.com/fwlink/?linkid=618336&clcid=0x409)beschreven coderings definities.

### <a name="input-and-output-metadata"></a>Invoer-en uitvoer meta gegevens
De coderings Programma's invoeren meta gegevens worden [hier](media-services-input-metadata-schema.md)beschreven.

De coderings Programma's uitvoer meta gegevens worden [hier](media-services-output-metadata-schema.md)beschreven.

### <a name="generate-thumbnails"></a>Miniaturen genereren
Zie [miniaturen genereren met behulp van Media Encoder Standard](media-services-advanced-encoding-with-mes.md)voor meer informatie.

### <a name="trim-videos-clipping"></a>Video's knippen (knippen)
Zie [Video's knippen met Media Encoder Standard](media-services-advanced-encoding-with-mes.md#trim_video)voor meer informatie.

### <a name="create-overlays"></a>Overlays maken
Zie [overlays maken met behulp van Media Encoder Standard](media-services-advanced-encoding-with-mes.md#overlay)voor meer informatie.

### <a name="see-also"></a>Zie ook
[Het Media Services blog](https://azure.microsoft.com/blog/2015/07/16/announcing-the-general-availability-of-media-encoder-standard/)

## <a name="media-encoder-premium-workflow"></a>Media Encoder Premium Workflow
### <a name="overview"></a>Overzicht
[Introductie van Premium-code ring in Azure Media Services](https://azure.microsoft.com/blog/2015/03/05/introducing-premium-encoding-in-azure-media-services/)

### <a name="how-to-use"></a>Gebruik
Media Encoder Premium Workflow is geconfigureerd met behulp van complexe werk stromen. Werk stroom bestanden kunnen worden gemaakt en bijgewerkt met het [Workflow Designer](media-services-workflow-designer.md) -hulp programma.

[Premium-code ring gebruiken in Azure Media Services](https://azure.microsoft.com/blog/2015/03/06/how-to-use-premium-encoding-in-azure-media-services/)

### <a name="known-issues"></a>Bekende problemen
Als uw invoer video geen ondertiteling bevat, bevat het uitvoer activum nog een leeg TTML-bestand.

## <a name="media-services-learning-paths"></a>Media Services-leertrajecten
[!INCLUDE [media-services-learning-paths-include](../../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geven
[!INCLUDE [media-services-user-voice-include](../../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a>Verwante artikelen:
* [Geavanceerde coderings taken uitvoeren door Media Encoder Standard voor instellingen aan te passen](media-services-custom-mes-presets-with-dotnet.md)
* [Quota en beperkingen](media-services-quotas-and-limitations.md)

<!--Reference links in article-->
[1]: https://azure.microsoft.com/pricing/details/media-services/
