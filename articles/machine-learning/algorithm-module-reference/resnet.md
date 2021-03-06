---
title: ResNet
titleSuffix: Azure Machine Learning
description: Meer informatie over het maken van een afbeeldings classificatie model met behulp van de ResNet-algoritme.
services: machine-learning
ms.service: machine-learning
ms.subservice: core
ms.topic: reference
author: likebupt
ms.author: keli19
ms.date: 05/26/2020
ms.openlocfilehash: 5d8806b8c93f5a8cbceaa6efa16dfff978dda42e
ms.sourcegitcommit: 53acd9895a4a395efa6d7cd41d7f78e392b9cfbe
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/22/2020
ms.locfileid: "90905199"
---
# <a name="resnet"></a>ResNet

In dit artikel wordt beschreven hoe u de **ResNet** -module in azure machine learning Designer gebruikt om een classificatie model voor installatie kopieën te maken met behulp van de ResNet-algoritme.  

Deze classificatie-algoritme is een geclassificeerde leer methode en vereist een gegevensset met een label. Raadpleeg [Convert to image directory](convert-to-image-directory.md) module voor meer informatie over het ophalen van een gelabelde map met afbeeldingen. U kunt het model trainen door een model en een gelabelde map met installatie kopieën op te geven als invoer voor het [trainen van Pytorch-model](train-pytorch-model.md). Het getrainde model kan vervolgens worden gebruikt om waarden voor de nieuwe invoer voorbeelden te voors pellen met behulp van [Score afbeeldings model](score-image-model.md).

### <a name="more-about-resnet"></a>Meer informatie over ResNet

Raadpleeg [dit artikel](https://pytorch.org/docs/stable/torchvision/models.html?highlight=resnext101_32x8d#torchvision.models.resnext101_32x8d) voor meer informatie over ResNet.

## <a name="how-to-configure-resnet"></a>ResNet configureren

1.  Voeg de module **ResNet** toe aan uw pijp lijn in de ontwerp functie.  

2.  Geef bij **model naam**een naam op van een bepaalde ResNet-structuur en u kunt kiezen uit de ondersteunde ResNet: ' resnet18 ', ' resnet34 ', ' resnet50 ', ' resnet101 ', ' resnet152 ', ' resnet152 ', ' resnext50 \_ 32x4d ', ' resnext101 \_ 32x8d ', ' wide_resnet50 \_ 2 ', ' wide_resnet101 \_ 2 '.

3.  Voor vooraf **getrainde**geeft u op of u een voor ImageNet wilt gebruiken. Indien geselecteerd, kunt u model verfijnen op basis van het geselecteerde vooraf getrainde model. Als u dit selectie vakje uitschakelt, kunt u helemaal zelf trainen.

4.  Verbind de uitvoer van de **DenseNet** -module, de trainings-en validatie afbeelding gegevensset-module naar het [Train Pytorch-model](train-pytorch-model.md). 

5. Verzend de pijp lijn.

## <a name="results"></a>Resultaten

Wanneer de uitvoering van de pijp lijn is voltooid, kunt u het model voor scores gebruiken door het model van [Train Pytorch](train-pytorch-model.md) te verbinden met een [Score image model](score-image-model.md)om waarden voor nieuwe invoer voorbeelden te voors pellen.

## <a name="technical-notes"></a>Technische opmerkingen  

###  <a name="module-parameters"></a>Module parameters  

| Name       | Bereik | Type    | Standaard           | Beschrijving                              |
| ---------- | ----- | ------- | ----------------- | ---------------------------------------- |
| Modelnaam | Elk   | Modus    | resnext101 \_ 32x8d | Naam van een bepaalde ResNet-structuur       |
| Voortraind | Elk   | Boolean-waarde | True              | Of u een vooraf getrainde model wilt gebruiken op ImageNet |
|            |       |         |                   |                                          |

###  <a name="output"></a>Uitvoer  

| Naam            | Type                    | Description                              |
| --------------- | ----------------------- | ---------------------------------------- |
| Niet-traind model | UntrainedModelDirectory | Een niet-traind ResNet-model dat kan worden verbonden met Train Pytorch model. |

## <a name="next-steps"></a>Volgende stappen

Bekijk de [set met modules die beschikbaar zijn](module-reference.md) voor Azure machine learning. 