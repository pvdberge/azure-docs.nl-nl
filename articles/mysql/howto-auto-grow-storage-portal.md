---
title: Opslag Azure Portal automatisch verg Roten-Azure Database for MySQL
description: In dit artikel wordt beschreven hoe u automatische groei opslag voor Azure Database for MySQL kunt inschakelen met behulp van Azure Portal
author: ambhatna
ms.author: ambhatna
ms.service: mysql
ms.topic: how-to
ms.date: 3/18/2020
ms.openlocfilehash: d4dc5c2690be7b9abbda685e78ea562878626b5c
ms.sourcegitcommit: 53acd9895a4a395efa6d7cd41d7f78e392b9cfbe
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/22/2020
ms.locfileid: "90902860"
---
# <a name="auto-grow-storage-in-azure-database-for-mysql-using-the-azure-portal"></a>Opslag in Azure Database for MySQL automatisch verg Roten met behulp van de Azure Portal
In dit artikel wordt beschreven hoe u een Azure Database for MySQL server-opslag kunt configureren om te groeien zonder dat dit van invloed is op de werk belasting.

Wanneer een server de toegewezen opslag limiet bereikt, is de server gemarkeerd als alleen-lezen. Als u automatisch verg Roten van opslag inschakelt, neemt de server opslag echter toe om de groeiende gegevens te verwerken. Voor servers met een ingerichte opslag van minder dan 100 GB wordt de ingerichte opslag grootte met 5 GB verhoogd zodra de beschik bare opslag onder het hoogste van 1 GB of 10% van de ingerichte opslag ligt. Voor servers met meer dan 100 GB ingerichte opslag wordt de ingerichte opslag grootte verhoogd met 5% wanneer de beschik bare opslag ruimte lager is dan 5% van de ingerichte opslag grootte. De maximale opslag limieten die [hier](https://docs.microsoft.com/azure/mysql/concepts-pricing-tiers#storage) zijn opgegeven, zijn van toepassing.

## <a name="prerequisites"></a>Vereisten
U hebt het volgende nodig om deze hand leiding te volt ooien:
- Een [Azure database for mysql server](quickstart-create-mysql-server-database-using-azure-portal.md)

## <a name="enable-storage-auto-grow"></a>Opslag automatisch verg Roten inschakelen 

Volg deze stappen voor het instellen van de automatische groei van MySQL-server opslag:

1. Selecteer in de [Azure Portal](https://portal.azure.com/)uw bestaande Azure database for mysql-server.

2. Klik op de pagina MySQL-server, onder **instellingen** kop, op **prijs categorie** om de pagina prijs categorie te openen.

3. In de sectie automatische groei selecteert u **Ja** om automatische groei van opslag in te scha kelen.

    :::image type="content" source="./media/howto-auto-grow-storage-portal/3-auto-grow.png" alt-text="Azure Database for MySQL-Settings_Pricing_tier-automatische groei":::

4. Klik op **OK** om de wijzigingen op te slaan.

5. Bij een melding wordt bevestigd dat automatisch uitbreiden is ingeschakeld.

    :::image type="content" source="./media/howto-auto-grow-storage-portal/5-auto-grow-success.png" alt-text="Azure Database for MySQL-automatisch groei geslaagd":::

## <a name="next-steps"></a>Volgende stappen

Meer informatie over [het maken van waarschuwingen over metrische gegevens](howto-alert-on-metric.md).
