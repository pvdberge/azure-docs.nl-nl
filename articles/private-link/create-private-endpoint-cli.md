---
title: Quickstart – Een Azure privé-eindpunt maken met behulp van de Azure CLI
description: Meer informatie over Azure-privé-eindpunt in deze Quickstart
services: private-link
author: malopMSFT
ms.service: private-link
ms.topic: quickstart
ms.date: 09/16/2019
ms.author: allensu
ms.custom: devx-track-azurecli
ms.openlocfilehash: e7c098ba06086781306960f76978aac9e4fa06bc
ms.sourcegitcommit: 11e2521679415f05d3d2c4c49858940677c57900
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/31/2020
ms.locfileid: "87502661"
---
# <a name="quickstart-create-a-private-endpoint-using-azure-cli"></a>Quickstart: Een privé-eindpunt maken met behulp van Azure CLI

Een privé-eindpunt is de fundamentele bouwsteen voor een Private Link in Azure. Het biedt Azure-resources, zoals virtuele machines, de mogelijkheid om Private Link-resources te gebruiken om privé met elkaar communiceren. In deze quickstart leert u hoe u een VM maakt in een virtueel netwerk, een server met een privé-eindpunt in SQL Database met behulp van Azure CLI. Vervolgens hebt u toegang tot de VM en kunt u veilig toegang krijgen tot de Private Link-resource (een privé server in SQL Database in dit voorbeeld).

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Als u ervoor kiest om Azure CLI lokaal te installeren en te gebruiken, moet u voor deze snelstart versie 2.0.28 of hoger van Azure CLI uitvoeren. Voer `az --version` uit om na te gaan welke versie er is geïnstalleerd. Zie [Azure CLI installeren](/cli/azure/install-azure-cli) voor installatie- of upgrade-informatie.

## <a name="create-a-resource-group"></a>Een resourcegroep maken

Voordat u een resource kunt maken, moet u een resourcegroep maken die het Virtual Network host. Maak een resourcegroep maken met [az group create](/cli/azure/group). Dit voorbeeld wordt een resourcegroep met de naam *myResourceGroup* gemaakt op de locatie *westcentralus*:

```azurecli-interactive
az group create --name myResourceGroup --location westcentralus
```

## <a name="create-a-virtual-network"></a>Een Virtual Network maken

Maak een Virtual Network met [az network vnet create](/cli/azure/network/vnet). In dit voorbeeld wordt een standaard Virtual Network gemaakt met de naam *myVirtualNetwork* met één subnet genaamd *mySubnet*:

```azurecli-interactive
az network vnet create \
 --name myVirtualNetwork \
 --resource-group myResourceGroup \
 --subnet-name mySubnet
```

## <a name="disable-subnet-private-endpoint-policies"></a>Beleid voor privé-eindpunten van subnet uitschakelen

