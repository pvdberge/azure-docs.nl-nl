---
title: Release opmerkingen bij Azure Media Services Video Indexer | Microsoft Docs
description: Om up-to-date te blijven met de meest recente ontwikkelingen, biedt dit artikel u de meest recente updates op Azure Media Services Video Indexer.
services: media-services
documentationcenter: ''
author: Juliako
manager: femila
editor: ''
ms.service: media-services
ms.subservice: video-indexer
ms.workload: na
ms.topic: article
ms.date: 09/03/2020
ms.author: juliako
ms.openlocfilehash: e2b45ebf9acea7334678110015d8cfd3022675f4
ms.sourcegitcommit: 59ea8436d7f23bee75e04a84ee6ec24702fb2e61
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/07/2020
ms.locfileid: "89505334"
---
# <a name="azure-media-services-video-indexer-release-notes"></a>Release opmerkingen bij Azure Media Services Video Indexer

>Ontvang een melding over wanneer u deze pagina voor updates opnieuw moet bezoeken door deze URL te kopiëren en te plakken: `https://docs.microsoft.com/api/search/rss?search=%22Azure+Media+Services+Video+Indexer+release+notes%22&locale=en-us` in uw RSS-feed-lezer.

Om u op de hoogte te houden van de nieuwste ontwikkelingen, biedt dit artikel u informatie over:

* De nieuwste releases
* Bekende problemen
* Opgeloste fouten
* Afgeschafte functionaliteit

## <a name="august-2020"></a>Augustus 2020

### <a name="mobile-design-for-the-video-indexer-website"></a>Mobiel ontwerp voor de Video Indexer-website

De ervaring van de Video Indexer website is nu het ondersteunen van mobiele apparaten. De gebruikers ervaring reageert op het aanpassen van de grootte van uw mobiele scherm (met uitzonde ring van aanpassings UIs). 

### <a name="accessibility-improvements-and-bug-fixes"></a>Verbeterde toegankelijkheid en oplossingen voor oplossingen 

Als onderdeel van de WCAG (richt lijnen voor toegankelijkheid van webinhoud) wordt de ervaring van de Video Indexer website uitgelijnd met categorie C als onderdeel van de micro soft-toegankelijkheids standaarden. Verschillende bugs en verbeteringen met betrekking tot toetsenbord navigatie, programmatische toegang en scherm lezer zijn opgelost. 

## <a name="july-2020"></a>Juli 2020

### <a name="ga-for-multi-language-identification"></a>GA voor multi-language-identificatie

Multi-language-identificatie wordt verplaatst van preview naar GA en klaar voor productief gebruik.

Er zijn geen prijs wijzigingen die betrekking hebben op de overgang ' preview to GA '.

### <a name="video-indexer-website-improvements"></a>Verbeterde website Video Indexer

#### <a name="adjustments-in-the-video-gallery"></a>Aanpassingen in de video galerie

Nieuwe zoek balk voor uitgebreid inzicht zoeken met extra filter mogelijkheden is toegevoegd. De zoek resultaten zijn ook verbeterd.

Nieuwe lijst weergave met de mogelijkheid om een video archief met meerdere bestanden te sorteren en te beheren.

#### <a name="new-panel-for-easy-selection-and-configuration"></a>Nieuw paneel voor eenvoudige selectie en configuratie

Side Panel voor eenvoudige selectie en gebruikers configuratie is toegevoegd, waardoor eenvoudig en snel accounts kunnen worden gemaakt en gedeeld, en configuratie kan worden ingesteld.

Side Panel wordt ook gebruikt voor gebruikers voorkeuren en Help.

## <a name="june-2020"></a>Juni 2020

### <a name="search-by-topics"></a>Zoeken op onderwerpen

U kunt nu de zoek-API gebruiken om te zoeken naar Video's met specifieke onderwerpen (alleen API).

