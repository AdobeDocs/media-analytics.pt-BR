---
title: Fim do estado
description: Sinal de que o reprodutor de mídia saiu de um estado de reprodutor rastreado.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 6%

---


# Fim do estado

O evento de fim de estado indica que o reprodutor de mídia saiu de um estado rastreado, como tela cheia, mudo ou legendas ocultas. Enviá-lo para fechar um estado aberto por [Início do estado](state-start.md). Os estados podem ser iniciados e encerrados na mesma chamada de evento. Um reprodutor pode sair de vários estados simultaneamente.

Nomes de estados válidos: `fullscreen`, `mute`, `closedCaptioning`, `pictureInPicture`, `inFocus`

* **Pré-requisitos**: [Início da sessão](../session/session-start.md), [Início do estado](state-start.md)
* **Métrica associada**: varia por estado; consulte [Rastrear estados do player](/help/implementation/events/player-state/overview.md)

## Tipos de implementação recomendados

>[!BEGINTABS]

>[!TAB Web SDK]

Chame [`sendEvent`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/collection/js/commands/sendevent/overview) com `eventType: "media.statesUpdate"` e o nome do estado em `statesEnd`:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesEnd: [{ name: "fullscreen" }],
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

Os estados podem ser iniciados e encerrados na mesma chamada:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesStart: [{ name: "mute" }],
      statesEnd: [{ name: "fullscreen" }],
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

>[!TAB iOS]

Use `trackPlayerStateEnd` com um objeto de estado criado a partir da constante `MediaConstants.PlayerState` apropriada.

```swift
let stateObject = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.FULLSCREEN)

tracker.trackEvent(event: MediaEvent.StateEnd, info: stateObject, metadata: nil)
```

>[!TAB Android]

Use `trackPlayerStateEnd` com um objeto de estado criado a partir da constante `MediaConstants.PlayerState` apropriada.

```kotlin
val stateObject = Media.createStateObject(MediaConstants.PlayerState.FULLSCREEN)

tracker.trackEvent(Media.Event.StateEnd, stateObject, null)
```

>[!TAB Roku Edge]

Chame `sendMediaEvent` com `eventType: "media.statesUpdate"` e o nome do estado em `statesEnd`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesEnd": [{ "name": "fullscreen" }],
            "playhead": 90
        }
    }
})
```

>[!TAB API do Media Edge]

Chame o ponto de extremidade [statesUpdate](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/statesupdate/) com o nome de estado em `statesEnd`:

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/statesUpdate?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.statesUpdate",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 90,
        "statesEnd": [{ "name": "fullscreen" }]
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

tracker.trackPlayerStateEnd(stateObject);
```

>[!TAB Chromecast]

Usar `ADBMobile.media.createStateObject` com a constante `ADBMobile.media.PlayerState` apropriada:

```javascript
var stateObject = ADBMobile.media.createStateObject(ADBMobile.media.PlayerState.FullScreen);

ADBMobile.media.trackEvent(ADBMobile.media.Event.StateEnd, stateObject);
```

>[!TAB Roku 2.x]

O rastreamento do estado do player não está disponível no Roku 2.x SDK. Para rastrear estados do player, use o [Roku Edge SDK](/help/implementation/edge/roku.md).

>[!TAB API da coleção de mídia]

Enviar uma POSTAGEM `stateEnd` para o [ponto de extremidade de eventos](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md):

```json
{
  "playerTime": { "playhead": 90, "ts": 1699523820000 },
  "eventType": "stateEnd",
  "params": {
    "media.state.name": "fullscreen"
  }
}
```

>[!ENDTABS]
