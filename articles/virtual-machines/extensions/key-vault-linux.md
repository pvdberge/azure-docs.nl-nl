---
title: VM-extensie Azure Key Vault voor Linux
description: Implementeer een agent die het automatisch vernieuwen van Key Vault-certificaten op virtuele machines uitvoert met behulp van een extensie van de virtuele machine.
services: virtual-machines-linux
author: msmbaldwin
tags: keyvault
ms.service: virtual-machines-linux
ms.topic: article
ms.date: 12/02/2019
ms.author: mbaldwin
ms.openlocfilehash: 4c5389e322fdf44e8a71baa8770f87c276c076c9
ms.sourcegitcommit: 5a3b9f35d47355d026ee39d398c614ca4dae51c6
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/02/2020
ms.locfileid: "89400395"
---
# <a name="key-vault-virtual-machine-extension-for-linux"></a>Extensie van de virtuele machine Key Vault voor Linux

De Key Vault VM-extensie biedt automatisch vernieuwen van certificaten die zijn opgeslagen in een Azure-sleutel kluis. De uitbrei ding bewaakt met name een lijst van waargenomen certificaten die zijn opgeslagen in sleutel kluizen.  Bij het detecteren van een wijziging haalt de extensie de bijbehorende certificaten op en installeert deze. De extensie van de Key Vault-VM wordt gepubliceerd en ondersteund door micro soft, momenteel op Linux Vm's. In dit document vindt u informatie over de ondersteunde platforms, configuraties en implementatie opties voor de Key Vault VM-extensie voor Linux. 

### <a name="operating-system"></a>Besturingssysteem

De Key Vault VM-extensie ondersteunt deze Linux-distributies:

- Ubuntu-1604
- Ubuntu-1804
- Debian-9
- SuSE-15 

### <a name="supported-certificate-content-types"></a>Ondersteunde inhouds typen voor certificaten

- PKCS #12
- PEM

## <a name="extension-schema"></a>Extensieschema

De volgende JSON toont het schema voor de extensie van de Key Vault-VM. Voor de extensie zijn geen beveiligde instellingen vereist: alle instellingen ervan worden beschouwd als informatie zonder gevolgen voor de beveiliging. De uitbrei ding vereist een lijst met bewaakte geheimen, polling frequentie en het doel certificaat archief. Specifiek:  
```json
    {
      "type": "Microsoft.Compute/virtualMachines/extensions",
      "name": "KVVMExtensionForLinux",
      "apiVersion": "2019-07-01",
      "location": "<location>",
      "dependsOn": [
          "[concat('Microsoft.Compute/virtualMachines/', <vmName>)]"
      ],
      "properties": {
      "publisher": "Microsoft.Azure.KeyVault",
      "type": "KeyVaultForLinux",
      "typeHandlerVersion": "1.0",
      "autoUpgradeMinorVersion": true,
      "settings": {
        "secretsManagementSettings": {
          "pollingIntervalInS": <polling interval in seconds, e.g. "3600">,
          "certificateStoreName": <It is ignored on Linux>,
          "linkOnRenewal": <Not available on Linux e.g.: false>,
          "certificateStoreLocation": <disk path where certificate is stored, default: "/var/lib/waagent/Microsoft.Azure.KeyVault">,
          "requireInitialSync": <initial synchronization of certificates e..g: true>,
          "observedCertificates": <list of KeyVault URIs representing monitored certificates, e.g.: "https://myvault.vault.azure.net/secrets/mycertificate"
        },
        "authenticationSettings": {
                "msiEndpoint":  <Optional MSI endpoint e.g.: "http://169.254.169.254/metadata/identity">,
                "msiClientId":  <Optional MSI identity e.g.: "c7373ae5-91c2-4165-8ab6-7381d6e75619">
        }
       }
      }
    }
```

> [!NOTE]
> De Url's van uw waargenomen certificaten moeten van het formulier zijn `https://myVaultName.vault.azure.net/secrets/myCertName` .
> 
> Dit komt doordat het `/secrets` pad het volledige certificaat retourneert, inclusief de persoonlijke sleutel, terwijl het `/certificates` pad niet. Meer informatie over certificaten vindt u hier: [Key Vault certificaten](../../key-vault/general/about-keys-secrets-certificates.md)

> [!IMPORTANT]
> De eigenschap authenticationSettings is alleen **vereist** voor vm's met door de **gebruiker toegewezen identiteiten**.
> Hiermee wordt de identiteit opgegeven die moet worden gebruikt voor de verificatie van Key Vault.


