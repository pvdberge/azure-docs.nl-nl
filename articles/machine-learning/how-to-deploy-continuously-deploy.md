---
title: Azure Machine Learning modellen continu implementeren
titleSuffix: Azure Machine Learning
description: Meer informatie over het continu implementeren van modellen met de DevOps-extensie Azure Machine Learning.
services: machine-learning
ms.service: machine-learning
ms.subservice: core
ms.author: gopalv
author: gvashishtha
ms.date: 08/03/2020
ms.topic: conceptual
ms.custom: how-to, tracking-python
ms.openlocfilehash: c95e1012decf1e3ae4ee3fbab8aae1a4c1a71be9
ms.sourcegitcommit: 8def3249f2c216d7b9d96b154eb096640221b6b9
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2020
ms.locfileid: "87544568"
---
# <a name="continuously-deploy-models"></a>Continu implementeren van modellen

In dit artikel wordt beschreven hoe u doorlopende implementatie in azure DevOps kunt gebruiken om automatisch te controleren op nieuwe versies van geregistreerde modellen en deze nieuwe modellen te pushen naar productie.

## <a name="prerequisites"></a>Vereisten

In dit artikel wordt ervan uitgegaan dat u al een model hebt geregistreerd in uw Azure Machine Learning-werk ruimte. Raadpleeg [deze zelf studie](how-to-train-scikit-learn.md) voor een voor beeld van training en het registreren van een scikit-leer model.

## <a name="continuously-deploy-models"></a>Continu implementeren van modellen

U kunt modellen voortdurend implementeren met behulp van de Machine Learning-extensie voor [Azure DevOps](https://azure.microsoft.com/services/devops/). U kunt de Machine Learning extensie voor Azure DevOps gebruiken om een implementatie pijplijn te activeren wanneer een nieuw machine learning model wordt geregistreerd in een Azure Machine Learning-werk ruimte.

1. Meld u aan voor [Azure-pijp lijnen](https://docs.microsoft.com/azure/devops/pipelines/get-started/pipelines-sign-up?view=azure-devops), wat een continue integratie en levering van uw toepassing naar elk platform of Cloud mogelijk maakt. (Houd er rekening mee dat Azure-pijp lijnen niet hetzelfde zijn als [machine learning pijp lijnen](concept-ml-pipelines.md#compare).)

1. [Een Azure DevOps-project maken.](https://docs.microsoft.com/azure/devops/organizations/projects/create-project?view=azure-devops)

1. Installeer de [machine learning extensie voor Azure-pijp lijnen](https://marketplace.visualstudio.com/items?itemName=ms-air-aiagility.vss-services-azureml&targetId=6756afbe-7032-4a36-9cb6-2771710cadc2&utm_source=vstsproduct&utm_medium=ExtHubManageList).

1. Gebruik service verbindingen voor het instellen van een Service-Principal-verbinding met uw Azure Machine Learning-werk ruimte, zodat u toegang hebt tot uw artefacten. Ga naar project instellingen, selecteer **service verbindingen**en selecteer vervolgens **Azure Resource Manager**:

    [![Azure Resource Manager selecteren](media/how-to-deploy-and-where/view-service-connection.png)](media/how-to-deploy-and-where/view-service-connection-expanded.png)

1. Selecteer **AzureMLWorkspace**in de lijst **bereik niveau** en voer de rest van de waarden in:

    ![AzureMLWorkspace selecteren](media/how-to-deploy-and-where/resource-manager-connection.png)

1. Als u uw machine learning model continu wilt implementeren met behulp van Azure-pijp lijnen, selecteert u onder pijp lijnen de optie **release**. Voeg een nieuw artefact toe en selecteer vervolgens het **model** artefact voor AzureML en de service verbinding die u eerder hebt gemaakt. Selecteer het model en de versie om een implementatie te activeren:

    [![AzureML-model selecteren](media/how-to-deploy-and-where/enable-modeltrigger-artifact.png)](media/how-to-deploy-and-where/enable-modeltrigger-artifact-expanded.png)

1. Schakel de model trigger in voor uw model artefact. Wanneer u de trigger inschakelt, wordt elke keer dat de opgegeven versie (dat wil zeggen, de nieuwste versie) van het model geregistreerd in uw werk ruimte, een Azure DevOps release-pijp lijn geactiveerd.

    [![De model trigger inschakelen](media/how-to-deploy-and-where/set-modeltrigger.png)](media/how-to-deploy-and-where/set-modeltrigger-expanded.png)

## <a name="next-steps"></a>Volgende stappen

Bekijk de onderstaande projecten op GitHub voor meer voor beelden van continue implementatie voor ML-modellen.

* [Micro soft-MLOps](https://github.com/Microsoft/MLOps)
* [Micro soft-MLOpsPython](https://github.com/microsoft/MLOpsPython)