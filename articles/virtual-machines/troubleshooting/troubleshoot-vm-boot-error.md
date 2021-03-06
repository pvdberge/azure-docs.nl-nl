---
title: Virtuele Linux-machine wordt opgestart naar grub-herstel
description: Het opstarten van de virtuele machine is mislukt omdat de virtuele machine een herstel console heeft opgegeven
services: virtual-machines-windows
documentationcenter: ''
author: v-miegge
manager: dcscontentpm
editor: ''
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: troubleshooting
ms.date: 08/28/2019
ms.author: tiag
ms.openlocfilehash: 5a2fd7fcfdae8559bfb39bffff7c73c7082a86aa
ms.sourcegitcommit: 8def3249f2c216d7b9d96b154eb096640221b6b9
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/03/2020
ms.locfileid: "87543279"
---
# <a name="linux-vm-boots-to-grub-rescue"></a>Virtuele Linux-machine wordt opgestart naar grub-herstel

We hebben vastgesteld dat uw virtuele machine (VM) een herstel console heeft ingevoerd. Het probleem treedt op wanneer de kernel-wijzigingen van uw Linux-VM recent zijn toegepast, zoals een kernel-upgrade, en die niet meer correct wordt gestart vanwege kernel-fouten tijdens het opstart proces. Wanneer de opstart lader tijdens het opstart proces probeert de Linux-kernel te vinden en de opstart besturing aan het systeem door te sturen, voert de virtuele machine een herstel console in wanneer het item is mislukt.

Als u merkt dat u in de toekomst geen verbinding kunt maken met een virtuele machine, ziet u een scherm opname van uw virtuele machine met behulp van de Blade diagnostische gegevens over opstarten in de Azure Portal. Dit kan helpen bij het vaststellen van de oorzaak van het probleem omdat u kunt bepalen of een vergelijkbare opstartfout mogelijk de oorzaak is.

## <a name="recommended-steps"></a>Aanbevolen stappen

Volg de onderstaande stappen, afhankelijk van de fout die u ontvangt:

### <a name="error---unknown-filesystem"></a>Fout-Onbekend bestands systeem

* Als u het fout bericht **Onbekend bestands**systeem krijgt, kan deze fout optreden als gevolg van een beschadigd bestandssysteem op de opstart partitie of een onjuiste kernel-configuratie.

   * Voor problemen met het bestands systeem volgt u de stappen in het artikel [Linux Recovery: kan geen SSH-naar-virtuele Linux-machine uitvoeren vanwege bestandssysteem fouten (fsck, inodes)](/archive/blogs/linuxonazure/linux-recovery-cannot-ssh-to-linux-vm-due-to-file-system-errors-fsck-inodes).
   * Volg voor kernel-problemen de stappen in het artikel [een virtuele machine van Azure Linux herstellen op basis van kernel-gerelateerde opstart problemen](https://support.microsoft.com/help/4091524/how-recover-azure-linux-vm-from-kernel-related-boot-related-issues)of [Linux-herstel: problemen oplossen die betrekking hebben op kernel-problemen met behulp van chroot](http://linuxonazure.azurewebsites.net/linux-recovery-fixing-non-boot-issues-related-to-kernel-problems-using-chroot/).
   
### <a name="error---file-not-found"></a>Fout: bestand niet gevonden

* Als de fout **15: bestand niet gevonden of eerste RAM-schijf** of **initrd/initramfs-bestand niet gevonden**is, volgt u de onderstaande stappen.

    * Voor het ontbrekende bestand `/boot/grub2/grub.cfg` of `initrd/initramfs` gaat u verder met het volgende proces:

    1. Zorg ervoor dat er `/etc/default/grub` bestaat en de juiste/gewenste instellingen heeft. Als u niet weet wat de standaard instellingen zijn, kunt u controleren met een werkende VM.

    2. Voer vervolgens de volgende opdracht uit om de configuratie opnieuw te genereren:`grub2-mkconfig -o /boot/grub2/grub.cfg`

   * Als het ontbrekende bestand is `/boot/grub/menu.lst` , is deze fout voor oudere versies van het besturings systeem (**RHEL 6. x**, **CentOS 6. x** en **Ubuntu 14,04**), zodat de opdrachten kunnen verschillen. U moet een oude server opzetten en testen om er zeker van te zijn dat de juiste opdrachten worden weer gegeven.

### <a name="error---no-such-partition"></a>Fout-er is geen partitie

* Als u het fout bericht **geen dergelijke partitie**krijgt, raadpleegt u scenario met de [fout melding ' geen dergelijke partitie ' tijdens het starten van de virtuele machine na een poging om het station van het besturings systeem uit te breiden](/archive/blogs/shwetanayak/case-scenario-no-such-partition-error-while-trying-to-start-the-vm-after-attempting-to-extend-the-os-drive).

### <a name="error---grubcfg-file-not-found"></a>Fout-grub. cfg-bestand niet gevonden

* Als het fout **/boot/grub2/grub.cfg bestand niet wordt gevonden**, volgt u de onderstaande stappen.

    * Voor het ontbrekende bestand `/boot/grub2/grub.cfg` of `initrd/initramfs` gaat u verder met het volgende proces:

    1. Zorg ervoor dat er `/etc/default/grub` bestaat en de juiste/gewenste instellingen heeft. Als u niet weet wat de standaard instellingen zijn, kunt u controleren met een werkende VM.

    2. Voer vervolgens de volgende opdracht uit om de configuratie opnieuw te genereren: `grub2-mkconfig -o /boot/grub2/grub.cfg` .

   * Als het ontbrekende bestand is `/boot/grub/menu.lst` , is deze fout voor oudere versies van het besturings systeem (**RHEL 6. x**, **CentOS 6. x** en **Ubuntu 14,04**), zodat de opdrachten kunnen worden uitgesteld. Geef een oude server op en test deze om te controleren of de juiste opdrachten worden gegeven.

## <a name="next-steps"></a>Volgende stappen

* [Overzicht van de agent voor virtuele Azure-machines](../extensions/agent-windows.md)
* [Extensies en functies van virtuele machines voor Windows](../extensions/features-windows.md)
