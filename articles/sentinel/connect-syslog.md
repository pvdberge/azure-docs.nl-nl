---
title: Syslog-gegevens verbinden met Azure-Sentinel | Microsoft Docs
description: Verbind elke computer of apparaat dat syslog ondersteunt op Azure Sentinel door gebruik te maken van een agent op een Linux-machine tussen het apparaat en de Sentinel. 
services: sentinel
documentationcenter: na
author: yelevin
manager: rkarlin
editor: ''
ms.service: azure-sentinel
ms.subservice: azure-sentinel
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/17/2020
ms.author: yelevin
ms.openlocfilehash: 7670d00a2dd25961a51d18c50c102e0f92b30975
ms.sourcegitcommit: 37afde27ac137ab2e675b2b0492559287822fded
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/18/2020
ms.locfileid: "88566145"
---
# <a name="collect-data-from-linux-based-sources-using-syslog"></a>Gegevens verzamelen van op Linux gebaseerde bronnen met behulp van syslog

U kunt gebeurtenissen streamen van op Linux gebaseerde machines of toestellen die met syslog worden ondersteund in azure Sentinel, met behulp van de Log Analytics-agent voor Linux (voorheen bekend als de OMS-agent). U kunt dit doen voor elke machine waarmee u de Log Analytics-agent rechtstreeks op de computer kunt installeren. Met de systeem eigen syslog-daemon van de machine worden lokale gebeurtenissen van de opgegeven typen verzameld en lokaal naar de agent doorgestuurd. deze worden naar uw Log Analytics-werk ruimte gestreamd.

> [!NOTE]
> - Als uw apparaat **algemene gebeurtenis indeling (CEF) via syslog**ondersteunt, wordt er een meer gegevens verzameling verzameld en worden de gegevens geparseerd bij het verzamelen. Kies deze optie en volg de instructies in [verbinding maken met uw externe oplossing met behulp van CEF](connect-common-event-format.md).
>
> - Log Analytics ondersteunt het verzamelen van berichten die worden verzonden door de **rsyslog** of **syslog-ng-** daemons, waarbij rsyslog de standaard waarde is. De standaard syslog-daemon op versie 5 van Red Hat Enterprise Linux (RHEL), CentOS en Oracle Linux versie (**sysklog**) wordt niet ondersteund voor de verzameling syslog-gebeurtenissen. Als u syslog-gegevens uit deze versie van deze distributies wilt verzamelen, moet de rsyslog-daemon worden geïnstalleerd en geconfigureerd om sysklog te vervangen.

## <a name="how-it-works"></a>Hoe het werkt

**Syslog** is een protocol voor gebeurtenis registratie dat algemeen is voor Linux. Wanneer de **log Analytics-agent voor Linux** op uw virtuele machine of apparaat is geïnstalleerd, wordt de lokale syslog-daemon geconfigureerd voor het door sturen van berichten naar de agent op TCP-poort 25224. De agent verzendt het bericht vervolgens naar uw Log Analytics-werk ruimte via HTTPS, waar het wordt geparseerd in een gebeurtenis logboek vermelding in de syslog-tabel in **Azure Sentinel >-logboeken**.

Zie [syslog-gegevens bronnen in azure monitor](../azure-monitor/platform/data-sources-syslog.md)voor meer informatie.

## <a name="configure-syslog-collection"></a>Syslog-verzameling configureren

### <a name="configure-your-linux-machine-or-appliance"></a>Uw Linux-machine of-apparaat configureren

1. Selecteer in azure Sentinel **Data connectors** en selecteer vervolgens de **syslog** -connector.

1. Selecteer op de Blade **syslog** de optie **connector pagina openen**.

