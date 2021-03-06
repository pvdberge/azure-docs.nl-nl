---
title: Problemen met de activering van virtuele Windows-machines in azure oplossen | Microsoft Docs
description: Biedt de probleemoplossings stappen voor het oplossen van problemen met de activering van Windows-virtuele machines in azure
services: virtual-machines-windows, azure-resource-manager
documentationcenter: ''
author: genlin
manager: dcscontentpm
editor: ''
tags: top-support-issue, azure-resource-manager
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.topic: troubleshooting
ms.date: 11/15/2018
ms.author: genli
ms.openlocfilehash: 8c89fcf22f669c97f2b17acce57c293eabcf96de
ms.sourcegitcommit: 3d79f737ff34708b48dd2ae45100e2516af9ed78
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/23/2020
ms.locfileid: "87009693"
---
# <a name="troubleshoot-azure-windows-virtual-machine-activation-problems"></a>Problemen met de activering van virtuele Microsoft Azure-machines oplossen

Als u problemen ondervindt bij het activeren van Azure Windows Virtual Machine (VM) die is gemaakt op basis van een aangepaste installatie kopie, kunt u de informatie in dit document gebruiken om het probleem op te lossen. 

## <a name="understanding-azure-kms-endpoints-for-windows-product-activation-of-azure-virtual-machines"></a>Algemene informatie over Azure KMS-eindpunten voor Windows-productactivering van Azure Virtual Machines

Azure gebruikt verschillende eind punten voor KMS-activering (Key Management Services), afhankelijk van de regio van de Cloud waar de virtuele machine zich bevindt. Wanneer u deze hand leiding voor probleem oplossing gebruikt, gebruikt u het juiste KMS-eind punt dat van toepassing is op uw regio.

* Open bare Cloud regio's van Azure: kms.core.windows.net:1688
* Azure China 21Vianet nationale Cloud regio's: kms.core.chinacloudapi.cn:1688
* Azure Duitsland National Cloud regio's: kms.core.cloudapi.de:1688
* Azure US Gov nationale Cloud regio's: kms.core.usgovcloudapi.net:1688

## <a name="symptom"></a>Symptoom

Wanneer u probeert een Azure Windows-VM te activeren, wordt een fout bericht weer gegeven dat lijkt op het volgende voor beeld:

**Fout: 0xC004F074 software-LicensingService heeft gerapporteerd dat de computer niet kan worden geactiveerd. Er kan geen verbinding worden gemaakt met Key ManagementService (KMS). Raadpleeg het gebeurtenis logboek van de toepassing voor meer informatie.**

## <a name="cause"></a>Oorzaak

Over het algemeen treden er activeringsproblemen met Azure-VM's op als de Windows-VM niet is geconfigureerd met de juiste installatiecode voor de KMS-client, of als de Windows-VM een probleem heeft met de connectiviteit met de Azure KMS-service (kms.core.windows.net, port 1688). 

## <a name="solution"></a>Oplossing

>[!NOTE]
>Als u een site-naar-site-VPN en geforceerde tunneling gebruikt, raadpleegt u [aangepaste Azure-routes gebruiken om de KMS-activering met geforceerde Tunneling in te scha kelen](../../vpn-gateway/vpn-gateway-about-forced-tunneling.md). 
>
>Zie [kan ik Internet connectiviteit met virtuele netwerken die zijn verbonden met ExpressRoute-circuits blok keren](../../expressroute/expressroute-faqs.md)als u ExpressRoute gebruikt en u een standaard route hebt gepubliceerd?.

### <a name="step-1-configure-the-appropriate-kms-client-setup-key"></a>Stap 1 de juiste installatie sleutel voor de KMS-client configureren

Voor de virtuele machine die is gemaakt op basis van een aangepaste installatie kopie, moet u de juiste installatie sleutel voor de KMS-client configureren voor de virtuele machine.

1. Voer **slmgr. vbs/dlv** uit vanaf een opdracht prompt met verhoogde bevoegdheden. Controleer de beschrijvings waarde in de uitvoer en bepaal of deze is gemaakt op basis van Retail-(DETAILHANDELKANAAL) of volume (VOLUME_KMSCLIENT)-licentie media:
  

    ```
    cscript c:\windows\system32\slmgr.vbs /dlv
    ```

2. Als in **slmgr.vbs /dlv** het kanaal RETAIL wordt weergegeven, voert u de volgende opdrachten uit om de [installatiecode voor de KMS-client](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj612867(v=ws.11)?f=255&MSPPError=-2147217396) in te stellen voor de gebruikte versie van Windows Server, en dwingt u af dat de activering opnieuw wordt uitgevoerd: 

    ```
    cscript c:\windows\system32\slmgr.vbs /ipk <KMS client setup key>

    cscript c:\windows\system32\slmgr.vbs /ato
     ```

    Bijvoorbeeld, voor Windows Server 2016 Data Center, voert u de volgende opdracht uit:

    ```
    cscript c:\windows\system32\slmgr.vbs /ipk CB7KF-BWN84-R7R2Y-793K2-8XDDG
    ```

### <a name="step-2-verify-the-connectivity-between-the-vm-and-azure-kms-service"></a>Stap 2 de connectiviteit tussen de virtuele machine en de Azure KMS-service controleren

