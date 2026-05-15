---
title: Em foco
description: Rastreie quando o reprodutor está em foco na tela do visualizador para que o back-end possa relatar o envolvimento do foco.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '290'
ht-degree: 8%

---


# Em foco

>[!BEGINSHADEBOX]

*Esta página aborda a coleta de dados para o estado do player **Em foco**. Consulte [Fluxos afetados pela função em foco](/help/reporting/metrics/in-focus-streams-impacted.md), [Contagens em foco](/help/reporting/metrics/in-focus-count.md) e [Duração total em foco](/help/reporting/metrics/in-focus-total-duration.md) para as métricas de relatório correspondentes.*

>[!ENDSHADEBOX]

O estado do player em foco é rastreado quando o player tem a atenção do visualizador. Acione um evento de início de estado quando o reprodutor obtém foco (normalmente quando a guia ou janela do reprodutor se torna ativa) e um evento de fim de estado quando o reprodutor perde foco. O back-end calcula três métricas desses eventos: fluxos afetados, contagem de entradas de estado e tempo total no estado.

| Propriedade | Valor |
| --- | --- |
| **Variáveis de dados de contexto** | `a.media.states.infocus.set`, `a.media.states.infocus.count`, `a.media.states.infocus.time` |
| **Campo da coleção XDM** | [`mediaCollection.statesStart[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-collection-details) e [`mediaCollection.statesEnd[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-collection-details) (entradas com `name: "inFocus"`) |
| **Características do Audience Manager** | `c_contextdata.a.media.states.infocus.set`, `c_contextdata.a.media.states.infocus.count`, `c_contextdata.a.media.states.infocus.time` |
| **Obrigatório** | Não |
| **Enviado com** | [Início do estado](/help/implementation/events/player-state/state-start.md), [término do estado](/help/implementation/events/player-state/state-end.md) |

## SDK da web

Use [`sendEvent`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/collection/js/commands/sendevent/overview) para enviar um evento `media.statesUpdate` com o estado adicionado a `statesStart`:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesStart: [{ name: "inFocus" }],
      sessionID: "{sid}",
      playhead: 60
    }
  }
});
```

Quando o reprodutor perder o foco, envie outro evento com o estado em `statesEnd`:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesEnd: [{ name: "inFocus" }],
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

## SDK móvel

Use `tracker.trackPlayerStateStart()` e `tracker.trackPlayerStateEnd()` com a constante `MediaConstants.PlayerState.IN_FOCUS`.

**iOS (Swift)**

```swift
let stateObject = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.IN_FOCUS)

tracker.trackPlayerStateStart(info: stateObject)
tracker.trackPlayerStateEnd(info: stateObject)
```

**Android (Kotlin)**

```kotlin
val stateObject = Media.createStateObject(MediaConstants.PlayerState.IN_FOCUS)

tracker.trackPlayerStateStart(stateObject)
tracker.trackPlayerStateEnd(stateObject)
```

## Roku (BrightScript)

Use `sendMediaEvent` para enviar um evento `media.statesUpdate` com o estado adicionado a `statesStart`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesStart": [{ "name": "inFocus" }],
            "playhead": 60
        }
    }
})
```

Quando o reprodutor perder o foco, envie outro evento com o estado em `statesEnd`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesEnd": [{ "name": "inFocus" }],
            "playhead": 90
        }
    }
})
```

## API de borda de mídia

Chame o ponto de extremidade [statesUpdate](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/statesupdate/) com `inFocus` em `statesStart` (ou `statesEnd` quando o player perder o foco):

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.statesUpdate",
      "mediaCollection": {
        "statesStart": [{ "name": "inFocus" }],
        "sessionID": "{sid}",
        "playhead": 60
      }
    }
  }]
}
```

## SDK de mídia

Use `ADB.Media.createStateObject` e a constante `ADB.Media.PlayerState.InFocus`:

```javascript
var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.InFocus);

tracker.trackPlayerStateStart(stateObject);
tracker.trackPlayerStateEnd(stateObject);
```

## API da coleção de mídia

Envie uma solicitação POST `stateStart` quando o player ganhar o foco e uma POST `stateEnd` quando ele perder o foco:

```json
{
  "playerTime": { "playhead": 60, "ts": 1699523820000 },
  "eventType": "stateStart",
  "params": {
    "media.state.name": "inFocus"
  }
}
```

Consulte a [Referência de eventos da API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) para obter a estrutura de solicitação completa.
