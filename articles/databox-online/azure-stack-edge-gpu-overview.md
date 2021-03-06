---
title: Overzicht van Microsoft Azure Stack Edge met GPU | Microsoft Docs
description: Hierin wordt Azure Stack Edge met GPU beschreven, een opslagoplossing die gebruikmaakt van een fysiek apparaat voor netwerkoverdracht naar Azure.
services: databox
author: alkohli
ms.service: databox
ms.subservice: edge
ms.topic: overview
ms.date: 08/27/2020
ms.author: alkohli
ms.openlocfilehash: a8e1c83573de53962b3646304389023d91ab6dd3
ms.sourcegitcommit: bcda98171d6e81795e723e525f81e6235f044e52
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/01/2020
ms.locfileid: "89256239"
---
# <a name="what-is-azure-stack-edge-with-gpu-preview"></a>Wat is Azure Stack Edge met GPU (Preview)?

Azure Stack Edge met GPU is een Edge-rekenapparaat met AI dat mogelijkheden voor netwerkgegevensoverdracht biedt. Dit artikel geeft een overzicht van de Azure Stack Edge-oplossing, voordelen, belangrijkste mogelijkheden en de scenario’s waarin u dit apparaat kunt implementeren.

Azure Stack Edge met GPU is een hardware-as-a-service-oplossing. Microsoft stuurt u een via de cloud beheerd apparaat dat werkt als een netwerkopslaggateway met een ingebouwde GPU (Graphical Processing Unit) die versnelde AI-deductie mogelijk maakt. 

> [!IMPORTANT]
> Azure Stack Edge met GPU is momenteel beschikbaar als preview-versie. Deze preview-versie wordt aangeboden zonder service level agreement en wordt niet aanbevolen voor productieworkloads. Misschien worden bepaalde functies niet ondersteund of zijn de mogelijkheden ervan beperkt. Zie [Supplemental Terms of Use for Microsoft Azure Previews (Aanvullende gebruiksvoorwaarden voor Microsoft Azure-previews)](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) voor meer informatie.

## <a name="use-cases"></a>Gebruiksvoorbeelden

Hier volgen de verschillende scenario's waarbij Azure Stack Edge kan worden gebruikt voor snelle machine learning-deductie aan de rand en het voorbewerken van gegevens voordat deze naar Azure worden verzonden.

