---
title: Azure Security Bench Mark v2-back-up en herstel
description: Back-up en herstel van Azure Security Bench Mark v2
author: msmbaldwin
ms.service: security
ms.topic: conceptual
ms.date: 09/13/2020
ms.author: mbaldwin
ms.custom: security-benchmark
ms.openlocfilehash: fe6861a3319b9d9c0e6535ee3303c90f0a0f26c8
ms.sourcegitcommit: 94c750edd4d755d6ecee50ac977328098a277479
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2020
ms.locfileid: "90059193"
---
# <a name="security-control-backup-and-recovery"></a>Beveiligings beheer: back-up en herstel

Back-up en herstel bestrijkt de controles om ervoor te zorgen dat de gegevens en configuratie back-ups in de verschillende service lagen worden uitgevoerd, gevalideerd en beveiligd.

## <a name="br-1-ensure-regular-automated-backups"></a>BR-1: controleren op regel matige automatische back-ups

| Azure-ID | CIS-besturings elementen v 7.1-ID ('s) | NIST SP800-53 R4-ID ('s) |
|--|--|--|--|
| BR-1 | 10.1 | CP-2, CP4, CP-6, CP-9 |

Zorg ervoor dat u een back-up van systemen en gegevens maakt om de bedrijfs continuïteit na een onverwachte gebeurtenis te hand haven. Dit moet richt lijnen zijn voor de doel stellingen voor herstel punt doelstelling (RPO) en de beoogde herstel tijd (RTO).

Schakel Azure Backup in en configureer de back-upbron (bijvoorbeeld Azure Vm's, SQL Server, HANA-data bases of bestands shares), evenals de gewenste frequentie en retentie periode.  

Voor een hoger redundantie niveau kunt u geografisch redundante opslag optie inschakelen om back-upgegevens naar een secundaire regio te repliceren en te herstellen met behulp van een herstel bewerking voor meerdere regio's.

- [Azure Backup inschakelen](/azure/backup/)

- [Het terugzetten van meerdere regio's inschakelen](/azure/backup/backup-azure-arm-restore-vms#cross-region-restore)

**Verantwoordelijkheid**: klant

**Beveiligings belanghebbenden**van de klant:

- [Beleid en standaarden](/azure/cloud-adoption-framework/organize/cloud-security-policy-standards)

- [Beveiligingsarchitectuur](/azure/cloud-adoption-framework/organize/cloud-security-architecture)

- [Infrastructuur- en eindpuntbeveiliging](/azure/cloud-adoption-framework/organize/cloud-security-infrastructure-endpoint)

- [Incidentvoorbereiding](/azure/cloud-adoption-framework/organize/cloud-security-incident-preparation)

## <a name="br-2-encrypt-backup-data"></a>BR-2: back-upgegevens versleutelen

| Azure-ID | CIS-besturings elementen v 7.1-ID ('s) | NIST SP800-53 R4-ID ('s) |
|--|--|--|--|
| BR-2 | 10,2 | CP-9 |

Zorg ervoor dat uw back-ups worden beschermd tegen aanvallen. Hierbij moet de back-ups worden versleuteld om te worden beveiligd tegen verlies van vertrouwelijkheid.   

Voor on-premises back-ups met Azure Backup, wordt versleuteling op rest aangeboden met de wachtwoordzin die u opgeeft. Voor reguliere back-ups van Azure service worden back-upgegevens automatisch versleuteld met door Azure-platforms beheerde sleutels. U kunt ervoor kiezen om de back-up te versleutelen met de door de klant beheerde sleutel. Zorg er in dit geval voor dat deze door de klant beheerde sleutel in de sleutel kluis zich ook in het back-upbereik bevindt. 

Gebruik op rollen gebaseerd toegangs beheer in Azure Backup, Azure Key Vault of andere bronnen voor het beveiligen van back-ups en door de klant beheerde sleutels. Daarnaast kunt u geavanceerde beveiligings functies inschakelen om MFA te vereisen voordat back-ups kunnen worden gewijzigd of verwijderd.

- [Overzicht van beveiligings functies in Azure Backup](/azure/backup/security-overview)

- [Versleuteling van back-upgegevens met door de klant beheerde sleutels](/azure/backup/encryption-at-rest-with-cmk) 

- [Back-ups maken van Key Vault sleutels in azure](/powershell/module/azurerm.keyvault/backup-azurekeyvaultkey?view=azurermps-6.13.0)

**Verantwoordelijkheid**: klant

**Beveiligings belanghebbenden**van de klant:

- [Beveiligingsarchitectuur](/azure/cloud-adoption-framework/organize/cloud-security-architecture)

- [Infrastructuur- en eindpuntbeveiliging](/azure/cloud-adoption-framework/organize/cloud-security-infrastructure-endpoint)

- Voor [bereiding van incidenten](/) Azure/Cloud-acceptatie-Framework/indelen/Cloud-beveiliging-incident-voor bereiding

## <a name="br-3-validate-all-backups-including-customer-managed-keys"></a>BR-3: alle back-ups valideren, inclusief door de klant beheerde sleutels

| Azure-ID | CIS-besturings elementen v 7.1-ID ('s) | NIST SP800-53 R4-ID ('s) |
|--|--|--|--|
| BR-3 | 10,3 | CP-4, CP-9 |

Maak regel matig gegevens herstel van uw back-up. Zorg ervoor dat u een back-up van door de klant beheerde sleutels kunt herstellen.

- [Bestanden herstellen vanuit back-up van Azure virtual machine](/azure/backup/backup-azure-restore-files-from-vm)

- [Key Vault sleutels herstellen in azure](/powershell/module/azurerm.keyvault/restore-azurekeyvaultkey?view=azurermps-6.13.0)

**Verantwoordelijkheid**: klant

**Beveiligings belanghebbenden**van de klant:

- [Incidentvoorbereiding](/azure/cloud-adoption-framework/organize/cloud-security-incident-preparation)

- [Beheer van beveiligings naleving](/azure/cloud-adoption-framework/organize/cloud-security-compliance-management)

## <a name="br-4-mitigate-risk-of-lost-keys"></a>BR-4: risico op verloren sleutels beperken

| Azure-ID | CIS-besturings elementen v 7.1-ID ('s) | NIST SP800-53 R4-ID ('s) |
|--|--|--|--|
| BR-4 | 10.4 | CP-9 |

Zorg ervoor dat u maat regelen hebt om te voor komen en te herstellen van het verlies van sleutels. Schakel de beveiliging van zacht verwijderen en opschonen in Azure Key Vault in om sleutels te beschermen tegen onbedoelde of schadelijke verwijdering.  

- [Zacht verwijderen en beveiliging opschonen inschakelen in Key Vault](/azure/storage/blobs/storage-blob-soft-delete?tabs=azure-portal)

**Verantwoordelijkheid**: klant

**Beveiligings belanghebbenden**van de klant:

- [Beveiligingsarchitectuur](/azure/cloud-adoption-framework/organize/cloud-security-architecture)

- [Incidentvoorbereiding](/azure/cloud-adoption-framework/organize/cloud-security-incident-preparation)

- [Gegevens beveiliging](/azure/cloud-adoption-framework/organize/cloud-security-data-security)

