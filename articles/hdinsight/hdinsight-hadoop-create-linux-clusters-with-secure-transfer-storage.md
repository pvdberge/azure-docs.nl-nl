---
title: Apache Hadoop & beveiligde overdrachts opslag-Azure HDInsight
description: Informatie over het maken van HDInsight-clusters met Azure-opslag-accounts voor veilige overdracht.
author: hrasheed-msft
ms.author: hrasheed
ms.reviewer: jasonh
ms.service: hdinsight
ms.topic: how-to
ms.custom: hdinsightactive
ms.date: 02/18/2020
ms.openlocfilehash: 43abe6a827af668f2b756e5f00497fbfe1698413
ms.sourcegitcommit: 124f7f699b6a43314e63af0101cd788db995d1cb
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/08/2020
ms.locfileid: "86083233"
---
# <a name="apache-hadoop-clusters-with-secure-transfer-storage-accounts-in-azure-hdinsight"></a>Apache Hadoop clusters met opslag accounts voor veilige overdracht in azure HDInsight

De functie [Veilige overdracht vereist](../storage/common/storage-require-secure-transfer.md) verhoogt de beveiliging van uw Azure-opslagaccount door alle aanvragen naar uw account af te dwingen via een beveiligde verbinding. Deze functie en het wasbs-schema worden alleen ondersteund door HDInsight-clusterversie 3.6 of nieuwer.

> [!IMPORTANT]
> Het inschakelen van beveiligde opslag overdracht na het maken van een cluster kan leiden tot fouten bij het gebruik van uw opslag account en wordt niet aanbevolen. Het is beter om een nieuw cluster te maken met behulp van een opslag account waarvoor beveiligde overdracht al is ingeschakeld.

## <a name="storage-accounts"></a>Opslagaccounts

### <a name="azure-portal"></a>Azure Portal

Standaard is de eigenschap beveiligde overdracht vereist ingeschakeld wanneer u een opslag account maakt in Azure Portal.

Zie voor het bijwerken van een bestaand opslag account met Azure Portal [vereisen beveiligde overdracht met Azure Portal](../storage/common/storage-require-secure-transfer.md#require-secure-transfer-for-an-existing-storage-account).

### <a name="powershell"></a>PowerShell

Zorg ervoor dat de para meter is ingesteld voor de Power shell-cmdlet [New-AzStorageAccount](https://docs.microsoft.com/powershell/module/az.storage/new-azstorageaccount) `-EnableHttpsTrafficOnly` `1` .

Zie [veilige overdracht vereisen met Power shell](../storage/common/storage-require-secure-transfer.md#require-secure-transfer-with-powershell)voor meer informatie over het bijwerken van een bestaand opslag account met Power shell.

### <a name="azure-cli"></a>Azure CLI

Voor de Azure CLI-opdracht [AZ Storage account create](https://docs.microsoft.com/cli/azure/storage/account?view=azure-cli-latest#az-storage-account-create), controleert u of de para meter `--https-only` is ingesteld op `true` .

Zie [veilige overdracht vereisen met Azure cli](../storage/common/storage-require-secure-transfer.md#require-secure-transfer-with-azure-cli)voor meer informatie over het bijwerken van een bestaand opslag account met Azure cli.

## <a name="add-additional-storage-accounts"></a>Extra opslagaccounts toevoegen

Er zijn verschillende opties om extra opslagaccounts met veilige overdracht toe te voegen:

* De Azure Resource Manager-sjabloon in de laatste sectie wijzigen.
* Een cluster maken met [Azure Portal](https://portal.azure.com) en een gekoppelde opslagaccount opgeven.
* Een scriptactie gebruiken om extra opslagaccounts met veilige overdracht toe te voegen aan een bestaand HDInsight-cluster. Zie [Extra opslagaccounts toevoegen aan HDInsight](hdinsight-hadoop-add-storage.md) voor meer informatie.

## <a name="next-steps"></a>Volgende stappen

* Het gebruik van Azure Storage (WASB) in plaats van [Apache HADOOP HDFS](https://hadoop.apache.org/docs/current/hadoop-project-dist/hadoop-hdfs/HdfsUserGuide.html) als de standaard gegevens opslag
* Zie [Azure Storage gebruiken met HDInsight](hdinsight-hadoop-use-blob-storage.md) voor meer informatie over hoe HDInsight Azure Storage gebruikt.
* Zie [Gegevens uploaden naar HDInsight](hdinsight-upload-data.md) voor meer informatie over het uploaden van gegevens naar HDInsight.
