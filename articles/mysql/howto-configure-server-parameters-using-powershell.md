---
title: Server parameters configureren-Azure PowerShell-Azure Database for MySQL
description: In dit artikel wordt beschreven hoe u de service parameters in Azure Database for MySQL kunt configureren met behulp van Power shell.
author: ajlam
ms.author: andrela
ms.service: mysql
ms.devlang: azurepowershell
ms.topic: how-to
ms.date: 4/29/2020
ms.custom: devx-track-azurepowershell
ms.openlocfilehash: cb17c8631392972c429220b846720447be48cecf
ms.sourcegitcommit: 11e2521679415f05d3d2c4c49858940677c57900
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/31/2020
ms.locfileid: "87495808"
---
# <a name="configure-server-parameters-in-azure-database-for-mysql-using-powershell"></a>Server parameters configureren in Azure Database for MySQL met behulp van Power shell

U kunt configuratie parameters voor een Azure Database for MySQL server weer geven, tonen en bijwerken met behulp van Power shell. Een subset van de engine configuraties wordt weer gegeven op server niveau en kan worden gewijzigd.

## <a name="prerequisites"></a>Vereisten

U hebt het volgende nodig om deze hand leiding te volt ooien:

- De [AZ Power shell-module](/powershell/azure/install-az-ps) die lokaal is geïnstalleerd of [Azure Cloud shell](https://shell.azure.com/) in de browser
- Een [Azure database for mysql server](quickstart-create-mysql-server-database-using-azure-powershell.md)

> [!IMPORTANT]
> Hoewel de AZ. MySql Power shell-module in preview is, moet u deze afzonderlijk van de AZ Power shell-module installeren met behulp van de volgende opdracht: `Install-Module -Name Az.MySql -AllowPrerelease` .
> Zodra de AZ. MySql Power shell-module algemeen beschikbaar is, wordt het onderdeel van toekomstige AZ Power shell-module releases en is deze systeem eigen beschikbaar vanuit Azure Cloud Shell.

Als u Power shell lokaal wilt gebruiken, maakt u verbinding met uw Azure-account met behulp van de cmdlet [Connect-AzAccount](/powershell/module/az.accounts/Connect-AzAccount) .

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="list-server-configuration-parameters-for-azure-database-for-mysql-server"></a>Server configuratie parameters voor Azure Database for MySQL server weer geven

Voer de cmdlet uit om alle para meters die kunnen worden gewijzigd op een server en hun waarden weer te geven `Get-AzMySqlConfiguration` .

In het volgende voor beeld worden de server configuratie parameters weer gegeven voor de server **mydemoserver** in de resource groep **myresourcegroup**.

```azurepowershell-interactive
Get-AzMySqlConfiguration -ResourceGroupName myresourcegroup -ServerName mydemoserver
```

Zie het gedeelte MySQL-verwijzing in [Server systeem variabelen](https://dev.mysql.com/doc/refman/5.7/en/server-system-variables.html)voor de definitie van elk van de vermelde para meters.

## <a name="show-server-configuration-parameter-details"></a>Details van server configuratie parameters weer geven

Als u details over een bepaalde configuratie parameter voor een server wilt weer geven, voert u de `Get-AzMySqlConfiguration` cmdlet uit en geeft u de para meter **name** op.

In dit voor beeld worden details weer gegeven van de configuratie parameter server van het **langzame \_ query \_ logboek** voor server **mydemoserver** onder resource groep **myresourcegroup**.

```azurepowershell-interactive
Get-AzMySqlConfiguration -Name slow_query_log -ResourceGroupName myresourcegroup -ServerName mydemoserver
```

## <a name="modify-a-server-configuration-parameter-value"></a>Een waarde voor de para meter server configuratie wijzigen

U kunt ook de waarde van een bepaalde server configuratie parameter wijzigen, waarmee de onderliggende configuratie waarde wordt bijgewerkt voor de MySQL-server engine. Gebruik de cmdlet om de configuratie bij te werken `Update-AzMySqlConfiguration` .

Voor het bijwerken van de configuratie parameter van de **langzame \_ query \_ logboek** server van server **mydemoserver** onder resource groep **myresourcegroup**.

```azurepowershell-interactive
Update-AzMySqlConfiguration -Name slow_query_log -ResourceGroupName myresourcegroup -ServerName mydemoserver -Value On
```

## <a name="next-steps"></a>Volgende stappen

> [!div class="nextstepaction"]
> [Opslag automatisch uitbreiden in azure database for mysql server met behulp van Power shell](howto-auto-grow-storage-powershell.md).