### <a name="property-values"></a>Eigenschaps waarden

| Naam | Waarde/voor beeld | Gegevenstype |
| ---- | ---- | ---- |
| apiVersion | 2019-07-01 | datum |
| publisher | Microsoft.Azure.KeyVault | tekenreeks |
| type | KeyVaultForLinux | tekenreeks |
| typeHandlerVersion | 1,0 | int |
| pollingIntervalInS | 3600 | tekenreeks |
| Naam certificaat archief | Het wordt genegeerd op Linux | tekenreeks |
| linkOnRenewal | false | boolean |
| certificateStoreLocation  | /var/lib/waagent/Microsoft.Azure.KeyVault | tekenreeks |
| requiredInitialSync | true | boolean |
| observedCertificates  | ["https://myvault.vault.azure.net/secrets/mycertificate"] | teken reeks matrix
| msiEndpoint | http://169.254.169.254/metadata/identity | tekenreeks |
| msiClientId | c7373ae5-91c2-4165-8ab6-7381d6e75619 | tekenreeks |


## <a name="template-deployment"></a>Sjabloonimplementatie

Azure VM-extensies kunnen worden geïmplementeerd met Azure Resource Manager sjablonen. Sjablonen zijn ideaal bij het implementeren van een of meer virtuele machines die na de implementatie van certificaten moeten worden vernieuwd. De uitbrei ding kan worden geïmplementeerd op afzonderlijke Vm's of virtuele-machine schaal sets. Het schema en de configuratie zijn gebruikelijk voor beide sjabloon typen. 

De JSON-configuratie voor een extensie van een virtuele machine moet zijn genest in het resource fragment van de virtuele machine van de sjabloon, met name `"resources": []` object voor de virtuele-machine sjabloon en in het geval van een schaalset voor virtuele machines onder `"virtualMachineProfile":"extensionProfile":{"extensions" :[]` object.

```json
    {
      "type": "Microsoft.Compute/virtualMachines/extensions",
      "name": "KeyVaultForLinux",
      "apiVersion": "2019-07-01",
      "location": "<location>",
      "dependsOn": [
          "[concat('Microsoft.Compute/virtualMachines/', <vmName>)]"
      ],
      "properties": {
      "publisher": "Microsoft.Azure.KeyVault",
      "type": "KeyVaultForLinux",
      "typeHandlerVersion": "1.0",
      "autoUpgradeMinorVersion": true,
      "settings": {
          "secretsManagementSettings": {
          "pollingIntervalInS": <polling interval in seconds, e.g. "3600">,
          "certificateStoreName": <ingnored on linux>,
          "certificateStoreLocation": <disk path where certificate is stored, default: "/var/lib/waagent/Microsoft.Azure.KeyVault">,
          "observedCertificates": <list of KeyVault URIs representing monitored certificates, e.g.: "https://myvault.vault.azure.net/secrets/mycertificate"
        }      
      }
      }
    }
```


## <a name="azure-powershell-deployment"></a>Azure PowerShell-implementatie
> [!WARNING]
> Power shell-clients voegen vaak toe `\` aan `"` in de settings.js, waardoor akvvm_service mislukt met de volgende fout: `[CertificateManagementConfiguration] Failed to parse the configuration settings with:not an object.`

De Azure PowerShell kan worden gebruikt om de Key Vault VM-extensie te implementeren op een bestaande virtuele machine of virtuele-machine schaalset. 

* De uitbrei ding implementeren op een virtuele machine:
    
    ```powershell
        # Build settings
        $settings = '{"secretsManagementSettings": 
        { "pollingIntervalInS": "' + <pollingInterval> + 
        '", "certificateStoreName": "' + <certStoreName> + 
        '", "certificateStoreLocation": "' + <certStoreLoc> + 
        '", "observedCertificates": ["' + <observedCerts> + '"] } }'
        $extName =  "KeyVaultForLinux"
        $extPublisher = "Microsoft.Azure.KeyVault"
        $extType = "KeyVaultForLinux"
       
    
        # Start the deployment
        Set-AzVmExtension -TypeHandlerVersion "1.0" -ResourceGroupName <ResourceGroupName> -Location <Location> -VMName <VMName> -Name $extName -Publisher $extPublisher -Type $extType -SettingString $settings
    
    ```

