---
title: Server opnieuw starten-Azure PowerShell-Azure Database for PostgreSQL
description: In dit artikel wordt beschreven hoe u een Azure Database for PostgreSQL server opnieuw kunt opstarten met behulp van Power shell.
author: rachel-msft
ms.author: raagyema
ms.service: postgresql
ms.topic: how-to
ms.date: 06/08/2020
ms.custom: devx-track-azurepowershell
ms.openlocfilehash: 3fd4bcdd2f80bfd5f79488e7e4c93219be97927c
ms.sourcegitcommit: 11e2521679415f05d3d2c4c49858940677c57900
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/31/2020
ms.locfileid: "87503545"
---
# <a name="restart-azure-database-for-postgresql-server-using-powershell"></a>Azure Database for PostgreSQL server opnieuw opstarten met Power shell

In dit onderwerp wordt beschreven hoe u een Azure Database for PostgreSQL server opnieuw kunt starten. Mogelijk moet u de server opnieuw opstarten om onderhouds redenen te zorgen, waardoor tijdens de bewerking een korte onderbreking optreedt.

Het opnieuw opstarten van de server wordt geblokkeerd als de service bezet is. De service kan bijvoorbeeld een eerder aangevraagde bewerking verwerken, zoals het schalen van vCores.

De hoeveelheid tijd die nodig is voor het volt ooien van een herstart is afhankelijk van het PostgreSQL-herstel proces. Om de herstarttijd te beperken, raden we u aan om de hoeveelheid activiteit die op de server plaatsvindt, te minimaliseren voordat de computer opnieuw wordt opgestart.

## <a name="prerequisites"></a>Vereisten

U hebt het volgende nodig om deze hand leiding te volt ooien:

- De [AZ Power shell-module](https://docs.microsoft.com/powershell/azure/install-az-ps) die lokaal is geïnstalleerd of [Azure Cloud shell](https://shell.azure.com/) in de browser
- Een [Azure database for postgresql server](quickstart-create-postgresql-server-database-using-azure-powershell.md)

> [!IMPORTANT]
> Hoewel de Az.PostgreSql PowerShell-module in preview is, moet u deze afzonderlijk van de Az PowerShell-module installeren met behulp van de volgende opdracht: `Install-Module -Name Az.PostgreSql -AllowPrerelease`.
> Zodra de Az.PostgreSql PowerShell-module algemeen beschikbaar is, wordt deze onderdeel van toekomstige releases van Az PowerShell-modules en is de module systeemeigen beschikbaar vanuit Azure Cloud Shell.

Als u Power shell lokaal wilt gebruiken, maakt u verbinding met uw Azure-account met behulp van de cmdlet [Connect-AzAccount](https://docs.microsoft.com/powershell/module/az.accounts/connect-azaccount) .

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="restart-the-server"></a>Start de server opnieuw

Start de server opnieuw op met de volgende opdracht:

```azurepowershell-interactive
Restart-AzPostgreSqlServer -Name mydemoserver -ResourceGroupName myresourcegroup
```

## <a name="next-steps"></a>Volgende stappen

> [!div class="nextstepaction"]
> [Een Azure Database for PostgreSQL-server maken met behulp van Power shell](quickstart-create-postgresql-server-database-using-azure-powershell.md)
