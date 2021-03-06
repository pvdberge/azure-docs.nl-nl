---
title: Azure Resource Manager-sjablonen
description: Azure Resource Manager-sjablonen voor gebruik bij Recovery Services-kluizen en Azure Backup-functies
ms.topic: sample
ms.date: 01/31/2019
ms.custom: mvc
ms.openlocfilehash: 29a2499bfd3125cad98e72f7543bb9a29293f624
ms.sourcegitcommit: afa1411c3fb2084cccc4262860aab4f0b5c994ef
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/23/2020
ms.locfileid: "88755191"
---
# <a name="azure-resource-manager-templates-for-azure-backup"></a>Azure Resource Manager-sjablonen voor Azure Backup

De volgende tabel bevat koppelingen naar Azure Resource Manager-sjablonen voor gebruik bij Recovery Services-kluizen en Azure Backup-functies. Zie [Microsoft.RecoveryServices resource types](/azure/templates/microsoft.recoveryservices/allversions) (Microsoft.RecoveryServices resourcetypen) voor informatie over de JSON-syntaxis en eigenschappen.

| Template | Beschrijving |
|---|---|
|**Recovery Services-kluis** | |
| [Een Recovery Services-kluis maken](https://github.com/Azure/azure-quickstart-templates/tree/master/101-recovery-services-vault-create)| Maak een Recovery Services-kluis. De kluis kan worden gebruikt voor Azure Backup en Azure Site Recovery. |
|**Back-up maken van virtuele machines**| |
| [Back-ups maken van Resource Manager-VM's](https://github.com/Azure/azure-quickstart-templates/tree/master/101-recovery-services-backup-vms) | Gebruik de bestaande Recovery Services-kluis en het back-upbeleid om back-ups te maken van Resource Manager-virtuele machines in dezelfde resourcegroep.|
| [Back-ups maken van IaaS-VM's naar een Recovery Services-kluis](https://github.com/Azure/azure-quickstart-templates/tree/master/201-recovery-services-backup-classic-resource-manager-vms) | Sjabloon voor het maken van back-ups van klassieke en Resource Manager-virtuele machines. |
| [Beleid voor wekelijkse back-up voor IaaS VM's maken](https://github.com/Azure/azure-quickstart-templates/tree/master/101-recovery-services-weekly-backup-policy-create) | Met de sjabloon wordt een Recovery Services-kluis en een beleid voor wekelijkse back-ups gemaakt dat wordt gebruikt voor het maken van back-ups van klassieke VM's en Resource Manager-virtuele machines.|
| [Beleid voor dagelijkse back-up voor IaaS VM's maken](https://github.com/Azure/azure-quickstart-templates/tree/master/101-recovery-services-daily-backup-policy-create) | Met de sjabloon wordt een Recovery Services-kluis en een beleid voor dagelijkse back-ups gemaakt dat wordt gebruikt voor het maken van back-ups van klassieke VM's en Resource Manager-virtuele machines.|
| [Windows Server-VM met back-up implementeren](https://github.com/Azure/azure-quickstart-templates/tree/master/101-recovery-services-create-vm-and-configure-backup) | Met de sjabloon wordt een Windows Server-VM en Recovery Services-kluis gemaakt met het standaard back-upbeleid ingeschakeld.|
|**Back-uptaken controleren** |  |
| [Logboeken van Azure Monitor gebruiken met Azure Backup](https://github.com/Azure/azure-quickstart-templates/tree/master/101-backup-oms-monitoring) | Met de sjabloon worden Azure Monitor-logboeken voor Azure Backup geïmplementeerd, waarmee u back-up- en hersteltaken, back-upwaarschuwingen en de cloudopslag in uw Recovery Services-kluizen kunt controleren.|  
|**Een back-up maken van SQL Server op Azure-VM** |  |
| [Een back-up maken van SQL Server op Azure-VM](https://github.com/Azure/azure-quickstart-templates/tree/master/101-recovery-services-vm-workload-backup) | Met de sjabloon wordt een Recovery Services-kluis en een back-upbeleid voor specifieke workloads gemaakt. De virtuele machine wordt geregistreerd bij de Azure Backup-service en de beveiliging wordt op die VM geconfigureerd. Op dit moment werkt dit alleen voor SQL-Galerie-installatiekopieën. |
|   |   |
