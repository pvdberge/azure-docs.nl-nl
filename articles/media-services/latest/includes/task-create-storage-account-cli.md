---
author: IngridAtMicrosoft
ms.service: media-services
ms.topic: include
ms.date: 08/17/2020
ms.author: inhenkel
ms.custom: CLI
ms.openlocfilehash: 313c8ea9046deea953b4143f1a0264f81da38764
ms.sourcegitcommit: 37afde27ac137ab2e675b2b0492559287822fded
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2020
ms.locfileid: "88602449"
---
<!-- ### Create a storage account -->

Als u een Media Services-account gaat maken, moet u de naam van een Azure Storage-accountresource opgeven. Het opgegeven opslagaccount wordt gekoppeld aan uw Media Services-account. Zie [Storage-accounts](../storage-account-concept.md) voor meer informatie over het gebruik van Storage-accounts in Media Services.

U moet één **primair** opslag account hebben en u kunt een onbeperkt aantal **secundaire** opslag accounts aan uw Media Services-account koppelen. Media Services ondersteunt **GPv2**-accounts (General-purpose v2) of **GPv1**-accounts (General-purpose v1). Blob-accounts kunt u niet instellen als **primaire** account. Zie [Opties voor Azure Storage-account](../../../storage/common/storage-account-overview.md) voor meer informatie over opslagaccounts. 

In dit voorbeeld maakt u een Standard LRS-account voor algemeen gebruik (v2). Als u wilt experimenteren met opslagaccounts, gebruikt u `--sku Standard_LRS`. Als u echter een SKU voor productie selecteert, kunt u overwegen om `--sku Standard_RAGRS` te gebruiken. Deze biedt geografische replicatie voor bedrijfscontinuïteit. Zie [Opslagaccounts](/cli/azure/storage/account?view=azure-cli-latest) voor meer informatie.

Met de volgende opdracht maakt u een Storage-account die wordt gekoppeld aan de Media Services-account. In het onderstaande script kunt u `storageaccountforams` door uw waarde vervangen. `amsResourceGroup` in de vorige stap moet overeenkomen met de waarde die u hebt opgegeven voor de resource groep. De naam van het opslag account moet minder dan 24 tekens lang zijn.

```azurecli
az storage account create --name storageaccountforams --kind StorageV2 --sku Standard_LRS -l westus2 -g amsResourceGroup
```
