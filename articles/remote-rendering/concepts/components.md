---
title: Onderdelen
description: Definitie van onderdelen in het bereik van Azure remote rendering
author: florianborn71
ms.author: flborn
ms.date: 02/04/2020
ms.topic: conceptual
ms.custom: devx-track-csharp
ms.openlocfilehash: a488e2499b92b290ad2b55120c3c70a18d45d426
ms.sourcegitcommit: f845ca2f4b626ef9db73b88ca71279ac80538559
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/09/2020
ms.locfileid: "89613943"
---
# <a name="components"></a>Onderdelen

Azure remote rendering maakt gebruik van het [systeem patroon entity component](https://en.wikipedia.org/wiki/Entity_component_system) . Hoewel [entiteiten](entities.md) de positie en de hiërarchische samen stelling van objecten vertegenwoordigen, zijn onderdelen verantwoordelijk voor het implementeren van het gedrag.

De meest gebruikte typen onderdelen zijn [:::no-loc text="mesh components":::](meshes.md) , waarmee u netten kunt toevoegen aan de rendering-pijp lijn. Op dezelfde manier worden [lichte onderdelen](../overview/features/lights.md) gebruikt voor het toevoegen van de onderdelen verlichting en [knip vlak](../overview/features/cut-planes.md) , waarmee open mazen worden geknipt.

Al deze onderdelen gebruiken de trans formatie (positie, rotatie, schaal) van de entiteit waaraan ze zijn gekoppeld, als referentie punt.

## <a name="working-with-components"></a>Werken met onderdelen

U kunt eenvoudig componenten programmatisch toevoegen, verwijderen en bewerken:

```cs
// create a point light component
AzureSession session = GetCurrentlyConnectedSession();
PointLightComponent lightComponent = session.Actions.CreateComponent(ObjectType.PointLightComponent, ownerEntity) as PointLightComponent;

lightComponent.Color = new Color4Ub(255, 150, 20, 255);
lightComponent.Intensity = 11;

// ...

// destroy the component
lightComponent.Destroy();
lightComponent = null;
```

```cpp
// create a point light component
ApiHandle<AzureSession> session = GetCurrentlyConnectedSession();

ApiHandle<PointLightComponent> lightComponent = session->Actions()->CreateComponent(ObjectType::PointLightComponent, ownerEntity)->as<PointLightComponent>();

// ...

// destroy the component
lightComponent->Destroy();
lightComponent = nullptr;
```

Een onderdeel wordt tijdens de aanmaak gekoppeld aan een entiteit. U kunt deze later niet naar een andere entiteit verplaatsen. Onderdelen worden expliciet verwijderd met `Component.Destroy()` of automatisch wanneer de entiteit eigenaar van het onderdeel wordt vernietigd.

Er kan slechts één exemplaar van elk onderdeel type tegelijk aan een entiteit worden toegevoegd.

## <a name="unity-specific"></a>Eenheids specifiek

De unit-integratie heeft aanvullende uitbreidings functies voor interactie met-onderdelen. Zie [Unit Game-objecten en-onderdelen](../how-tos/unity/objects-components.md).

## <a name="api-documentation"></a>API-documentatie

* [C#-ComponentBase](https://docs.microsoft.com/dotnet/api/microsoft.azure.remoterendering.componentbase)
* [C# RemoteManager. CreateComponent ()](https://docs.microsoft.com/dotnet/api/microsoft.azure.remoterendering.remotemanager.createcomponent)
* [C#-entiteit. FindComponentOfType ()](https://docs.microsoft.com/dotnet/api/microsoft.azure.remoterendering.entity.findcomponentoftype)
* [C++ ComponentBase](https://docs.microsoft.com/cpp/api/remote-rendering/componentbase)
* [C++ RemoteManager:: CreateComponent ()](https://docs.microsoft.com/cpp/api/remote-rendering/remotemanager#createcomponent)
* [C++-entiteit:: FindComponentOfType ()](https://docs.microsoft.com/cpp/api/remote-rendering/entity#findcomponentoftype)

## <a name="next-steps"></a>Volgende stappen

* [Objectgrenzen](object-bounds.md)
* [Meshes](meshes.md)
