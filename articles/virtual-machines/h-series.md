---
title: H-serie-Azure Virtual Machines
description: Specificaties voor de virtuele machines uit de H-serie.
author: ju-shim
ms.service: virtual-machines
ms.subservice: sizes
ms.topic: conceptual
ms.date: 09/08/2020
ms.author: amverma
ms.reviewer: jushiman
ms.openlocfilehash: b1f30e91b9ce96daf8b2eb8ac6c8cb38b86b347f
ms.sourcegitcommit: 1b320bc7863707a07e98644fbaed9faa0108da97
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/09/2020
ms.locfileid: "89594404"
---
# <a name="h-series"></a>H-serie

Virtuele machines uit de H-serie zijn geoptimaliseerd voor toepassingen die worden aangedreven door hoge CPU-frequenties of grote geheugen per kern vereisten. Met de H-serie Vm's functie 8 of 16 Intel Xeon E5 2667 v3-processor kernen, tot 14 GB aan RAM per CPU-kern en zonder hyperthreading. Functies van de H-serie 56 GB/sec Mellanox FDR InfiniBand in een niet-blokkerende Fat-structuur configuratie voor consistente RDMA-prestaties. Virtuele machines uit de H-serie zijn momenteel niet SR-IOV ingeschakeld en ondersteunen Intel MPI 5. x en MS-MPI.

ACU: 290-300

Premium Storage: niet ondersteund

Premium Storage caching: niet ondersteund

Livemigratie: niet ondersteund

Updates voor het behouden van geheugen: niet ondersteund

| Grootte | vCPU | Processor | Geheugen (GB) | Geheugen bandbreedte GB/s | Basis-CPU-frequentie (GHz) | Frequentie van alle kernen (GHz, piek) | Frequentie met één kern geheugen (GHz, piek) | RDMA-prestaties (GB/s) | MPI-ondersteuning | Tijdelijke opslag (GB) | Max. aantal gegevensschijven | Max. doorvoer schijf: IOPS | Maximum aantal Ethernet Nic's |
| --- | --- |--- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Standard_H8   | 8  | Intel Xeon E5 2667 v3 | 56 | 40 | 3.2 | 3,3 | 3,6 | - | Intel 5. x, MS-MPI | 1000 | 32 | 32 x 500 | 2 |
| Standard_H16  | 16 | Intel Xeon E5 2667 v3 | 112 | 80 | 3.2 | 3,3 | 3,6 | - | Intel 5. x, MS-MPI | 2000 | 64 | 64 x 500 | 4 |
| Standard_H8m  | 8  | Intel Xeon E5 2667 v3 | 112 | 40 | 3.2 | 3,3 | 3,6 | - | Intel 5. x, MS-MPI | 1000 | 32 | 32 x 500 | 2 |
| Standard_H16m | 16 | Intel Xeon E5 2667 v3 | 224 | 80 | 3.2 | 3,3 | 3,6 | - | Intel 5. x, MS-MPI | 2000 | 64 | 64 x 500 | 4 |
| Standard_H16r <sup>1</sup>  | 16 | Intel Xeon E5 2667 v3 | 112 | 80 | 3.2 | 3,3 | 3,6 | 56 | Intel 5. x, MS-MPI | 2000 | 64 | 64 x 500 | 4 |
| Standard_H16mr <sup>1</sup> | 16 | Intel Xeon E5 2667 v3 | 224 | 80 | 3.2 | 3,3 | 3,6 | 56 | Intel 5. x, MS-MPI | 2000 | 64 | 64 x 500 | 4 |

<sup>1</sup> voor mpi-toepassingen is het gereserveerde RDMA-back-end-netwerk ingeschakeld door het FDR InfiniBand-netwerk.

[!INCLUDE [virtual-machines-common-sizes-table-defs](../../includes/virtual-machines-common-sizes-table-defs.md)]

> [!NOTE]
> De H-serie van de [RDMA-compatibele vm's](sizes-hpc.md#rdma-capable-instances)zijn niet-SR-IOV ingeschakeld. Daarom zijn de ondersteunde [VM-installatie kopieën](./workloads/hpc/configure.md#vm-images), [InfiniBand-stuur programma](./workloads/hpc/enable-infiniband.md) vereisten en ondersteunde [mpi-bibliotheken](./workloads/hpc/setup-mpi.md) verschillend van de op SR-IOV ingeschakelde vm's.

## <a name="other-sizes"></a>Andere grootten

- [Algemeen gebruik](sizes-general.md)
- [Geoptimaliseerd geheugen](sizes-memory.md)
- [Geoptimaliseerde opslag](sizes-storage.md)
- [Geoptimaliseerde GPU](sizes-gpu.md)
- [Krachtig rekenvermogen](sizes-hpc.md)
- [Vorige generaties](sizes-previous-gen.md)

## <a name="next-steps"></a>Volgende stappen

- Meer informatie over [het configureren van uw vm's, het](./workloads/hpc/configure.md) [inschakelen van Infiniband](./workloads/hpc/enable-infiniband.md), het [instellen van MPI](./workloads/hpc/setup-mpi.md) en het optimaliseren van HPC-toepassingen voor Azure bij [HPC-workloads](./workloads/hpc/overview.md).
- Lees over de laatste aankondigingen en enkele HPC-voorbeelden en -resultaten in de [Azure Compute Tech Community-blogs](https://techcommunity.microsoft.com/t5/azure-compute/bg-p/AzureCompute).
- Zie [High Performance Computing (HPC) op Azure](/azure/architecture/topics/high-performance-computing/) voor een gedetailleerdere architectuurweergave van HPC-workloads die worden uitgevoerd.
- Meer informatie over hoe [Azure Compute units (ACU)](acu.md) u kan helpen bij het vergelijken van de reken prestaties in azure-sku's.
