---
title: bestand opnemen
description: bestand opnemen
services: virtual-machines
author: roygara
ms.service: virtual-machines
ms.topic: include
ms.date: 06/15/2020
ms.author: rogarana
ms.custom: include file
ms.openlocfilehash: c696bea902a25571c173d04e0eaa7304ed657151
ms.sourcegitcommit: 877491bd46921c11dd478bd25fc718ceee2dcc08
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/02/2020
ms.locfileid: "85610428"
---
1. Zorg ervoor dat u de nieuwste [versie van Azure PowerShell](/powershell/azure/install-az-ps)hebt geïnstalleerd en dat u bent aangemeld bij een Azure-account in met Connect-AzAccount

1. Maak een instantie van Azure Key Vault en versleutelings sleutel.

    Wanneer u het Key Vault-exemplaar maakt, moet u de beveiliging voor voorlopig verwijderen en leegmaken inschakelen. Met zacht verwijderen zorgt u ervoor dat de Key Vault een verwijderde sleutel bevat voor een bepaalde Bewaar periode (standaard 90 dagen). Bij het opschonen van de beveiliging wordt ervoor gezorgd dat een verwijderde sleutel pas definitief kan worden verwijderd als de retentie periode is verstreken. Met deze instellingen wordt voor komen dat gegevens verloren gaan als gevolg van onbedoeld verwijderen. Deze instellingen zijn verplicht wanneer u een Key Vault gebruikt voor het versleutelen van Managed disks.
    
    ```powershell
    $ResourceGroupName="yourResourceGroupName"
    $LocationName="westcentralus"
    $keyVaultName="yourKeyVaultName"
    $keyName="yourKeyName"
    $keyDestination="Software"
    $diskEncryptionSetName="yourDiskEncryptionSetName"

    $keyVault = New-AzKeyVault -Name $keyVaultName -ResourceGroupName $ResourceGroupName -Location $LocationName -EnableSoftDelete -EnablePurgeProtection

    $key = Add-AzKeyVaultKey -VaultName $keyVaultName -Name $keyName -Destination $keyDestination  
    ```

1.    Maak een instantie van een DiskEncryptionSet. 
    
        ```powershell
        $desConfig=New-AzDiskEncryptionSetConfig -Location $LocationName -SourceVaultId $keyVault.ResourceId -KeyUrl $key.Key.Kid -IdentityType SystemAssigned
        
        $des=New-AzDiskEncryptionSet -Name $diskEncryptionSetName -ResourceGroupName $ResourceGroupName -InputObject $desConfig 
        ```

1.    Verleen de DiskEncryptionSet-resource toegang tot de sleutel kluis.

        > [!NOTE]
        > Het kan enkele minuten duren voordat Azure de identiteit van uw DiskEncryptionSet in uw Azure Active Directory heeft gemaakt. Als er een fout optreedt, zoals ' kan het Active Directory-object niet vinden ' tijdens het uitvoeren van de volgende opdracht, wacht u enkele minuten en probeert u het opnieuw.
        
        ```powershell  
        Set-AzKeyVaultAccessPolicy -VaultName $keyVaultName -ObjectId $des.Identity.PrincipalId -PermissionsToKeys wrapkey,unwrapkey,get
        ```
