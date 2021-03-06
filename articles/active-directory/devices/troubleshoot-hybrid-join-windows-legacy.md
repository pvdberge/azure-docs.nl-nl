---
title: Problemen met legacy Hybrid Azure Active Directory gekoppelde apparaten oplossen
description: Het oplossen van problemen met hybride Azure Active Directory gekoppelde apparaten op hetzelfde niveau.
services: active-directory
ms.service: active-directory
ms.subservice: devices
ms.topic: troubleshooting
ms.date: 11/21/2019
ms.author: joflore
author: MicrosoftGuyJFlo
manager: daveba
ms.reviewer: jairoc
ms.collection: M365-identity-device-management
ms.openlocfilehash: e168deea1ba442d48f483264c1e97ce618040f18
ms.sourcegitcommit: 877491bd46921c11dd478bd25fc718ceee2dcc08
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/02/2020
ms.locfileid: "74379108"
---
# <a name="troubleshooting-hybrid-azure-active-directory-joined-down-level-devices"></a>Problemen oplossen met hybride Azure Active Directory-gekoppelde, downlevel apparaten 

Dit artikel is alleen van toepassing op de volgende apparaten: 

- Windows 7 
- Windows 8.1 
- Windows Server 2008 R2 
- Windows Server 2012 
- Windows Server 2012 R2 

Zie [problemen met hybride Azure Active Directory voor Windows 10-en Windows server 2016-apparaten oplossen](troubleshoot-hybrid-join-windows-current.md)voor Windows 10 of windows server 2016.

In dit artikel wordt ervan uitgegaan dat u [hybride Azure Active Directory gekoppelde apparaten hebt geconfigureerd](hybrid-azuread-join-plan.md) om de volgende scenario's te ondersteunen:

- Voorwaardelijke toegang op basis van het apparaat

In dit artikel vindt u richt lijnen voor probleem oplossing voor het oplossen van potentiële problemen.  

**Wat u moet weten:** 