- **Deductie met Azure Machine Learning**: met Azure Stack Edge kunt u ML-modellen uitvoeren om snel resultaten te verkrijgen op basis waarvan actie kan worden ondernomen voordat de gegevens naar de cloud worden verzonden. De volledige gegevensset kan desgewenst worden overgedragen om uw ML-modellen te blijven trainen en verbeteren. Zie [Hardware-versnelde Azure ML-modellen implementeren op Azure Stack Edge](https://docs.microsoft.com/azure/machine-learning/how-to-deploy-fpga-web-service#deploy-to-a-local-edge-server) voor meer informatie over het gebruiken van de met hardware versnelde Azure ML-modellen op het Azure Stack Edge-apparaat.

- **Gegevens voorbewerken** gegevens transformeren voordat ze naar Azure worden verzonden om een bruikbaardere gegevensset te creëren. Voorverwerking kan worden gebruikt om: 

    - Gegevens samen te voegen.
    - Gegevens te wijzigen, bijvoorbeeld om persoonlijke gegevens te verwijderen.
    - Een subset van gegevens maken voor het optimaliseren van opslag en bandbreedte, of voor verdere analyse.
    - IoT-gebeurtenissen te analyseren en erop te reageren. 

- **Gegevens via een netwerk naar Azure overdragen**: Gebruik Azure Stack Edge om gegevens gemakkelijk en snel naar Azure over te dragen voor verdere berekeningen en analyses of voor archivering. 

## <a name="key-capabilities"></a>Belangrijkste mogelijkheden

Azure Stack Edge biedt de volgende mogelijkheden:

|Mogelijkheid |Beschrijving  |
|---------|---------|
|Versnelde AI-deductie| Mogelijk gemaakt door de ingebouwde GPU (een of twee, afhankelijk van het model).|
|Edge-computing      |Gegevens kunnen worden geanalyseerd, verwerkt of gefilterd. Ondersteunt VM's en Kubernetes-clusters.|
|Hoge prestaties | High Performance compute en gegevensoverdracht.|
|Toegang tot gegevens     | Rechtstreekse gegevenstoegang vanuit Azure Storage Blobs en Azure Files met behulp van cloud-API’s voor aanvullende gegevensverwerking in de cloud. Lokale cache op het apparaat wordt gebruikt voor snelle toegang tot laatst gebruikte bestanden.|
|Beheerd via de cloud     |Het apparaat en de service worden beheerd via de Azure-portal.  |
|Offline upload     | Modus zonder verbinding ondersteunt scenario’s voor offline uploaden.|
|Ondersteunde protocollen     | Ondersteuning voor de standaardprotocollen SMB, NFS en REST voor gegevensopname. <br> Ga naar [Systeemvereisten voor Azure Stack Edge](azure-stack-edge-system-requirements.md) voor meer informatie over ondersteunde versies.|
|Gegevensvernieuwing     | Mogelijkheid om lokale bestanden te vernieuwen met de meest recente uit de cloud.|
|Versleuteling    | BitLocker-ondersteuning om gegevens lokaal te versleutelen en de gegevensoverdracht naar de cloud via *HTTPS* te beveiligen.|
|Bandbreedtebeperking| Beperking om het bandbreedtegebruik tijdens piekuren te verminderen.|
|ExpressRoute | Extra beveiliging via ExpressRoute. Gebruik peering-configuratie waarbij verkeer van lokale apparaten naar de cloudopslageindpunten via ExpressRoute wordt geleid. Raadpleeg [Overzicht van ExpressRoute](../expressroute/expressroute-introduction.md) voor meer informatie.

## <a name="components"></a>Onderdelen

De Azure Stack Edge-oplossing bestaat uit een Azure Stack Edge-resource, een fysiek Azure Stack Edge-apparaat en een lokale webinterface.

* **Fysiek Azure Stack Edge-apparaat**: een 1U rackserver die door Microsoft wordt geleverd en die kan worden geconfigureerd om gegevens naar Azure te verzenden.
    
* **Azure Stack Edge-resource**: een resource in de Azure-portal waarmee u een Azure Stack Edge-apparaat kunt beheren via een webinterface waartoe u toegang hebt vanaf verschillende geografische locaties. Gebruik de Azure Stack Edge-resource om resources te maken en beheren, apparaten en waarschuwingen te bekijken en beheren, en shares te beheren.  

    Ga voor meer informatie naar [Uw Azure Stack Edge-apparaat bestellen](azure-stack-edge-gpu-deploy-prep.md#create-a-new-resource).

* **Lokale Azure Stack Edge-webinterface**: Gebruik de lokale webinterface om diagnoses uit te voeren, het Azure Stack Edge-apparaat uit te schakelen of opnieuw op te starten, logboeken met kopieerbewerkingen te bekijken en contact op te nemen met Microsoft Ondersteuning om een serviceaanvraag in te dienen.

    Ga naar [De webgebaseerde gebruikersinterface gebruiken om uw Azure Stack Edge te beheren](azure-stack-edge-manage-access-power-connectivity-mode.md) voor informatie over het gebruik van de webgebaseerde gebruikersinterface.

## <a name="region-availability"></a>Beschikbaarheid in regio’s

Het fysieke Azure Stack Edge-apparaat, de Azure-resource en het doelopslagaccount waarnaar u gegevens overdraagt hoeven zich niet allemaal in dezelfde regio te bevinden.

- **Beschikbaarheid van resource**: voor deze preview-versie is de resource beschikbaar in de regio's US - oost, EU - west en Azië - zuidoost.
    
- **Doelopslagaccounts**: De opslagaccounts waarin de gegevens worden opgeslagen, zijn beschikbaar in alle Azure-regio’s. De regio's waar de opslagaccounts Azure Stack Edge-gegevens opslaan, moeten zich voor optimale prestaties dicht bij het apparaat bevinden. Een opslagaccount dat zich ver van het apparaat vandaan bevindt, resulteert in lange latenties en tragere prestaties.

## <a name="next-steps"></a>Volgende stappen

- De [Systeemvereisten voor Azure Stack Edge](azure-stack-edge-gpu-system-requirements.md) lezen.
- De [Limieten voor Azure Stack Edge](azure-stack-edge-limits.md) begrijpen.
- [Azure Stack Edge](azure-stack-edge-gpu-deploy-prep.md) in de Azure-portal implementeren.
