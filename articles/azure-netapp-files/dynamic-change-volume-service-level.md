---
title: Het service niveau van een volume voor Azure NetApp Files dynamisch wijzigen | Microsoft Docs
description: Hierin wordt beschreven hoe u het service niveau van een volume dynamisch kunt wijzigen.
services: azure-netapp-files
documentationcenter: ''
author: b-juche
manager: ''
editor: ''
ms.assetid: ''
ms.service: azure-netapp-files
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: how-to
ms.date: 08/26/2020
ms.author: b-juche
ms.openlocfilehash: fb83b30f0844b9bf0e362e6f1e3a3822ba0044d1
ms.sourcegitcommit: e69bb334ea7e81d49530ebd6c2d3a3a8fa9775c9
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/27/2020
ms.locfileid: "88949997"
---
# <a name="dynamically-change-the-service-level-of-a-volume"></a>Het serviceniveau van een volume dynamisch wijzigen

U kunt het service niveau van een bestaand volume wijzigen door het volume te verplaatsen naar een andere capaciteits groep die gebruikmaakt van het gewenste [service niveau](azure-netapp-files-service-levels.md) voor het volume. Deze in-place wijziging op service niveau voor het volume vereist niet dat u gegevens migreert. Het heeft ook geen invloed op de toegang tot het volume.  

Met deze functionaliteit kunt u op aanvraag voldoen aan de behoeften van uw werk belasting.  U kunt een bestaand volume wijzigen om een hoger service niveau te gebruiken voor betere prestaties, of om een lager service niveau te gebruiken voor de kosten optimalisatie. Als het volume zich op dit moment bevindt in een capaciteits groep die gebruikmaakt van het *standaard* service niveau en u wilt dat het volume het *Premium* -service niveau gebruikt, kunt u het volume dynamisch verplaatsen naar een capaciteits groep die gebruikmaakt van het *Premium* -service niveau.  

De capaciteits groep waarnaar u het volume wilt verplaatsen, moet al bestaan. De capaciteits pool kan andere volumes bevatten.  Als u het volume wilt verplaatsen naar een merk-nieuwe capaciteits groep, moet u [de capaciteits groep maken](azure-netapp-files-set-up-capacity-pool.md) voordat u het volume verplaatst.  

## <a name="considerations"></a>Overwegingen

* Nadat het volume is verplaatst naar een andere capaciteits groep, hebt u geen toegang meer tot de vorige volume activiteiten logboeken en de metrische gegevens van het volume. Het volume wordt gestart met nieuwe activiteiten logboeken en metrische gegevens onder de nieuwe capaciteits groep.

* Als u een volume verplaatst naar een capaciteits groep van een hoger service niveau (bijvoorbeeld van *Standard* naar *Premium* of *Ultra* service niveau), moet u Mini maal zeven dagen wachten voordat u dat volume *opnieuw* kunt verplaatsen naar een capaciteits groep van een lager service niveau (bijvoorbeeld verplaatsen van *Ultra* naar *Premium* of *Standard*).  

## <a name="register-the-feature"></a>De functie registreren

De functie voor het verplaatsen van een volume naar een andere capaciteits groep is momenteel beschikbaar als preview-versie. Als u deze functie voor de eerste keer gebruikt, moet u eerst de functie registreren.

1. De functie registreren: 

    ```azurepowershell-interactive
    Register-AzProviderFeature -ProviderNamespace Microsoft.NetApp -FeatureName ANFTierChange
    ```

2. Controleer de status van de functie registratie: 

    > [!NOTE]
    > Het **RegistrationState** kan `Registering` tot 60 minuten duren voordat de status wordt gewijzigd in `Registered` . Wacht totdat de status is **geregistreerd** voordat u doorgaat.

    ```azurepowershell-interactive
    Get-AzProviderFeature -ProviderNamespace Microsoft.NetApp -FeatureName ANFTierChange
    ```
U kunt ook Azure CLI-opdrachten [`az feature register`](https://docs.microsoft.com/cli/azure/feature?view=azure-cli-latest#az-feature-register) gebruiken [`az feature show`](https://docs.microsoft.com/cli/azure/feature?view=azure-cli-latest#az-feature-show) om de functie te registreren en de registratie status weer te geven. 

## <a name="move-a-volume-to-another-capacity-pool"></a>Een volume verplaatsen naar een andere capaciteits groep

1.  Klik op de pagina volumes met de rechter muisknop op het volume waarvan u het service niveau wilt wijzigen. Selecteer **groep wijzigen**.

    ![Klik met de rechter muisknop op volume](../media/azure-netapp-files/right-click-volume.png)

2. Selecteer in het venster groep wijzigen de capaciteits groep waarnaar u het volume wilt verplaatsen. 

    ![Groep wijzigen](../media/azure-netapp-files/change-pool.png)

3.  Klik op **OK**.


## <a name="next-steps"></a>Volgende stappen  

* [Serviceniveau's voor Azure NetApp Files](azure-netapp-files-service-levels.md)
* [Een capaciteitspool instellen](azure-netapp-files-set-up-capacity-pool.md)
