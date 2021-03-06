---
author: IEvangelist
ms.author: dapine
ms.date: 06/25/2019
ms.service: cognitive-services
ms.topic: include
ms.openlocfilehash: ce4cc68826b39b5707549afc799d2d214e8876c6
ms.sourcegitcommit: cd0a1ae644b95dbd3aac4be295eb4ef811be9aaa
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/19/2020
ms.locfileid: "88638930"
---
Als u een HTTP-proxy wilt configureren voor het maken van uitgaande aanvragen, gebruikt u deze twee argumenten:

| Name | Gegevenstype | Beschrijving |
|--|--|--|
|HTTPS_PROXY|tekenreeks|De proxy die moet worden gebruikt, bijvoorbeeld `https://proxy:8888`<br>`<proxy-url>`|
|HTTPS_PROXY_CREDS|tekenreeks|Alle referenties die nodig zijn voor verificatie bij de proxy, bijvoorbeeld gebruikers naam: wacht woord.|
|`<proxy-user>`|tekenreeks|De gebruiker voor de proxy.|
|`<proxy-password>`|tekenreeks|Het wacht woord dat is gekoppeld aan `<proxy-user>` de proxy.|
||||


```bash
docker run --rm -it -p 5000:5000 \
--memory 2g --cpus 1 \
--mount type=bind,src=/home/azureuser/output,target=/output \
<registry-location>/<image-name> \
Eula=accept \
Billing=<endpoint> \
ApiKey=<api-key> \
HTTPS_PROXY=<proxy-url> \
HTTPS_PROXY_CREDS=<proxy-user>:<proxy-password> \
```
