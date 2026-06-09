---
title: Picture in picture
description: Rastreie quando o visualizador entra e sai da reprodução picture-in-picture para que o back-end possa relatar o engajamento do PiP.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 5%

---


# Picture in picture

>[!BEGINSHADEBOX]

*Esta página aborda a coleta de dados para o estado do player **Picture in picture**. Consulte [Fluxos afetados pela picture in picture](/help/reporting/metrics/picture-in-picture-streams-impacted.md), [Contagens de Picture in picture](/help/reporting/metrics/picture-in-picture-count.md) e [Duração total da Picture in picture](/help/reporting/metrics/picture-in-picture-total-duration.md) para as métricas de relatório correspondentes.*

>[!ENDSHADEBOX]

O estado da imagem no player de imagem é rastreado quando o visualizador entra e sai da reprodução picture-in-picture. Acione um evento de início de estado quando a picture-in-picture começar e um evento de fim de estado quando terminar. O back-end calcula três métricas desses eventos: fluxos afetados, contagem de entradas de estado e tempo total no estado.

| Propriedade | Valor |
| --- | --- |
| **Variáveis de dados de contexto** | `a.media.states.pictureinpicture.set`, `a.media.states.pictureinpicture.count`, `a.media.states.pictureinpicture.time` |
| **Campo da coleção XDM** | [`xdm.mediaCollection.statesStart[]`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/media-collection-details) e [`xdm.mediaCollection.statesEnd[]`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/media-collection-details) (entradas com `name: "pictureInPicture"`) |
| **Características do Audience Manager** | `c_contextdata.a.media.states.pictureinpicture.set`, `c_contextdata.a.media.states.pictureinpicture.count`, `c_contextdata.a.media.states.pictureinpicture.time` |
| **Obrigatório** | Não |
| **Enviado com** | [Início do estado](/help/implementation/events/player-state/state-start.md), [término do estado](/help/implementation/events/player-state/state-end.md) |

## Tipos de implementação recomendados

>[!BEGINTABS]

>[!TAB Web SDK]

Use [`sendEvent`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/collection/js/commands/sendevent/overview) para enviar um evento `media.statesUpdate` com o estado adicionado a `statesStart`:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesStart: [{ name: "pictureInPicture" }],
      sessionID: "{sid}",
      playhead: 60
    }
  }
});
```

Quando o visualizador sair do picture-in-picture, envie outro evento com o estado em `statesEnd`:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesEnd: [{ name: "pictureInPicture" }],
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

>[!TAB iOS]

Use `tracker.trackPlayerStateStart()` e `tracker.trackPlayerStateEnd()` com a constante `MediaConstants.PlayerState.PICTURE_IN_PICTURE`.

```swift
let stateObject = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.PICTURE_IN_PICTURE)

tracker.trackPlayerStateStart(info: stateObject)
tracker.trackPlayerStateEnd(info: stateObject)
```

>[!TAB Android]

Use `tracker.trackPlayerStateStart()` e `tracker.trackPlayerStateEnd()` com a constante `MediaConstants.PlayerState.PICTURE_IN_PICTURE`.

```kotlin
val stateObject = Media.createStateObject(MediaConstants.PlayerState.PICTURE_IN_PICTURE)

tracker.trackPlayerStateStart(stateObject)
tracker.trackPlayerStateEnd(stateObject)
```

>[!TAB Roku Edge]

Use `sendMediaEvent` para enviar um evento `media.statesUpdate` com o estado adicionado a `statesStart`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesStart": [{ "name": "pictureInPicture" }],
            "playhead": 60
        }
    }
})
```

Quando o visualizador sair do picture-in-picture, envie outro evento com o estado em `statesEnd`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesEnd": [{ "name": "pictureInPicture" }],
            "playhead": 90
        }
    }
})
```

>[!TAB API do Media Edge]

Chame o ponto de extremidade [statesUpdate](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/statesupdate/) com `pictureInPicture` em `statesStart` (ou `statesEnd` quando o visualizador sair do PiP):

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.statesUpdate",
      "mediaCollection": {
        "statesStart": [{ "name": "pictureInPicture" }],
        "sessionID": "{sid}",
        "playhead": 60
      }
    }
  }]
}
```

>[!ENDTABS]

## Tipos de implementação herdada (somente Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Use `ADB.Media.createStateObject` e a constante `ADB.Media.PlayerState.PictureInPicture`:

```javascript
var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.PictureInPicture);

tracker.trackPlayerStateStart(stateObject);
tracker.trackPlayerStateEnd(stateObject);
```

>[!TAB Chromecast]

Use `ADBMobile.media.createStateObject` com a cadeia de caracteres `"pictureInPicture"` diretamente, pois o Chromecast não tem constantes `PlayerState` nomeadas:

```javascript
var stateObject = ADBMobile.media.createStateObject("pictureInPicture");
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateStart, stateObject);
// When the viewer exits picture-in-picture:
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateEnd, stateObject);
```

>[!TAB Roku 2.x]

O rastreamento do estado do player não está disponível no Roku 2.x SDK. Para rastrear estados do player, use o [Roku Edge SDK](/help/implementation/edge/roku.md).

>[!TAB API da coleção de mídia]

Enviar uma solicitação POST `stateStart` quando o picture-in-picture começar, e um POST `stateEnd` quando terminar:

```json
{
  "playerTime": { "playhead": 60, "ts": 1699523820000 },
  "eventType": "stateStart",
  "params": {
    "media.state.name": "pictureInPicture"
  }
}
```

Consulte a [Referência de eventos da API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) para obter a estrutura de solicitação completa.

>[!ENDTABS]
