---
title: Azure IoT Edge installeren in Linux | Microsoft Docs
description: Installatie-instructies Azure IoT Edge op Linux-apparaten met Ubuntu of Raspbian
author: kgremban
manager: philmea
ms.reviewer: veyalla
ms.service: iot-edge
services: iot-edge
ms.topic: conceptual
ms.date: 09/04/2020
ms.author: kgremban
ms.openlocfilehash: 21fde76dc5791030a7afa280e00642119cbe464c
ms.sourcegitcommit: f8d2ae6f91be1ab0bc91ee45c379811905185d07
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/10/2020
ms.locfileid: "89660032"
---
# <a name="install-the-azure-iot-edge-runtime-on-debian-based-linux-systems"></a>De Azure IoT Edge-runtime op op Debian gebaseerde Linux-systemen installeren

Met de Azure IoT Edge runtime wordt een apparaat omgezet in een IoT Edge apparaat. De runtime kan worden geïmplementeerd op apparaten als een Raspberry Pi of zo groot als een industriële server. Zodra een apparaat is geconfigureerd met de IoT Edge-runtime, kunt u beginnen met het implementeren van bedrijfslogica vanuit de cloud. Zie [inzicht krijgen in de Azure IOT Edge runtime en de bijbehorende architectuur](iot-edge-runtime.md)voor meer informatie.

