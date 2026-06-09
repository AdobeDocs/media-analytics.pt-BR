---
title: Tela cheia
description: Rastreie quando o visualizador entra e sai da reprodução em tela cheia, para que o back-end possa relatar o envolvimento em tela cheia.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '333'
ht-degree: 6%

---


# Tela cheia

>[!BEGINSHADEBOX]

*Esta página aborda a coleta de dados para o estado do player **Tela cheia**. Consulte [Fluxos afetados pela tela cheia](/help/reporting/metrics/full-screen-streams-impacted.md), [Contagens de tela cheia](/help/reporting/metrics/full-screen-count.md) e [Duração total da tela cheia](/help/reporting/metrics/full-screen-total-duration.md) para as métricas de relatório correspondentes.*

>[!ENDSHADEBOX]

O estado do player em tela cheia é rastreado quando o visualizador entra e sai da reprodução em tela cheia. Acione um evento de início de estado sempre que o visualizador entrar em tela cheia e um evento de fim de estado quando o visualizador sair. O back-end calcula três métricas desses eventos: fluxos afetados, contagem de entradas de estado e tempo total no estado.

| Propriedade | Valor |
| --- | --- |
| **Variáveis de dados de contexto** | `a.media.states.fullscreen.set`, `a.media.states.fullscreen.count`, `a.media.states.fullscreen.time` |
| **Campo da coleção XDM** | [`xdm.mediaCollection.statesStart[]`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/media-collection-details) e [`xdm.mediaCollection.statesEnd[]`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/media-collection-details) (entradas com `name: "fullscreen"`) |
| **Características do Audience Manager** | `c_contextdata.a.media.states.fullscreen.set`, `c_contextdata.a.media.states.fullscreen.count`, `c_contextdata.a.media.states.fullscreen.time` |
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
      statesStart: [{ name: "fullscreen" }],
      sessionID: "{sid}",
      playhead: 60
    }
  }
});
```

Quando o visualizador sair da tela cheia, envie outro evento com o estado em `statesEnd`:

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

>[!TAB iOS]

Use `tracker.trackPlayerStateStart()` e `tracker.trackPlayerStateEnd()` com a constante `MediaConstants.PlayerState.FULLSCREEN`.

```swift
let stateObject = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.FULLSCREEN)

tracker.trackPlayerStateStart(info: stateObject)
// ...later, when the user exits full-screen:
tracker.trackPlayerStateEnd(info: stateObject)
```

>[!TAB Android]

Use `tracker.trackPlayerStateStart()` e `tracker.trackPlayerStateEnd()` com a constante `MediaConstants.PlayerState.FULLSCREEN`.

```kotlin
val stateObject = Media.createStateObject(MediaConstants.PlayerState.FULLSCREEN)

tracker.trackPlayerStateStart(stateObject)
// ...later, when the user exits full-screen:
tracker.trackPlayerStateEnd(stateObject)
```

>[!TAB Roku Edge]

Use `sendMediaEvent` para enviar um evento `media.statesUpdate` com o estado adicionado a `statesStart`:

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

Quando o visualizador sair da tela cheia, envie outro evento com o estado em `statesEnd`:

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

Chame o ponto de extremidade [statesUpdate](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/statesupdate/) com `fullscreen` em `statesStart` (ou `statesEnd` quando o visualizador sair):

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.statesUpdate",
      "mediaCollection": {
        "statesStart": [{ "name": "fullscreen" }],
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

Use `ADB.Media.createStateObject` e a constante `ADB.Media.PlayerState.FullScreen`:

```javascript
var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.FullScreen);

tracker.trackPlayerStateStart(stateObject);
// ...later, when the user exits full-screen:
tracker.trackPlayerStateEnd(stateObject);
```

>[!TAB Chromecast]

Use `ADBMobile.media.createStateObject` com a cadeia de caracteres `"fullscreen"` diretamente, pois o Chromecast não tem constantes `PlayerState` nomeadas:

```javascript
var stateObject = ADBMobile.media.createStateObject("fullscreen");
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateStart, stateObject);
// When the user exits full-screen:
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateEnd, stateObject);
```

>[!TAB Roku 2.x]

O rastreamento do estado do player não está disponível no Roku 2.x SDK. Para rastrear estados do player, use o [Roku Edge SDK](/help/implementation/edge/roku.md).

>[!TAB API da coleção de mídia]

Envie uma solicitação de POST `stateStart` quando o visualizador entrar em tela cheia, e uma POST `stateEnd` quando eles saírem:

```json
{
  "playerTime": { "playhead": 60, "ts": 1699523820000 },
  "eventType": "stateStart",
  "params": {
    "media.state.name": "fullscreen"
  }
}
```

```json
{
  "playerTime": { "playhead": 90, "ts": 1699523850000 },
  "eventType": "stateEnd",
  "params": {
    "media.state.name": "fullscreen"
  }
}
```

Consulte a [Referência de eventos da API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) para obter a estrutura de solicitação completa.

>[!ENDTABS]