- Hybride Azure AD-deelname voor down level Windows-apparaten werkt iets anders dan in Windows 10. Veel klanten realiseren zich niet dat ze AD FS nodig hebben (voor federatieve domeinen) of naadloze SSO geconfigureerd (voor beheerde domeinen).
- Als het service aansluitpunt (SCP) zo is geconfigureerd dat deze verwijst naar de naam van het beheerde domein (bijvoorbeeld contoso.onmicrosoft.com in plaats van contoso.com), werkt de hybride Azure AD-deelname voor down level Windows-apparaten niet.
- Het maximum aantal apparaten per gebruiker is momenteel ook van toepassing op Down Level Hybrid Azure AD gekoppelde apparaten. 
- Hetzelfde fysieke apparaat wordt meerdere keren weer gegeven in azure AD wanneer meerdere domein gebruikers zich aanmelden bij de Down Level Hybrid Azure AD gekoppelde apparaten.  Als bijvoorbeeld *jdoe* -en *jharnett* -aanmelding bij een apparaat, wordt er een afzonderlijke registratie (DeviceID) gemaakt voor elk van deze op het tabblad **gebruikers** gegevens. 
- U kunt ook meerdere vermeldingen voor een apparaat vinden op het tabblad gebruikers gegevens, omdat het besturings systeem opnieuw wordt geïnstalleerd of hand matig opnieuw wordt geregistreerd.
- De eerste registratie/samen voeging van apparaten is geconfigureerd voor het uitvoeren van een poging bij het aanmelden of vergren delen/ontgrendelen. Er kan een vertraging van 5 minuten worden geactiveerd door een taak planner taak. 
- Zorg ervoor dat [KB4284842](https://support.microsoft.com/help/4284842) is geïnstalleerd in het geval van Windows 7 SP1 of windows server 2008 R2 SP1. Deze update voor komt toekomstige verificatie fouten als gevolg van het toegangs verlies van de klant tot beveiligde sleutels na het wijzigen van het wacht woord.

## <a name="step-1-retrieve-the-registration-status"></a>Stap 1: de registratie status ophalen 

**De registratie status verifiëren:**  

1. Meld u aan met het gebruikers account dat een hybride Azure AD-deelname heeft uitgevoerd.
1. Open de opdracht prompt 
1. Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe" /i`

Met deze opdracht wordt een dialoog venster weer gegeven met informatie over de status van de samen voeging.

![Workplace Join voor Windows](./media/troubleshoot-hybrid-join-windows-legacy/01.png)

## <a name="step-2-evaluate-the-hybrid-azure-ad-join-status"></a>Stap 2: de deelname status van de hybride Azure AD evalueren 

Als het apparaat niet aan hybride Azure AD is toegevoegd, kunt u proberen om hybride Azure AD join uit te voeren door te klikken op de knop toevoegen. Als de poging om hybride Azure AD-deelname uit te voeren mislukt, wordt de informatie over de fout weer gegeven.

**De meest voorkomende problemen zijn:**

- Een onjuist geconfigureerde AD FS-of Azure AD-of netwerk problemen

    ![Workplace Join voor Windows](./media/troubleshoot-hybrid-join-windows-legacy/02.png)
    
   - Autoworkplace.exe kan niet op de achtergrond worden geverifieerd met Azure AD of AD FS. Dit kan worden veroorzaakt door ontbrekende of onjuist geconfigureerde AD FS (voor federatieve domeinen) of ontbrekende of niet-geconfigureerde Azure AD-naadloze eenmalige aanmelding (voor beheerde domeinen) of netwerk problemen. 
   - Het kan zijn dat multi-factor Authentication (MFA) is ingeschakeld/geconfigureerd voor de gebruiker en WIAORMULTIAUTHN niet is geconfigureerd op de AD FS-server. 
   - Een andere mogelijkheid is dat de HRD-pagina (Home realm Discovery) wacht op gebruikers interactie, waarmee wordt voor komen dat **autoworkplace.exe** een token op de achtergrond aanvraagt.
   - Het kan zijn dat AD FS en Azure AD-Url's ontbreken in de intranet zone van Internet op de client.
   - Problemen met de netwerk verbinding kunnen verhinderen dat **autoworkplace.exe** AD FS of de Azure AD-url's bereikt. 
   - **Autoworkplace.exe** vereist dat de client rechtstreeks regel niveau van de client naar de on-premises AD-domein controller van de organisatie kan worden genoteerd. Dit betekent dat de deelname van de hybride Azure AD alleen lukt wanneer de client is verbonden met het intranet van de organisatie.
   - Uw organisatie maakt gebruik van de naadloze eenmalige aanmelding van Azure AD `https://autologon.microsoftazuread-sso.com` of is `https://aadg.windows.net.nsatc.net` niet aanwezig op de intranet instellingen van het apparaat, en het is niet **mogelijk om updates van de status balk via script in te** scha kelen voor de intranet zone.
- U bent niet aangemeld als een domein gebruiker

   ![Workplace Join voor Windows](./media/troubleshoot-hybrid-join-windows-legacy/03.png)

   Er zijn verschillende redenen waarom dit kan gebeuren:

   - De aangemelde gebruiker is geen domein gebruiker (bijvoorbeeld een lokale gebruiker). Hybride Azure AD-deelname op Down Level-apparaten wordt alleen ondersteund voor domein gebruikers.
   - De client kan geen verbinding maken met een domein controller.    
- Er is een quotum bereikt

    ![Workplace Join voor Windows](./media/troubleshoot-hybrid-join-windows-legacy/04.png)

- De service reageert niet 

    ![Workplace Join voor Windows](./media/troubleshoot-hybrid-join-windows-legacy/05.png)

U kunt de status informatie ook vinden in het gebeurtenis logboek onder: **toepassingen en services Log\Microsoft-Workplace toevoegen**
  
**De meest voorkomende oorzaken voor een mislukte hybride Azure AD-deelname zijn:** 

- Uw computer is niet verbonden met het interne netwerk van uw organisatie of een VPN met een verbinding met uw on-premises AD-domein controller.
- U bent aangemeld bij uw computer met een lokale computer account. 
- Problemen met de service configuratie: 
   - De AD FS-server is niet geconfigureerd voor de ondersteuning van **WIAORMULTIAUTHN**. 
   - Het forest van uw computer heeft geen object voor het service verbindings punt dat verwijst naar de naam van het geverifieerde domein in azure AD 
   - Of als uw domein wordt beheerd, is naadloze SSO niet geconfigureerd of werkt het niet.
   - Een gebruiker heeft de limiet van apparaten bereikt. 

## <a name="next-steps"></a>Volgende stappen

Zie [Veelgestelde vragen over Apparaatbeheer](faq.md) voor meer informatie.  
