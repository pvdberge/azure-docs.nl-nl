---
title: Opmerkingen bij de release van Azure Media Services v3 | Microsoft Docs
description: Om up-to-date te blijven met de meest recente ontwikkelingen, biedt dit artikel u de meest recente updates op Azure Media Services v3.
services: media-services
documentationcenter: ''
author: IngridAtMicrosoft
manager: femila
editor: ''
ms.service: media-services
ms.workload: na
ms.topic: article
ms.date: 08/31/2020
ms.author: inhenkel
ms.openlocfilehash: 5a22bd9508feac1348bcd8042fa6ac791864c261
ms.sourcegitcommit: ac5cbef0706d9910a76e4c0841fdac3ef8ed2e82
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/03/2020
ms.locfileid: "89425633"
---
# <a name="azure-media-services-v3-release-notes"></a>Release opmerkingen bij Azure Media Services v3

[!INCLUDE [media services api v3 logo](./includes/v3-hr.md)]

>Ontvang een melding over wanneer u deze pagina voor updates opnieuw moet bezoeken door deze URL te kopiëren en te plakken: `https://docs.microsoft.com/api/search/rss?search=%22Azure+Media+Services+v3+release+notes%22&locale=en-us` in uw RSS-feed-lezer.

Om u op de hoogte te houden van de nieuwste ontwikkelingen, biedt dit artikel u informatie over:

* De nieuwste releases
* Bekende problemen
* Opgeloste fouten
* Afgeschafte functionaliteit

## <a name="known-issues"></a>Bekende problemen

