---
title: FQDN maken voor een virtuele machine in de Azure Portal
description: Meer informatie over het maken van een FQDN-naam (Fully Qualified Domain Name) voor een virtuele machine op basis van een resource manager in de Azure Portal.
author: cynthn
ms.service: virtual-machines
ms.subservice: networking
ms.topic: how-to
ms.workload: infrastructure-services
ms.date: 08/15/2018
ms.author: cynthn
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 9ac44c8d157102a39df9c580938589862dafd0a4
ms.sourcegitcommit: f353fe5acd9698aa31631f38dd32790d889b4dbb
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/29/2020
ms.locfileid: "87371886"
---
# <a name="create-a-fully-qualified-domain-name-in-the-azure-portal-for-a-linux-vm"></a>Een Fully Qualified Domain Name maken in de Azure Portal voor een Linux-VM

Wanneer u een virtuele machine (VM) maakt in de [Azure Portal](https://portal.azure.com), wordt er automatisch een open bare IP-resource voor de virtuele machine gemaakt. U gebruikt dit IP-adres om op afstand toegang te krijgen tot de virtuele machine. Hoewel de portal geen [Fully Qualified Domain name](https://en.wikipedia.org/wiki/Fully_qualified_domain_name)of FQDN maakt, kunt u één keer toevoegen wanneer de virtuele machine is gemaakt. In dit artikel worden de stappen beschreven voor het maken van een DNS-naam of FQDN.

## <a name="create-a-fqdn"></a>Een FQDN maken
In dit artikel wordt ervan uitgegaan dat u al een virtuele machine hebt gemaakt. Als dat nodig is, kunt u [een virtuele machine maken in de portal](quick-create-portal.md) of [met de Azure cli](quick-create-cli.md). Volg deze stappen als uw virtuele machine actief is:

[!INCLUDE [virtual-machines-common-portal-create-fqdn](../../../includes/virtual-machines-common-portal-create-fqdn.md)]

U kunt nu extern verbinding maken met de virtuele machine met behulp van deze DNS-naam, zoals bij `ssh azureuser@mydns.westus.cloudapp.azure.com` .

## <a name="next-steps"></a>Volgende stappen
Nu uw VM een open bare IP-en DNS-naam heeft, kunt u algemene toepassings raamwerken of-services implementeren, zoals nginx, MongoDB, docker, enzovoort.

U kunt ook meer lezen over het [gebruik van Resource Manager](../../azure-resource-manager/management/overview.md) voor tips over het bouwen van uw Azure-implementaties.