* De uitbrei ding implementeren op een schaalset voor virtuele machines:

    ```powershell
    
        # Build settings
        $settings = '{"secretsManagementSettings": 
        { "pollingIntervalInS": "' + <pollingInterval> + 
        '", "certificateStoreName": "' + <certStoreName> + 
        '", "certificateStoreLocation": "' + <certStoreLoc> + 
        '", "observedCertificates": ["' + <observedCerts> + '"] } }'
        $extName = "KeyVaultForLinux"
        $extPublisher = "Microsoft.Azure.KeyVault"
        $extType = "KeyVaultForLinux"
        
        # Add Extension to VMSS
        $vmss = Get-AzVmss -ResourceGroupName <ResourceGroupName> -VMScaleSetName <VmssName>
        Add-AzVmssExtension -VirtualMachineScaleSet $vmss  -Name $extName -Publisher $extPublisher -Type $extType -TypeHandlerVersion "1.0" -Setting $settings

        # Start the deployment
        Update-AzVmss -ResourceGroupName <ResourceGroupName> -VMScaleSetName <VmssName> -VirtualMachineScaleSet $vmss 
    
    ```

## <a name="azure-cli-deployment"></a>Implementatie van Azure CLI

De Azure CLI kan worden gebruikt om de Key Vault VM-extensie te implementeren op een bestaande virtuele machine of virtuele-machine schaalset. 
 
* De uitbrei ding implementeren op een virtuele machine:
    
    ```azurecli
       # Start the deployment
         az vm extension set -n "KeyVaultForLinux" `
         --publisher Microsoft.Azure.KeyVault `
         -g "<resourcegroup>" `
         --vm-name "<vmName>" `
         --settings '{\"secretsManagementSettings\": { \"pollingIntervalInS\": \"<pollingInterval>\", \"certificateStoreName\": \"<certStoreName>\", \"certificateStoreLocation\": \"<certStoreLoc>\", \"observedCertificates\": [\ <observedCerts>\"] }}'
    ```

* De uitbrei ding implementeren op een schaalset voor virtuele machines:

   ```azurecli
        # Start the deployment
        az vmss extension set -n "KeyVaultForLinux" `
        --publisher Microsoft.Azure.KeyVault `
        -g "<resourcegroup>" `
        --vm-name "<vmName>" `
        --settings '{\"secretsManagementSettings\": { \"pollingIntervalInS\": \"<pollingInterval>\", \"certificateStoreName\": \"<certStoreName>\", \"certificateStoreLocation\": \"<certStoreLoc>\", \"observedCertificates\": [\ <observedCerts>\"] }}'
    ```

Houd rekening met de volgende beperkingen/vereisten:
- Key Vault beperkingen:
  - Deze moet op het moment van de implementatie bestaan 
  - Het Key Vault toegangs beleid moet worden ingesteld voor de virtuele machine-VMSS met behulp van een beheerde identiteit. Zie [verifiëren bij Key Vault](/azure/key-vault/general/authentication) en [een Key Vault toegangs beleid toewijzen](/azure/key-vault/general/assign-access-policy-cli).


## <a name="troubleshoot-and-support"></a>Problemen oplossen en ondersteuning

### <a name="troubleshoot"></a>Problemen oplossen

Gegevens over de status van uitbreidings implementaties kunnen worden opgehaald uit de Azure Portal en met behulp van de Azure PowerShell. Als u de implementatie status van extensies voor een bepaalde virtuele machine wilt bekijken, voert u de volgende opdracht uit met behulp van de Azure PowerShell.

## <a name="azure-powershell"></a>Azure PowerShell
```powershell
Get-AzVMExtension -VMName <vmName> -ResourceGroupname <resource group name>
```

## <a name="azure-cli"></a>Azure CLI
```azurecli
 az vm get-instance-view --resource-group <resource group name> --name  <vmName> --query "instanceView.extensions"
```
### <a name="logs-and-configuration"></a>Logboeken en configuratie

```
/var/log/waagent.log
/var/log/azure/Microsoft.Azure.KeyVault.KeyVaultForLinux/*
/var/lib/waagent/Microsoft.Azure.KeyVault.KeyVaultForLinux-<most recent version>/config/*
```

### <a name="support"></a>Ondersteuning

Als u op elk moment in dit artikel meer hulp nodig hebt, kunt u contact opnemen met de Azure-experts op [MSDN Azure en stack overflow forums](https://azure.microsoft.com/support/forums/). U kunt ook een ondersteunings incident voor Azure opslaan. Ga naar de [ondersteunings site van Azure](https://azure.microsoft.com/support/options/) en selecteer ondersteuning verkrijgen. Lees de [Veelgestelde vragen over ondersteuning voor Microsoft Azure](https://azure.microsoft.com/support/faq/)voor meer informatie over het gebruik van Azure-ondersteuning.
