---
title: Hora de início
description: Defina o tempo de inicialização do reprodutor, em milissegundos, para que o back-end possa relatar a qualidade do tempo até o primeiro quadro.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 12%

---


# Hora de início

>[!BEGINSHADEBOX]

*Esta página aborda a coleta de dados da variável **Hora de início**. Consulte [Hora de início](/help/reporting/dimensions/time-to-start.md) para obter a dimensão e a métrica de relatório correspondentes.*

>[!ENDSHADEBOX]

O tempo para iniciar a variável é o tempo decorrido, em milissegundos, entre o reprodutor iniciar a reprodução e a renderização do primeiro quadro. Defina-o no objeto QoE antes do acionamento do evento de início da sessão. O Adobe armazena e relata o valor em segundos; passa milissegundos e o Adobe converte ao assimilar.

| Propriedade | Valor |
| --- | --- |
| **Variável de dados de contexto** | `a.media.qoe.timeToStart` |
| **Campo da coleção XDM** | [`mediaCollection.qoeDataDetails.timeToStart`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/qoe-data-details-collection) |
| **Característica do Audience Manager** | `c_contextdata.a.media.qoe.timeToStart` |
| **Obrigatório** | Não |
| **Enviado com** | [Início da sessão](/help/implementation/events/session/session-start.md), fechamento da sessão |

## SDK da web

Definir `timeToStart` dentro de `mediaCollection.qoeDataDetails` em `media.sessionStart` ao chamar [`sendEvent`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/collection/js/commands/sendevent/overview):

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        name: "video-123",
        length: 128,
        contentType: "vod",
        playerName: "HTML5 Player",
        channel: "Sports",
        streamType: "video"
      },
      qoeDataDetails: {
        timeToStart: 30000
      },
      playhead: 0
    }
  }
});
```

## SDK móvel

Passa o tempo de inicialização como segundo argumento (`startupTime`) para `createQoEObject`.

**iOS (Swift)**

```swift
let qoeObject = Media.createQoEObjectWith(bitrate: 3200,
                                       startupTime: 30000,
                                               fps: 24,
                                     droppedFrames: 0)

tracker.updateQoEObject(qoe: qoeObject)
```

**Android (Kotlin)**

```kotlin
val qoeObject = Media.createQoEObject(3200L,
                                      30000.0,
                                      24.0,
                                      0L)

tracker.updateQoEObject(qoeObject)
```

## Roku (BrightScript)

Definir `timeToStart` dentro de `mediaCollection.qoeDataDetails` em `media.sessionStart` ao chamar `createMediaSession`:

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "name": "video-123",
                "length": 128,
                "contentType": "vod",
                "playerName": "Roku Player",
                "channel": "Sports",
                "streamType": "video"
            },
            "qoeDataDetails": {
                "timeToStart": 30000
            },
            "playhead": 0
        }
    }
})
```

## API de borda de mídia

Chame o ponto de extremidade [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) com `timeToStart` dentro de `mediaCollection.qoeDataDetails`:

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.sessionStart",
      "mediaCollection": {
        "sessionDetails": {
          "name": "video-123",
          "length": 128,
          "contentType": "vod",
          "playerName": "HTML5 Player",
          "channel": "Sports"
        },
        "qoeDataDetails": {
          "timeToStart": 30000
        },
        "playhead": 0
      }
    }
  }]
}
```

## SDK de mídia

Passar o tempo para iniciar como segundo argumento para `ADB.Media.createQoEObject`:

```javascript
var qoeObject = ADB.Media.createQoEObject(3200, 30000, 24, 0);
tracker.updateQoEObject(qoeObject);
```

## API da coleção de mídia

Incluir `media.qoe.timeToStart` no objeto `params` em `sessionStart`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.qoe.timeToStart": 30000
  }
}
```

Consulte a [Referência de sessões da API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md) para obter a estrutura de solicitação completa.