> [!NOTE]
> U kunt de [Azure Portal](https://portal.azure.com/) gebruiken om v3 [Live-gebeurtenissen](live-events-outputs-concept.md)te beheren, v3- [assets](assets-concept.md) en-taken weer te geven, informatie over het openen van api's te verkrijgen, inhoud te versleutelen. Gebruik voor alle andere beheer taken (bijvoorbeeld trans formaties en taken beheren) de [rest API](https://aka.ms/ams-v3-rest-ref), [cli](https://aka.ms/ams-v3-cli-ref)of een van de ondersteunde [sdk's](media-services-apis-overview.md#sdks).
>
> Zie voor meer informatie: [de Azure Portal beperkingen voor Media Services v3](frequently-asked-questions.md#what-are-the-azure-portal-limitations-for-media-services-v3).


## <a name="august-2020"></a>Augustus 2020

### <a name="dynamic-encryption"></a>Dynamische versleuteling
Ondersteuning voor de verouderde (PIFF 1,1) versleuteling van de oudere PlayReady-bestands indeling is nu beschikbaar in de dynamische Pakketset. Dit biedt ondersteuning voor verouderde slimme TV-sets van Samsung en LG waarmee de vroege concepten van de Common Encryption Standard (CENC) die door micro soft zijn gepubliceerd, zijn geïmplementeerd.  De PIFF 1,1-indeling wordt ook wel bekend als de versleutelings indeling die eerder werd ondersteund door de Silverlight-client bibliotheek. Het enige use-case scenario voor deze versleutelings indeling is het doel van de verouderde Smart TV-markt als er een niet-trivial aantal Smart TV-apparaten in sommige regio's aanwezig zijn die alleen Smooth Streaming ondersteunen met PIFF 1,1-versleuteling. 

Als u de nieuwe ondersteuning voor PIFF 1,1-versleuteling wilt gebruiken, wijzigt u de versleutelings waarde in ' piff ' in het URL-pad van de streaming-Locator. Zie [Content Protection-overzicht](content-protection-overview.md) voor meer informatie.
Bijvoorbeeld: `https://amsv3account-usw22.streaming.media.azure.net/00000000-0000-0000-0000-000000000000/ignite.ism/manifest(encryption=piff)`|

> [!NOTE]
> Ondersteuning voor PIFF 1,1 wordt geboden als een achterwaarts compatibele oplossing voor slimme TV (Samsung, LG) waarmee de vroege versie van Silverlight van Common Encryption is geïmplementeerd. U wordt aangeraden alleen de PIFF-indeling te gebruiken wanneer dit nodig is voor de ondersteuning van oudere Samsung-en LG Smart Tv's die worden verzonden tussen 2009-2015 en die de PIFF 1,1-versie van PlayReady-versleuteling ondersteunen. 

## <a name="july-2020"></a>Juli 2020

### <a name="live-transcriptions"></a>Live-transcripties

Live transcripties ondersteunt nu 19 talen en 8 regio's.

### <a name="protecting-your-content-with-media-services-and-azure-ad"></a>Uw inhoud beveiligen met Media Services en Azure AD

We hebben een zelf studie gepubliceerd met de naam [end-to-end inhouds beveiliging met behulp van Azure AD](./azure-ad-content-protection.md).

### <a name="high-availablity"></a>High-Beschik baarheid

We hebben een hoge Beschik baarheid gepubliceerd met het [overzicht](./media-services-high-availability-encoding.md) van Media Services en video on demand (VOD) en voor [beeld](https://github.com/Azure-Samples/media-services-v3-dotnet/tree/master/HighAvailabilityEncodingStreaming).

## <a name="june-2020"></a>Juni 2020

### <a name="live-video-analytics-on-iot-edge-preview-release"></a>Preview-versie van live video-analyses op IoT Edge

De preview-versie van live video Analytics op IoT Edge openbaar geworden. Zie [release opmerkingen](../live-video-analytics-edge/release-notes.md)voor meer informatie.

Live video Analytics op IoT Edge is een uitbrei ding van de media service familie. Zo kunt u live video analyseren met AI-modellen van uw keuze op uw eigen edge-apparaten en deze video optioneel vastleggen en opnemen. U kunt nu apps bouwen met realtime video analyses aan de rand zonder dat u zich zorgen hoeft te maken over de complexiteit van het bouwen en gebruiken van een live video pijplijn.

## <a name="may-2020"></a>Mei 2020

Azure Media Services is nu algemeen beschikbaar in de volgende regio's: "Duitsland-noord", "Duitsland-west-centraal", "Zwitserland-noord" en "Zwitserland-west". Klanten kunnen Media Services naar deze regio's implementeren met behulp van de Azure Portal.

## <a name="april-2020"></a>April 2020

### <a name="improvements-in-documentation"></a>Verbeteringen in de documentatie

Azure Media Player documenten zijn gemigreerd naar de [Azure-documentatie](../azure-media-player/azure-media-player-overview.md).

## <a name="january-2020"></a>Januari 2020

### <a name="improvements-in-media-processors"></a>Verbeteringen in Media-processors

- Verbeterde ondersteuning voor geïnterlinieerde bronnen in video analyse: dergelijke inhoud wordt nu niet-geïnterlinieerd voordat ze worden verzonden naar interferentie-engines.
- Wanneer u miniaturen genereert met de ' beste ' modus, zoekt het coderings programma nu meer dan 30 seconden om een frame te selecteren dat niet Monochromatic is.

### <a name="azure-government-cloud-updates"></a>Cloud updates Azure Government

Media Services GA'ed in de volgende Azure Government regio's: *USGov Arizona* en *USGov Texas*.

## <a name="december-2019"></a>December 2019

CDN-ondersteuning is toegevoegd voor de *oorsprong: prefetch-* headers voor Live en video on-demand streaming; beschikbaar voor klanten die een direct-contract met Akamai CDN hebben. Origin-assisteren CDN-prefetch-functie omvat de volgende HTTP-header-uitwisselingen tussen Akamai CDN en Azure Media Services Origin:

|HTTP-header|Waarden|Afzender|Ontvanger|Doel|
| ---- | ---- | ---- | ---- | ----- |
|CDN-oorsprong-assistentie-prefetch-ingeschakeld | 1 (standaard) of 0 |CDN|Oorsprong|Om aan te geven dat CDN prefetch is ingeschakeld|
|CDN-oorsprong-assisteren-prefetch-pad| Voorbeeld: <br/>Fragmenten (video = 1400000000, Format = mpd-time-CMAF)|Oorsprong|CDN|Het prefetch-pad naar CDN opgeven|
|CDN-oorsprong-assistentie-prefetch-aanvraag|1 (prefetch-aanvraag) of 0 (normale aanvraag)|CDN|Oorsprong|Om aan te geven dat de aanvraag van CDN een prefetch is|

Als u een deel van de koptekst uitwisseling in actie wilt zien, kunt u de volgende stappen uitvoeren:

1. Gebruik postman of krul om een aanvraag voor het Media Services van de oorsprong van een audio-of video segment of fragment uit te geven. Zorg ervoor dat u de koptekst CDN-oorsprong-assistentie-prefetch-ingeschakeld: 1 in de aanvraag toevoegt.
2. In het antwoord ziet u de header CDN-Origin-Assist-prefetch-pad met een relatief pad als waarde.

## <a name="november-2019"></a>November 2019

### <a name="live-transcription-preview"></a>Live transcriptie preview

Live transcriptie is nu beschikbaar in de open bare preview-versie en kan worden gebruikt in de regio vs-West 2.

Live transcriptie is ontworpen om samen te werken met Live-gebeurtenissen als een invoeg toepassing.  Het wordt ondersteund op zowel Pass-through-als standaard-of Premium-code ring van Live-gebeurtenissen.  Als deze functie is ingeschakeld, gebruikt de service de functie voor [spraak-naar-tekst](../../cognitive-services/speech-service/speech-to-text.md) van Cognitive Services om de gesp roken woorden in de binnenkomende audio naar tekst te transcriberen. Deze tekst wordt vervolgens beschikbaar gesteld voor levering en video en audio in MPEG-DASH-en HLS-protocollen. De facturering is gebaseerd op een nieuwe add-on meter die extra kosten voor de live-gebeurtenis is wanneer de status wordt uitgevoerd.  Zie [Live transcriptie](live-transcription.md) voor meer informatie over Live transcriptie en facturering

> [!NOTE]
> Live transcriptie is momenteel alleen beschikbaar als preview-functie in de regio vs-West 2. Het biedt alleen ondersteuning voor transcriptie van gesp roken woorden in het Engels (en-US).

### <a name="content-protection"></a>Inhoudsbeveiliging

De functie voor het voor *komen van tokens* voor het opnieuw afspelen in een beperkt aantal regio's in september is nu beschikbaar in alle regio's.
Media Services klanten kunnen nu een limiet instellen voor het aantal keren dat hetzelfde token kan worden gebruikt om een sleutel of licentie aan te vragen. Zie [token replay voor komen](content-protection-overview.md#token-replay-prevention)voor meer informatie.

### <a name="new-recommended-live-encoder-partners"></a>Nieuwe aanbevolen partners voor Live encoders

Er is ondersteuning toegevoegd voor de volgende nieuwe aanbevolen partner encoders voor RTMP live streamen:

- [Cambria Live 4,3](https://www.capellasystems.net/products/cambria-live/)
- [GoPro Hero7/8 en Max. actie camera's](https://gopro.com/help/articles/block/getting-started-with-live-streaming)
- [Restream.io](https://restream.io/)

### <a name="file-encoding-enhancements"></a>Verbeteringen voor bestands codering

- Er is nu een nieuwe voor instelling voor het coderen van inhoud beschikbaar. Er wordt een set GOP terug-uitgelijnde Mp4's gemaakt met behulp van inhoud-bewuste code ring. Op basis van de invoer inhoud voert de service een eerste licht gewicht analyse van de invoer inhoud uit. Deze resultaten worden gebruikt om het optimale aantal lagen, de juiste bitsnelheid en resolutie-instellingen voor levering door adaptieve streaming te bepalen. Deze standaard instelling is met name van toepassing op Video's met een lage complexiteit en middel grote complexiteit, waarbij de uitvoer bestanden een lagere bitsnelheid hebben, maar met een kwaliteit die nog steeds een goede ervaring voor kijkers biedt. De uitvoer bevat MP4-bestanden met Interleaved video-en audio-indeling. Zie de [open API-specificaties](https://github.com/Azure/azure-rest-api-specs/blob/master/specification/mediaservices/resource-manager/Microsoft.Media/stable/2018-07-01/Encoding.json)voor meer informatie.
- Verbeterde prestaties en meerdere threads voor de nieuwe grootte in de standaard encoder. Onder specifieke voor waarden moet de klant een prestatie verbetering van 5-40% VOD-code ring zien. Inhoud met weinig complexiteit die is gecodeerd in meerdere bitsnelheden, ziet de hoogste prestatie verhoging. 
- Standaard codering onderhoudt nu een reguliere GOP terug-uitgebracht voor de VFR-inhoud (variable frame rate) tijdens VOD-code ring wanneer u de GOP terug-instelling op basis van tijd gebruikt.  Dit betekent dat de klant de prijs informatie voor gemengde frames indient die varieert tussen 15-30 fps, bijvoorbeeld de normale GOP terug-afstanden die worden berekend voor de uitvoer naar Adaptive Bitrate Streaming MP4-bestanden. Dit verbetert de mogelijkheid om naadloos tussen sporen te scha kelen bij het leveren van HLS of een streepje. 
-  Verbeterde AV-synchronisatie voor variabele frame frequentie (VFR)-bron inhoud

### <a name="video-indexer-video-analytics"></a>Video Indexer, video analyse

- Keyframes die zijn geëxtraheerd met behulp van de VideoAnalyzer-voor instelling zijn nu in de oorspronkelijke resolutie van de video in plaats van het formaat te wijzigen. Met de High-Solution-extractie van keyframes beschikt u over originele installatie kopieën en kunt u gebruikmaken van de op installatie kopieën gebaseerde kunst matige intelligentie modellen die worden verstrekt door de micro soft-Computer Vision en Custom Vision-Services om nog meer inzicht te krijgen in uw video.

## <a name="september-2019"></a>September 2019

###  <a name="media-services-v3"></a>Media Services v3  

#### <a name="live-linear-encoding-of-live-events"></a>Live lineaire code ring van Live Events

Media Services v3 kondigt de preview van 24 uur x 365 dagen aan live lineaire code ring van Live Events aan.

###  <a name="media-services-v2"></a>Media Services v2  

#### <a name="deprecation-of-media-processors"></a>Afschaffing van media processors

Er wordt een afschaffing van *Azure media indexer* en *Azure media indexer 2 Preview*aangekondigd. Zie het onderwerp  [oudere onderdelen](../previous/legacy-components.md) voor de pensioen datums. [Azure Media Services video indexer](../video-indexer/index.yml) vervangt deze verouderde media processors.

Zie [Migrate from Azure media indexer en Azure media indexer 2 to Azure Media Services video indexer](../previous/migrate-indexer-v1-v2.md)voor meer informatie.

## <a name="august-2019"></a>Augustus 2019

###  <a name="media-services-v3"></a>Media Services v3  

#### <a name="south-africa-regional-pair-is-open-for-media-services"></a>Zuid-Afrika regionale paar is geopend voor Media Services 

Media Services is nu beschikbaar in Zuid-Afrika-noord en Zuid-Afrika-west regio's.

Zie [Clouds en regio's waarin Media Services v3 bestaat](azure-clouds-regions.md)voor meer informatie.

###  <a name="media-services-v2"></a>Media Services v2  

#### <a name="deprecation-of-media-processors"></a>Afschaffing van media processors

Er wordt een afschaffing van de media processors van *Windows Azure Media Encoder* (WAME) en *Azure Media Encoder* (AAM) aangekondigd. deze worden buiten gebruik gesteld. Voor de pensioen datums raadpleegt u dit onderwerp over [oudere onderdelen](../previous/legacy-components.md) .

Zie [WAME migreren naar Media Encoder Standard](https://go.microsoft.com/fwlink/?LinkId=2101334) en [aam migreren naar Media Encoder Standard](https://go.microsoft.com/fwlink/?LinkId=2101335)voor meer informatie.
 
## <a name="july-2019"></a>Juli 2019

### <a name="content-protection"></a>Inhoudsbeveiliging

Wanneer inhoud die wordt beveiligd met token beperking wordt gestreamd, moeten eind gebruikers een token verkrijgen dat wordt verzonden als onderdeel van de aanvraag voor de sleutel levering. Met de functie voor het voor *komen van tokens* kunnen Media Services klanten een limiet instellen voor het aantal keren dat hetzelfde token kan worden gebruikt om een sleutel of licentie aan te vragen. Zie [token replay voor komen](content-protection-overview.md#token-replay-prevention)voor meer informatie.

Vanaf juli was de preview-functie alleen beschikbaar in VS Centraal en VS-West-centraal.

## <a name="june-2019"></a>Juni 2019

### <a name="video-subclipping"></a>Video subknipsel

U kunt nu een video knippen of subfragmenten wanneer u deze codeert met behulp van een [taak](/rest/api/media/jobs). 

Deze functionaliteit werkt met elke [trans formatie](/rest/api/media/transforms) die is gebouwd met behulp van de [BuiltInStandardEncoderPreset](/rest/api/media/transforms/createorupdate#builtinstandardencoderpreset) -voor instellingen of de [StandardEncoderPreset](/rest/api/media/transforms/createorupdate#standardencoderpreset) -voor waarden. 

Zie voor beelden:

* [Een video met .NET knippen](subclip-video-dotnet-howto.md)
* [Een video met REST samenknippen](subclip-video-rest-howto.md)

## <a name="may-2019"></a>Mei 2019

### <a name="azure-monitor-support-for-media-services-diagnostic-logs-and-metrics"></a>Azure Monitor ondersteuning voor Media Services Diagnostische logboeken en metrische gegevens

U kunt nu Azure Monitor gebruiken om telemetriegegevens weer te geven die zijn verzonden door Media Services.

* Gebruik de diagnostische logboeken van Azure Monitor om aanvragen te bewaken die worden verzonden door het Media Services key delivery-eind punt. 
* Bewaak de metrische gegevens die worden verzonden door Media Services [streaming-eind punten](streaming-endpoint-concept.md).   

Zie [Media Services metrische gegevens en Diagnostische logboeken bewaken](media-services-metrics-diagnostic-logs.md)voor meer informatie.

### <a name="multi-audio-tracks-support-in-dynamic-packaging"></a>Ondersteuning voor meerdere audio-tracks in dynamische pakketten 

Bij het streamen van assets met meerdere audio sporen met meerdere codecs en talen, ondersteunt [dynamische verpakking](dynamic-packaging-overview.md) nu meerdere audio sporen voor de HLS-uitvoer (versie 4 of hoger).

### <a name="korea-regional-pair-is-open-for-media-services"></a>Het regionale paar van Korea is geopend voor Media Services 

Media Services is nu beschikbaar in Korea-centraal en Korea-zuid regio's. 

Zie [Clouds en regio's waarin Media Services v3 bestaat](azure-clouds-regions.md)voor meer informatie.

### <a name="performance-improvements"></a>Prestatieverbeteringen

Er zijn updates toegevoegd die Media Services prestatie verbeteringen bevatten.

* De maximale bestands grootte die wordt ondersteund voor de verwerking, is bijgewerkt. Zie, [quota en limieten](limits-quotas-constraints.md).
* De [versleutelings snelheid wordt verbeterd](media-reserved-units-cli-how-to.md#choosing-between-different-reserved-unit-types).

## <a name="april-2019"></a>April 2019

### <a name="new-presets"></a>Nieuwe voor instellingen

* [FaceDetectorPreset](/rest/api/media/transforms/createorupdate#facedetectorpreset) is toegevoegd aan de ingebouwde analyse-voor instellingen.
* [ContentAwareEncodingExperimental](/rest/api/media/transforms/createorupdate#encodernamedpreset) is toegevoegd aan de ingebouwde coderings definities. Zie voor meer informatie [code ring met inhoud](content-aware-encoding.md). 

## <a name="march-2019"></a>Maart 2019

Dynamische verpakking ondersteunt nu Dolby Atmos. Zie [Audio codecs die worden ondersteund door dynamische pakketten](dynamic-packaging-overview.md#audio-codecs-supported-by-dynamic-packaging)voor meer informatie.

U kunt nu een lijst met Asset-of account filters opgeven die van toepassing zijn op uw streaming-Locator. Zie [filters koppelen aan streaming-Locator](filters-concept.md#associating-filters-with-streaming-locator)voor meer informatie.

## <a name="february-2019"></a>Februari 2019

Media Services V3 wordt nu ondersteund in azure National Clouds. Niet alle functies zijn nog in alle Clouds beschikbaar. Zie [Clouds en regio's waarin Azure Media Services v3 bestaat](azure-clouds-regions.md)voor meer informatie.

De gebeurtenis [micro soft. media. JobOutputProgress](media-services-event-schemas.md#monitoring-job-output-progress) is toegevoegd aan de Azure Event grid-schema's voor Media Services.

## <a name="january-2019"></a>Januari 2019

### <a name="media-encoder-standard-and-mpi-files"></a>Media Encoder Standard-en MPI-bestanden 

Bij het coderen met Media Encoder Standard voor het maken van MP4-bestand (en), wordt er een nieuw. mpi-bestand gegenereerd en toegevoegd aan de uitvoer Asset. Dit MPI-bestand is bedoeld om de prestaties te verbeteren voor [dynamische pakket](dynamic-packaging-overview.md) -en streaming-scenario's.

U moet het MPI-bestand niet wijzigen of verwijderen of afhankelijk van de aanwezigheid (of niet) van een dergelijk bestand afnemen in uw service.

## <a name="december-2018"></a>December 2018

Updates van de GA-versie van de V3 API zijn onder andere:
       
* De **PresentationTimeRange** -eigenschappen zijn niet meer vereist voor **Asset filters** en **account filters**. 
* De query opties $top en $skip voor **taken** en **trans formaties** zijn verwijderd en $OrderBy is toegevoegd. Als onderdeel van het toevoegen van de nieuwe ordenings functionaliteit werd ontdekt dat de opties voor $top en $skip per ongeluk werden weer gegeven, zelfs als ze niet zijn geïmplementeerd.
* De Enumeration-uitbreid baarheid is opnieuw ingeschakeld. Deze functie is ingeschakeld in de Preview-versies van de SDK en is per ongeluk uitgeschakeld in de GA-versie.
* Er zijn twee vooraf gedefinieerde stroomsgewijze beleids regels gewijzigd. **SecureStreaming** is nu **MultiDrmCencStreaming**. **SecureStreamingWithFairPlay** is nu **Predefined_MultiDrmStreaming**.

## <a name="november-2018"></a>November 2018

De CLI 2,0-module is nu beschikbaar voor [Azure Media Services v3 ga](/cli/azure/ams?view=azure-cli-latest) – v-2.0.50.

### <a name="new-commands"></a>Nieuwe opdrachten

- [AZ AMS account](/cli/azure/ams/account?view=azure-cli-latest)
- [AZ AMS account-filter](/cli/azure/ams/account-filter?view=azure-cli-latest)
- [AZ AMS Asset](/cli/azure/ams/asset?view=azure-cli-latest)
- [AZ AMS Asset-filter](/cli/azure/ams/asset-filter?view=azure-cli-latest)
- [AZ AMS content-Key-policy](/cli/azure/ams/content-key-policy?view=azure-cli-latest)
- [AZ AMS job](/cli/azure/ams/job?view=azure-cli-latest)
- [AZ AMS Live-Event](/cli/azure/ams/live-event?view=azure-cli-latest)
- [AZ AMS live-output](/cli/azure/ams/live-output?view=azure-cli-latest)
- [AZ AMS streaming-Endpoint](/cli/azure/ams/streaming-endpoint?view=azure-cli-latest)
- [AZ AMS streaming-Locator](/cli/azure/ams/streaming-locator?view=azure-cli-latest)
- [AZ AMS account MRU](/cli/azure/ams/account/mru?view=azure-cli-latest) -Hiermee kunt u gereserveerde media-eenheden beheren. Zie [gereserveerde media-eenheden schalen](media-reserved-units-cli-how-to.md)voor meer informatie.

### <a name="new-features-and-breaking-changes"></a>Nieuwe functies en belang rijke wijzigingen

#### <a name="asset-commands"></a>Asset-opdrachten

- ```--storage-account``` en ```--container``` argumenten zijn toegevoegd.
- Standaard waarden voor verloop tijd (nu + 23h) en machtigingen (lezen) in de ```az ams asset get-sas-url``` opdracht toegevoegd.

#### <a name="job-commands"></a>Opdracht opdrachten

- ```--correlation-data``` en ```--label``` argumenten toegevoegd
- ```--output-asset-names``` de naam is gewijzigd in ```--output-assets``` . Nu accepteert het een lijst met door spaties gescheiden activa in de indeling ' assets = label '. Activa zonder label kunnen als volgt worden verzonden: ' assets = '.

#### <a name="streaming-locator-commands"></a>Opdrachten voor streaming-Locator

- ```az ams streaming locator``` de basis opdracht is vervangen door ```az ams streaming-locator``` .
- ```--streaming-locator-id``` en ```--alternative-media-id support``` argumenten zijn toegevoegd.
- ```--content-keys argument``` het argument is bijgewerkt.
- ```--content-policy-name``` de naam is gewijzigd in ```--content-key-policy-name``` .

#### <a name="streaming-policy-commands"></a>Streaming-beleids opdrachten

- ```az ams streaming policy``` de basis opdracht is vervangen door ```az ams streaming-policy``` .
- De ondersteuning voor versleutelings parameters is ```az ams streaming-policy create``` toegevoegd.

#### <a name="transform-commands"></a>Opdrachten transformeren

- ```--preset-names``` het argument is vervangen door ```--preset``` . Nu kunt u slechts één uitvoer/voor instelling per keer instellen (om meer informatie toe te voegen om uit te voeren ```az ams transform output add``` ). U kunt ook aangepaste StandardEncoderPreset instellen door het pad naar uw aangepaste JSON door te geven.
- ```az ams transform output remove``` kan worden uitgevoerd door de uitvoer index door te geven die moet worden verwijderd.
- ```--relative-priority, --on-error, --audio-language and --insights-to-extract``` argumenten die zijn toegevoegd in ```az ams transform create``` en ```az ams transform output add``` opdrachten.

## <a name="october-2018---ga"></a>Oktober 2018-GA

In deze sectie worden Azure Media Services updates (AMS) van oktober beschreven.

### <a name="rest-v3-ga-release"></a>REST v3 GA release

De [rest v3 ga-release](https://github.com/Azure/azure-rest-api-specs/tree/master/specification/mediaservices/resource-manager/Microsoft.Media/stable/2018-07-01) bevat meer Api's voor Live, account/Asset level-manifest filters en DRM-ondersteuning.

#### <a name="azure-resource-management"></a>Azure-resource beheer 

Ondersteuning voor Azure Resource Management maakt Unified management en Operations API mogelijk (nu alles op één plek).

Vanaf deze release kunt u Resource Manager-sjablonen gebruiken om live-gebeurtenissen te maken.

#### <a name="improvement-of-asset-operations"></a>Verbetering van activa bewerkingen 

De volgende verbeteringen zijn geïntroduceerd:

- Opname van HTTP (s) Url's of Azure Blob Storage SAS-Url's.
- Geef de naam van de container voor assets op. 
- Eenvoudigere uitvoer ondersteuning voor het maken van aangepaste werk stromen met Azure Functions.

#### <a name="new-transform-object"></a>Nieuw Transform-object

Het nieuwe object **transform** vereenvoudigt het coderings model. Met het nieuwe object kunt u eenvoudig sjabloon en voor instellingen voor het maken en delen van coderings bronnen beheren. 

#### <a name="azure-active-directory-authentication-and-rbac"></a>Azure Active Directory-verificatie en RBAC

Met Azure AD-verificatie en op rollen gebaseerde Access Control (RBAC) kunt u beveiligde trans formaties, LiveEvents, beleids regels voor inhouds sleutels of activa op rol of gebruikers in azure AD inschakelen.

#### <a name="client-sdks"></a>Client-SDK 's  

Talen die worden ondersteund in Media Services V3: .NET core, Java, Node.js, Ruby, type script, python en go.

#### <a name="live-encoding-updates"></a>Live encoding-updates

De volgende Live encoding-updates worden geïntroduceerd:

- Nieuwe modus voor de lage latentie voor Live (10 seconden end-to-end).
- Verbeterde RTMP-ondersteuning (verbeterde stabiliteit en meer ondersteuning voor broncode encoders).
- RTMP beveiligde opname.

    Wanneer u een live gebeurtenis maakt, krijgt u nu vier opname-Url's. De 4 opname-Url's zijn bijna identiek, hebben hetzelfde streaming token (AppId), alleen het poort nummer onderdeel is anders. Twee van de Url's zijn primaire en back-ups voor RTMP. 
- ondersteuning voor trans codering met 24 uur. 
- Verbeterde ondersteuning voor AD-Signa lering in RTMP via SCTE35.

#### <a name="improved-event-grid-support"></a>Verbeterde ondersteuning voor Event Grid

U kunt de volgende Event Grid verbeteringen voor de ondersteuning bekijken:

- Azure Event Grid integratie voor eenvoudiger ontwikkeling met Logic Apps en Azure Functions. 
- Abonneer u op gebeurtenissen op code ring, Live kanalen en meer.

### <a name="cmaf-support"></a>CMAF-ondersteuning

Ondersteuning voor CMAF en ' cbcs-versleuteling voor Apple HLS (iOS 11 +) en MPEG-DASH-spelers die CMAF ondersteunen.

### <a name="video-indexer"></a>Video Indexer

Video Indexer GA release is in augustus aangekondigd. Zie [Wat is video indexer](../video-indexer/video-indexer-overview.md?bc=/azure/media-services/video-indexer/breadcrumb/toc.json&toc=/azure/media-services/video-indexer/toc.json)voor nieuwe informatie over momenteel ondersteunde functies. 

### <a name="plans-for-changes"></a>Plannen voor wijzigingen

#### <a name="azure-cli-20"></a>Azure CLI 2.0
 
De Azure CLI 2,0-module die bewerkingen bevat voor alle functies (waaronder Live, beleids regels voor inhouds sleutels, accounts/Asset-filters, streaming-beleid) is binnenkort beschikbaar. 

### <a name="known-issues"></a>Bekende problemen

De volgende problemen zijn alleen van invloed op klanten die de preview-API voor activa of AccountFilters hebben gebruikt.

Als u activa of account filters hebt gemaakt tussen 09/28 en 10/12 met Media Services v3 CLI of Api's, moet u alle asset-en AccountFilters verwijderen en opnieuw maken vanwege een versie conflict. 

## <a name="may-2018---preview"></a>Mei 2018-preview

### <a name="net-sdk"></a>.NET SDK

De volgende functies zijn aanwezig in de .NET SDK:

* **Trans formaties** en **taken** voor het coderen of analyseren van media-inhoud. Zie voor voor beelden [stroom bestanden](stream-files-tutorial-with-api.md) en [analyseren](analyze-videos-tutorial-with-api.md).
* **Streaming-Locators** voor het publiceren en streamen van inhoud op apparaten van eind gebruikers
* **Stroomsgewijze beleids regels** en **beleids regels voor inhouds sleutels** voor het configureren van key delivery and Content Protection (DRM) bij het leveren van inhoud.
* **Live Events** en **Live outputs** voor het configureren van de opname en het archiveren van inhoud voor live streamen.
* **Activa** voor het opslaan en publiceren van media-inhoud in azure Storage. 
* **Streaming-eind punten** voor het configureren en schalen van dynamische pakketten, versleuteling en streaming voor zowel live als on-demand media-inhoud.

### <a name="known-issues"></a>Bekende problemen

* Bij het verzenden van een taak kunt u opgeven dat u uw bron video wilt opnemen met behulp van HTTPS-Url's, SAS-Url's of paden naar bestanden die zich in Azure Blob Storage bevinden. Media Services V3 biedt momenteel geen ondersteuning voor gesegmenteerde overdrachts codering via HTTPS-Url's.

## <a name="ask-questions-give-feedback-get-updates"></a>Vragen stellen, feedback geven, updates ophalen

Ga naar het artikel van de [Azure Media Services-community](media-services-community.md) voor verschillende manieren om vragen te stellen, feedback te geven en updates voor Media Services op te halen.

## <a name="see-also"></a>Zie ook

[Migratie richtlijnen voor het overstappen van Media Services versie 2 naar v3](migrate-from-v2-to-v3.md#known-issues).

## <a name="next-steps"></a>Volgende stappen

- [Overzicht](media-services-overview.md)
- [Media Services v3-documentatie-updates](docs-release-notes.md)
- [Release opmerkingen bij Media Services v2](../previous/media-services-release-notes.md)
