---
title: Netwerk configuratie voor Azure App Service synchroniseren
titleSuffix: Azure SQL Managed Instance
description: In dit artikel wordt beschreven hoe u uw netwerk configuratie synchroniseert voor Azure App Service hosting abonnement met uw door Azure SQL beheerd exemplaar.
services: sql-database
ms.service: sql-managed-instance
ms.subservice: operations
ms.custom: sqldbrb=1
ms.devlang: ''
ms.topic: conceptual
author: srdan-bozovic-msft
ms.author: srbozovi
ms.reviewer: sstein, bonova, carlrab
ms.date: 12/13/2018
ms.openlocfilehash: a0192f204fdb0797d98947a174bf6d669034b666
ms.sourcegitcommit: 877491bd46921c11dd478bd25fc718ceee2dcc08
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/02/2020
ms.locfileid: "84695450"
---
# <a name="sync-networking-configuration-for-azure-app-service-hosting-plan-with-azure-sql-managed-instance"></a>De netwerk configuratie voor het hosten van Azure App Service met Azure SQL Managed instance synchroniseren
[!INCLUDE[appliesto-sqlmi](../includes/appliesto-sqlmi.md)]

Het kan gebeuren dat u [uw app hebt geïntegreerd met een Azure-Virtual Network](../../app-service/web-sites-integrate-with-vnet.md), maar u kunt geen verbinding maken met een SQL-beheerd exemplaar. U kunt dit probleem oplossen door de netwerk configuratie voor uw service plan te vernieuwen of te synchroniseren. 

## <a name="sync-network-configuration"></a>Netwerkconfiguratie synchroniseren 

Voer hiervoor de volgende stappen uit:  

1. Ga naar uw web apps App Service plan.

   ![Scherm opname van App Service plan](./media/azure-app-sync-network-configuration/app-service-plan.png)

2. Selecteer **netwerken** en selecteer vervolgens **Klik hier om te beheren**.

   ![Scherm opname van service abonnement beheren](./media/azure-app-sync-network-configuration/manage-plan.png)

3. Selecteer uw **VNet** en klik op **netwerk synchroniseren**.

   ![Scherm opname van het synchronisatie netwerk](./media/azure-app-sync-network-configuration/sync.png)

4. Wacht totdat de synchronisatie is voltooid.
  
   ![Scherm opname van synchronisatie is voltooid](./media/azure-app-sync-network-configuration/sync-done.png)

U kunt nu proberen om de verbinding met uw door SQL beheerde instantie te herstellen.

## <a name="next-steps"></a>Volgende stappen

- Zie voor meer informatie over het configureren van uw VNet voor SQL Managed instance de [vnet-architectuur voor SQL Managed instance](connectivity-architecture-overview.md) en [het configureren van bestaande vnet](vnet-existing-add-subnet.md).
