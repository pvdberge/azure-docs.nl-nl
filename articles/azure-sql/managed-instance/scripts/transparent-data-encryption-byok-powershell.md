---
title: 'Power shell: enable-your-own-Key (BYOK) TDE'
titleSuffix: Azure SQL Managed Instance
description: Meer informatie over het configureren van een Azure SQL Managed instance om met behulp van Power shell (BYOK) Transparent Data Encryption (TDE) te gaan gebruiken voor versleuteling-at-rest.
services: sql-database
ms.service: sql-managed-instance
ms.subservice: security
ms.custom: sqldbrb=1
ms.devlang: ''
ms.topic: conceptual
author: MladjoA
ms.author: mlandzic
ms.reviewer: vanto, carlrab
ms.date: 08/25/2020
ms.openlocfilehash: c812dfa0be3e5ced40b7f347639aeb2540b75351
ms.sourcegitcommit: 927dd0e3d44d48b413b446384214f4661f33db04
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/26/2020
ms.locfileid: "88871527"
---
# <a name="transparent-data-encryption-in-sql-managed-instance-using-your-own-key-from-azure-key-vault"></a>Transparent Data Encryption in SQL Managed instance met uw eigen sleutel vanuit Azure Key Vault

[!INCLUDE[appliesto-sqldb](../../includes/appliesto-sqlmi.md)]

Met dit Power shell-voorbeeld script wordt Transparent Data Encryption (TDE) geconfigureerd met een door de klant beheerde sleutel voor Azure SQL Managed instance, met behulp van een sleutel van Azure Key Vault. Dit wordt vaak een BYOK-scenario (proyour-own-Key) genoemd voor TDE. Zie [Azure SQL transparent Data Encryption met door de klant beheerde sleutel](../../database/transparent-data-encryption-byok-overview.md)voor meer informatie.

## <a name="prerequisites"></a>Vereisten

- Een bestaand beheerd exemplaar. Zie [Power shell gebruiken om een beheerd exemplaar te maken](create-configure-managed-instance-powershell.md).

[!INCLUDE [quickstarts-free-trial-note](../../../../includes/quickstarts-free-trial-note.md)]
[!INCLUDE [updated-for-az](../../../../includes/updated-for-az.md)]
[!INCLUDE [cloud-shell-try-it.md](../../../../includes/cloud-shell-try-it.md)]

Voor het lokaal gebruiken van Power shell of het gebruik van Azure Cloud Shell is Azure PowerShell 2.3.2 of een latere versie vereist. Als u een upgrade wilt uitvoeren, raadpleegt u [Azure PowerShell-module installeren](/powershell/azure/install-az-ps)of voert u het onderstaande voorbeeld script uit om de module voor de huidige gebruiker te installeren:

`Install-Module -Name Az -AllowClobber -Scope CurrentUser`

Als u PowerShell lokaal uitvoert, moet u ook `Connect-AzAccount` uitvoeren om verbinding te kunnen maken met Azure.

## <a name="sample-scripts"></a>Voorbeeldscripts 

[!code-powershell-interactive[main](../../../../powershell_scripts/sql-database/transparent-data-encryption/setup-tde-byok-sqlmi.ps1 "Set up BYOK TDE for SQL Managed Instance")]

## <a name="next-steps"></a>Volgende stappen

Zie [Documentatie over Azure PowerShell](/powershell/azure/) voor meer informatie over Azure PowerShell.

Extra PowerShell-voorbeeldscripts voor SQL Managed Instance vindt u in [PowerShell-scripts voor Azure SQL Managed Instance](../../database/powershell-script-content-guide.md).
