---
title: Een tensor flow-model trainen en implementeren
titleSuffix: Azure Machine Learning
description: Meer informatie over het uitvoeren van tensor flow-trainings scripts op schaal met behulp van Azure Machine Learning.
services: machine-learning
ms.service: machine-learning
ms.subservice: core
ms.author: maxluk
author: maxluk
ms.date: 08/20/2019
ms.topic: conceptual
ms.custom: how-to
ms.openlocfilehash: 840ccec1da6df0df1ccd710d83634b850d7370fa
ms.sourcegitcommit: 53acd9895a4a395efa6d7cd41d7f78e392b9cfbe
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/22/2020
ms.locfileid: "90904910"
---
# <a name="build-a-tensorflow-deep-learning-model-at-scale-with-azure-machine-learning"></a>Bouw een tensor flow-Learning model op schaal met Azure Machine Learning


Dit artikel laat u zien hoe u uw [tensor flow](https://www.tensorflow.org/overview) -trainings scripts op schaal kunt uitvoeren met behulp van de [tensor flow Estimator](https://docs.microsoft.com/python/api/azureml-train-core/azureml.train.dnn.tensorflow?view=azure-ml-py&preserve-view=true) -klasse van Azure machine learning. In dit voor beeld wordt een tensor flow-model getraind en geregistreerd om handgeschreven cijfers te classificeren met behulp van een diepe Neural Network (DNN).

Of u nu een tensor flow-model ontwikkelt of een [bestaand model](how-to-deploy-existing-model.md) in de Cloud brengt, u kunt Azure machine learning gebruiken voor het uitschalen van open-source trainings taken om productie-kwaliteits modellen te bouwen, te implementeren, te maken en te bewaken.

Meer informatie over [uitgebreide kennis en machine learning](concept-deep-learning-vs-machine-learning.md).

## <a name="prerequisites"></a>Vereisten

Voer deze code uit in een van de volgende omgevingen:

 - Azure Machine Learning Compute-instantie-geen down loads of installatie vereist

     - Voltooi de [zelf studie: installatie omgeving en werk ruimte](tutorial-1st-experiment-sdk-setup.md) om een toegewezen notebook server te maken vooraf geladen met de SDK en de voor beeld-opslag plaats.
    - Zoek in de map met uitgebreide trainingen op de notebook server een volledig en uitgebreid notitie blok door naar deze map te navigeren: **How-to-use-azureml > ml-frameworks > tensor flow > deployment > Train-afstemming-Tune-Deploy-with-tensor flow** . 
 
 - Uw eigen Jupyter Notebook-server

    - [Installeer de Azure machine learning SDK](https://docs.microsoft.com/python/api/overview/azure/ml/install?view=azure-ml-py&preserve-view=true).
    - [Maak een configuratie bestand voor de werk ruimte](how-to-configure-environment.md#workspace).
    - [De voorbeeld script bestanden downloaden](https://github.com/Azure/MachineLearningNotebooks/tree/master/how-to-use-azureml/ml-frameworks/tensorflow/deployment/train-hyperparameter-tune-deploy-with-tensorflow) `mnist-tf.py` maar `utils.py`
     
    U kunt ook een voltooide [Jupyter notebook versie](https://github.com/Azure/MachineLearningNotebooks/blob/master/how-to-use-azureml/ml-frameworks/tensorflow/deployment/train-hyperparameter-tune-deploy-with-tensorflow/train-hyperparameter-tune-deploy-with-tensorflow.ipynb) van deze hand leiding vinden op de pagina met voor beelden van github. Het notitie blok bevat uitgebreide secties die betrekking hebben op intelligent afstemming tuning, model implementatie en notebook widgets.

## <a name="set-up-the-experiment"></a>Het experiment instellen

In deze sectie wordt het trainings experiment opgesteld door het laden van de vereiste Python-pakketten, het initialiseren van een werk ruimte, het maken van een experiment en het uploaden van de trainings gegevens en trainings scripts.

### <a name="import-packages"></a>Pakketten importeren

Importeer eerst de benodigde python-bibliotheken.

```Python
import os
import urllib
import shutil
import azureml

from azureml.core import Experiment
from azureml.core import Workspace, Run

from azureml.core.compute import ComputeTarget, AmlCompute
from azureml.core.compute_target import ComputeTargetException
from azureml.train.dnn import TensorFlow
```

### <a name="initialize-a-workspace"></a>Een werk ruimte initialiseren

De [Azure machine learning werk ruimte](concept-workspace.md) is de resource op het hoogste niveau voor de service. Het biedt u een centrale locatie voor het werken met alle artefacten die u maakt. In de python-SDK hebt u toegang tot de werkruimte artefacten door een [`workspace`](https://docs.microsoft.com/python/api/azureml-core/azureml.core.workspace.workspace?view=azure-ml-py&preserve-view=true) object te maken.

Maak een werkruimte object op basis van het `config.json` bestand dat in de [sectie vereisten](#prerequisites)is gemaakt.

```Python
ws = Workspace.from_config()
```

### <a name="create-a-deep-learning-experiment"></a>Een diep leer experiment maken

Maak een experiment en een map om uw trainings scripts te bewaren. In dit voor beeld maakt u een experiment met de naam ' TF-mnist '.

```Python
script_folder = './tf-mnist'
os.makedirs(script_folder, exist_ok=True)

exp = Experiment(workspace=ws, name='tf-mnist')
```

### <a name="create-a-file-dataset"></a>Een bestands gegevensset maken

Een- `FileDataset` object verwijst naar een of meer bestanden in uw werk ruimte of open bare url's. De bestanden hebben een wille keurige indeling en de-klasse biedt u de mogelijkheid om de bestanden te downloaden of te koppelen aan uw computer. Door een te maken `FileDataset` , maakt u een verwijzing naar de locatie van de gegevens bron. Als u trans formaties hebt toegepast op de gegevensset, worden deze ook opgeslagen in de gegevens verzameling. De gegevens blijven bewaard op de bestaande locatie, dus maakt u geen extra opslagkosten. Raadpleeg de [hand leiding van het](https://docs.microsoft.com/azure/machine-learning/how-to-create-register-datasets) `Dataset` pakket voor meer informatie.

```python
from azureml.core.dataset import Dataset

web_paths = [
            'http://yann.lecun.com/exdb/mnist/train-images-idx3-ubyte.gz',
            'http://yann.lecun.com/exdb/mnist/train-labels-idx1-ubyte.gz',
            'http://yann.lecun.com/exdb/mnist/t10k-images-idx3-ubyte.gz',
            'http://yann.lecun.com/exdb/mnist/t10k-labels-idx1-ubyte.gz'
            ]
dataset = Dataset.File.from_files(path=web_paths)
```

Gebruik de- `register()` methode om de gegevensset te registreren in uw werk ruimte, zodat deze kan worden gedeeld met anderen, opnieuw worden gebruikt in verschillende experimenten en waarnaar wordt verwezen met de naam in uw trainings script.

```python
dataset = dataset.register(workspace=ws,
                           name='mnist dataset',
                           description='training and test dataset',
                           create_new_version=True)

# list the files referenced by dataset
dataset.to_path()
```

## <a name="create-a-compute-target"></a>Een rekendoel maken

Maak een compute-doel voor uw tensor flow-taak om uit te voeren. In dit voor beeld maakt u een Azure Machine Learning Compute-cluster waarvoor GPU is ingeschakeld.

```Python
cluster_name = "gpucluster"

try:
    compute_target = ComputeTarget(workspace=ws, name=cluster_name)
    print('Found existing compute target')
except ComputeTargetException:
    print('Creating a new compute target...')
    compute_config = AmlCompute.provisioning_configuration(vm_size='STANDARD_NC6', 
                                                           max_nodes=4)

    compute_target = ComputeTarget.create(ws, cluster_name, compute_config)

    compute_target.wait_for_completion(show_output=True, min_node_count=None, timeout_in_minutes=20)
```

[!INCLUDE [low-pri-note](../../includes/machine-learning-low-pri-vm.md)]

Zie voor meer informatie over Compute-doelen het artikel [Wat is een reken doel](concept-compute-target.md) .

## <a name="create-a-tensorflow-estimator"></a>Een tensor flow-Estimator maken

De [tensor flow Estimator](https://docs.microsoft.com/python/api/azureml-train-core/azureml.train.dnn.tensorflow?view=azure-ml-py&preserve-view=true) biedt een eenvoudige manier om een tensor flow-trainings taak te starten op een compute-doel.

De tensor flow Estimator wordt geïmplementeerd via de algemene [`estimator`](https://docs.microsoft.com//python/api/azureml-train-core/azureml.train.estimator.estimator?view=azure-ml-py&preserve-view=true) klasse, die kan worden gebruikt ter ondersteuning van een Framework. Voor meer informatie over trainings modellen die gebruikmaken van de algemene Estimator, raadpleegt [u modellen met Azure machine learning met behulp van Estimator](how-to-train-ml-models.md)

Als uw trainings script extra PIP-of Conda-pakketten nodig heeft om uit te voeren, kunt u de pakketten op de resulterende docker-installatie kopie installeren door hun namen door te geven via de `pip_packages` `conda_packages` argumenten en.


> [!WARNING]
> Azure Machine Learning trainings scripts worden uitgevoerd door de hele bronmap te kopiëren. Als u gevoelige gegevens hebt die u niet wilt uploaden, gebruikt u een [. ignore-bestand](how-to-save-write-experiment-files.md#storage-limits-of-experiment-snapshots) of neemt u het niet op in de bron directory. In plaats daarvan opent u uw gegevens met behulp van een gegevens [opslag](https://docs.microsoft.com/python/api/azureml-core/azureml.data?view=azure-ml-py&preserve-view=true).


```python
script_params = {
    '--data-folder': dataset.as_named_input('mnist').as_mount(),
    '--batch-size': 50,
    '--first-layer-neurons': 300,
    '--second-layer-neurons': 100,
    '--learning-rate': 0.01
}

est = TensorFlow(source_directory=script_folder,
                 entry_script='tf_mnist.py',
                 script_params=script_params,
                 compute_target=compute_target,
                 use_gpu=True,
                 pip_packages=['azureml-dataprep[pandas,fuse]'])
```

> [!TIP]
> Ondersteuning voor **tensor flow 2,0** is toegevoegd aan de tensor flow Estimator-klasse. Zie het [blog bericht](https://azure.microsoft.com/blog/tensorflow-2-0-on-azure-fine-tuning-bert-for-question-tagging/) voor meer informatie.

Zie [omgevingen maken en beheren voor training en implementatie](how-to-use-environments.md)voor meer informatie over het aanpassen van uw python-omgeving. 

## <a name="submit-a-run"></a>Een run verzenden

Het [object run](https://docs.microsoft.com/python/api/azureml-core/azureml.core.run%28class%29?view=azure-ml-py&preserve-view=true) biedt de interface voor de uitvoerings geschiedenis terwijl de taak wordt uitgevoerd en nadat deze is voltooid.

```Python
run = exp.submit(est)
run.wait_for_completion(show_output=True)
```

Wanneer de uitvoering wordt uitgevoerd, worden de volgende fasen door lopen:

- **Voorbereiden**: een docker-installatie kopie wordt gemaakt op basis van de tensor flow-Estimator. De afbeelding wordt geüpload naar het container register van de werk ruimte en opgeslagen in de cache voor latere uitvoeringen. Logboeken worden ook gestreamd naar de uitvoerings geschiedenis en kunnen worden weer gegeven om de voortgang te bewaken.

- **Schalen**: het cluster probeert omhoog te schalen als het batch AI-cluster meer knoop punten nodig heeft om de uitvoering uit te voeren dan momenteel beschikbaar zijn.

- **Uitvoeren**: alle scripts in de map script worden geüpload naar het Compute-doel, gegevens archieven worden gekoppeld of gekopieerd en de entry_script worden uitgevoerd. Uitvoer van stdout en de map./logs worden gestreamd naar de uitvoerings geschiedenis en kunnen worden gebruikt om de uitvoering te bewaken.

- **Na de verwerking**: de map./outputs van de uitvoering wordt gekopieerd naar de uitvoerings geschiedenis.

## <a name="register-or-download-a-model"></a>Een model registreren of downloaden

Zodra u het model hebt getraind, kunt u het registreren in uw werk ruimte. Met model registratie kunt u uw modellen in uw werk ruimte opslaan en versieren om het [model beheer en de implementatie](concept-model-management-and-deployment.md)te vereenvoudigen. Door de para meters op te geven, en wordt de `model_framework` `model_framework_version` implementatie van `resource_configuration` geen code model beschikbaar. Zo kunt u uw model rechtstreeks implementeren als een webservice van het geregistreerde model en het `ResourceConfiguration` object definieert de reken resource voor de webservice.

```Python
from azureml.core import Model
from azureml.core.resource_configuration import ResourceConfiguration

model = run.register_model(model_name='tf-dnn-mnist', 
                           model_path='outputs/model',
                           model_framework=Model.Framework.TENSORFLOW,
                           model_framework_version='1.13.0',
                           resource_configuration=ResourceConfiguration(cpu=1, memory_in_gb=0.5))
```

U kunt ook een lokale kopie van het model downloaden met behulp van het object run. In het trainings script `mnist-tf.py` wordt het model door een tensor flow-beveiligings object naar een lokale map (lokaal naar het Compute-doel) bewaard. U kunt het object run gebruiken om een kopie te downloaden.

```Python
# Create a model folder in the current directory
os.makedirs('./model', exist_ok=True)

for f in run.get_file_names():
    if f.startswith('outputs/model'):
        output_file_path = os.path.join('./model', f.split('/')[-1])
        print('Downloading from {} to {} ...'.format(f, output_file_path))
        run.download_file(name=f, output_file_path=output_file_path)
```

## <a name="distributed-training"></a>Gedistribueerde training

De [`TensorFlow`](https://docs.microsoft.com/python/api/azureml-train-core/azureml.train.dnn.tensorflow?view=azure-ml-py&preserve-view=true) Estimator biedt ook ondersteuning voor gedistribueerde training over CPU-en GPU-clusters. U kunt eenvoudig gedistribueerde tensor flow-taken uitvoeren en de indeling wordt door Azure Machine Learning beheerd.

Azure Machine Learning ondersteunt twee methoden van gedistribueerde training in tensor flow:

- [Mpi](https://www.open-mpi.org/) gedistribueerde training met behulp van het [Horovod](https://github.com/uber/horovod) -Framework
- Systeem eigen [gedistribueerde tensor flow](https://www.tensorflow.org/deploy/distributed) met de para meter server methode

### <a name="horovod"></a>Horovod

[Horovod](https://github.com/uber/horovod) is een open-source framework voor gedistribueerde training ontwikkeld door uber. Het biedt een eenvoudig pad naar gedistribueerde GPU tensor flow-taken.

Als u Horovod wilt gebruiken, geeft u een [`MpiConfiguration`](https://docs.microsoft.com/python/api/azureml-core/azureml.core.runconfig.mpiconfiguration?view=azure-ml-py&preserve-view=true) object op voor de `distributed_training` para meter in de tensor flow-constructor. Deze para meter zorgt ervoor dat de Horovod-bibliotheek wordt geïnstalleerd zodat u deze kunt gebruiken in uw trainings script.

```Python
from azureml.core.runconfig import MpiConfiguration
from azureml.train.dnn import TensorFlow

# Tensorflow constructor
estimator= TensorFlow(source_directory=project_folder,
                      compute_target=compute_target,
                      script_params=script_params,
                      entry_script='script.py',
                      node_count=2,
                      process_count_per_node=1,
                      distributed_training=MpiConfiguration(),
                      framework_version='1.13',
                      use_gpu=True,
                      pip_packages=['azureml-dataprep[pandas,fuse]'])
```

### <a name="parameter-server"></a>Parameter Server

U kunt ook [systeem eigen gedistribueerde tensor flow](https://www.tensorflow.org/deploy/distributed)uitvoeren. Dit maakt gebruik van het parameter server model. In deze methode traint u in een cluster met parameter servers en werk rollen. De werk nemers berekenen de verlopen tijdens de training, terwijl de parameter servers de kleur overgangen samen voegen.

Als u de methode van de parameter server wilt gebruiken, geeft u een [`TensorflowConfiguration`](https://docs.microsoft.com/python/api/azureml-core/azureml.core.runconfig.tensorflowconfiguration?view=azure-ml-py&preserve-view=true) object op voor de `distributed_training` para meter in de tensor flow-constructor.

```Python
from azureml.train.dnn import TensorFlow

distributed_training = TensorflowConfiguration()
distributed_training.worker_count = 2

# Tensorflow constructor
tf_est= TensorFlow(source_directory=project_folder,
                      compute_target=compute_target,
                      script_params=script_params,
                      entry_script='script.py',
                      node_count=2,
                      process_count_per_node=1,
                      distributed_training=distributed_training,
                      use_gpu=True,
                      pip_packages=['azureml-dataprep[pandas,fuse]'])

# submit the TensorFlow job
run = exp.submit(tf_est)
```

#### <a name="define-cluster-specifications-in-tf_config"></a>Cluster specificaties definiëren in de TF_CONFIG

U hebt ook de netwerk adressen en poorten van het cluster nodig voor de [`tf.train.ClusterSpec`](https://www.tensorflow.org/api_docs/python/tf/train/ClusterSpec) , zodat Azure machine learning de `TF_CONFIG` omgevings variabele voor u instelt.

De `TF_CONFIG` omgevings variabele is een JSON-teken reeks. Hier volgt een voor beeld van de variabele voor een parameter Server:

```JSON
TF_CONFIG='{
    "cluster": {
        "ps": ["host0:2222", "host1:2222"],
        "worker": ["host2:2222", "host3:2222", "host4:2222"],
    },
    "task": {"type": "ps", "index": 0},
    "environment": "cloud"
}'
```

Voor de API op hoog niveau van tensor flow [`tf.estimator`](https://www.tensorflow.org/api_docs/python/tf/estimator) parseert tensor flow de `TF_CONFIG` variabele en bouwt de cluster specificatie voor u.

Voor de kern-Api's van tensor flow voor training moet u de variabele parseren `TF_CONFIG` en de `tf.train.ClusterSpec` in uw trainings code bouwen.

```Python
import os, json
import tensorflow as tf

tf_config = os.environ.get('TF_CONFIG')
if not tf_config or tf_config == "":
    raise ValueError("TF_CONFIG not found.")
tf_config_json = json.loads(tf_config)
cluster_spec = tf.train.ClusterSpec(cluster)

```

## <a name="deploy-a-tensorflow-model"></a>Een tensor flow-model implementeren

Het model dat u zojuist hebt geregistreerd, kan op dezelfde manier worden geïmplementeerd als andere geregistreerde modellen in Azure Machine Learning, ongeacht welke Estimator u hebt gebruikt voor de training. De implementatie-instructie bevat een sectie over het registreren van modellen, maar u kunt direct door gaan naar het [maken van een reken doel](how-to-deploy-and-where.md#choose-a-compute-target) voor implementatie, omdat u al een geregistreerd model hebt.

## <a name="preview-no-code-model-deployment"></a>Evaluatie Implementatie van geen code model

In plaats van de traditionele implementatie route kunt u ook de functie voor het implementeren van geen code (preview) gebruiken voor tensor flow. Als u het model registreert zoals hierboven wordt weer gegeven, `model_framework` `model_framework_version` `resource_configuration` kunt u gewoon de `deploy()` statische functie gebruiken om uw model te implementeren.

```python
service = Model.deploy(ws, "tensorflow-web-service", [model])
```

De volledige [instructies voor](how-to-deploy-and-where.md) het implementeren van een implementatie in azure machine learning meer dieper.

## <a name="next-steps"></a>Volgende stappen

In dit artikel hebt u een tensor flow-model getraind en geregistreerd en hebt u geleerd over opties voor implementatie. Raadpleeg de volgende artikelen voor meer informatie over Azure Machine Learning.

* [Metrische uitvoerings gegevens tijdens de training volgen](how-to-track-experiments.md)
* [Hyperparameters afstemmen](how-to-tune-hyperparameters.md)
* [Referentie architectuur voor gedistribueerde training van diep gaande lessen in azure](/azure/architecture/reference-architectures/ai/training-deep-learning)