Azure implementeert resources in een subnet binnen een virtueel netwerk, dus moet u het subnet maken of bijwerken om beleid voor privé-eindpunt netwerk uit te schakelen. Update een subnet-configuratie met de naam *mySubnet* met [az network vnet subnet update](https://docs.microsoft.com/cli/azure/network/vnet/subnet?view=azure-cli-latest#az-network-vnet-subnet-update):

```azurecli-interactive
az network vnet subnet update \
 --name mySubnet \
 --resource-group myResourceGroup \
 --vnet-name myVirtualNetwork \
 --disable-private-endpoint-network-policies true
```

## <a name="create-the-vm"></a>De virtuele machine maken

Maak een VM met az vm create. Wanneer u hierom wordt gevraagd, geeft u een wachtwoord op dat moet worden gebruikt als de aanmeldingsreferenties voor de VM. In het volgende voorbeeld wordt een VM gemaakt met de naam *myVm*:

```azurecli-interactive
az vm create \
  --resource-group myResourceGroup \
  --name myVm \
  --image Win2019Datacenter
```

Het openbare IP-adres van de virtuele machine van VM noteren. U gebruikt dit adres om in de volgende stap verbinding te maken met de virtuele machine via internet.

## <a name="create-a-server-in-sql-database"></a>Een server maken in de SQL Database

Maak een server met de opdracht az sql server create in de SQL Database. Houd er rekening mee dat de naam van uw server uniek moet zijn in Azure, dus vervang de tijdelijke aanduiding tussen vierkante haken door uw eigen unieke waarde:

```azurecli-interactive
# Create a server in the resource group
az sql server create \
    --name "myserver"\
    --resource-group myResourceGroup \
    --location WestUS \
    --admin-user "sqladmin" \
    --admin-password "CHANGE_PASSWORD_1"

# Create a database in the server with zone redundancy as false
az sql db create \
    --resource-group myResourceGroup  \
    --server myserver \
    --name mySampleDatabase \
    --sample-name AdventureWorksLT \
    --edition GeneralPurpose \
    --family Gen4 \
    --capacity 1
```

De server-id is vergelijkbaar met ```/subscriptions/subscriptionId/resourceGroups/myResourceGroup/providers/Microsoft.Sql/servers/myserver.``` U gebruikt de server-id in de volgende stap.

## <a name="create-the-private-endpoint"></a>Privé-eindpunt maken

Maak een privé-eindpunt voor de logische SQL Server in uw Virtual Network:

```azurecli-interactive
az network private-endpoint create \  
    --name myPrivateEndpoint \  
    --resource-group myResourceGroup \  
    --vnet-name myVirtualNetwork  \  
    --subnet mySubnet \  
    --private-connection-resource-id "<server ID>" \  
    --group-ids sqlServer \  
    --connection-name myConnection  
 ```

## <a name="configure-the-private-dns-zone"></a>Privé-DNS-zone configureren

Maak een Privé-DNS-zone voor SQL Database-domein, maak een koppelingslink met het Virtual Network en maak een DNS-zonegroep om het privé-eindpunt aan de Privé-DNS-zone te koppelen. 

```azurecli-interactive
az network private-dns zone create --resource-group myResourceGroup \
   --name  "privatelink.database.windows.net"
az network private-dns link vnet create --resource-group myResourceGroup \
   --zone-name  "privatelink.database.windows.net"\
   --name MyDNSLink \
   --virtual-network myVirtualNetwork \
   --registration-enabled false
az network private-endpoint dns-zone-group create \
   --resource-group myResourceGroup \
   --endpoint-name myPrivateEndpoint \
   --name MyZoneGroup \
   --private-dns-zone "privatelink.database.windows.net" \
   --zone-name sql
```

## <a name="connect-to-a-vm-from-the-internet"></a>Verbinding maken met een virtuele machine via internet

Maak als volgt verbinding met de VM *myVm* van Internet:

1. Voer in de zoekbalk van de portal *myVm* in.

1. Selecteer de knop **Verbinding maken**. Na het selecteren van de knop **Verbinden** wordt **Verbinden met virtuele machine** geopend.

1. Selecteer **RDP-bestand downloaden**. In Azure wordt een *RDP*-bestand (Remote Desktop Protocol) gemaakt en het bestand wordt gedownload naar de computer.

1. Open het downloaded.rdp*-bestand.

    1. Selecteer **Verbinding maken** wanneer hierom wordt gevraagd.

    1. Voer de gebruikersnaam en het wachtwoord in die u hebt opgegeven bij het maken van de virtuele machine.

        > [!NOTE]
        > Mogelijk moet u **Meer opties** > **Een ander account gebruiken** selecteren om de referenties op te geven die u hebt ingevoerd tijdens het maken van de VM.

1. Selecteer **OK**.

1. Er wordt mogelijk een certificaatwaarschuwing weergegeven tijdens het aanmelden. Als er een certificaatwaarschuwing wordt weergegeven, selecteert u **Ja** of **Doorgaan**.

1. Wanneer het VM-bureaublad wordt weergegeven, minimaliseert u het om terug te gaan naar het lokale bureaublad.  

## <a name="access-sql-database-privately-from-the-vm"></a>Privé-toegang tot SQL Database vanuit de VM

In deze sectie maakt u verbinding met de SQL Database van de VM met behulp van het privé-eindpunt.

1. Open PowerShell in het extern bureaublad van *myVM*.
2. Voer nslookupmyserver.database.windows.net in

   U ontvangt een bericht dat er ongeveer als volgt uitziet:

    ```
    Server:  UnKnown
    Address:  168.63.129.16
    Non-authoritative answer:
    Name:    myserver.privatelink.database.windows.net
    Address:  10.0.0.5
    Aliases:  myserver.database.windows.net
    ```

3. Installeer SQL Server Management Studio
4. Typ of selecteer in Verbinding maken met server de volgende gegevens:

   - Servertype: Selecteer Database Engine.
   - Servernaam: Selecteer myserver.database.windows.net
   - Gebruikersnaam: Voer een gebruikersnaam in die tijdens het maken is opgegeven.
   - Wachtwoord: Voer een wachtwoord in dat tijdens het maken is opgegeven.
   - Wachtwoord onthouden: Selecteer Ja.

5. Selecteer **Verbinden**.
6. Blader in het menu aan de linkerkant door **Databases**.
7. (Optioneel) U kunt *mydatabase* maken of er een query op uitvoeren
8. Sluit de externe bureaubladverbinding met *myVm*.

## <a name="clean-up-resources"></a>Resources opschonen

U kunt az group delete gebruiken om de resourcegroep en alle resources die deze bevat te verwijderen, als deze niet meer nodig zijn:

```azurecli-interactive
az group delete --name myResourceGroup --yes
```

## <a name="next-steps"></a>Volgende stappen

Meer informatie over [Azure Private Link](private-link-overview.md)
