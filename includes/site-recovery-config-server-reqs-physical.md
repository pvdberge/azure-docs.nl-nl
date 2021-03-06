---
title: bestand opnemen
description: bestand opnemen
services: site-recovery
author: rayne-wiselman
manager: carmonm
ms.service: site-recovery
ms.topic: include
ms.date: 09/03/2018
ms.author: raynew
ms.custom: include file
ms.openlocfilehash: afeae4af9b41bf434b26833a3bd927118a4697ae
ms.sourcegitcommit: 877491bd46921c11dd478bd25fc718ceee2dcc08
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/02/2020
ms.locfileid: "67176261"
---
**Vereisten voor de configuratie/proces server voor de replicatie van de fysieke server**

**Onderdeel** | **Vereiste** 
--- | ---
**HARDWARE-INSTELLINGEN** | 
CPU-kernen | 8 
RAM | 16 GB
Aantal schijven | 3, met inbegrip van de besturingssysteem schijf, de cache schijf van de proces server en het Bewaar station voor failback 
Vrije schijf ruimte (cache van proces server) | 600 GB
Vrije schijf ruimte (Bewaar schijf) | 600 GB
 | 
**SOFTWARE-INSTELLINGEN** | 
Besturingssysteem | Windows Server 2012 R2 <br> Windows Server 2016
Landinstelling van het besturingssysteem | Engels (en-us)
Windows Server-functies | Deze rollen niet inschakelen: <br> - Active Directory Domain Services <br>- Internet Information Services <br> - Hyper-V 
Groeps beleid | Dit groeps beleid niet inschakelen: <br> -Toegang tot de opdracht prompt voor komen. <br> -Toegang tot register bewerkings Programma's verhinderen. <br> -Logica vertrouwen voor bestands bijlagen. <br> -Schakel uitvoering van script in. <br> [Meer informatie](https://technet.microsoft.com/library/gg176671(v=ws.10).aspx)
IIS | -Geen vooraf bestaande standaard website <br> -Geen bestaande website/toepassing die luistert op poort 443 <br>- [Anonieme verificatie](https://technet.microsoft.com/library/cc731244(v=ws.10).aspx) inschakelen <br> - [Fastcgi](https://technet.microsoft.com/library/cc753077(v=ws.10).aspx) -instelling inschakelen.
Type IP-adres | Statisch 
| 
**TOEGANGS INSTELLINGEN** | 
MYSQL | MySQL moet worden geïnstalleerd op de configuratie server. U kunt hand matig installeren, of Site Recovery kunt dit installeren tijdens de implementatie. Controleer of de computer kan worden bereikt om Site Recovery te installeren http://cdn.mysql.com/archives/mysql-5.5/mysql-5.5.37-win32.msi .
URL's | De configuratie server moet toegang hebben tot deze Url's (rechtstreeks of via proxy):<br/><br/> Azure AD: `login.microsoftonline.com` ; `login.microsoftonline.us` ;`*.accesscontrol.windows.net`<br/><br/> Replicatie gegevens overdracht: `*.backup.windowsazure.com` ;`*.backup.windowsazure.us`<br/><br/> Replicatie beheer: `*.hypervrecoverymanager.windowsazure.com` ; `*.hypervrecoverymanager.windowsazure.us` ; `https://management.azure.com` ;`*.services.visualstudio.com`<br/><br/> Toegang tot opslag: `*.blob.core.windows.net` ;`*.blob.core.usgovcloudapi.net`<br/><br/> Tijd synchronisatie: `time.nist.gov` ;`time.windows.com`<br/><br/> Telemetrie (optioneel):`dc.services.visualstudio.com`
Firewall | Firewall regels op basis van IP-adressen moeten communicatie met Azure-Url's toestaan. Om het IP-bereik te vereenvoudigen en te beperken, kunt u het beste URL-filters gebruiken.<br/><br/>**Voor commerciële Ip's:**<br/><br/>-De [IP-bereiken van het Azure-Data Center](https://www.microsoft.com/download/confirmation.aspx?id=41653)en de HTTPS-poort (443) toestaan.<br/><br/> -IP-adresbereiken toestaan voor de VS West (gebruikt voor Access Control en identiteits beheer).<br/><br/> -IP-adresbereiken toestaan voor de Azure-regio van uw abonnement, ter ondersteuning van de benodigde Url's voor Azure Active Directory, back-up, replicatie en opslag.<br/><br/> **Voor overheids Ip's:**<br/><br/> -De IP-bereiken van het Azure Government Data Center en de HTTPS-poort (443) toestaan.<br/><br/> -IP-adresbereiken toestaan voor alle US Gov regio's (Virginia, Texas, Arizona en Iowa), ter ondersteuning van de Url's die nodig zijn voor Azure Active Directory, back-up, replicatie en opslag.
Poorten | 443 toestaan (indeling van besturings kanaal)<br/><br/> 9443 toestaan (gegevens transport) 


**Vereisten voor de grootte van de configuratie/proces server**

**CPU** | **Geheugen** | **Cache schijf** | **Gegevens wijzigings frequentie** | **Gerepliceerde machines**
--- | --- | --- | --- | ---
8 Vcpu's<br/><br/> 2 sockets * 4 kernen \@ 2,5 GHz | Maxi | 300 GB | 500 GB of minder | < 100-machines
12 Vcpu's<br/><br/> 2 SOCKS * 6 kernen \@ 2,5 GHz | 18 GB | 600 GB | 500 GB-1 TB | 100 tot 150 computers
16 Vcpu's<br/><br/> 2 SOCKS * 8 kernen \@ 2,5 GHz | 32 GB | 1 TB | 1-2 TB | 150-200 computers

