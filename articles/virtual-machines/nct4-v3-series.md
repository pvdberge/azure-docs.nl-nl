---
title: NCas T4 v3-serie
description: Specificaties voor de virtuele machines uit de NCas T4 v3-serie.
services: virtual-machines
ms.subservice: sizes
author: vikancha-MSFT
ms.service: virtual-machines
ms.topic: conceptual
ms.date: 08/10/2020
ms.author: vikancha
ms.openlocfilehash: af9f7eb21d533bc5fb365e7cbf1fb8fc18184fa7
ms.sourcegitcommit: 3246e278d094f0ae435c2393ebf278914ec7b97b
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/02/2020
ms.locfileid: "89375224"
---
# <a name="ncast4_v3-series-in-preview"></a>NCasT4_v3-serie (in preview-versie) 

De virtuele machines uit de NCasT4_v3-serie worden aangedreven door [Nvidia Tesla T4](https://www.nvidia.com/en-us/data-center/tesla-t4/) GPU'S en AMD EPYC 7V12 (Rome) cpu's. De virtuele machines beschikken over Maxi maal 4 NVIDIA T4-Gpu's met 16 GB geheugen per, Maxi maal 64 niet-multi threaded AMD EPYC 7V12 (Rome)-processor kernen en 440 GiB van het systeem geheugen. Deze virtuele machines zijn ideaal voor het uitvoeren van ML-en AI-workloads die gebruikmaken van CUDA, tensor flow, Pytorch, Caffe en andere frameworks of de grafische werk belasting met behulp van de NVIDIA GRID-technologie. NCasT4_v3-serie is ideaal voor het uitvoeren van inactieve werk belastingen.

U kunt [een aanvraag indienen](https://aka.ms/NCT4v3Preview) om deel te uitmaken van het preview-programma.

<br>

ACU: 230-260

Premium Storage: ondersteund

Premium Storage caching: ondersteund

Livemigratie: niet ondersteund

Updates voor het behouden van geheugen: niet ondersteund

| Grootte | vCPU | Geheugen: GiB | Tijdelijke opslag (SSD) GiB | GPU | GPU-geheugen: GiB | Max. aantal gegevensschijven | Max. aantal NIC's |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Standard_NC4as_T4_v3 |4 |28 |180 | 1 | 16 | 8 | 2 |
| Standard_NC8as_T4_v3 |8 |56 |360 | 1 | 16 | 16 | 4  |
| Standard_NC16as_T4_v3 |16 |110 |360 | 1 | 16 | 32 | 8  |
| Standard_NC64as_T4_v3 |64 |440 |2880 | 4 | 64 | 32 | 8  |


[!INCLUDE [virtual-machines-common-sizes-table-defs](../../includes/virtual-machines-common-sizes-table-defs.md)]

## <a name="supported-operating-systems-and-drivers"></a>Ondersteunde besturingssystemen en stuurprogramma’s

Als u gebruik wilt maken van de GPU-mogelijkheden van Azure NCasT4_v3-serie Vm's waarop Windows of Linux wordt uitgevoerd, moeten de NVIDIA GPU-Stuur Programma's zijn geïnstalleerd.

Als u de NVIDIA GPU-Stuur Programma's hand matig wilt installeren, raadpleegt u [N-Series GPU-stuur programma-installatie voor Windows](./windows/n-series-driver-setup.md) voor ondersteunde besturings systemen, stuur Programma's, installatie en verificaties tappen.

## <a name="other-sizes"></a>Andere grootten

- [Algemeen gebruik](sizes-general.md)
- [Geoptimaliseerd geheugen](sizes-memory.md)
- [Geoptimaliseerde opslag](sizes-storage.md)
- [Geoptimaliseerde GPU](sizes-gpu.md)
- [Krachtig rekenvermogen](sizes-hpc.md)
- [Vorige generaties](sizes-previous-gen.md)

## <a name="next-steps"></a>Volgende stappen

Meer informatie over hoe [Azure Compute units (ACU)](acu.md) u kan helpen bij het vergelijken van de reken prestaties in azure-sku's.