1. Down load en pak het [PSping](/sysinternals/downloads/psping) -hulp programma uit naar een lokale map in de virtuele machine die niet wordt geactiveerd. 

2. Ga naar Start, zoek op Windows Power shell, klik met de rechter muisknop op Windows Power shell en selecteer vervolgens als administrator uitvoeren.

3. Zorg ervoor dat de VM is geconfigureerd om de juiste Azure KMS-server te gebruiken. Voer hiervoor de volgende opdracht uit:
  
    ```powershell
    Invoke-Expression "$env:windir\system32\cscript.exe $env:windir\system32\slmgr.vbs /skms kms.core.windows.net:1688"
    ```

    De opdracht moet retour neren: de computer naam van de Key Management-service is ingesteld op kms.core.windows.net:1688.

4. Controleer met behulp van Psping of er connectiviteit is met de KMS-server. Ga naar de map waarin u het gedownloade bestand Pstools.zip hebt uitgepakt en voer vervolgens het volgende uit:
  
    ```
    .\psping.exe kms.core.windows.net:1688
    ```
   Controleer op de tweede tot laatste regel van de uitvoer of u ziet: verzonden = 4, ontvangen = 4, verloren = 0 (0% verlies).

   Als verloren is groter dan 0 (nul), is de virtuele machine niet verbonden met de KMS-server. Als de virtuele machine zich in een virtueel netwerk bevindt en een aangepaste DNS-server is opgegeven, moet u ervoor zorgen dat de DNS-server kms.core.windows.net kan omzetten. U kunt ook de DNS-server wijzigen in een die kms.core.windows.net omzetten.

   Als u alle DNS-servers uit een virtueel netwerk verwijdert, gebruiken Vm's de interne DNS-service van Azure. Met deze service kunt u kms.core.windows.net omzetten.
  
    Zorg er ook voor dat het uitgaande netwerk verkeer naar het KMS-eind punt met de 1688-poort niet wordt geblokkeerd door de firewall in de virtuele machine.

5. Controleer met [Network Watcher volgende hop](../../network-watcher/network-watcher-next-hop-overview.md) of het type van de volgende hop van de virtuele machine in kwestie naar het doel-IP-23.102.135.246 (voor KMS.core.Windows.net) of het IP-adres van het juiste KMS-eind punt dat van toepassing is op uw regio **Internet**is.  Als het resultaat VirtualAppliance of VirtualNetworkGateway is, is er waarschijnlijk een standaard route aanwezig.  Neem contact op met uw netwerk beheerder en werk ermee om de juiste gedrags duur te bepalen.  Dit kan een [aangepaste route](./custom-routes-enable-kms-activation.md) zijn als die oplossing overeenkomt met het beleid van uw organisatie.

6. Nadat u hebt geverifieerd dat de connectiviteit met kms.core.windows.net is geslaagd, voert u de volgende opdracht uit wanneer een Windows PowerShell-opdrachtprompt met verhoogde bevoegdheid wordt weergegeven. Met deze opdracht wordt meerdere keren geprobeerd te activeren.

    ```powershell
    1..12 | ForEach-Object { Invoke-Expression "$env:windir\system32\cscript.exe $env:windir\system32\slmgr.vbs /ato" ; start-sleep 5 }
    ```

    Na een geslaagde activering worden gegevens geretourneerd die er ongeveer als volgt uitzien:
    
    **Windows (R), ServerDatacenter Edition (12345678-1234-1234-1234-12345678) activeren...  Het product is geactiveerd.**

## <a name="faq"></a>Veelgestelde vragen 

### <a name="i-created-the-windows-server-2016-from-azure-marketplace-do-i-need-to-configure-kms-key-for-activating-the-windows-server-2016"></a>Ik heb Windows Server 2016 van Azure Marketplace gemaakt. Moet ik de KMS-sleutel voor het activeren van de Windows Server 2016 configureren? 

 
Nee. Voor de installatie kopie in azure Marketplace is de juiste installatie sleutel voor de KMS-client al geconfigureerd. 

### <a name="does-windows-activation-work-the-same-way-regardless-if-the-vm-is-using-azure-hybrid-use-benefit-hub-or-not"></a>Werkt Windows activeren op dezelfde manier, ongeacht of de virtuele machine gebruikmaakt van Azure Hybrid Use Benefit (HUB) of niet? 

 
Ja. 
 

### <a name="what-happens-if-windows-activation-period-expires"></a>Wat gebeurt er als de Windows-activerings periode verloopt? 

 
Wanneer de respijt periode is verlopen en Windows nog steeds niet wordt geactiveerd, worden in Windows Server 2008 R2 en latere versies van Windows aanvullende meldingen over het activeren weer gegeven. De achtergrond van het bureau blad blijft zwart en Windows Update installeert alleen beveiligings-en essentiële updates, maar geen optionele updates. Zie de sectie meldingen onder aan de pagina [licentie voorwaarden](/previous-versions/tn-archive/ff793403(v=technet.10)) .   

## <a name="need-help-contact-support"></a>Hebt u hulp nodig? Neem contact op met ondersteuning.

Als u nog steeds hulp nodig hebt, neemt u [contact op met de ondersteuning](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade) om uw probleem snel op te lossen.
