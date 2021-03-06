---
title: Een Azure-bestandsshare koppelen via SMB met macOS | Microsoft Docs
description: Meer informatie over het koppelen van een Azure-bestands share over SMB met macOS met Finder of Terminal. Azure Files  is het eenvoudig te gebruiken cloudbestandssysteem van Microsoft.
author: RenaShahMSFT
ms.service: storage
ms.topic: how-to
ms.date: 09/19/2017
ms.author: renash
ms.subservice: files
ms.openlocfilehash: 2cddf8a7d3dbc7abcc25fb76aba8a0af1790fe4d
ms.sourcegitcommit: bfeae16fa5db56c1ec1fe75e0597d8194522b396
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/10/2020
ms.locfileid: "88034444"
---
# <a name="mount-azure-file-share-over-smb-with-macos"></a>Een Azure-bestandsshare koppelen via SMB met macOS
[Azure Files ](storage-files-introduction.md) is het eenvoudig te gebruiken cloudbestandssysteem van Microsoft. Azure-bestandsshares kunnen aan het SMB 3-protocol (industrienorm) worden gekoppeld met macOS El Capitan 10.11+. Dit artikel behandelt twee verschillende manieren om een Azure-bestandsshare te koppelen op macOS: met de Finder-gebruikersinterface en met Terminal.

> [!Note]  
> We raden u aan om het tekenen van SMB-pakketten uit te schakelen voordat u een Azure-bestandsshare koppelt via SMB. Als u dit niet doet, zorgt dit mogelijk voor slechte prestaties bij het openen van de Azure-bestandsshare in macOS. De SMB-verbinding is versleuteld, dus dit heeft geen invloed op de beveiliging van de verbinding. Vanaf de terminal schakelen de volgende opdrachten het ondertekenen van SMB-pakketten uit, zoals beschreven door dit [ondersteuningsartikel van Apple over het uitschakelen van SMB-pakketondertekening](https://support.apple.com/HT205926):  
>    ```
>    sudo -s
>    echo "[default]" >> /etc/nsmb.conf
>    echo "signing_required=no" >> /etc/nsmb.conf
>    exit
>    ```

## <a name="prerequisites-for-mounting-an-azure-file-share-on-macos"></a>Vereisten voor het koppelen van een Azure-bestandsshare op macOS
* **Naam van opslag account**: als u een Azure-bestands share wilt koppelen, hebt u de naam van het opslag account nodig.

* **Sleutel van het opslag account**: voor het koppelen van een Azure-bestands share hebt u de primaire (of secundaire) opslag sleutel nodig. SAS-sleutels worden momenteel niet ondersteund voor koppelen.

* **Zorg ervoor dat poort 445 is geopend**: SMB communiceert via TCP-poort 445. Controleer op de clientcomputer (Mac) of uw firewall TCP-poort 445 niet blokkeert.

## <a name="mount-an-azure-file-share-via-finder"></a>Een Azure-bestandsshare koppelen via Finder
1. **Open Finder**: Finder is standaard geopend op Mac OS, maar u kunt controleren of het de geselecteerde toepassing is door te klikken op het 'gezichtspictogram van Mac OS' op de dock:  
    ![Het gezichtspictogram van Mac OS](./media/storage-how-to-use-files-mac/mount-via-finder-1.png)

2. **Selecteer ' verbinding maken met server ' in het menu ' go '**: gebruik het UNC-pad in de vereisten, converteer het begin dubbele back slash ( `\\` ) naar `smb://` en alle andere backslashes () `\` om schuine strepen () door te sturen `/` . De link moet er als volgt uitzien: ![het dialoogvenster 'Verbinden met server'](./media/storage-how-to-use-files-mac/mount-via-finder-2.png)

3. **Gebruik de naam en sleutel van het opslagaccount wanneer u wordt gevraagd om een gebruikersnaam en wachtwoord**: wanneer u klikt op 'Verbinden' in het dialoogvenster 'Verbinden met server', wordt u gevraagd om de gebruikersnaam en het wachtwoord (hier wordt uw macOS-gebruikersnaam automatisch ingevuld). U hebt de mogelijkheid om de naam/sleutel van het opslagaccount in uw macOS-sleutelhanger op te slaan.

4. **Gebruik de Azure-bestands share naar wens**: nadat u de share naam en de sleutel van het opslag account hebt vervangen door voor de gebruikers naam en het wacht woord, wordt de share gekoppeld. U kunt deze gebruiken zoals u een lokale map/bestandsshare zou gebruiken. Zo kunt u bestanden naar de bestandsshare slepen en neerzetten:

    ![Een momentopname van een gekoppelde Azure-bestandsshare](./media/storage-how-to-use-files-mac/mount-via-finder-3.png)

## <a name="mount-an-azure-file-share-via-terminal"></a>Een Azure-bestandsshare koppelen via Terminal
1. Vervang `<storage-account-name>` door de naam van uw opslagaccount. Geef de sleutel van het opslagaccount als wachtwoord wanneer hierom wordt gevraagd. 

    ```
    mount_smbfs //<storage-account-name>@<storage-account-name>.file.core.windows.net/<share-name> <desired-mount-point>
    ```

2. **Gebruik de Azure-bestands share naar wens**: de Azure-bestands share wordt gekoppeld op het koppel punt dat is opgegeven met de vorige opdracht.  

    ![Een momentopname van de gekoppelde Azure-bestandsshare](./media/storage-how-to-use-files-mac/mount-via-terminal-1.png)

## <a name="next-steps"></a>Volgende stappen
Raadpleeg de volgende koppelingen voor meer informatie over Azure Files.

* [Helpartikel van Apple: Verbinding maken met Bestandsdeling op een Mac](https://support.apple.com/HT204445)
* [Veelgestelde vragen](../storage-files-faq.md)
* [Problemen oplossen in Windows](storage-troubleshoot-windows-file-connection-problems.md)      
* [Problemen oplossen in Linux](storage-troubleshoot-linux-file-connection-problems.md)    