Dit artikel bevat de stappen voor het installeren van de Azure IoT Edge runtime op een x64-, ARM32-of ARM64 Linux-apparaat. We bieden installatie pakketten voor Ubuntu Server 16,04, Ubuntu Server 18,04 en Raspbian stretch. Raadpleeg [Azure IOT Edge ondersteunde systemen](support.md#operating-systems) voor een lijst met ondersteunde Linux-besturings systemen en architecturen.

> [!NOTE]
> Pakketten in de Linux-software opslagplaatsen zijn onderworpen aan de licentie voorwaarden in elk pakket (/usr/share/doc/*package name*). Lees de licentie voorwaarden voordat u het pakket gebruikt. Uw installatie en het gebruik van het pakket zijn uw acceptatie van deze voor waarden. Als u niet akkoord gaat met de licentie voorwaarden, mag u het pakket niet gebruiken.

## <a name="install-container-runtime-and-iot-edge"></a>Container runtime en IoT Edge installeren

Gebruik de volgende secties om de meest recente versie van de Azure IoT Edge-runtime op uw apparaat te installeren.

>[!NOTE]
>Ondersteuning voor ARM64-apparaten is beschikbaar in de [open bare preview](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

### <a name="register-microsoft-key-and-software-repository-feed"></a>Feed voor micro soft-sleutel en software opslagplaats registreren

Bereid uw apparaat voor op de installatie van IoT Edge runtime.

Installeer de configuratie van de opslag plaats. Kies de **16,04** -of **18,04** -opdracht die overeenkomt met het besturings systeem van uw apparaat:

* **Ubuntu-Server 16,04**:

   ```bash
   curl https://packages.microsoft.com/config/ubuntu/16.04/multiarch/prod.list > ./microsoft-prod.list
   ```

* **Ubuntu-Server 18,04**:

   ```bash
   curl https://packages.microsoft.com/config/ubuntu/18.04/multiarch/prod.list > ./microsoft-prod.list
   ```

* **Raspbian stretch**:

   ```bash
   curl https://packages.microsoft.com/config/debian/stretch/multiarch/prod.list > ./microsoft-prod.list
   ```

Kopieer de gegenereerde lijst.

   ```bash
   sudo cp ./microsoft-prod.list /etc/apt/sources.list.d/
   ```

Installeer de open bare sleutel van micro soft GPG.

   ```bash
   curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
   sudo cp ./microsoft.gpg /etc/apt/trusted.gpg.d/
   ```

### <a name="install-a-container-runtime"></a>Een container-runtime installeren

Azure IoT Edge is afhankelijk van een [met OCI compatibele](https://www.opencontainers.org/) container runtime. Voor productie scenario's wordt u aangeraden de [op Moby gebaseerde](https://mobyproject.org/) engine te gebruiken die hieronder wordt beschreven. De Moby-engine is de enige container engine die officieel wordt ondersteund met Azure IoT Edge. Docker CE/EE container installatie kopieën zijn compatibel met de Moby-runtime.

Pakket lijsten bijwerken op het apparaat.

   ```bash
   sudo apt-get update
   ```

Installeer de Moby-engine.

   ```bash
   sudo apt-get install moby-engine
   ```

Installeer de Moby-opdracht regel interface (CLI). De CLI is handig voor ontwikkeling, maar is optioneel voor productie-implementaties.

   ```bash
   sudo apt-get install moby-cli
   ```

Als er fouten optreden bij het installeren van de Moby-container runtime, volgt u de stappen om [uw Linux-kernel te controleren op Moby-compatibiliteit](#verify-your-linux-kernel-for-moby-compatibility), zoals verderop in dit artikel wordt beschreven.

### <a name="install-the-azure-iot-edge-security-daemon"></a>Installeer de Azure IoT Edge Security daemon

De **IOT Edge Security daemon** biedt en onderhoudt beveiligings standaarden op het IOT edge apparaat. De daemon begint op elke keer dat de computer wordt opgestart en Boots trapt het apparaat door de rest van de IoT Edge runtime te starten.

Pakket lijsten bijwerken op het apparaat.

   ```bash
   sudo apt-get update
   ```

Controleer welke versies van IoT Edge beschikbaar zijn.

   ```bash
   apt list -a iotedge
   ```

Als u de meest recente versie van de beveiligings-daemon wilt installeren, gebruikt u de volgende opdracht waarmee ook de meest recente versie van het **libiothsm-STD-** pakket wordt geïnstalleerd:

   ```bash
   sudo apt-get install iotedge
   ```

Als u een specifieke versie van de beveiligings-daemon wilt installeren, geeft u de versie op uit de uitvoer van de apt-lijst. U kunt ook dezelfde versie opgeven voor het **libiothsm-STD-** pakket, waarbij anders de meest recente versie wordt geïnstalleerd. Met de volgende opdracht wordt bijvoorbeeld de meest recente versie van de 1.0.8-release geïnstalleerd:

   ```bash
   sudo apt-get install iotedge=1.0.8* libiothsm-std=1.0.8*
   ```

Als de versie die u wilt installeren niet wordt weer gegeven, volgt u de stappen in [runtime installeren met behulp van release-assets](#install-runtime-using-release-assets). In deze sectie wordt beschreven hoe u een eerdere versie van de IoT Edge Security daemon of versie van de Candi date kunt richten.

Zodra IoT Edge met succes is geïnstalleerd `/etc/iotedge/` , wordt u door de uitvoer gevraagd het configuratie bestand bij te werken. Ga door naar de volgende sectie voor het volt ooien van de inrichting van het apparaat.

## <a name="configure-the-security-daemon"></a>De beveiligings-daemon configureren

Configureer de IoT Edge runtime om uw fysieke apparaat te koppelen aan een apparaat-id die bestaat in een Azure IoT-hub.

De daemon kan worden geconfigureerd met behulp van het configuratie bestand op `/etc/iotedge/config.yaml` . Het bestand is standaard beveiligd tegen schrijven. mogelijk hebt u verhoogde machtigingen nodig om het te bewerken.

Eén IoT Edge apparaat kan hand matig worden ingericht met behulp van een apparaat verbindings reeks die is geleverd door IoT Hub. U kunt ook de Device Provisioning Service gebruiken om apparaten automatisch in te richten. Dit is handig wanneer u veel apparaten moet inrichten. Afhankelijk van uw inrichtings keuze, kiest u het juiste installatie script.

### <a name="option-1-manual-provisioning"></a>Optie 1: hand matig inrichten

Als u een apparaat hand matig wilt inrichten, moet u het voorzien van een [apparaat Connection String](how-to-register-device.md#register-in-the-azure-portal) dat u kunt maken door een nieuw apparaat te registreren in uw IOT-hub.

Open het configuratie bestand.

```bash
sudo nano /etc/iotedge/config.yaml
```

Zoek de inrichtings configuraties van het bestand en verwijder de sectie **hand matige inrichtings configuratie** . Werk de waarde van **device_connection_string** met de Connection String van uw IOT edge-apparaat bij. Zorg ervoor dat alle andere inrichtings secties van commentaar zijn. Zorg ervoor dat het **inrichten:** de regel heeft geen voorafgaande spatie en dat geneste items met twee spaties worden inge sprongen.

```yml
# Manual provisioning configuration
provisioning:
  source: "manual"
  device_connection_string: "<ADD DEVICE CONNECTION STRING HERE>"
```

De inhoud van het klem bord plakken in nano `Shift+Right Click` of Press `Shift+Insert` .

Sla het bestand op en sluit het.

   `CTRL + X`, `Y`, `Enter`

Nadat u de inrichtings gegevens in het configuratie bestand hebt ingevoerd, start u de daemon opnieuw op:

```bash
sudo systemctl restart iotedge
```

### <a name="option-2-automatic-provisioning"></a>Optie 2: automatisch inrichten

IoT Edge apparaten kunnen automatisch worden ingericht met behulp van de [Azure IOT hub Device Provisioning Service (DPS)](../iot-dps/index.yml). IoT Edge ondersteunt momenteel drie Attestation-mechanismen bij het gebruik van automatische inrichting, maar uw hardware-vereisten kunnen van invloed zijn op uw keuzes. Zo worden Raspberry Pi-apparaten standaard niet geleverd met een Trusted Platform Module TPM-chip. Raadpleeg voor meer informatie de volgende artikelen:

* [Een IoT Edge apparaat maken en inrichten met een virtuele TPM op een Linux-VM](how-to-auto-provision-simulated-device-linux.md)
* [Een IoT Edge apparaat maken en inrichten met X. 509-certificaten](how-to-auto-provision-x509-certs.md)
* [Een IoT Edge apparaat maken en inrichten met behulp van symmetrische sleutel attest](how-to-auto-provision-symmetric-keys.md)

Deze artikelen begeleiden u bij het instellen van inschrijvingen in DPS en het genereren van de juiste certificaten of sleutels voor Attestation. Ongeacht het Attestation-mechanisme dat u kiest, wordt de inrichtings informatie toegevoegd aan het IoT Edge configuratie bestand op uw IoT Edge-apparaat.

Open het configuratie bestand.

```bash
sudo nano /etc/iotedge/config.yaml
```

Zoek de inrichtings configuraties van het bestand en verwijder de sectie die geschikt is voor uw Attestation-mechanisme. Zorg ervoor dat alle andere inrichtings secties van commentaar zijn. De **inrichting:** regel mag geen voor gaande witruimte hebben en geneste items moeten worden inge sprongen met twee spaties. Werk de waarde van **scope_id** bij met de waarde van uw IOT hub Device Provisioning Service instantie en geef de juiste waarden op voor de Attestation-velden.

TPM-Attestation:

```yml
# DPS TPM provisioning configuration
provisioning:
  source: "dps"
  global_endpoint: "https://global.azure-devices-provisioning.net"
  scope_id: "<SCOPE_ID>"
  attestation:
    method: "tpm"
    registration_id: "<REGISTRATION_ID>"
```

X. 509-Attestation:

```yml
# DPS X.509 provisioning configuration
provisioning:
  source: "dps"
  global_endpoint: "https://global.azure-devices-provisioning.net"
  scope_id: "<SCOPE_ID>"
  attestation:
    method: "x509"
#   registration_id: "<OPTIONAL REGISTRATION ID. LEAVE COMMENTED OUT TO REGISTER WITH CN OF identity_cert>"
    identity_cert: "<REQUIRED URI TO DEVICE IDENTITY CERTIFICATE>"
    identity_pk: "<REQUIRED URI TO DEVICE IDENTITY PRIVATE KEY>"
```

Attestation van symmetrische sleutels:

```yml
# DPS symmetric key provisioning configuration
provisioning:
  source: "dps"
  global_endpoint: "https://global.azure-devices-provisioning.net"
  scope_id: "<SCOPE_ID>"
  attestation:
    method: "symmetric_key"
    registration_id: "<REGISTRATION_ID>"
    symmetric_key: "<SYMMETRIC_KEY>"
```

De inhoud van het klem bord plakken in nano `Shift+Right Click` of Press `Shift+Insert` .

Sla het bestand op en sluit het. `CTRL + X`, `Y`, `Enter`

Nadat u de inrichtings gegevens in het configuratie bestand hebt ingevoerd, start u de daemon opnieuw op:

```bash
sudo systemctl restart iotedge
```

## <a name="verify-successful-installation"></a>Geslaagde installatie controleren

Als u de **hand matige configuratie** stappen in de vorige sectie hebt gebruikt, moet de IOT Edge runtime worden ingericht en op het apparaat worden uitgevoerd. Als u de stappen voor **automatische configuratie** hebt gebruikt, moet u extra stappen uitvoeren, zodat de runtime uw apparaat kan registreren bij uw IOT-hub namens u. Zie voor de volgende stappen [een gesimuleerde TPM maken en inrichten IOT edge apparaat op een virtuele Linux-machine](how-to-auto-provision-simulated-device-linux.md#give-iot-edge-access-to-the-tpm).

U kunt de status van de IoT Edge-daemon controleren:

```bash
systemctl status iotedge
```

Daemon-logboeken onderzoeken:

```bash
journalctl -u iotedge --no-pager --no-full
```

Voer het [hulp programma voor probleem oplossing](troubleshoot.md#run-the-check-command) uit om te controleren op de meest voorkomende configuratie-en netwerk fouten:

```bash
sudo iotedge check
```

De **$edgeHub** systeem module wordt niet geïmplementeerd op het apparaat totdat u uw eerste module implementeert voor IOT Edge op het apparaat. Als gevolg hiervan geeft de geautomatiseerde controle een fout melding voor de `Edge Hub can bind to ports on host` connectiviteits controle. Deze fout kan worden genegeerd, tenzij deze optreedt nadat een module op het apparaat is geïmplementeerd.

Ten slotte lijst met actieve modules:

```bash
sudo iotedge list
```

Na de installatie van IoT Edge op het apparaat, is de enige module die u moet zien, **edgeAgent**. Wanneer u uw eerste implementatie hebt gemaakt, wordt de andere systeem module **$edgeHub** ook gestart op het apparaat. Zie [IOT Edge-modules implementeren](how-to-deploy-modules-portal.md)voor meer informatie.

## <a name="tips-and-troubleshooting"></a>Tips en problemen oplossen

U hebt verhoogde bevoegdheden nodig om `iotedge`-opdrachten uit te voeren. Nadat u de runtime hebt geïnstalleerd, meldt u zich af bij uw computer en meldt u zich weer aan om uw machtigingen automatisch bij te werken. Tot slot gebruikt u **sudo** vóór alle `iotedge` opdrachten.

Op apparaten die zijn beperkt, wordt het ten zeerste aanbevolen om de *OptimizeForPerformance* -omgevings variabele in te stellen op *False* volgens instructies in de [hand leiding](troubleshoot.md)voor het oplossen van problemen.

Als uw apparaat geen verbinding kan maken met IoT Hub en uw netwerk een proxy server heeft, volgt u de stappen in [uw IOT edge-apparaat configureren om te communiceren via een proxy server](how-to-configure-proxy-support.md).

### <a name="verify-your-linux-kernel-for-moby-compatibility"></a>De Linux-kernel voor Moby-compatibiliteit controleren

Veel fabrikanten van Inge sloten apparaten verzenden installatie kopieën van apparaten die aangepaste Linux-kernels bevatten zonder de functies die vereist zijn voor compatibiliteit met container-runtime. Als u problemen ondervindt tijdens het installeren van de aanbevolen Moby-container runtime, kunt u mogelijk problemen met de configuratie van de Linux-kernel oplossen met behulp van het [controle-configuratie](https://raw.githubusercontent.com/moby/moby/master/contrib/check-config.sh) script van de officiële [Moby github-opslag plaats](https://github.com/moby/moby). Voer de volgende opdrachten uit op het apparaat om de configuratie van de kernel te controleren:

   ```bash
   curl -sSL https://raw.githubusercontent.com/moby/moby/master/contrib/check-config.sh -o check-config.sh
   chmod +x check-config.sh
   ./check-config.sh
   ```

Met deze opdracht geeft u een gedetailleerde uitvoer weer die de status bevat van de kernel-functies die worden gebruikt door de Moby-runtime. U moet ervoor zorgen dat alle items onder `Generally Necessary` en  `Network Drivers` worden ingeschakeld om ervoor te zorgen dat uw kernel volledig compatibel is met de Moby-runtime.  Als u ontbrekende onderdelen hebt geïdentificeerd, schakelt u deze in door de kernel opnieuw te bouwen op basis van de bron en de bijbehorende modules te selecteren voor opname in de juiste kernel. config.  En als u een configuratie Generator van een kernel gebruikt `defconfig` , zoals of, kunt u `menuconfig` de betreffende functies zoeken en inschakelen en de kernel opnieuw samen stellen.  Nadat u de zojuist gewijzigde kernel hebt geïmplementeerd, voert u het script check-config opnieuw uit om te controleren of alle vereiste onderdelen zijn ingeschakeld.

## <a name="install-runtime-using-release-assets"></a>Runtime installeren met behulp van release-assets

Volg de stappen in deze sectie als u een specifieke versie van de Azure IoT Edge runtime wilt installeren die niet beschikbaar is via `apt-get install` . De lijst met micro soft-pakketten bevat alleen een beperkt aantal recente versies en de bijbehorende subversies. deze stappen zijn dus voor iedereen die een oudere versie of versie van een release Candi date wil installeren.

Met behulp van krul opdrachten kunt u de onderdeel bestanden rechtstreeks vanuit de IoT Edge GitHub-opslag plaats richten. Gebruik de volgende stappen om libiothsm en de IoT Edge Security daemon te installeren.

1. Laat uw apparaat voor bereid zijn op de installatie van een container engine. Als u geen container engine hebt, volgt u de stappen voor het registreren van de micro soft-opslag plaats en het installeren van Moby in de sectie [installatie container runtime en IOT Edge](#install-container-runtime-and-iot-edge) in dit artikel.

2. Ga naar de [Azure IOT Edge releases](https://github.com/Azure/azure-iotedge/releases)en zoek de release versie die u wilt richten.

3. Vouw de sectie **assets** uit voor die versie.

4. Elke release moet nieuwe bestanden hebben voor de IoT Edge Security daemon en de hsmlib. Gebruik de volgende opdrachten om deze onderdelen bij te werken.

   1. Zoek het bestand **libiothsm-STD** dat overeenkomt met de architectuur van uw IOT edge-apparaat. Klik met de rechter muisknop op de bestands koppeling en kopieer het koppelings adres.

   2. Gebruik de gekopieerde koppeling in de volgende opdracht om die versie van de hsmlib te installeren:

      ```bash
      curl -L <libiothsm-std link> -o libiothsm-std.deb && sudo dpkg -i ./libiothsm-std.deb
      ```

   3. Zoek het **iotedge** -bestand dat overeenkomt met de architectuur van uw IOT edge-apparaat. Klik met de rechter muisknop op de bestands koppeling en kopieer het koppelings adres.

   4. Gebruik de gekopieerde koppeling in de volgende opdracht om die versie van de IoT Edge Security daemon te installeren.

      ```bash
      curl -L <iotedge link> -o iotedge.deb && sudo dpkg -i ./iotedge.deb
      ```

Zodra IoT Edge met succes is geïnstalleerd `/etc/iotedge` , wordt u door de uitvoer gevraagd het configuratie bestand bij te werken. Volg de stappen in de sectie [de Security daemon configureren voor het](#configure-the-security-daemon) volt ooien van de inrichting van het apparaat.

## <a name="uninstall-iot-edge"></a>IoT Edge verwijderen

Als u de IoT Edge-installatie van uw Linux-apparaat wilt verwijderen, gebruikt u de volgende opdrachten vanaf de opdracht regel.

De IoT Edge-runtime verwijderen.

```bash
sudo apt-get remove --purge iotedge
```

Wanneer de IoT Edge runtime wordt verwijderd, worden de gemaakte containers gestopt, maar nog steeds aanwezig op het apparaat. Bekijk alle containers om te zien welke er aanwezig zijn.

```bash
sudo docker ps -a
```

Verwijder de containers van het apparaat, met inbegrip van de twee runtime-containers.

```bash
sudo docker rm -f <container name>
```

Ten slotte verwijdert u de container runtime van het apparaat.

```bash
sudo apt-get remove --purge moby-cli
sudo apt-get remove --purge moby-engine
```

## <a name="next-steps"></a>Volgende stappen

Nu u een IoT Edge apparaat hebt ingericht terwijl de runtime is geïnstalleerd, kunt u [IOT Edge modules implementeren](how-to-deploy-modules-portal.md).

Raadpleeg de pagina [probleem oplossing](troubleshoot.md) als u problemen ondervindt met het installeren van IOT Edge runtime.

Zie [de IOT Edge Security daemon en runtime bijwerken](how-to-update-iot-edge.md)als u een bestaande installatie wilt bijwerken naar de nieuwste versie van IOT Edge.
