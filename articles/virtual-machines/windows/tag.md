---
title: Een virtuele machine labelen met behulp van Power shell
description: Meer informatie over het coderen van een virtuele machine met behulp van Power shell
author: mmccrory
ms.service: virtual-machines-windows
ms.topic: how-to
ms.workload: infrastructure-services
ms.date: 07/05/2016
ms.author: memccror
ms.openlocfilehash: 3aa40ed396e87b342207fc51576cd28170c7d4e9
ms.sourcegitcommit: 5ed504a9ddfbd69d4f2d256ec431e634eb38813e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/02/2020
ms.locfileid: "89322378"
---
# <a name="how-to-tag-a-virtual-machine-in-azure-using-powershell"></a>Een virtuele machine in azure labelen met behulp van Power shell
In dit artikel worden verschillende manieren beschreven om een virtuele Windows-machine in azure te coderen via het Resource Manager-implementatie model. Tags zijn door de gebruiker gedefinieerde sleutel/waarde-paren die rechtstreeks kunnen worden geplaatst op een resource of resource groep. Azure ondersteunt momenteel Maxi maal 50 Tags per resource en resource groep. Labels kunnen worden geplaatst op een resource op het moment dat ze worden gemaakt of worden toegevoegd aan een bestaande resource. Tags worden alleen ondersteund voor resources die zijn gemaakt via het Resource Manager-implementatie model. Als u een virtuele machine wilt labelen met behulp van de Azure CLI, raadpleegt u [een virtuele machine in azure labelen met behulp van de Azure cli](../linux/tag.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

[!INCLUDE [virtual-machines-common-tag](../../../includes/virtual-machines-common-tag.md)]

## <a name="tagging-with-powershell"></a>Labelen met Power shell
Als u tags wilt maken, toevoegen en verwijderen via Power shell, moet u eerst uw [Power shell-omgeving instellen met Azure Resource Manager][PowerShell environment with Azure Resource Manager]. Nadat u de installatie hebt voltooid, kunt u tags plaatsen op compute-, netwerk-en opslag resources tijdens het maken of nadat de resource is gemaakt via Power shell. Dit artikel richt zich op het weer geven/bewerken van tags die op Virtual Machines zijn geplaatst.

 

Ga eerst naar een virtuele machine via de `Get-AzVM` cmdlet.

```azurepowershell
PS C:\> Get-AzVM -ResourceGroupName "MyResourceGroup" -Name "MyTestVM"
```

Als uw virtuele machine al Tags bevat, ziet u alle tags in uw resource:

```json
Tags : {
        "Application": "MyApp1",
        "Created By": "MyName",
        "Department": "MyDepartment",
        "Environment": "Production"
        }
```

Als u tags wilt toevoegen via Power shell, kunt u de opdracht gebruiken `Set-AzResource` . Opmerking bij het bijwerken van Tags via Power shell worden Tags bijgewerkt als geheel. Als u bijvoorbeeld één tag toevoegt aan een resource die al Tags heeft, moet u alle labels opnemen die u op de resource wilt plaatsen. Hieronder ziet u een voor beeld van het toevoegen van extra tags aan een resource via Power shell-cmdlets.

Met deze eerste cmdlet worden alle tags die op *MyTestVM* zijn geplaatst, ingesteld op de variabele *$Tags* , met behulp van de- `Get-AzResource` en- `Tags` eigenschap.

```azurepowershell
PS C:\> $tags = (Get-AzResource -ResourceGroupName MyResourceGroup -Name MyTestVM).Tags
```

Met de tweede opdracht worden de labels voor de opgegeven variabele weer gegeven.

```azurepowershell
PS C:\> $tags

Key           Value
----          -----
Department    MyDepartment
Application   MyApp1
Created By    MyName
Environment   Production
```

De derde opdracht voegt een extra tag toe aan de variabele *$Tags* . Let op het gebruik van de **+=** om de nieuwe sleutel/waarde-paar toe te voegen aan de *$Tags* lijst.

```azurepowershell
PS C:\> $tags += @{Location="MyLocation"}
```

Met de vierde opdracht worden alle labels die in de *$Tags* variabele zijn gedefinieerd, ingesteld op de opgegeven resource. In dit geval is het MyTestVM.

```azurepowershell
PS C:\> Set-AzResource -ResourceGroupName MyResourceGroup -Name MyTestVM -ResourceType "Microsoft.Compute/VirtualMachines" -Tag $tags
```

Met de vijfde opdracht worden alle labels op de resource weer gegeven. Zoals u ziet, is *locatie* nu als een tag met *MyLocation* als de waarde gedefinieerd.

```azurepowershell
PS C:\> (Get-AzResource -ResourceGroupName MyResourceGroup -Name MyTestVM).Tags

Key           Value
----          -----
Department    MyDepartment
Application   MyApp1
Created By    MyName
Environment   Production
Location      MyLocation
```

Raadpleeg de [Azure resource-cmdlets][Azure Resource Cmdlets]voor meer informatie over het coderen via Power shell.

[!INCLUDE [virtual-machines-common-tag-usage](../../../includes/virtual-machines-common-tag-usage.md)]

## <a name="next-steps"></a>Volgende stappen
* Zie [Azure Resource Manager Overview][Azure Resource Manager Overview] en [Tags gebruiken om uw Azure-resources te organiseren][Using Tags to organize your Azure Resources]voor meer informatie over het coderen van uw Azure-resources.
* Als u wilt zien hoe Tags u kunnen helpen bij het beheren van uw gebruik van Azure-resources, raadpleegt u [inzicht in uw Azure-factuur][Understanding your Azure Bill] en [krijgt u inzicht in uw Microsoft Azure Resource verbruik][Gain insights into your Microsoft Azure resource consumption].

[PowerShell environment with Azure Resource Manager]: ../../azure-resource-manager/management/manage-resources-powershell.md
[Azure Resource Cmdlets]: /powershell/module/az.resources/
[Azure Resource Manager Overview]: ../../azure-resource-manager/management/overview.md
[Using Tags to organize your Azure Resources]: ../../azure-resource-manager/management/tag-resources.md
[Understanding your Azure Bill]:../../cost-management-billing/understand/review-individual-bill.md
[Gain insights into your Microsoft Azure resource consumption]:../../cost-management-billing/manage/usage-rate-card-overview.md
