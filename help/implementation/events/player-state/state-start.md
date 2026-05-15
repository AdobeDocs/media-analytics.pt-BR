---
title: Início do estado
description: Sinal de que o reprodutor de mídia entrou em um estado de reprodutor rastreado.
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 13%

---


# Início do estado

O evento de início de estado indica que o reprodutor de mídia entrou em um estado rastreado, como tela cheia, mudo ou legendas ocultas. Um reprodutor pode estar em vários estados simultaneamente e os estados podem ser iniciados e encerrados na mesma chamada de evento. Feche cada estado com um evento [State end](state-end.md).

Nomes de estados válidos: `fullscreen`, `mute`, `closedCaptioning`, `pictureInPicture`, `inFocus`

* **Pré-requisitos**: [Início da sessão](../session/session-start.md)
* **Métrica associada**: varia por estado; consulte [Rastreamento do estado do player](/help/use-cases/player-state-tracking/implementation-and-reporting.md)

## SDK da web

Chame [`sendEvent`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/collection/js/commands/sendevent/overview) com `eventType: "media.statesUpdate"` e o nome do estado em `statesStart`:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesStart: [{ name: "fullscreen" }],
      sessionID: "{sid}",
      playhead: 60
    }
  }
});
```

Vários estados podem ser iniciados na mesma chamada:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesStart: [
        { name: "fullscreen" },
        { name: "mute" }
      ],
      sessionID: "{sid}",
      playhead: 60
    }
  }
});
```

## SDK móvel

Use `trackPlayerStateStart` com um objeto de estado criado a partir da constante `MediaConstants.PlayerState` apropriada.

**iOS (Swift)**

```swift
let stateObject = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.FULLSCREEN)

tracker.trackEvent(event: MediaEvent.StateStart, info: stateObject, metadata: nil)
```

**Android (Kotlin)**

```kotlin
val stateObject = Media.createStateObject(MediaConstants.PlayerState.FULLSCREEN)

tracker.trackEvent(Media.Event.StateStart, stateObject, null)
```

## Roku (BrightScript)

Chame `sendMediaEvent` com `eventType: "media.statesUpdate"` e o nome do estado em `statesStart`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesStart": [{ "name": "fullscreen" }],
            "playhead": 60
        }
    }
})
```

## API de borda de mídia

Chame o ponto de extremidade [statesUpdate](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/statesupdate/) com o nome de estado em `statesStart`:

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/statesUpdate?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.statesUpdate",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 60,
        "statesStart": [{ "name": "fullscreen" }]
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## SDK de mídia

Usar `ADB.Media.createStateObject` com a constante `ADB.Media.PlayerState` apropriada:

```javascript
var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.Fullscreen);

tracker.trackPlayerStateStart(stateObject);
```

## API da coleção de mídia

Enviar uma POSTAGEM `stateStart` para o [ponto de extremidade de eventos](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md):

```json
{
  "playerTime": { "playhead": 60, "ts": 1699523820000 },
  "eventType": "stateStart",
  "params": {
    "media.state.name": "fullscreen"
  }
}
```
