---
title: Overzicht van SQL Server AlwaysOn-beschikbaarheids groepen
description: In dit artikel worden SQL Server AlwaysOn-beschikbaarheids groepen in azure Virtual Machines geïntroduceerd.
services: virtual-machines
documentationCenter: na
author: MashaMSFT
editor: monicar
tags: azure-service-management
ms.assetid: 601eebb1-fc2c-4f5b-9c05-0e6ffd0e5334
ms.service: virtual-machines-sql
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/13/2017
ms.author: mathoma
ms.custom: seo-lt-2019, devx-track-azurecli
ms.openlocfilehash: 705c7dd602d9c908ec9048d131ba66b21c5b2103
ms.sourcegitcommit: 419cf179f9597936378ed5098ef77437dbf16295
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/27/2020
ms.locfileid: "89006503"
---
# <a name="introducing-sql-server-always-on-availability-groups-on-azure-virtual-machines"></a>Introductie van SQL Server AlwaysOn-beschikbaarheids groepen in azure Virtual Machines

[!INCLUDE[appliesto-sqlvm](../../includes/appliesto-sqlvm.md)]

In dit artikel worden SQL Server-beschikbaarheids groepen in azure Virtual Machines geïntroduceerd. 

AlwaysOn-beschikbaarheids groepen op Azure Virtual Machines zijn vergelijkbaar met AlwaysOn-beschikbaarheids groepen on-premises. Zie AlwaysOn [Availability groups (SQL Server)](https://msdn.microsoft.com/library/hh510230.aspx)voor meer informatie. 

In het volgende diagram ziet u de onderdelen van een volledige SQL Server-beschikbaarheids groep in azure Virtual Machines.

![Beschikbaarheidsgroep](./media/availability-group-overview/00-EndstateSampleNoELB.png)

Het belangrijkste verschil voor een beschikbaarheids groep op Azure Virtual Machines is dat voor deze virtuele machines (Vm's) een [Load Balancer](../../../load-balancer/load-balancer-overview.md)is vereist. Het load balancer bevat de IP-adressen voor de beschikbaarheids groep-listener. Als u meer dan één beschikbaarheids groep hebt, is voor elke groep een listener vereist. Een load balancer kan meerdere listeners ondersteunen.

Daarnaast wordt in een Azure IaaS VM-gast-failovercluster aanbevolen één NIC per server (cluster knooppunt) en één subnet. Azure Networking heeft fysieke redundantie, waardoor extra Nic's en subnetten overbodig zijn op een Azure IaaS VM-gast cluster. Hoewel het clustervalidatierapport een waarschuwing zal bevatten dat de knooppunten alleen bereikbaar zijn in één netwerk, kan deze waarschuwing zonder problemen worden genegeerd in het geval van failover-gastclusters voor een Azure IaaS-VM. 

Om redundantie en maximale Beschik baarheid te verbeteren, moeten de SQL Server Vm's zich in dezelfde [beschikbaarheidsset](availability-group-manually-configure-prerequisites-tutorial.md#create-availability-sets)bevinden of in verschillende [beschikbaarheids zones](/azure/availability-zones/az-overview). 

|  | Windows Server-versie | SQL Server versie | SQL Server-editie | Configuratie van WSFC-quorum | DR met meerdere regio's | Ondersteuning voor meerdere subnetten | Ondersteuning voor een bestaande AD | DR met meerdere zones met dezelfde regio | Ondersteuning voor dist-AG zonder AD-domein | Ondersteuning voor VERD-AG zonder cluster |  
| :------ | :-----| :-----| :-----| :-----| :-----| :-----| :-----| :-----| :-----| :-----|
| **[Azure Portal](availability-group-azure-portal-configure.md)** | 2019 </br> 2016 | 2019 </br>2017 </br>2016   | ENT | Cloudwitness | Nee | Ja | Ja | Ja | Nee | Nee |
| **[Azure CLI/Power shell](availability-group-az-cli-configure.md)** | 2019 </br> 2016 | 2019 </br>2017 </br>2016   | ENT | Cloudwitness | Nee | Ja | Ja | Ja | Nee | Nee |
| **[Quick Start-sjablonen](availability-group-quickstart-template-configure.md)** | 2019 </br> 2016 | 2019 </br>2017 </br>2016  | ENT | Cloudwitness | Nee | Ja | Ja | Ja | Nee | Nee |
| **[Handmatig](availability-group-manually-configure-prerequisites-tutorial.md)** | Alles | Alles | Alles | Alles | Ja | Ja | Ja | Ja | Ja | Ja |

De sjabloon **voor het SQL Server AlwaysOn-cluster (preview)** is verwijderd uit de Azure Marketplace en is niet meer beschikbaar. 

Raadpleeg deze zelf studies wanneer u klaar bent om een SQL Server-beschikbaarheids groep te maken in azure Virtual Machines.

## <a name="manually-with-azure-cli"></a>Hand matig met Azure CLI

Het is raadzaam om Azure CLI te gebruiken voor het configureren en implementeren van een beschikbaarheids groep, omdat het de eenvoudigste en snelste is om te implementeren. Met Azure CLI is het maken van het Windows-failovercluster, het samen voegen van SQL Server Vm's aan het cluster en het maken van de listener en interne Load Balancer allemaal binnen 30 minuten. Voor deze optie moet de beschikbaarheids groep nog steeds hand matig worden gemaakt, maar alle andere nood zakelijke configuratie stappen worden geautomatiseerd. 

Zie voor meer informatie Azure SQL VM CLI gebruiken voor het configureren van AlwaysOn- [beschikbaarheids groep voor SQL Server op een virtuele machine van Azure](availability-group-az-cli-configure.md). 

## <a name="automatically-with-azure-quickstart-templates"></a>Automatisch met Azure Quick Start-sjablonen

In de Azure Quick Start-sjablonen wordt gebruikgemaakt van de resource provider van de SQL-VM om het Windows-failovercluster te implementeren, SQL Server Vm's aan toe te voegen, de listener te maken en de interne Load Balancer te configureren. Voor deze optie is nog steeds een hand matig maken van de beschikbaarheids groep en de interne Load Balancer (ILB) vereist. Het automatiseert en vereenvoudigt echter alle andere nood zakelijke configuratie stappen, waaronder de configuratie van de ILB. 

Zie voor meer informatie Azure Quick Start-sjabloon gebruiken voor het configureren van AlwaysOn- [beschikbaarheids groep voor SQL Server op een virtuele machine van Azure](availability-group-quickstart-template-configure.md).


## <a name="automatically-with-an-azure-portal-template"></a>Automatisch met een Azure Portal sjabloon

[AlwaysOn AlwaysOn-beschikbaarheids groep configureren in azure VM automatisch-Resource Manager](availability-group-azure-marketplace-template-configure.md)


## <a name="manually-in-the-azure-portal"></a>Hand matig in de Azure Portal

U kunt de virtuele machines ook zelf maken zonder de sjabloon. Vul eerst de vereisten in en maak vervolgens de beschikbaarheids groep. Zie de volgende onderwerpen: 

- [Vereisten configureren voor SQL Server AlwaysOn-beschikbaarheids groepen in azure Virtual Machines](availability-group-manually-configure-prerequisites-tutorial.md)

- [AlwaysOn-beschikbaarheids groep maken om de beschik baarheid en herstel na nood gevallen te verbeteren](availability-group-manually-configure-tutorial.md)

## <a name="next-steps"></a>Volgende stappen

[Een SQL Server always on-beschikbaarheids groep configureren op Azure Virtual Machines in verschillende regio's](availability-group-manually-configure-multiple-regions.md)
