---
title: Azure PowerShell-voorbeeldscript - Het RDP-poortbereik wijzigen | Microsoft Docs
description: Azure PowerShell-voorbeeldscript - Wijzigt het RDP-poortbereik van een geïmplementeerd cluster.
services: service-fabric
tags: azure-service-management
author: athinanthny
ms.author: atsenthi
ms.service: service-fabric
ms.workload: multiple
ms.topic: sample
ms.date: 03/19/2018
ms.custom: sfrev
ms.openlocfilehash: 5cc72423d7e901f82cdf7e40f5de72bd54e9cec1
ms.sourcegitcommit: 3d79f737ff34708b48dd2ae45100e2516af9ed78
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/23/2020
ms.locfileid: "87076165"
---
# <a name="update-the-rdp-port-range-values"></a>De waarden voor het RDP-poortbereik bijwerken

Met dit voorbeeldscript worden de waarden voor het RDP-poortbereik op de clusterknooppunt-VM's gewijzigd nadat het cluster is geïmplementeerd.  Azure PowerShell wordt gebruikt, zodat de onderliggende VM's niet uit en aan hoeven te worden gezet.  Het script haalt de `Microsoft.Network/loadBalancers`-resource in de resourcegroep van het cluster op en werkt de waarden `inboundNatPools.frontendPortRangeStart` en `inboundNatPools.frontendPortRangeEnd` bij. Pas de parameters zo nodig aan.

[!INCLUDE [updated-for-az](../../../includes/updated-for-az.md)]

Installeer zo nodig Azure PowerShell met behulp van de instructies in de [Azure PowerShell-handleiding](/powershell/azure/).

## <a name="sample-script"></a>Voorbeeldscript

[!code-powershell[main](../../../powershell_scripts/service-fabric/change-rdp-port-range/change-rdp-port-range.ps1 "Update the RDP port range values")]

## <a name="script-explanation"></a>Uitleg van het script

In dit script worden de volgende opdrachten gebruikt. Elke opdracht in de tabel is een koppeling naar specifieke documentatie over de opdracht.

| Opdracht | Opmerkingen |
|---|---|
| [Get-AzResource](/powershell/module/az.resources/get-azresource) | Haalt de `Microsoft.Network/loadBalancers`-resource op. |
|[Set-AzResource](/powershell/module/az.resources/set-azresource)|Werkt de `Microsoft.Network/loadBalancers`-resource bij.|

## <a name="next-steps"></a>Volgende stappen

Zie voor meer informatie over de Azure PowerShell-module de [documentatie van Azure PowerShell](/powershell/azure/).

Meer voorbeelden voor Azure Powershell voor Azure Service Fabric vindt u in de [voorbeelden van Azure PowerShell](../service-fabric-powershell-samples.md).
