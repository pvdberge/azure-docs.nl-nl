---
ms.openlocfilehash: ed7be82146f38cc7ae57fd863bb0c1b8e6910fd2
ms.sourcegitcommit: 56cbd6d97cb52e61ceb6d3894abe1977713354d9
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/20/2020
ms.locfileid: "88690955"
---
Volg deze stappen om de voorbeeldcode uit te voeren:

1. Ga in Visual Studio Code naar *src/cloud-to-device-console-app/operations.json*.
1. Controleer op het knooppunt **GraphTopologySet** of u de volgende waarde ziet:

    `"topologyUrl" : "https://raw.githubusercontent.com/Azure/live-video-analytics/master/MediaGraph/topologies/motion-detection/topology.json"`
1. Controleer of op de knooppunten **GraphInstanceSet** en **GraphTopologyDelete** de waarde van `topologyName` overeenkomt met de waarde van de eigenschap `name` in de graaftopologie:

    `"topologyName" : "MotionDetection"`
    
1. Start een foutopsporingssessie door de toets F5 te selecteren. In het **TERMINAL**-venster worden enkele berichten weergegeven.
1. Het bestand *operations.json-* wordt gestart met aanroepen naar `GraphTopologyList` en `GraphInstanceList`. Als u na het voltooien van vorige quickstarts resources hebt opgeschoond, worden er lege lijsten geretourneerd en wordt het proces gepauzeerd. Selecteer de Enter-toets om door te gaan.

    ```
    --------------------------------------------------------------------------
    Executing operation GraphTopologyList
    -----------------------  Request: GraphTopologyList  --------------------------------------------------
    {
        "@apiVersion": "1.0"
    }
    ---------------  Response: GraphTopologyList - Status: 200  ---------------
    {
        "value": []
    }
    --------------------------------------------------------------------------
    Executing operation WaitForInput
    Press Enter to continue
    ```
    
    In het **TERMINAL**-venster wordt de volgende set aanroepen van directe methoden weergegeven:
     * Een aanroep van `GraphTopologySet` waarin gebruik wordt gemaakt van de voorgaande `topologyUrl`
     * Een aanroep van `GraphInstanceSet` waarin gebruik wordt gemaakt van de volgende hoofdtekst:
         
    ```
    {
      "@apiVersion": "1.0",
      "name": "Sample-Graph",
      "properties": {
        "topologyName": "MotionDetection",
        "description": "Sample graph description",
        "parameters": [
          {
            "name": "rtspUrl",
            "value": "rtsp://rtspsim:554/media/camera-300s.mkv"
          },
          {
            "name": "rtspUserName",
            "value": "testuser"
          },
          {
            "name": "rtspPassword",
            "value": "testpassword"
          }
        ]
      }
    }
    ```
     
    * Een aanroep van `GraphInstanceActivate` waarmee de instantie van de grafiek en de videostroom worden gestart.
    * Een tweede aanroep van `GraphInstanceList` waarmee wordt weergegeven dat het grafiekexemplaar wordt uitgevoerd.
1. De uitvoer in het **TERMINAL**-venster wordt gepauzeerd bij `Press Enter to continue`. Selecteer Enter nog niet. Schuif omhoog om de nettoladingen voor het JSON-antwoord te zien voor de directe methoden die u hebt aangeroepen.
1. Schakel naar het **UITVOER**-venster in Visual Studio Code. Er zijn berichten te zien die door de module Live Video Analytics in IoT Edge worden verzonden naar de IoT-hub. In de volgende sectie van deze quickstart worden deze berichten besproken.
1. Het uitvoeren van de mediagraaf wordt vervolgd en de resultaten worden afgedrukt. Via de RTSP-simulator wordt de bronvideo continu herhaald. Als u de mediagraaf wilt stoppen, keert u terug naar het **TERMINAL**-venster en selecteert u Enter. 

    Met de volgende reeks aanroepen worden resources opgeschoond:

    * Met een aanroep van `GraphInstanceDeactivate` wordt het graafexemplaar gedeactiveerd.
    * Met een aanroep van `GraphInstanceDelete` wordt het exemplaar verwijderd.
    * Met een aanroep van `GraphTopologyDelete` wordt de topologie verwijderd.
    * Met een aanroep van `GraphTopologyList` wordt ten slotte aangegeven dat de lijst leeg is.
