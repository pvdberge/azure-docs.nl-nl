---
title: 'Quickstart: Content Moderator Python-clientbibliotheek'
titleSuffix: Azure Cognitive Services
description: In deze quickstart leert u hoe u aan de slag kunt gaan met de Azure Cognitive Services Content Moderator-clientbibliotheek voor Python.
services: cognitive-services
author: PatrickFarley
manager: nitinme
ms.service: cognitive-services
ms.subservice: content-moderator
ms.topic: include
ms.date: 08/17/2020
ms.author: pafarley
ms.openlocfilehash: 9a8076dcf23c4049ce2728c5099d691f9e865a5f
ms.sourcegitcommit: 54d8052c09e847a6565ec978f352769e8955aead
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2020
ms.locfileid: "88510089"
---
Ga aan de slag met de Content Moderator-clientbibliotheek voor Python. Volg deze stappen om het pakket te installeren en de voorbeeldcode voor basistaken uit te proberen. Content Moderator is een cognitieve service waarmee tekst, afbeeldingen en video-inhoud van materiaal wordt gecontroleerd op mogelijk aanstootgevende, riskante of anderszins ongewenst inhoud. Wanneer dergelijk materiaal wordt gevonden, past de service de relevante labels (vlaggen) op de inhoud toe. Uw app kan gelabelde inhoud vervolgens afhandelen om te voldoen aan de regelgeving of om een beoogde omgeving voor gebruikers te beheren.

Gebruik de Content Moderator-clientbibliotheek voor Python om het volgende te doen:

