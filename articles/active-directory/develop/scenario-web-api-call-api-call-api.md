---
title: Web-API voor het aanroepen van web-Api's-micro soft Identity-platform | Azure
description: Meer informatie over het bouwen van een web-API voor het aanroepen van web-Api's.
services: active-directory
author: jmprieur
manager: CelesteDG
ms.service: active-directory
ms.subservice: develop
ms.topic: conceptual
ms.workload: identity
ms.date: 05/07/2019
ms.author: jmprieur
ms.custom: aaddev
ms.openlocfilehash: b756d7df03bd3c06b703617dbf84a194d716f1e3
ms.sourcegitcommit: 3d79f737ff34708b48dd2ae45100e2516af9ed78
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 07/23/2020
ms.locfileid: "87026370"
---
# <a name="a-web-api-that-calls-web-apis-call-an-api"></a>Een web-API die web-Api's aanroept: een API aanroepen

Nadat u een token hebt, kunt u een beveiligde web-API aanroepen. U kunt dit doen vanuit de controller van uw web-API.

## <a name="controller-code"></a>Controller code

# <a name="aspnet-core"></a>[ASP.NET Core](#tab/aspnetcore)

Met de volgende code wordt de voorbeeld code die wordt weer gegeven in [een web-API die web-api's aanroept, voortgezet: Schaf een token voor de app aan](scenario-web-api-call-api-acquire-token.md). De code wordt aangeroepen in de acties van de API-controllers. Er wordt een stroomafwaartse API met de naam *ToDoList*aangeroepen.

Nadat u het token hebt aangeschaft, kunt u dit als Bearer-token gebruiken om de downstream API aan te roepen.

```csharp
private async Task CallTodoListService(string accessToken)
{

// After the token has been returned by Microsoft Identity Web, add it to the HTTP authorization header before making the call to access the To Do list service.
_httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);

// Call the To Do list service.
HttpResponseMessage response = await _httpClient.GetAsync(TodoListBaseAddress + "/api/todolist");
...
}
```

# <a name="java"></a>[Java](#tab/java)

Met de volgende code wordt de voorbeeld code die wordt weer gegeven in [een web-API die web-api's aanroept, voortgezet: Schaf een token voor de app aan](scenario-web-api-call-api-acquire-token.md). De code wordt aangeroepen in de acties van de API-controllers. Het roept de downstream API MS Graph aan.

Nadat u het token hebt aangeschaft, kunt u dit als Bearer-token gebruiken om de downstream API aan te roepen.

```Java
private String callMicrosoftGraphMeEndpoint(String accessToken){
    RestTemplate restTemplate = new RestTemplate();

    HttpHeaders headers = new HttpHeaders();
    headers.setContentType(MediaType.APPLICATION_JSON);

    headers.set("Authorization", "Bearer " + accessToken);

    HttpEntity<String> entity = new HttpEntity<>(null, headers);

    String result = restTemplate.exchange("https://graph.microsoft.com/v1.0/me", HttpMethod.GET,
            entity, String.class).getBody();

    return result;
}
```

# <a name="python"></a>[Python](#tab/python)
Een voor beeld van het demonstreren van deze stroom met MSAL python is nog niet beschikbaar.

---

## <a name="next-steps"></a>Volgende stappen

> [!div class="nextstepaction"]
> [Een web-API die web-Api's aanroept: verplaatsen naar productie](scenario-web-api-call-api-production.md)