1. Installeer de Linux-agent. Onder **Kies waar u de agent wilt installeren:**
    
    **Voor een Azure Linux-VM:**
      
    1. Selecteer **agent installeren op virtuele machine van Azure Linux**.
    
    1. Klik op de koppeling **& installatie agent voor virtuele machines van Azure Linux installeren >** . 
    
    1. Klik op de Blade **virtuele machines** op een virtuele machine waarop u de agent wilt installeren en klik vervolgens op **verbinding maken**. Herhaal deze stap voor elke virtuele machine die u wilt verbinden.
    
    **Voor elke andere Linux-machine:**

    1. **Installatie agent selecteren op een niet-Azure Linux-computer**

    1. Klik op de koppeling **& installatie agent downloaden voor niet-Azure Linux-machines >** . 

    1. Klik op de Blade **agents beheren** op het tabblad **Linux-servers** en kopieer vervolgens de opdracht voor het **downloaden en voorbereiden van de agent voor Linux** en voer deze uit op uw Linux-computer. 
    
   > [!NOTE]
   > Zorg ervoor dat u de beveiligings instellingen voor deze computers configureert op basis van het beveiligings beleid van uw organisatie. U kunt bijvoorbeeld de netwerk instellingen zodanig configureren dat deze worden uitgelijnd met het netwerk beveiligings beleid van uw organisatie en de poorten en protocollen in de daemon wijzigen, zodat deze overeenkomen met de beveiligings vereisten.

### <a name="configure-the-log-analytics-agent"></a>De Log Analytics-agent configureren

1. Klik onder aan de Blade syslog-connector op de koppeling **configuratie van geavanceerde instellingen van uw werk ruimte openen >** .