* [Tekst modereren](#moderate-text)
* [Aangepaste begrippenlijst gebruiken](#use-a-custom-terms-list)
* [Afbeeldingen modereren](#moderate-images)
* [Een aangepaste afbeeldingslijst gebruiken](#use-a-custom-image-list)
* [Een beoordeling maken](#create-a-review)

[Referentiedocumentatie](https://docs.microsoft.com/python/api/overview/azure/cognitiveservices/contentmoderator?view=azure-python) | [Broncode bibliotheek](https://github.com/Azure/azure-sdk-for-python/tree/master/sdk/cognitiveservices/azure-cognitiveservices-vision-contentmoderator) | [Package (PiPy)](https://pypi.org/project/azure-cognitiveservices-vision-contentmoderator/) | [Voorbeelden](https://github.com/Azure-Samples/cognitive-services-python-sdk-samples)

## <a name="prerequisites"></a>Vereisten

* Azure-abonnement: [Krijg een gratis abonnement](https://azure.microsoft.com/free/cognitive-services/)
* [Python 3.x](https://www.python.org/)

## <a name="setting-up"></a>Instellen

### <a name="create-a-content-moderator-azure-resource"></a>Een Azure-resource voor Content Moderator maken

Azure Cognitive Services worden vertegenwoordigd door Azure-resources waarop u zich abonneert. Maak een resource voor Content Moderator met behulp van de [Azure-portal](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) of [Azure CLI](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account-cli) op uw lokale machine. U kunt ook het volgende doen:

* Uw resource bekijken in de [Azure-portal](https://portal.azure.com/)

Nadat u een sleutel hebt verkregen van uw resource, gaat u [omgevingsvariabelen maken](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account#configure-an-environment-variable-for-authentication) voor de sleutel en de eindpunt-URL, respectievelijk `CONTENT_MODERATOR_SUBSCRIPTION_KEY` en `CONTENT_MODERATOR_ENDPOINT` genaamd.
 
### <a name="create-a-python-script"></a>Een Python-script maken

Maak een nieuw Python-script en open het in uw favoriete editor of IDE. Voeg bovenaan het bestand de volgende `import`-instructies toe.

[!code-python[](~/cognitive-services-quickstart-code/python/ContentModerator/ContentModeratorQuickstart.py?name=snippet_imports)]

Maak vervolgens variabelen voor de eindpuntlocatie en sleutel van uw resource als omgevingsvariabelen. 

[!code-python[](~/cognitive-services-quickstart-code/python/ContentModerator/ContentModeratorQuickstart.py?name=snippet_vars)]

> [!NOTE]
> Als u de omgevingsvariabelen hebt gemaakt nadat u de toepassing hebt gestart, moet u de editor, IDE of shell waarmee deze wordt uitgevoerd, sluiten en opnieuw openen om toegang te krijgen tot de variabelen.

### <a name="install-the-client-library"></a>De clientbibliotheek installeren

U kunt de Content Moderator-clientbibliotheek installeren met de volgende opdracht:

```console
pip install --upgrade azure-cognitiveservices-vision-contentmoderator
```

## <a name="object-model"></a>Objectmodel

De volgende klassen worden gebruikt voor enkele van de belangrijkste functies van de Content Moderator Python-clientbibliotheek.

|Naam|Beschrijving|
|---|---|
|[ContentModeratorClient](https://docs.microsoft.com/python/api/azure-cognitiveservices-vision-contentmoderator/azure.cognitiveservices.vision.contentmoderator.content_moderator_client.contentmoderatorclient?view=azure-python)|Deze klasse is nodig voor alle Content Moderator-functionaliteit. U instantieert deze klasse met uw abonnementsgegevens en gebruikt deze om instanties van andere klassen te maken.|
|[ImageModerationOperations](https://docs.microsoft.com/python/api/azure-cognitiveservices-vision-contentmoderator/azure.cognitiveservices.vision.contentmoderator.operations.imagemoderationoperations?view=azure-python)|Deze klasse biedt de functionaliteit voor het analyseren van afbeeldingen op inhoud voor volwassenen, persoonlijke gegevens of menselijke gezichten.|
|[TextModerationOperations](https://docs.microsoft.com/python/api/azure-cognitiveservices-vision-contentmoderator/azure.cognitiveservices.vision.contentmoderator.operations.textmoderationoperations?view=azure-python)|Deze klasse biedt de functionaliteit voor het analyseren van tekst op taal, grove taal, fouten en persoonlijke gegevens.|
[ReviewsOperations](https://docs.microsoft.com/python/api/azure-cognitiveservices-vision-contentmoderator/azure.cognitiveservices.vision.contentmoderator.operations.reviewsoperations?view=azure-python)|Deze klasse biedt de functionaliteit van de Review-API's, waaronder de methoden voor het maken van taken, aangepaste werkstromen en menselijke beoordelingen.|

## <a name="code-examples"></a>Codevoorbeelden

Deze codefragmenten laten zien hoe u de volgende taken kunt uitvoeren met de Content Moderator-clientbibliotheek voor Python:

* [De client verifiëren](#authenticate-the-client)
* [Tekst modereren](#moderate-text)
* [Aangepaste begrippenlijst gebruiken](#use-a-custom-terms-list)
* [Afbeeldingen modereren](#moderate-images)
* [Een aangepaste afbeeldingslijst gebruiken](#use-a-custom-image-list)
* [Een beoordeling maken](#create-a-review)

## <a name="authenticate-the-client"></a>De client verifiëren

> [!NOTE]
> In deze quickstart wordt ervan uitgegaan dat u [omgevingsvariabelen hebt gemaakt](../../../cognitive-services-apis-create-account.md#configure-an-environment-variable-for-authentication) voor uw Content Moderator-sleutel en -eindpunt.

Instantieer een client met uw eindpunt en sleutel. Maak een [CognitiveServicesCredentials](https://docs.microsoft.com/python/api/msrest/msrest.authentication.cognitiveservicescredentials?view=azure-python)-object met uw sleutel en gebruik het met uw eindpunt om een [ContentModeratorClient-](https://docs.microsoft.com/python/api/azure-cognitiveservices-vision-contentmoderator/azure.cognitiveservices.vision.contentmoderator.content_moderator_client.contentmoderatorclient?view=azure-python)-object te maken.

[!code-python[](~/cognitive-services-quickstart-code/python/ContentModerator/ContentModeratorQuickstart.py?name=snippet_client)]

## <a name="moderate-text"></a>Tekst modereren

In de volgende code wordt een Content Moderator-client gebruikt om een stuk tekst te analyseren en de resultaten af te drukken naar de console. Maak eerst de map **text_files/** in de hoofdmap van het project en voeg een bestand met de naam *content_moderator_text_moderation.txt* toe. Voeg uw eigen tekst toe aan dit bestand, of gebruik de volgende voorbeeldtekst:

```
Is this a grabage email abcdef@abcd.com, phone: 4255550111, IP: 255.255.255.255, 1234 Main Boulevard, Panapolis WA 96555.
Crap is the profanity here. Is this information PII? phone 2065550111
```

Voeg een verwijzing toe naar de nieuwe map.

[!code-python[](~/cognitive-services-quickstart-code/python/ContentModerator/ContentModeratorQuickstart.py?name=snippet_textfolder)]

Voeg de volgende code toe aan uw Python-script.

[!code-python[](~/cognitive-services-quickstart-code/python/ContentModerator/ContentModeratorQuickstart.py?name=snippet_textmod)]

## <a name="use-a-custom-terms-list"></a>Aangepaste termenlijst gebruiken

De volgende code laat zien hoe u een lijst met aangepaste termen voor tekstmoderatie beheert. U kunt de klasse [ListManagementTermListsOperations](https://docs.microsoft.com/python/api/azure-cognitiveservices-vision-contentmoderator/azure.cognitiveservices.vision.contentmoderator.operations.listmanagementtermlistsoperations?view=azure-python) gebruiken om een lijst met termen te maken, de afzonderlijke termen te beheren en andere teksten ermee te screenen.

### <a name="get-sample-text"></a>Voorbeeldtekst ophalen

Om dit voorbeeld te gebruiken moet u de map **text_files/** maken in de hoofdmap van het project en een bestand met de naam *content_moderator_term_list.txt* toevoegen. Dit bestand moet organische tekst bevatten die wordt gecontroleerd aan de hand van de lijst met termen. U kunt de volgende voorbeeldtekst gebruiken:

```
This text contains the terms "term1" and "term2".
```

Voeg een verwijzing naar de map toe als u deze nog niet hebt gedefinieerd.

[!code-python[](~/cognitive-services-quickstart-code/python/ContentModerator/ContentModeratorQuickstart.py?name=snippet_textfolder)]

### <a name="create-a-list"></a>Een lijst maken

Voeg de volgende code toe aan het Python-script om een lijst met aangepaste termen te maken en de id-waarde op te slaan.

[!code-python[](~/cognitive-services-quickstart-code/python/ContentModerator/ContentModeratorQuickstart.py?name=snippet_termslist_create)]

### <a name="define-list-details"></a>Lijstdetails definiëren

U kunt de ID van een lijst gebruiken om de naam en beschrijving ervan te bewerken.

[!code-python[](~/cognitive-services-quickstart-code/python/ContentModerator/ContentModeratorQuickstart.py?name=snippet_termslist_details)]

### <a name="add-a-term-to-the-list"></a>Een term toevoegen aan de lijst

Met de volgende code worden de termen `"term1"` en `"term2"` aan de lijst toegevoegd.

[!code-python[](~/cognitive-services-quickstart-code/python/ContentModerator/ContentModeratorQuickstart.py?name=snippet_termslist_add)]

### <a name="get-all-terms-in-the-list"></a>Alle termen in de lijst ophalen

U kunt de lijst-id gebruiken om alle termen in de lijst te retourneren.

[!code-python[](~/cognitive-services-quickstart-code/python/ContentModerator/ContentModeratorQuickstart.py?name=snippet_termslist_getterms)]

### <a name="refresh-the-list-index"></a>De lijstindex vernieuwen

Wanneer u termen aan de lijst toevoegt of eruit verwijdert, moet u de index vernieuwen voordat u de bijgewerkte lijst kunt gebruiken.

[!code-python[](~/cognitive-services-quickstart-code/python/ContentModerator/ContentModeratorQuickstart.py?name=snippet_termslist_refresh)]

### <a name="screen-text-against-the-list"></a>Tekst screenen op basis van de lijst

De belangrijkste functionaliteit van de lijst met aangepaste termen is het vergelijken van teksten met de lijst om te zien of er overeenkomende termen zijn. 

[!code-python[](~/cognitive-services-quickstart-code/python/ContentModerator/ContentModeratorQuickstart.py?name=snippet_termslist_screen)]

### <a name="remove-a-term-from-a-list"></a>Een term uit een lijst verwijderen

Met de volgende code wordt de term `"term1"` verwijderd uit de lijst.

[!code-python[](~/cognitive-services-quickstart-code/python/ContentModerator/ContentModeratorQuickstart.py?name=snippet_termslist_remove)]

### <a name="remove-all-terms-from-a-list"></a>Alle termen uit een lijst verwijderen

Gebruik de volgende code om alle termen van een lijst te wissen.

[!code-python[](~/cognitive-services-quickstart-code/python/ContentModerator/ContentModeratorQuickstart.py?name=snippet_termslist_removeall)]

### <a name="delete-list"></a>Lijst verwijderen

Gebruik de volgende code om een lijst met aangepaste termen te verwijderen.

[!code-python[](~/cognitive-services-quickstart-code/python/ContentModerator/ContentModeratorQuickstart.py?name=snippet_termslist_deletelist)]

## <a name="moderate-images"></a>Afbeeldingen modereren

In de volgende code wordt een Content Moderator-client samen met een [ImageModerationOperations](https://docs.microsoft.com/python/api/azure-cognitiveservices-vision-contentmoderator/azure.cognitiveservices.vision.contentmoderator.operations.imagemoderationoperations?view=azure-python)-object gebruikt om externe afbeeldingen te analyseren op inhoud voor volwassenen.

### <a name="get-images"></a>Afbeeldingen ophalen

Definieer een verwijzing naar enkele te analyseren afbeeldingen.

[!code-python[](~/cognitive-services-quickstart-code/python/ContentModerator/ContentModeratorQuickstart.py?name=snippet_imagemodvars)]

Voeg vervolgens de volgende code toe om uw afbeeldingen te doorlopen. De rest van de code in deze sectie wordt binnen deze lus geplaatst.

[!code-python[](~/cognitive-services-quickstart-code/python/ContentModerator/ContentModeratorQuickstart.py?name=snippet_imagemod_iterate)]

### <a name="check-for-adultracy-content"></a>Controleren op inhoud voor volwassenen/gewaagde inhoud

Met de volgende code wordt de afbeelding op de opgegeven URL gecontroleerd op inhoud voor volwassenen of gewaagde inhoud en worden de resultaten afgedrukt naar de console. Zie de handleiding [Concepten voor afbeeldingsmoderatie](../../image-moderation-api.md) voor informatie over de betekenis van deze begrippen.

[!code-python[](~/cognitive-services-quickstart-code/python/ContentModerator/ContentModeratorQuickstart.py?name=snippet_imagemod_ar)]

### <a name="check-for-visible-text"></a>Controleren op zichtbare tekst

Met de volgende code wordt de afbeelding gecontroleerd op zichtbare tekstinhoud en worden de resultaten afgedrukt naar de console.

[!code-python[](~/cognitive-services-quickstart-code/python/ContentModerator/ContentModeratorQuickstart.py?name=snippet_imagemod_text)]

### <a name="check-for-faces"></a>Controleren op gezichten

Met de volgende code wordt de afbeelding gecontroleerd op menselijke gezichten en worden de resultaten afgedrukt naar de console.

[!code-python[](~/cognitive-services-quickstart-code/python/ContentModerator/ContentModeratorQuickstart.py?name=snippet_imagemod_face)]

## <a name="use-a-custom-image-list"></a>Een aangepaste afbeeldingslijst gebruiken

De volgende code laat zien hoe u een aangepaste lijst met afbeeldingen voor afbeeldingsmoderatie beheert. Deze functie is handig als uw platform vaak exemplaren van dezelfde set afbeeldingen ontvangt die u eruit wilt filteren. Door een lijst bij te houden van deze specifieke afbeeldingen, kunt u de prestaties verbeteren. Met de klasse [ListManagementImageListsOperations](https://docs.microsoft.com/python/api/azure-cognitiveservices-vision-contentmoderator/azure.cognitiveservices.vision.contentmoderator.operations.listmanagementimagelistsoperations?view=azure-python) kunt u een lijst met afbeeldingen maken, de afzonderlijke afbeeldingen in de lijst beheren en andere afbeeldingen ermee vergelijken.

Maak de volgende tekstvariabelen om de afbeeldings-URL's op te slaan die u in dit scenario gebruikt.

[!code-python[](~/cognitive-services-quickstart-code/python/ContentModerator/ContentModeratorQuickstart.py?name=snippet_imagelistvars)]

> [!NOTE]
> Dit is niet de eigenlijke lijst zelf, maar een informele lijst met afbeeldingen die worden toegevoegd in de sectie `add images` van de code.


### <a name="create-an-image-list"></a>Een afbeeldingslijst maken

Voeg de volgende code toe om een lijst met afbeeldingen te maken en sla een verwijzing naar de id ervan op te slaan.

[!code-python[](~/cognitive-services-quickstart-code/python/ContentModerator/ContentModeratorQuickstart.py?name=snippet_imagelist_create)]

### <a name="add-images-to-a-list"></a>Afbeeldingen toevoegen aan een lijst

Met de volgende code worden al uw afbeeldingen aan de lijst toegevoegd.

[!code-python[](~/cognitive-services-quickstart-code/python/ContentModerator/ContentModeratorQuickstart.py?name=snippet_imagelist_add)]

Definieer de hulpfunctie **add_images** elders in het script.

[!code-python[](~/cognitive-services-quickstart-code/python/ContentModerator/ContentModeratorQuickstart.py?name=snippet_imagelist_addhelper)]

### <a name="get-images-in-list"></a>Afbeeldingen in lijst ophalen

Met de volgende code worden de namen van alle afbeeldingen in uw lijst afgedrukt.

[!code-python[](~/cognitive-services-quickstart-code/python/ContentModerator/ContentModeratorQuickstart.py?name=snippet_imagelist_getimages)]

### <a name="update-list-details"></a>Lijstdetails bijwerken

U kunt de lijst-id gebruiken om de naam en beschrijving van de lijst bij te werken.

[!code-python[](~/cognitive-services-quickstart-code/python/ContentModerator/ContentModeratorQuickstart.py?name=snippet_imagelist_updatedetails)]

### <a name="get-list-details"></a>Lijstdetails ophalen

Gebruik de volgende code om de huidige details van de lijst af te drukken.

[!code-python[](~/cognitive-services-quickstart-code/python/ContentModerator/ContentModeratorQuickstart.py?name=snippet_imagelist_getdetails)]

### <a name="refresh-the-list-index"></a>De lijstindex vernieuwen

Nadat u afbeeldingen hebt toegevoegd of verwijderd, moet u de lijstindex vernieuwen voordat u deze kunt gebruiken om andere afbeeldingen te screenen.

[!code-python[](~/cognitive-services-quickstart-code/python/ContentModerator/ContentModeratorQuickstart.py?name=snippet_imagelist_refresh)]

### <a name="match-images-against-the-list"></a>Afbeeldingen vergelijken met de lijst

De belangrijkste functie van lijsten met afbeeldingen is nieuwe afbeeldingen ermee te vergelijken en te controleren of er overeenkomsten zijn.

[!code-python[](~/cognitive-services-quickstart-code/python/ContentModerator/ContentModeratorQuickstart.py?name=snippet_imagelist_match)]

### <a name="remove-an-image-from-the-list"></a>Een afbeelding verwijderen uit de lijst

Met de volgende code wordt een item uit de lijst verwijderd. In dit geval is het een afbeelding die niet in de lijstcategorie past.

[!code-python[](~/cognitive-services-quickstart-code/python/ContentModerator/ContentModeratorQuickstart.py?name=snippet_imagelist_remove)]

### <a name="remove-all-images-from-a-list"></a>Alle afbeeldingen uit een lijst verwijderen

Gebruik de volgende code om een lijst met afbeeldingen leeg te maken.

[!code-python[](~/cognitive-services-quickstart-code/python/ContentModerator/ContentModeratorQuickstart.py?name=snippet_imagelist_removeall)]

### <a name="delete-the-image-list"></a>De lijst met afbeeldingen verwijderen

Gebruik de volgende code om een lijst met afbeeldingen te verwijderen.

[!code-python[](~/cognitive-services-quickstart-code/python/ContentModerator/ContentModeratorQuickstart.py?name=snippet_imagelist_delete)]

## <a name="create-a-review"></a>Een beoordeling maken

U kunt de Content Moderator Python-clientbibliotheek gebruiken om inhoud naar het [Review-programma](https://contentmoderator.cognitive.microsoft.com) te sturen zodat menselijke moderators die kunnen beoordelen. Zie de [conceptgids over het beoordelingsprogramma](../../review-tool-user-guide/human-in-the-loop.md) voor meer informatie over het beoordelingsprogramma.

In de volgende code wordt de [Reviews](https://docs.microsoft.com/python/api/azure-cognitiveservices-vision-contentmoderator/azure.cognitiveservices.vision.contentmoderator.operations.reviewsoperations?view=azure-python)-klasse gebruikt om een beoordeling te maken, de id ervan op te halen en de gegevens ervan te controleren na menselijke invoer te hebben gekregen via de webportal van het Review-programma.

### <a name="get-review-credentials"></a>Review-referentie ophalen

Begin door u aan te melden bij het Review-programma en uw teamnaam op te halen. Wijs deze vervolgens toe aan de juiste variabele in de code. U kunt desgewenst een callback-eindpunt instellen om updates te ontvangen over de activiteit van de beoordeling.

[!code-python[](~/cognitive-services-quickstart-code/python/ContentModerator/ContentModeratorQuickstart.py?name=snippet_imagereview_vars)]

### <a name="create-an-image-review"></a>Een afbeeldingsbeoordeling maken

Voeg de volgende code toe om een beoordeling te maken en te posten voor de opgegeven afbeeldings-URL. Met de code wordt een verwijzing naar de beoordelings-id opgeslagen. 
[!code-python[](~/cognitive-services-quickstart-code/python/ContentModerator/ContentModeratorQuickstart.py?name=snippet_imagereview_create)]

### <a name="get-review-details"></a>Beoordelingsdetails ophalen

Gebruik de volgende code om de details van een bepaalde beoordeling te controleren. Nadat u de beoordeling hebt gemaakt, kunt u zelf naar het Review-programma gaan en werken met de inhoud. Zie de [Instructiegids voor Review](https://docs.microsoft.com/azure/cognitive-services/content-moderator/review-tool-user-guide/review-moderated-images) voor informatie hierover. Wanneer u klaar bent, kunt u deze code opnieuw uitvoeren en worden de resultaten van het beoordelingsproces opgehaald.

[!code-python[](~/cognitive-services-quickstart-code/python/ContentModerator/ContentModeratorQuickstart.py?name=snippet_imagereview_getdetails)]

Als u in dit scenario een callback-eindpunt hebt gebruikt, zou het een gebeurtenis in deze indeling moeten ontvangen:

```console
{'callback_endpoint': 'https://requestb.in/qmsakwqm',
 'content': '',
 'content_id': '3ebe16cb-31ed-4292-8b71-1dfe9b0e821f',
 'created_by': 'cspythonsdk',
 'metadata': [{'key': 'sc', 'value': 'True'}],
 'review_id': '201901i14682e2afe624fee95ebb248643139e7',
 'reviewer_result_tags': [{'key': 'a', 'value': 'True'},
                          {'key': 'r', 'value': 'True'}],
 'status': 'Complete',
 'sub_team': 'public',
 'type': 'Image'}
```

## <a name="run-the-application"></a>De toepassing uitvoeren

Voer de toepassing uit met de opdracht `python` in uw quickstart-bestand.

```console
python quickstart-file.py
```

## <a name="clean-up-resources"></a>Resources opschonen

Als u een Cognitive Services-abonnement wilt opschonen en verwijderen, kunt u de resource of resourcegroep verwijderen. Als u de resourcegroep verwijdert, worden ook alle bijbehorende resources verwijderd.

* [Portal](../../../cognitive-services-apis-create-account.md#clean-up-resources)
* [Azure-CLI](../../../cognitive-services-apis-create-account-cli.md#clean-up-resources)

## <a name="next-steps"></a>Volgende stappen

In deze quickstart hebt u geleerd hoe u de Content Moderator Python-bibliotheek kunt gebruiken om moderatietaken uit te voeren. Nu kunt u doorgaan en in conceptgids meer lezen over het modereren van afbeeldingen en andere media.

> [!div class="nextstepaction"]
>[Concepten voor afbeeldingsmoderatie](https://docs.microsoft.com/azure/cognitive-services/content-moderator/image-moderation-api)

* [Wat is Azure Content Moderator?](../../overview.md)
* De broncode voor dit voorbeeld is te vinden op [GitHub](https://github.com/Azure-Samples/cognitive-services-quickstart-code/blob/master/python/ContentModerator/ContentModeratorQuickstart.py).