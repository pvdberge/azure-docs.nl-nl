---
author: DCtheGeek
ms.service: azure-policy
ms.topic: include
ms.date: 09/04/2020
ms.author: dacoulte
ms.custom: generated
ms.openlocfilehash: 4c895a796a23fb62bb5f65e7a82a96916be9c438
ms.sourcegitcommit: de2750163a601aae0c28506ba32be067e0068c0c
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/04/2020
ms.locfileid: "89487562"
---
|Naam<br /><sub>(Azure-portal)</sub> |Beschrijving |Gevolg(en) |Versie<br /><sub>(GitHub)</sub> |
|---|---|---|---|
|[Azure Backup moet zijn ingeschakeld voor virtuele machines](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F013e242c-8828-4970-87b3-ab247555486d) |Dit beleid helpt te controleren of Azure Backup-service is ingeschakeld voor alle virtuele machines. Azure Backup is een voordelige back-upoplossing voor eenvoudig gegevensherstel en is makkelijker in te schakelen dan andere services voor cloudback-ups. |AuditIfNotExists, uitgeschakeld |[1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Backup/VirtualMachines_EnableAzureBackup_Audit.json) |
|[Instellen dat VM's die op een locatie worden gemaakt naar een bestaande centrale kluis op dezelfde locatie een back-up krijgen](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F09ce66bc-1220-4153-8104-e3f51c936913) |Met dit beleid configureert u Azure Backup-beveiliging op VM's op een bepaalde locatie naar een bestaande centrale kluis op dezelfde locatie. Dit geldt alleen voor VM’s die nog niet zijn geconfigureerd voor back-up. Het is raadzaam dat dit beleid aan niet meer dan 200 VM's wordt toegewezen. Als het beleid is toegewezen aan meer dan 200 Vm's, kan dit ertoe leiden dat de back-up enkele uren na het gedefinieerde schema wordt geactiveerd. Dit beleid zal worden uitgebreid om meer VM-installatiekopieën te ondersteunen. |deployIfNotExists, auditIfNotExists, uitgeschakeld |[1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Backup/VirtualMachineBackup_Backup_DeployIfNotExists.json) |
