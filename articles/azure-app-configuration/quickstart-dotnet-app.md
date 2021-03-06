---
title: Quickstart voor Azure-appconfiguratie met .NET Framework | Microsoft Docs
description: In dit artikel maakt u een .NET Framework-app met Azure App Configuration om opslag en beheer van toepassingsinstellingen gescheiden van uw code te centraliseren.
services: azure-app-configuration
documentationcenter: ''
author: lisaguthrie
ms.service: azure-app-configuration
ms.custom: devx-track-csharp
ms.topic: quickstart
ms.date: 12/17/2019
ms.author: lcozzens
ms.openlocfilehash: 6795d10950ddd7b03dfa505ab44d2f43837c9045
ms.sourcegitcommit: 02ca0f340a44b7e18acca1351c8e81f3cca4a370
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/19/2020
ms.locfileid: "88590265"
---
# <a name="quickstart-create-a-net-framework-app-with-azure-app-configuration"></a>Quickstart: Een .NET Framework-app maken met Azure-appconfiguratie

In deze quickstart neemt u Azure App Configuration op in een op .NET Framework gebaseerde console-app om opslag en beheer van toepassingsinstellingen gescheiden van uw code te centraliseren.

## <a name="prerequisites"></a>Vereisten

- Azure-abonnement: [u kunt een gratis abonnement nemen](https://azure.microsoft.com/free/)
- [Visual Studio 2019](https://visualstudio.microsoft.com/vs)
- [.NET Framework 4.7.2](https://dotnet.microsoft.com/download)

## <a name="create-an-app-configuration-store"></a>Een App Configuration-archief maken

[!INCLUDE [azure-app-configuration-create](../../includes/azure-app-configuration-create.md)]

6. Selecteer **Configuratieverkenner** > **Maken** > **Sleutelwaarde** om de volgende sleutel-waardeparen toe te voegen:

    | Sleutel | Waarde |
    |---|---|
    | TestApp:Settings:Message | Gegevens van Azure App Configuration |

    Laat **Label** en **Inhoudstype** nog even leeg.

7. Selecteer **Toepassen**.

## <a name="create-a-net-console-app"></a>Een .NET Core-consoletoepassing maken

1. Start Visual Studio en selecteer **Bestand** > **Nieuw** > **Project**.

1. In **Een nieuw project maken**, filtert u op het projecttype **Console** en klikt u op **Console-app (.NET Framework)** . Selecteer **Next**.

1. Voer in **Uw nieuwe project configureren** een projectnaam in. Selecteer onder **Framework** **.NET Framework 4.7.1** of hoger. Selecteer **Maken**.

## <a name="connect-to-an-app-configuration-store"></a>Verbinding maken met een App Configuration-archief

1. Klik met de rechtermuisknop op het project en selecteer **NuGet-pakketten beheren**. Zoek op het tabblad **Bladeren** de volgende NuGet-pakketten op en voeg deze toe aan uw project.

    ```
    Microsoft.Configuration.ConfigurationBuilders.AzureAppConfiguration 1.0.0 or later
    Microsoft.Configuration.ConfigurationBuilders.Environment 2.0.0 or later
    System.Configuration.ConfigurationManager version 4.6.0 or later
    ```

1. Werk het bestand *App.config* van uw project als volgt bij:

    ```xml
    <configSections>
        <section name="configBuilders" type="System.Configuration.ConfigurationBuildersSection, System.Configuration, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a" restartOnExternalChanges="false" requirePermission="false" />
    </configSections>

    <configBuilders>
        <builders>
            <add name="MyConfigStore" mode="Greedy" connectionString="${ConnectionString}" type="Microsoft.Configuration.ConfigurationBuilders.AzureAppConfigurationBuilder, Microsoft.Configuration.ConfigurationBuilders.AzureAppConfiguration" />
            <add name="Environment" mode="Greedy" type="Microsoft.Configuration.ConfigurationBuilders.EnvironmentConfigBuilder, Microsoft.Configuration.ConfigurationBuilders.Environment" />
        </builders>
    </configBuilders>

    <appSettings configBuilders="Environment,MyConfigStore">
        <add key="AppName" value="Console App Demo" />
        <add key="ConnectionString" value ="Set via an environment variable - for example, dev, test, staging, or production connection string." />
    </appSettings>
    ```

   De verbindingstekenreeks van uw App Configuration-archief wordt gelezen vanuit de omgevingsvariabele `ConnectionString`. Voeg de `Environment`-configuratiebouwer toe vóór de `MyConfigStore` in de eigenschap `configBuilders` van de sectie `appSettings`.

1. Open *Program.cs* en werk de methode `Main` bij voor het gebruik van App Configuration door de methode `ConfigurationManager` aan te roepen.

    ```csharp
    static void Main(string[] args)
    {
        string message = System.Configuration.ConfigurationManager.AppSettings["TestApp:Settings:Message"];

        Console.WriteLine(message);
    }
    ```

## <a name="build-and-run-the-app-locally"></a>De app lokaal compileren en uitvoeren

1. Stel een omgevingsvariabele met de naam **ConnectionString** in en stel deze in op de toegangssleutel van uw App Configuration-archief. Als u de Windows-opdrachtprompt gebruikt, moet u de volgende opdracht uitvoeren:

    ```cmd
        setx ConnectionString "connection-string-of-your-app-configuration-store"
    ```

    Als u Windows PowerShell gebruikt, voert u de volgende opdracht uit:

    ```azurepowershell
        $Env:ConnectionString = "connection-string-of-your-app-configuration-store"
    ```
1. Start Visual Studio opnieuw zodat de wijziging kan worden doorgevoerd. Druk op Ctrl + F5 om de consoletoepassing te bouwen en uit te voeren.

## <a name="clean-up-resources"></a>Resources opschonen

[!INCLUDE [azure-app-configuration-cleanup](../../includes/azure-app-configuration-cleanup.md)]

## <a name="next-steps"></a>Volgende stappen

In deze quickstart hebt u een nieuw App Configuration-archief gemaakt en dit gebruikt met een .NET Core console-app. De waarde `AppSettings` van `ConfigurationManager` wordt niet gewijzigd nadat de toepassing is gestart. De bibliotheek van de .NET Standard-configuratieprovider van App Configuration kan echter ook worden gebruikt in een .NET Framework-app. Ga door naar de volgende zelfstudie voor meer informatie over het configureren van uw .NET Framework-app om configuratie-instellingen dynamisch te vernieuwen.

> [!div class="nextstepaction"]
> [Dynamische configuratie inschakelen](./enable-dynamic-configuration-dotnet.md)
