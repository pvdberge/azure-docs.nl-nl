---
title: HB-serie
description: Specificaties voor de virtuele machines uit de HB-serie.
author: ju-shim
ms.service: virtual-machines
ms.subservice: sizes
ms.topic: conceptual
ms.date: 09/08/2020
ms.author: amverma
ms.reviewer: jushiman
ms.openlocfilehash: 14d5e5af6f485346b0e1f070e84843a9bf085126
ms.sourcegitcommit: 1b320bc7863707a07e98644fbaed9faa0108da97
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/09/2020
ms.locfileid: "89595339"
---
# <a name="hb-series"></a>HB-serie

Vm's uit de HB-serie zijn geoptimaliseerd voor toepassingen die worden aangedreven door geheugen bandbreedte, zoals een Hydraulic-Dynamics, een expliciete, beperkte element analyse en weer modellen. HB Vm's feature 60 AMD EPYC 7551-processor kernen, 4 GB RAM per CPU-kern en zonder gelijktijdige multi threading. Een HB-VM biedt tot 260 GB/sec. geheugen bandbreedte.

HB-serie-Vm's functie 100 GB/sec Mellanox EDR InfiniBand. Deze Vm's zijn verbonden met een niet-blokkerende Fat-structuur voor geoptimaliseerde en consistente RDMA-prestaties. Deze Vm's ondersteunen adaptieve route ring en het dynamische Connected Trans Port (DCT, in aanvulling op Standard RC en UD Transports). Deze functies verbeteren de prestaties, schaal baarheid en consistentie van toepassingen, en het gebruik ervan wordt ten zeerste aanbevolen.

ACU: 199-216

Premium Storage: ondersteund

Premium Storage caching: ondersteund

Livemigratie: niet ondersteund

Updates voor het behouden van geheugen: niet ondersteund

| Grootte | vCPU | Processor | Geheugen (GB) | Geheugen bandbreedte GB/s | Basis-CPU-frequentie (GHz) | Frequentie van alle kernen (GHz, piek) | Frequentie met één kern geheugen (GHz, piek) | RDMA-prestaties (GB/s) | MPI-ondersteuning | Tijdelijke opslag (GB) | Max. aantal gegevensschijven | Maximum aantal Ethernet Nic's |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Standard_HB60rs | 60 | AMD EPYC 7551 | 240 | 263 | 2,0 | 2.55 | 2.55 | 100 | Alles | 700 | 4 | 1 |

[!INCLUDE [virtual-machines-common-sizes-table-defs](../../includes/virtual-machines-common-sizes-table-defs.md)]

## <a name="other-sizes"></a>Andere grootten

- [Algemeen gebruik](sizes-general.md)
- [Geoptimaliseerd geheugen](sizes-memory.md)
- [Geoptimaliseerde opslag](sizes-storage.md)
- [Geoptimaliseerde GPU](sizes-gpu.md)
- [Krachtig rekenvermogen](sizes-hpc.md)
- [Vorige generaties](sizes-previous-gen.md)

## <a name="next-steps"></a>Volgende stappen
- Meer informatie over [het configureren van uw vm's, het](./workloads/hpc/configure.md) [inschakelen van Infiniband](./workloads/hpc/enable-infiniband.md), het [instellen van MPI](./workloads/hpc/setup-mpi.md)en het optimaliseren van HPC-toepassingen voor Azure bij [HPC-workloads](./workloads/hpc/overview.md).
- Lees over de laatste aankondigingen en enkele HPC-voorbeelden en -resultaten in de [Azure Compute Tech Community-blogs](https://techcommunity.microsoft.com/t5/azure-compute/bg-p/AzureCompute).
- Zie [High Performance Computing (HPC) op Azure](/azure/architecture/topics/high-performance-computing/) voor een gedetailleerdere architectuurweergave van HPC-workloads die worden uitgevoerd.
- Meer informatie over hoe [Azure Compute units (ACU)](acu.md) u kan helpen bij het vergelijken van de reken prestaties in azure-sku's.
