---
title: Início do estado
description: Sinal de que o reprodutor de mídia entrou em um estado de reprodutor rastreado.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 7%

---


# Início do estado

O evento de início de estado indica que o reprodutor de mídia entrou em um estado rastreado, como tela cheia, mudo ou legendas ocultas. Um reprodutor pode estar em vários estados simultaneamente e os estados podem ser iniciados e encerrados na mesma chamada de evento. Feche cada estado com um evento [State end](state-end.md).

Nomes de estados válidos: `fullscreen`, `mute`, `closedCaptioning`, `pictureInPicture`, `inFocus`

* **Pré-requisitos**: [Início da sessão](../session/session-start.md)
* **Métrica associada**: varia por estado; consulte [Rastrear estados do player](/help/implementation/events/player-state/overview.md)

## Tipos de implementação recomendados

>[!BEGINTABS]

>[!TAB Web SDK]

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

>[!TAB iOS]

Use `trackPlayerStateStart` com um objeto de estado criado a partir da constante `MediaConstants.PlayerState` apropriada.

```swift
let stateObject = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.FULLSCREEN)

tracker.trackEvent(event: MediaEvent.StateStart, info: stateObject, metadata: nil)
```

>[!TAB Android]

Use `trackPlayerStateStart` com um objeto de estado criado a partir da constante `MediaConstants.PlayerState` apropriada.

```kotlin
val stateObject = Media.createStateObject(MediaConstants.PlayerState.FULLSCREEN)

tracker.trackEvent(Media.Event.StateStart, stateObject, null)
```

>[!TAB Roku]

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

>[!TAB API do Media Edge]

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

>[!ENDTABS]

## Tipos de implementação herdada (somente Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Usar `ADB.Media.createStateObject` com a constante `ADB.Media.PlayerState` apropriada:

```javascript
var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.Fullscreen);

tracker.trackPlayerStateStart(stateObject);
```

>[!TAB Chromecast]

Usar `ADBMobile.media.createStateObject` com a constante `ADBMobile.media.PlayerState` apropriada:

```javascript
var stateObject = ADBMobile.media.createStateObject(ADBMobile.media.PlayerState.FullScreen);

ADBMobile.media.trackEvent(ADBMobile.media.Event.StateStart, stateObject);
```

>[!TAB API da coleção de mídia]

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

>[!ENDTABS]
