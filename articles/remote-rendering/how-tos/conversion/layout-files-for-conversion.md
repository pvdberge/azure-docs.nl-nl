---
title: Bestanden indelen voor conversie
description: Aanbevelingen over hoe het beste bestanden in de invoer container plaatst.
author: MalcolmTyrrell
ms.author: matyrr
ms.date: 09/03/2020
ms.topic: how-to
ms.openlocfilehash: 8acd19408c328ef3f534ba7bc41c96e395f768be
ms.sourcegitcommit: 655e4b75fa6d7881a0a410679ec25c77de196ea3
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/07/2020
ms.locfileid: "89510972"
---
# <a name="laying-out-files-for-conversion"></a>Bestanden indelen voor conversie

Voor een juiste verwerking van een Asset moet de conversie service alle invoer bestanden kunnen vinden.
Deze bestaan uit het bestand van het hoofd activum dat wordt geconverteerd en meestal enkele andere bestanden waarnaar wordt verwezen door paden binnen het activa bestand.
De aanvraag voor het converteren van een activum krijgt twee para meters die bepalen hoe de conversie service deze bestanden vindt: de `input.folderPath` (optioneel) en de `input.inputAssetPath` .
Ze zijn volledig gedocumenteerd op de pagina [conversie rest API](conversion-rest-api.md) .
Voor het indelen van bestanden is het belang rijk om te weten dat de `folderPath` volledige set met bestanden die beschikbaar zijn voor de conversie service tijdens het verwerken van de Asset wordt bepaald.

## <a name="placing-files-so-they-can-be-found"></a>Bestanden plaatsen zodat ze kunnen worden gevonden

Wanneer een bron activum gebruikmaakt van externe bestanden, worden paden naar deze bestanden opgeslagen in de Asset.
De conversie service moet deze paden interpreteren in een bestands systeem dat verschilt van het oorspronkelijke bestands systeem van het actief.
Als de paden worden opgeslagen als relatieve paden en de relatieve locatie tussen de bron-en het bestand waarnaar wordt verwezen, ongewijzigd is, is het eenvoudig om de conversie service te vinden van het bestand waarnaar wordt verwezen.

> [!Note]
> We raden u aan bestanden in de invoer container te plaatsen, zodat de relatieve locaties van de bestanden hetzelfde zijn als toen de Asset werd gemaakt.

## <a name="finding-textures"></a>Structuren zoeken

Als gevolg van de vele manieren waarop activa kunnen worden gegenereerd, moet de conversie service flexibel zijn.
Het heeft met name betrekking op situaties waarbij de paden in het activum en de locatie van bitmappatronen niet exact overeenkomen.
Een voor beeld hiervan is wanneer assets worden gegenereerd die absolute paden bevatten, omdat deze paden nooit overeenkomen met het bestands systeem dat door de conversie service wordt gebruikt.
Voor het afhandelen van deze situatie wordt gebruikgemaakt van een aanbevolen aanpak voor het zoeken van structuren.

De algoritme voor het zoeken van bitmappatronen is als volgt: als u een pad hebt opgegeven dat is opgeslagen in een Asset, zoekt u het langste subpad achtervoegsel dat, wanneer dit wordt gebruikt als een relatief pad van de locatie van de bron-Asset, een bestand dat bestaat.
Als geen enkel subpad (inclusief het hele pad) een bestand bedoelt, wordt de textuur als ontbrekend beschouwd.

Houd rekening met het volgende contrived-bestands systeem: 
```
G:\CONVERSION
├───Assets
│   │   myAsset.fbx
│   │   myTexture.png            <- A
│   │
│   └───Textures
│       │   myTexture.png        <- B
│       │
│       └───MyAssetTextures
│               myTexture.png    <- C
│
└───Textures
    │   myTexture.png            <- D
    │
    └───MyAssetTextures
            myTexture.png        <- E
```
Als myAsset. fbx naar een bitmappatroon met het relatieve pad verwijst `..\Textures\MyAssetTextures\myTexture.png` , gebruikt de conversie service bestand E. Het kan zelfs een van de bestanden A, C en E gebruiken als deze bestaan, omdat het bestand E voor de voor keur heeft, omdat het is gevonden met het langste achtervoegsel.
De bestanden B en D worden nooit gebruikt, omdat `Textures\myTexture.png` deze geen deel uitmaakt van een achtervoegsel van het opgeslagen pad.
Als de asset in plaats daarvan de paden bevat `H:\Foo\Bar\Textures\MyAssetTextures\myTexture.png` of `..\..\..\Foo\Bar\Textures\MyAssetTextures\myTexture.png` , dan kan de conversie service de bestanden A en C vinden als deze bestaan (vóór de overdracht van C over a). E kan echter niet op deze manier worden gevonden en het bestand moet worden verplaatst.
Dit kan worden opgelost door de map textures naast het activum te verplaatsen.

> [!Note]
> Als er geen bitmappatronen worden gevonden, is een mogelijke oplossing om ervoor te zorgen dat het activum een item op hetzelfde niveau is van een substructuur die de bitmappatronen bevat.

## <a name="next-steps"></a>Volgende stappen

- [Modelconversie](model-conversion.md)
