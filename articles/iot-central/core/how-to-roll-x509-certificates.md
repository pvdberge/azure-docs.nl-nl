---
title: Roll X. 509-certificaten in azure IoT Central
description: Hoe kan ik X. 509-certificaten samen met uw IoT Central-toepassing
author: v-krghan
ms.author: v-krghan
ms.date: 07/31/2020
ms.topic: how-to
ms.service: iot-central
services: iot-central
ms.openlocfilehash: 76e2b9542d20b5788a2875dec89d447ce38276a0
ms.sourcegitcommit: b8702065338fc1ed81bfed082650b5b58234a702
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/11/2020
ms.locfileid: "88122020"
---
# <a name="how-to-roll-x509-device-certificates-in-iot-central-application"></a>Hoe kan ik X. 509-certificaat voor apparaten in IoT Central toepassing

Tijdens de levens cyclus van uw IoT-oplossing moet u certificaten totaliseren. Twee van de belangrijkste redenen voor Rolling certificaten zijn een schending van de beveiliging en het verlopen van certificaten. 

Rolling certificaten is een beveiligings best practice om uw systeem te helpen beveiligen in geval van een schending. Als onderdeel van een [overtredings methodologie](https://download.microsoft.com/download/C/1/9/C1990DBA-502F-4C2A-848D-392B93D9B9C3/Microsoft_Enterprise_Cloud_Red_Teaming.pdf)heeft micro soft de nood zaak voor het opnieuw activeren van beveiligings processen samen met preventieve maat regelen te nemen. Als onderdeel van deze beveiligings processen moet u de certificaten van het apparaat meenemen. De frequentie waarmee u uw certificaten inrollen, is afhankelijk van de beveiligings behoeften van uw oplossing. Klanten met oplossingen waarbij zeer gevoelige gegevens worden betrokken, kunnen dagelijks certificaten samen vouwen, terwijl anderen hun certificaten elk paar jaar draaien.


## <a name="obtain-new-x509-certificates"></a>Nieuwe X. 509-certificaten verkrijgen

U kunt uw eigen X. 509-certificaten maken met een hulp programma zoals OpenSSL. Deze aanpak is ideaal voor het testen van X. 509-certificaten, maar biedt een aantal garanties rond de beveiliging. Gebruik deze methode alleen voor test doeleinden, tenzij u bent voor bereid om te fungeren als uw eigen CA-provider.


## <a name="enrollment-groups-and-security-breaches"></a>Inschrijvings groepen en schending van beveiliging

Als u een groeps registratie wilt bijwerken in reactie op een schending van de beveiliging, moet u de volgende aanpak gebruiken waarmee het huidige certificaat direct wordt bijgewerkt:

1. Ga in het linkerdeel venster naar **beheer** en klik op **verbinding met apparaat**.

2. Klik op **registratie groepen**en klik op de groeps naam in de lijst.

    ![Apparaat-verbinding](./media/how-to-roll-x509-certificates/device-connection.png)


3. Klik voor certificaat update op **primair beheren** of **secundair beheren**.

    ![Certificaten beheren](./media/how-to-roll-x509-certificates/certificates.png)


4. Het certificaat root X. 509 toevoegen en verifiëren in de registratie groep.

   Voer deze stappen uit voor de primaire en secundaire certificaten als beide zijn aangetast.



## <a name="enrollment-groups-and-certificate-expiration"></a>Inschrijvings groepen en certificaat verlopen

Als u certificaten doorloopt voor het afhandelen van certificaat verloop, gebruikt u de volgende aanpak om het huidige certificaat direct bij te werken:

1. Ga in het linkerdeel venster naar **beheer** en klik op **verbinding met apparaat**. 

2. Klik op **registratie groepen**en klik op de groeps naam in de lijst.

    ![Apparaat-verbinding](./media/how-to-roll-x509-certificates/device-connection.png)


3. Klik voor certificaat update op **primair beheren**.

    ![Apparaat-verbinding](./media/how-to-roll-x509-certificates/manage-certs.png)

4. Het certificaat root X. 509 toevoegen en verifiëren in de registratie groep.

5. Later wanneer het secundaire certificaat is verlopen, keert u terug en werkt u het secundaire certificaat bij.



## <a name="individual-enrollments-and-security-breaches"></a>Individuele inschrijvingen en inbreuken op de beveiliging

Als u certificaten doorgeeft als reactie op een schending van de beveiliging, gebruikt u de volgende aanpak om het huidige certificaat direct bij te werken:


1. Klik op **apparaten**en selecteer het apparaat. 

2. Klik op **verbinden**en selecteer methode verbinden als **afzonderlijke registratie**

3. Selecteer **certificaten (X. 509)** als mechanisme.

    ![Afzonderlijke inschrijvingen beheren](./media/how-to-roll-x509-certificates/certificate-update.png)

4. Klik voor certificaat update op het mappictogram om het nieuwe certificaat te selecteren dat u voor de inschrijvings vermelding wilt uploaden. Klik op **Opslaan**.

    Voer deze stappen uit voor de primaire en secundaire certificaten als beide zijn aangetast



## <a name="individual-enrollments-and-certificate-expiration"></a>Individuele inschrijvingen en verlopen van certificaten

Als u certificaten laat verlopen voor het afhandelen van certificaat verloopt, moet u de configuratie van het secundaire certificaat als volgt gebruiken om de uitval tijd te verminderen voor apparaten die proberen in te richten.

Later wanneer het secundaire certificaat bijna is verlopen en moet worden gedistribueerd, kunt u met de primaire configuratie draaien. Als u de primaire en secundaire certificaten op deze manier draait, vermindert u de downtime voor apparaten die worden ingericht.

1. Klik op **apparaten**en selecteer het apparaat.

2. Klik op **verbinden**en selecteer methode verbinden als **afzonderlijke registratie**

3. Selecteer **certificaten (X. 509)** als mechanisme.

    ![Afzonderlijke inschrijvingen beheren](./media/how-to-roll-x509-certificates/certificate-update.png)

4. Voor een secundaire certificaat update klikt u op het mappictogram om het nieuwe certificaat te selecteren dat u voor de inschrijvings vermelding wilt uploaden. Klik op **Opslaan**.


5. Later wanneer het primaire certificaat is verlopen, keert u terug en werkt u dat primaire certificaat bij.


## <a name="next-steps"></a>Volgende stappen

Nu u hebt geleerd hoe u X. 509-certificaten in uw Azure IoT Central-toepassing kunt weer geven, hebt u [verbinding met Azure IOT Central](concepts-get-connected.md).


