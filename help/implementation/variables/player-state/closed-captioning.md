---
title: Legendas ocultas
description: Rastreie quando o visualizador ativa e desativa as legendas ocultas para que o back-end possa relatar o envolvimento de legendas.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 5%

---


# Legendas ocultas

>[!BEGINSHADEBOX]

*Esta página aborda a coleta de dados para o estado de player **Legendas ocultas**. Consulte [Fluxos afetados pelas legendas ocultas](/help/reporting/metrics/closed-captioning-streams-impacted.md), [Contagens de legendas ocultas](/help/reporting/metrics/closed-captioning-count.md) e [Duração total das legendas ocultas](/help/reporting/metrics/closed-captioning-total-duration.md) para as métricas de relatório correspondentes.*

>[!ENDSHADEBOX]

O estado das legendas ocultas do player é rastreado quando o visualizador ativa e desativa as legendas. Acione um evento de início de estado quando as legendas estiverem ativadas e um evento de fim de estado quando as legendas estiverem desativadas. O back-end calcula três métricas desses eventos: fluxos afetados, contagem de entradas de estado e tempo total no estado.

| Propriedade | Valor |
| --- | --- |
| **Variáveis de dados de contexto** | `a.media.states.closedcaptioning.set`, `a.media.states.closedcaptioning.count`, `a.media.states.closedcaptioning.time` |
| **Campo da coleção XDM** | [`xdm.mediaCollection.statesStart[]`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/media-collection-details) e [`xdm.mediaCollection.statesEnd[]`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/media-collection-details) (entradas com `name: "closedCaptioning"`) |
| **Características do Audience Manager** | `c_contextdata.a.media.states.closedcaptioning.set`, `c_contextdata.a.media.states.closedcaptioning.count`, `c_contextdata.a.media.states.closedcaptioning.time` |
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
      statesStart: [{ name: "closedCaptioning" }],
      sessionID: "{sid}",
      playhead: 60
    }
  }
});
```

Quando o visualizador desabilitar legendas, enviar outro evento com o estado em `statesEnd`:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesEnd: [{ name: "closedCaptioning" }],
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

>[!TAB iOS]

Use `tracker.trackPlayerStateStart()` e `tracker.trackPlayerStateEnd()` com a constante `MediaConstants.PlayerState.CLOSED_CAPTION`.

```swift
let stateObject = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.CLOSED_CAPTION)

tracker.trackPlayerStateStart(info: stateObject)
tracker.trackPlayerStateEnd(info: stateObject)
```

>[!TAB Android]

Use `tracker.trackPlayerStateStart()` e `tracker.trackPlayerStateEnd()` com a constante `MediaConstants.PlayerState.CLOSED_CAPTION`.

```kotlin
val stateObject = Media.createStateObject(MediaConstants.PlayerState.CLOSED_CAPTION)

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
            "statesStart": [{ "name": "closedCaptioning" }],
            "playhead": 60
        }
    }
})
```

Quando o visualizador desabilitar legendas, enviar outro evento com o estado em `statesEnd`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesEnd": [{ "name": "closedCaptioning" }],
            "playhead": 90
        }
    }
})
```

>[!TAB API do Media Edge]

Chame o ponto de extremidade [statesUpdate](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/statesupdate/) com `closedCaptioning` em `statesStart` (ou `statesEnd` quando o visualizador desabilitar legendas):

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.statesUpdate",
      "mediaCollection": {
        "statesStart": [{ "name": "closedCaptioning" }],
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

Use `ADB.Media.createStateObject` e a constante `ADB.Media.PlayerState.ClosedCaptioning`:

```javascript
var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.ClosedCaptioning);

tracker.trackPlayerStateStart(stateObject);
tracker.trackPlayerStateEnd(stateObject);
```

>[!TAB Chromecast]

Use `ADBMobile.media.createStateObject` com a cadeia de caracteres `"closedCaptioning"` diretamente, pois o Chromecast não tem constantes `PlayerState` nomeadas:

```javascript
var stateObject = ADBMobile.media.createStateObject("closedCaptioning");
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateStart, stateObject);
// When the viewer disables captions:
ADBMobile.media.trackEvent(ADBMobile.media.Event.StateEnd, stateObject);
```

>[!TAB Roku 2.x]

O rastreamento do estado do player não está disponível no Roku 2.x SDK. Para rastrear estados do player, use o [Roku Edge SDK](/help/implementation/edge/roku.md).

>[!TAB API da coleção de mídia]

Enviar uma solicitação POST `stateStart` quando as legendas estiverem habilitadas, e uma POST `stateEnd` quando estiverem desabilitadas:

```json
{
  "playerTime": { "playhead": 60, "ts": 1699523820000 },
  "eventType": "stateStart",
  "params": {
    "media.state.name": "closedCaptioning"
  }
}
```

Consulte a [Referência de eventos da API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) para obter a estrutura de solicitação completa.

>[!ENDTABS]