Onderwerpen worden toegevoegd als onderdeel van de `textScope` (optionele para meter). Zie de [API](https://api-portal.videoindexer.ai/docs/services/Operations/operations/Search-Videos) voor meer informatie.  

### <a name="labels-enhancement"></a>Uitbrei ding van labels

Het label Tagger is bijgewerkt en bevat nu meer visuele labels die kunnen worden geïdentificeerd.

## <a name="may-2020"></a>Mei 2020

### <a name="video-indexer-deployed-in-the-east-us"></a>Video Indexer geïmplementeerd in het VS-Oost

U kunt nu een Video Indexer betaalde account maken in de regio VS-Oost.
 
### <a name="video-indexer-url"></a>Video Indexer URL

Video Indexer regionale eind punten zijn allemaal gecombineerd om te starten met www. Er is geen actie-item vereist.

Vanaf nu bereikt u www.videoindexer.ai of het gaat om widgets in te sluiten of u aan te melden Video Indexer webtoepassingen.

Wus.videoindexer.ai wordt ook omgeleid naar www. Meer informatie is beschikbaar in [Inge sloten video indexer widgets in uw apps](video-indexer-embed-widgets.md).

## <a name="april-2020"></a>April 2020

### <a name="new-widget-parameters-capabilities"></a>Mogelijkheden van nieuwe widget parameters

De widget **inzichten** bevat nieuwe para meters: `language` en `control` .

De **Player** -widget heeft een nieuwe `locale` para meter. `locale` `language` De para meters en zijn van invloed op de taal van de speler.

Zie de sectie [typen widget](video-indexer-embed-widgets.md#widget-types) voor meer informatie. 

### <a name="new-player-skin"></a>Nieuwe Player-weer gave

Er is een nieuwe Player-weer gave gestart met een bijgewerkt ontwerp.

### <a name="prepare-for-upcoming-changes"></a>Voorbereiden op aanstaande wijzigingen

* De volgende Api's retour neren vandaag een account object:

    * [Create-betaald-account](https://api-portal.videoindexer.ai/docs/services/Operations/operations/Create-Paid-Account)
    * [Get-account](https://api-portal.videoindexer.ai/docs/services/Operations/operations/Get-Account)
    * [Get-accounts-Authorization](https://api-portal.videoindexer.ai/docs/services/Operations/operations/Get-Accounts-Authorization)
    * [Get-accounts-with-token](https://api-portal.videoindexer.ai/docs/services/Operations/operations/Get-Accounts-With-Token)
 
    Het account object heeft een `Url` veld dat verwijst naar de locatie van de [video indexer website](https://www.videoindexer.ai/).
Voor betaalde accounts `Url` verwijst het veld momenteel naar een interne URL in plaats van naar de open bare website.
In de komende weken wordt dit gewijzigd en wordt de URL van de [video indexer website](https://www.videoindexer.ai/) voor alle accounts (proef en betaalde) geretourneerd.

    Gebruik niet de interne Url's, u moet de [video indexer open bare api's](https://api-portal.videoindexer.ai/)gebruiken.
* Als u Video Indexer Url's insluit in uw toepassingen en de Url's niet verwijzen naar de [video indexer website](https://www.videoindexer.ai/) of het video indexer API-eind punt ( `https://api.videoindexer.ai` ), maar in plaats van naar een regionaal eind punt (bijvoorbeeld `https://wus2.videoindexer.ai` ), genereert u de url's opnieuw.

   U kunt dit doen door een van de volgende handelingen uit te voeren:

    * Door de URL te vervangen door een URL die verwijst naar de Video Indexer-widget-Api's (bijvoorbeeld de [widget Insights](https://api-portal.videoindexer.ai/docs/services/Operations/operations/Get-Video-Insights-Widget))
    * De Video Indexer-website gebruiken om een nieuwe Inge sloten URL te genereren:
         
         Druk op **Play** om naar de pagina van de video te gaan > Klik op de knop ** &lt; / &gt; insluiten** -> de URL naar uw toepassing kopiëren:
   
    De regionale Url's worden niet ondersteund en worden in de komende weken geblokkeerd.

## <a name="january-2020"></a>Januari 2020
 
### <a name="custom-language-support-for-additional-languages"></a>Aangepaste taal ondersteuning voor extra talen

Video Indexer ondersteunt nu aangepaste taal modellen voor `ar-SY` , `en-UK` en `en-AU` (alleen API).
 
### <a name="delete-account-timeframe-action-update"></a>Update van tijds bestek actie verwijderen

Met account actie verwijderen wordt het account nu binnen 90 dagen verwijderd in plaats van 48 uur.
 
### <a name="new-video-indexer-github-repository"></a>Nieuwe Video Indexer GitHub-opslag plaats

Een nieuwe Video Indexer GitHub met verschillende projecten, aan de slag-hand leidingen en code voorbeelden is nu beschikbaar: https://github.com/Azure-Samples/media-services-video-indexer
 
### <a name="swagger-update"></a>Update Swagger

Video Indexer gecombineerde **authenticaties** en **bewerkingen** in één [video indexer OpenAPI-specificatie (Swagger)](https://api-portal.videoindexer.ai/docs/services/Operations/export?DocumentFormat=OpenApiJson). Ontwikkel aars kunnen de Api's vinden in [video indexer ontwikkelaars Portal](https://api-portal.videoindexer.ai/).

## <a name="december-2019"></a>December 2019

### <a name="update-transcript-with-the-new-api"></a>Transcript bijwerken met de nieuwe API

Werk een specifieke sectie in het transcript bij met de API [Update-video-index](https://api-portal.videoindexer.ai/docs/services/Operations/operations/Update-Video-Index?&pattern=update) .

### <a name="fix-account-configuration-from-the-video-indexer-portal"></a>De account configuratie van de Video Indexer Portal herstellen

U kunt nu Media Services configuratie van de verbinding bijwerken om zelf hulp te krijgen met problemen als: 

* onjuiste Azure Media Services resource
* wachtwoord wijzigingen
* Media Services resources zijn verplaatst tussen abonnementen  

Als u de account configuratie wilt herstellen, gaat u in het Video Indexer Portal naar instellingen > account tabblad (als eigenaar).

### <a name="configure-the-custom-vision-account"></a>Het aangepaste gezichts account configureren

Configureer het aangepaste gezichts account op betaalde accounts met behulp van de Video Indexer-Portal (voorheen werd dit alleen ondersteund door de API). Als u dit wilt doen, meldt u zich aan bij de Video Indexer-Portal en kiest u model aanpassing > animatie tekens > configureren. 

### <a name="scenes-shots-and-keyframes--now-in-one-insight-pane"></a>Scènes, afbeeldingen en keyframes: nu in één inzicht deel venster

Scènes, afbeeldingen en keyframes zijn nu samengevoegd in één inzicht voor eenvoudiger gebruik en navigatie. Wanneer u de gewenste scène selecteert, kunt u zien welke opnamen en keyframes het bevat. 

### <a name="notification-about-a-long-video-name"></a>Melding over een lange video naam

Wanneer een video naam langer is dan 80 tekens, bevat Video Indexer een beschrijvende fout bij het uploaden.

### <a name="streaming-endpoint-is-disabled-notification"></a>Melding van streaming-eind punt is uitgeschakeld

Wanneer streaming-eind punt is uitgeschakeld, wordt in Video Indexer een beschrijvende fout weer gegeven op de pagina van de speler.

### <a name="error-handling-improvement"></a>Verbetering van fout afhandeling

De status code 409 wordt nu geretourneerd door de [video opnieuw te indexeren](https://api-portal.videoindexer.ai/docs/services/Operations/operations/Re-Index-Video?https://api-portal.videoindexer.ai/docs/services/Operations/operations/Re-Index-Video?) en [video-index](https://api-portal.videoindexer.ai/docs/services/Operations/operations/Update-Video-Index?) api's bij te werken voor het geval een video actief wordt geïndexeerd, om te voor komen dat de huidige herindex wijzigingen per ongeluk worden overschreven.

## <a name="november-2019"></a>November 2019
 
* Ondersteuning voor Koreaanse aangepaste taal modellen

    Video indexer ondersteunt nu aangepaste taal modellen in Koreaans ( `ko-KR` ) in zowel de API als de portal. 
* Nieuwe talen die worden ondersteund voor spraak naar tekst (STT)

    Video Indexer-Api's bieden nu ondersteuning voor STT in Arabische Levantine (AR-SY), Engels UK dialect (en-GB) en Engels Australisch dialect (en-AU).
    
    Als u video wilt uploaden, worden de HANS naar zh-CN vervangen, maar worden beide ondersteund, maar wordt zh-CN aanbevolen en nauw keuriger.
    
## <a name="october-2019"></a>Oktober 2019
 
* Zoeken naar tekst met animatie in de galerie

    Wanneer u animatie tekens indexeert, kunt u deze nu zoeken in de video-drukproef weergave van het account. Zie [herkenning van animatie tekens](animated-characters-recognition.md)voor meer informatie.

## <a name="september-2019"></a>September 2019
 
Meerdere verbeteringen aangekondigd op IBC 2019:
 
* Animatie teken herkenning (open bare preview)

    De mogelijkheid om groeps advertenties te herkennen in inhoud met animatie, via integratie met aangepaste visie. Zie voor meer informatie [tekst detectie met animatie](animated-characters-recognition.md).
* Multi-language Identification (open bare preview)

    Detecteer segmenten in meerdere talen in het audio spoor en maak een meertalige transcript op basis hiervan. Eerste ondersteuning: Engels, Spaans, Duits en Frans. Zie [Inhoud in meerdere talen automatisch identificeren en transcriberen](multi-language-identification-transcription.md) voor meer informatie.
* Extractie van benoemde entiteiten voor personen en locatie

    Pakt merken, locaties en mensen uit vanuit spraak en visuele tekst via natuurlijke taal verwerking (NLP).
* Classificatie van type redactionele shot

    Het labelen van afbeeldingen met redactionele typen zoals close up, middel grote opname, twee opnamen, binnen en buiten, enzovoort. Zie [redactionele shot type Detection](scenes-shots-keyframes.md#editorial-shot-type-detection)(Engelstalig) voor meer informatie.
* Uitbrei ding voor het afdekken van het onderwerp-nu dekking van niveau 2
    
    Het model voor het defragmenteren van het onderwerp ondersteunt nu een diepere granulatie van de IPTC-taxonomie. Lees de volledige details op [Azure Media Services nieuwe, AI-innovaties](https://azure.microsoft.com/blog/azure-media-services-new-ai-powered-innovation/).

## <a name="august-2019"></a>Augustus 2019
 
### <a name="video-indexer-deployed-in-uk-south"></a>Video Indexer geïmplementeerd in UK-zuid

U kunt nu een Video Indexer betaalde account maken in de regio UK Zuid.

### <a name="new-editorial-shot-type-insights-available"></a>Nieuwe redactionele-afbeeldings type inzichten beschikbaar

Nieuwe tags die aan video opnamen worden toegevoegd, bieden redactionele ' shot types ' om ze te identificeren met veelvoorkomende redactionele woord groepen die in de werk stroom voor het maken van inhoud worden gebruikt, zoals: extreme close, close, Wide, medium, two shot, buiten, binnen, links en rechts gezicht (beschikbaar in de JSON).

### <a name="new-people-and-locations-entities-extraction-available"></a>Uitpakken van nieuwe personen en locaties-entiteiten beschikbaar

Video Indexer identificeert benoemde locaties en personen via natuurlijke taal verwerking (NLP) van de OCR-en transcriptie van de video. Video Indexer gebruikt machine learning algoritme om te herkennen wanneer specifieke locaties (bijvoorbeeld de Eiffel-Tower) of mensen (bijvoorbeeld John Splinter) worden aangeroepen in een video.

### <a name="keyframes-extraction-in-native-resolution"></a>Extractie van hoofd frames in systeem eigen resolutie

Hoofd frames die door Video Indexer worden geëxtraheerd, zijn beschikbaar in de oorspronkelijke resolutie van de video.
 
### <a name="ga-for-training-custom-face-models-from-images"></a>GA naar aangepaste gezichts modellen van afbeeldingen

Trainings gezichten van afbeeldingen die zijn verplaatst van de preview-modus naar GA (beschikbaar via API en in de portal).

> [!NOTE]
> Er zijn geen prijs wijzigingen die betrekking hebben op de overgang ' preview to GA '.

### <a name="hide-gallery-toggle-option"></a>Schakel optie galerie verbergen

De gebruiker kan kiezen om het tabblad Galerie van de portal te verbergen (vergelijkbaar met het verbergen van het tabblad voor beelden).
 
### <a name="maximum-url-size-increased"></a>De maximale URL-grootte is verhoogd

Ondersteuning voor URL-query teken reeks van 4096 (in plaats van 2048) bij het indexeren van een video.
 
### <a name="support-for-multi-lingual-projects"></a>Ondersteuning voor projecten met meerdere talen

Projecten kunnen nu worden gemaakt op basis van Video's die in verschillende talen zijn geïndexeerd (alleen API).

## <a name="july-2019"></a>Juli 2019

### <a name="editor-as-a-widget"></a>Editor als een widget

De Video Indexer AI-editor is nu beschikbaar als widget die moeten worden inge sloten in klant toepassingen.

### <a name="update-custom-language-model-from-closed-caption-file-from-the-portal"></a>Aangepast taal model bijwerken vanuit ondertitelings bestand vanuit de portal

Klanten kunnen VTT-, SRT-en TTML-bestands indelingen opgeven als invoer voor taal modellen op de pagina aanpassing van de portal.

## <a name="june-2019"></a>Juni 2019

### <a name="video-indexer-deployed-to-japan-east"></a>Video Indexer geïmplementeerd in Japan-Oost

U kunt nu een Video Indexer betaalde account maken in de regio Japan Oost.

### <a name="create-and-repair-account-api-preview"></a>Account-API maken en herstellen (preview-versie)

Er is een nieuwe API toegevoegd waarmee u [het eind punt of de sleutel van de Azure media service-verbinding kunt bijwerken](https://api-portal.videoindexer.ai/docs/services/Operations/operations/Update-Paid-Account-Azure-Media-Services?&groupBy=tag).

### <a name="improve-error-handling-on-upload"></a>Fout afhandeling bij uploaden verbeteren 

Er wordt een beschrijvende bericht weer gegeven in geval van een onjuiste configuratie van het onderliggende Azure Media Services-account.

### <a name="player-timeline-keyframes-preview"></a>Voor beeld van tijdlijn hoofdframes in de speler 

U kunt nu een voor beeld van een afbeelding zien voor elke keer op de tijd lijn van de speler.

### <a name="editor-semi-select"></a>De editor semi-Select

U kunt nu een voor beeld zien van alle inzichten die zijn geselecteerd als gevolg van het kiezen van een specifieke inzichten periode in de editor.

## <a name="may-2019"></a>Mei 2019

### <a name="update-custom-language-model-from-closed-caption-file"></a>Aangepast taal model bijwerken vanuit ondertitelings bestand

[Aangepaste taal model maken](https://api-portal.videoindexer.ai/docs/services/Operations/operations/Create-Language-Model?&groupBy=tag) en [aangepaste taal modellen bijwerken](https://api-portal.videoindexer.ai/docs/services/Operations/operations/Update-Language-Model?&groupBy=tag) api's bieden nu ondersteuning voor VTT-, SRT-en TTML-bestands indelingen als invoer voor taal modellen.

Bij het aanroepen van de [Update video transcriptie-API](https://api-portal.videoindexer.ai/docs/services/Operations/operations/Update-Video-Transcript?&pattern=transcript)wordt de transcripten automatisch toegevoegd. Het trainings model dat is gekoppeld aan de video wordt automatisch bijgewerkt. Zie [een taal model aanpassen met video indexer](customize-language-model-overview.md)voor meer informatie over het aanpassen en trainen van uw taal modellen.

### <a name="new-download-transcript-formats--txt-and-csv"></a>Nieuwe indelingen voor het downloaden van transcripten – TXT en CSV

Naast de indeling voor ondertiteling die al wordt ondersteund (SRT, VTT en TTML), ondersteunt Video Indexer nu het downloaden van transcripten in TXT-en CSV-indelingen.

## <a name="next-steps"></a>Volgende stappen

[Overzicht](video-indexer-overview.md)