1. Selecteer op de Blade **Geavanceerde instellingen** de optie **gegevens**  >  **syslog**. Voeg vervolgens de voorzieningen toe die door de connector moeten worden verzameld.
    
    - Voeg de faciliteiten toe die uw syslog-apparaat in de logboek headers heeft opgenomen. 
    
    - Als u afwijkende SSH-aanmeldings detectie wilt gebruiken met de gegevens die u verzamelt, voegt u **auth** en **authpriv**toe. Raadpleeg de [volgende sectie](#configure-the-syslog-connector-for-anomalous-ssh-login-detection) voor meer informatie.

1. Wanneer u alle faciliteiten hebt toegevoegd die u wilt bewaken en de ernst opties voor elke functie hebt aangepast, schakelt u het selectie vakje **op de onderstaande configuratie Toep assen op mijn computers in**.

1. Selecteer **Opslaan**. 

1. Controleer op uw virtuele machine of apparaat of u de door u opgegeven faciliteiten wilt verzenden.

1. Als u de gegevens van het syslog-logboek in **Logboeken**wilt opvragen, typt u `Syslog` in het query venster.

1. U kunt de query parameters die worden beschreven in [functies gebruiken in azure monitor logboek query's](../azure-monitor/log-query/functions.md) gebruiken om uw syslog-berichten te parseren. U kunt de query vervolgens opslaan als een nieuwe Log Analytics functie en deze gebruiken als een nieuw gegevens type.

> [!NOTE]
> **Dezelfde computer gebruiken voor het door sturen van zowel normale syslog- *als* CEF-berichten**
>
>
> U kunt uw bestaande [CEF-logboek-doorstuur machine](connect-cef-agent.md) gebruiken voor het verzamelen en door sturen van logboeken van normale syslog-bronnen. U moet echter wel de volgende stappen uitvoeren om te voor komen dat gebeurtenissen in beide indelingen naar Azure Sentinel worden verzonden. Dit leidt ertoe dat gebeurtenissen worden gedupliceerd.
>
>    Het [verzamelen van gegevens is al ingesteld op basis van uw CEF-bronnen en u](connect-common-event-format.md)hebt de log Analytics agent zo geconfigureerd:
>
> 1. Op elke computer die Logboeken in CEF-indeling verzendt, moet u het syslog-configuratie bestand bewerken om de faciliteiten te verwijderen die worden gebruikt om CEF-berichten te verzenden. Op deze manier worden de functies die in CEF worden verzonden, ook niet in syslog verzonden. Zie [syslog op Linux-agent configureren](../azure-monitor/platform/data-sources-syslog.md#configure-syslog-on-linux-agent) voor gedetailleerde instructies over hoe u dit doet.
>
> 1. U moet de volgende opdracht uitvoeren op die computers om de synchronisatie van de agent met de syslog-configuratie in azure Sentinel uit te scha kelen. Dit zorgt ervoor dat de configuratie wijziging die u in de vorige stap hebt aangebracht, niet wordt overschreven.<br>
> `sudo su omsagent -c 'python /opt/microsoft/omsconfig/Scripts/OMS_MetaConfigHelper.py --disable'`


### <a name="configure-the-syslog-connector-for-anomalous-ssh-login-detection"></a>De syslog-connector configureren voor de detectie van afwijkende SSH-aanmeldingen

> [!IMPORTANT]
> De detectie van afwijkende SSH-aanmeldingen is momenteel beschikbaar als open bare preview.
> Deze functie wordt zonder service level agreement gegeven en wordt niet aanbevolen voor productie werkbelastingen.
> Zie [Supplemental Terms of Use for Microsoft Azure Previews (Aanvullende gebruiksvoorwaarden voor Microsoft Azure-previews)](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) voor meer informatie.

Azure Sentinel kan machine learning (ML) Toep assen op de syslog-gegevens om de aanmeldings activiteit voor afwijkende Secure Shell (SSH) te identificeren. Scenario's zijn onder andere:

- Onmogelijk traject: wanneer twee geslaagde aanmeldings gebeurtenissen plaatsvinden vanaf twee locaties die niet kunnen bereiken binnen het tijds bestek van de twee aanmeldings gebeurtenissen.
- Onverwachte locatie: de locatie van waaruit een geslaagde aanmeldings gebeurtenis is opgetreden verdacht. De locatie is bijvoorbeeld niet recent gezien.
 
Voor deze detectie is een specifieke configuratie van de syslog-gegevens connector vereist: 

1. Zorg ervoor dat voor stap 5 in de vorige procedure zowel **auth** als **authpriv** zijn geselecteerd als te bewaken faciliteiten. Behoud de standaard instellingen voor de ernst opties, zodat deze allemaal zijn geselecteerd. Bijvoorbeeld:
    
    > [!div class="mx-imgBorder"]
    > ![Voorzieningen die zijn vereist voor afwijkende SSH-aanmeldings detectie](./media/connect-syslog/facilities-ssh-detection.png)

2. Zorg dat er voldoende tijd is om syslog-gegevens te verzamelen. Ga vervolgens naar **Azure Sentinel-logs**en kopieer en plak de volgende query:
    
    ```console
    Syslog |  where Facility in ("authpriv","auth")| extend c = extract( "Accepted\\s(publickey|password|keyboard-interactive/pam)\\sfor ([^\\s]+)",1,SyslogMessage)| where isnotempty(c) | count 
    ```
    
    Wijzig het **tijds bereik** indien nodig en selecteer **uitvoeren**.
    
    Als het resulterende aantal nul is, bevestigt u de configuratie van de connector en controleert u of de bewaakte computers geslaagde aanmeldings activiteiten hebben voor de periode die u voor uw query hebt opgegeven.
    
    Als het resulterende aantal groter is dan nul, zijn uw syslog-gegevens geschikt voor afwijkende SSH-aanmeldings detectie. U schakelt deze detectie in op basis van **analyse**  >   **regel sjablonen**  >  **(preview) afwijkende SSH-aanmeldings detectie**.

## <a name="next-steps"></a>Volgende stappen
In dit document hebt u geleerd hoe u op on-premises syslog-apparaten verbindt met Azure Sentinel. Zie de volgende artikelen voor meer informatie over Azure Sentinel:
- Meer informatie over het [verkrijgen van inzicht in uw gegevens en mogelijke bedreigingen](quickstart-get-visibility.md).
- Ga aan de slag met [het detecteren van bedreigingen met Azure Sentinel](tutorial-detect-threats-built-in.md).
- [Gebruik werkmappen](tutorial-monitor-your-data.md) om uw gegevens te bewaken.

