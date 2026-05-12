---
title: Mudo
description: Rastrear quando o visualizador ativar o som e desativar o som do áudio para que o back-end possa relatar o envolvimento do mudo.
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 10%

---


# Mudo

>[!BEGINSHADEBOX]

*Esta página aborda a coleta de dados para o estado do player **Mudo**. Consulte [Fluxos afetados pela função mudo](/help/reporting/metrics/mute-streams-impacted.md), [Contagens de mudo](/help/reporting/metrics/mute-count.md) e [Duração total da função mudo](/help/reporting/metrics/mute-total-duration.md) para as métricas de relatório correspondentes.*

>[!ENDSHADEBOX]

O estado mudo do player é rastreado quando o visualizador silencia e desativa o áudio. Acione um evento de início de estado quando o visualizador for silenciado e um evento de fim de estado quando o visualizador for desativado. O back-end calcula três métricas desses eventos: fluxos afetados, contagem de entradas de estado e tempo total no estado.

| Propriedade | Valor |
| --- | --- |
| **Variáveis de dados de contexto** | `a.media.states.mute.set`, `a.media.states.mute.count`, `a.media.states.mute.time` |
| **Campo da coleção XDM** | [`mediaCollection.statesStart[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-collection-details) e [`mediaCollection.statesEnd[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-collection-details) (entradas com `name: "mute"`) |
| **Obrigatório** | Não |
| **Enviado com** | Início do estado, término do estado |

## SDK da web

Use [`sendEvent`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/collection/js/commands/sendevent/overview) para enviar um evento `media.statesUpdate` com o estado adicionado a `statesStart`:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesStart: [{ name: "mute" }],
      sessionID: "{sid}",
      playhead: 60
    }
  }
});
```

Quando o visualizador ativar a função mudo, enviar outro evento com o estado em `statesEnd`:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.statesUpdate",
    mediaCollection: {
      statesEnd: [{ name: "mute" }],
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

## SDK móvel

Use `tracker.trackPlayerStateStart()` e `tracker.trackPlayerStateEnd()` com a constante `MediaConstants.PlayerState.MUTE`.

**iOS (Swift)**

```swift
let stateObject = Media.createStateObjectWith(stateName: MediaConstants.PlayerState.MUTE)

tracker.trackPlayerStateStart(info: stateObject)
tracker.trackPlayerStateEnd(info: stateObject)
```

**Android (Kotlin)**

```kotlin
val stateObject = Media.createStateObject(MediaConstants.PlayerState.MUTE)

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
            "statesStart": [{ "name": "mute" }],
            "playhead": 60
        }
    }
})
```

Quando o visualizador ativar a função mudo, enviar outro evento com o estado em `statesEnd`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.statesUpdate",
        "mediaCollection": {
            "statesEnd": [{ "name": "mute" }],
            "playhead": 90
        }
    }
})
```

## API de borda de mídia

Chame o ponto de extremidade [statesUpdate](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/statesupdate/) com `mute` em `statesStart` (ou `statesEnd` quando o visualizador ativar o áudio):

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.statesUpdate",
      "mediaCollection": {
        "statesStart": [{ "name": "mute" }],
        "sessionID": "{sid}",
        "playhead": 60
      }
    }
  }]
}
```

## SDK de mídia

Use `ADB.Media.createStateObject` e a constante `ADB.Media.PlayerState.Mute`:

```javascript
var stateObject = ADB.Media.createStateObject(ADB.Media.PlayerState.Mute);

tracker.trackPlayerStateStart(stateObject);
tracker.trackPlayerStateEnd(stateObject);
```

## API da coleção de mídia

Envie uma solicitação POST `stateStart` quando o visualizador ativar o som, e uma POST `stateEnd` quando o som for ativado:

```json
{
  "playerTime": { "playhead": 60, "ts": 1699523820000 },
  "eventType": "stateStart",
  "params": {
    "media.state.name": "mute"
  }
}
```

Consulte a [Referência de eventos da API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) para obter a estrutura de solicitação completa.
