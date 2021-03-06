---
title: Een schaalset maken op basis van een gegeneraliseerde installatie kopie met Azure CLI
description: Een schaalset maken met behulp van een gegeneraliseerde installatie kopie in een galerie met gedeelde afbeeldingen.
author: cynthn
ms.service: virtual-machine-scale-sets
ms.subservice: imaging
ms.workload: infrastructure-services
ms.topic: how-to
ms.date: 05/01/2020
ms.author: cynthn
ms.reviewer: akjosh
ms.openlocfilehash: 3cde06b652befa8fbb655273c19f65bd2f38e850
ms.sourcegitcommit: 3d79f737ff34708b48dd2ae45100e2516af9ed78
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/23/2020
ms.locfileid: "87069847"
---
# <a name="create-a-scale-set-from-a-generalized-image-with-azure-cli"></a>Een schaalset maken op basis van een gegeneraliseerde installatie kopie met Azure CLI

Een schaalset maken van een gegeneraliseerde installatie kopie-versie die is opgeslagen in een [Galerie met gedeelde afbeeldingen](shared-image-galleries.md) met behulp van de Azure cli. Zie [instanties van een schaalset maken op basis van een gespecialiseerde](instance-specialized-image-version-cli.md)afbeelding als u een schaalset wilt maken met behulp van een gespecialiseerde afbeeldings versie.

Als u ervoor kiest om de CLI lokaal te installeren en te gebruiken, moet u Azure CLI 2.4.0 of hoger gebruiken voor deze zelfstudie. Voer `az --version` uit om de versie te bekijken. Zie [Azure CLI installeren]( /cli/azure/install-azure-cli) als u de CLI wilt installeren of een upgrade wilt uitvoeren.

Vervang resourcenamen naar behoefte in dit voorbeeld. 

De afbeeldings definities in een galerie weer geven met behulp van [AZ sig Image List-definitie lijst](/cli/azure/sig/image-definition#az-sig-image-definition-list) om de naam en id van de definities weer te geven.

```azurecli-interactive 
resourceGroup=myGalleryRG
gallery=myGallery
az sig image-definition list \
   --resource-group $resourceGroup \
   --gallery-name $gallery \
   --query "[].[name, id]" \
   --output tsv
```

Maak de schaalset met behulp van [`az vmss create`](/cli/azure/vmss#az-vmss-create) . 

Gebruik de definitie-ID van de installatie kopie `--image` om de instanties van de schaalset te maken op basis van de meest recente versie van de installatie kopie die beschikbaar is. U kunt ook instanties van een schaalset maken op basis van een specifieke versie door de versie-ID van de installatie kopie op te geven voor `--image` . Houd er rekening mee dat automatisering met behulp van een specifieke versie van de installatie kopie kan mislukken als deze specifieke installatie kopie versie niet beschikbaar is omdat deze is verwijderd of uit de regio is verwijderd. U kunt het beste de definitie-ID van de installatie kopie gebruiken voor het maken van uw nieuwe VM, tenzij een specifieke installatie kopie versie vereist is.

In dit voor beeld maken we instanties van de nieuwste versie van de *myImageDefinition* -installatie kopie.

```azurecli
az group create --name myResourceGroup --location eastus
az vmss create \
   --resource-group myResourceGroup \
   --name myScaleSet \
   --image "/subscriptions/<Subscription ID>/resourceGroups/myGalleryRG/providers/Microsoft.Compute/galleries/myGallery/images/myImageDefinition" 
   --admin-username azureuser \
   --generate-ssh-keys
```

Het duurt enkele minuten om alle schaalsetresources en VM's te maken en te configureren.

## <a name="next-steps"></a>Volgende stappen
Met [Azure Image Builder (preview)](../virtual-machines/linux/image-builder-overview.md) kunt u het maken van de installatie kopie versie automatiseren, maar u kunt deze zelfs gebruiken om [een nieuwe installatie kopie versie te maken op basis van een bestaande versie van de installatie kopie](../virtual-machines/linux/image-builder-gallery-update-image-version.md). 

U kunt ook een resource voor de galerie met gedeelde afbeeldingen maken met behulp van sjablonen. Er zijn verschillende Azure Quick Start-sjablonen beschikbaar: 

- [Een gedeelde installatiekopiegalerie maken](https://azure.microsoft.com/resources/templates/101-sig-create/)
- [Een installatiekopiedefinitie maken in een gedeelde installatiekopiegalerie](https://azure.microsoft.com/resources/templates/101-sig-image-definition-create/)
- [Een installatiekopieversie maken in een gedeelde installatiekopiegalerie](https://azure.microsoft.com/resources/templates/101-sig-image-version-create/)

Zie het [overzicht](shared-image-galleries.md)voor meer informatie over gedeelde afbeeldings galerieën. Als u problemen ondervindt, raadpleegt u [problemen met de galerie met gedeelde afbeeldingen oplossen](troubleshooting-shared-images.md).