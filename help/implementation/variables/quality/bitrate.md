---
title: Taxa de bits
description: Defina a taxa de bits de reprodução atual (em kbps) no objeto de QoE para que o back-end possa calcular métricas de taxa de bits.
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 10%

---


# Taxa de bits

>[!BEGINSHADEBOX]

*Esta página aborda a coleta de dados da variável **Taxa de bits**. Consulte [Taxa média de bits (dimensão)](/help/reporting/dimensions/average-bitrate.md) e [Taxa média de bits (métrica)](/help/reporting/metrics/average-bitrate.md) para as variáveis de relatório correspondentes.*

>[!ENDSHADEBOX]

A variável bitrate é a taxa de bits de reprodução atual, em kilobits por segundo. Defina-o no objeto de QoE sempre que o player negociar uma taxa de bits e atualize o objeto de QoE quando a taxa de bits mudar. O back-end usa valores de taxa de bits para calcular a taxa média de bits, a dimensão por taxa de bits e a métrica de alterações na taxa de bits.

| Propriedade | Valor |
| --- | --- |
| **Variável de dados de contexto** | `a.media.qoe.bitrateAverageBucket` |
| **Campo da coleção XDM** | [`mediaCollection.qoeDataDetails.bitrate`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-collection) |
| **Obrigatório** | Não |
| **Enviado com** | Eventos de qualidade (alteração da taxa de bits, buffer, erro), fechamento da sessão |

## SDK da web

Defina `bitrate` dentro de `mediaCollection.qoeDataDetails` em `media.bitrateChange` (ou qualquer evento relacionado à qualidade) ao chamar [`sendEvent`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/collection/js/commands/sendevent/overview):

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.bitrateChange",
    mediaCollection: {
      qoeDataDetails: {
        bitrate: 3200,
        droppedFrames: 0,
        framesPerSecond: 24,
        timeToStart: 0
      },
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

## SDK móvel

Transmita a taxa de bits como o primeiro argumento para `createQoEObject`. Atualize o objeto de QoE no rastreador antes de qualquer evento de qualidade ser acionado.

**iOS (Swift)**

```swift
let qoeObject = Media.createQoEObjectWith(bitrate: 3200,
                                       startupTime: 0,
                                               fps: 24,
                                     droppedFrames: 0)

tracker.updateQoEObject(qoe: qoeObject)
```

**Android (Kotlin)**

```kotlin
val qoeObject = Media.createQoEObject(3200L,
                                      0.0,
                                      24.0,
                                      0L)

tracker.updateQoEObject(qoeObject)
```

## Roku (BrightScript)

Defina `bitrate` dentro de `mediaCollection.qoeDataDetails` ao chamar `sendMediaEvent` para eventos de qualidade como `media.bitrateChange`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.bitrateChange",
        "mediaCollection": {
            "qoeDataDetails": {
                "bitrate": 3200,
                "droppedFrames": 0,
                "framesPerSecond": 24,
                "timeToStart": 0
            },
            "playhead": 90
        }
    }
})
```

## API de borda de mídia

Chame o ponto de extremidade [bitrateChange](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/bitratechange/#bitratechange) com `bitrate` dentro de `mediaCollection.qoeDataDetails`:

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.bitrateChange",
      "mediaCollection": {
        "qoeDataDetails": {
          "bitrate": 3200
        },
        "sessionID": "{sid}",
        "playhead": 90
      }
    }
  }]
}
```

## SDK de mídia

Passe a taxa de bits como primeiro argumento para `ADB.Media.createQoEObject` e atualize o rastreador:

```javascript
var qoeObject = ADB.Media.createQoEObject(
  3200,  // bitrate (kbps)
  0,     // startup time (ms)
  24,    // fps
  0      // dropped frames
);

tracker.updateQoEObject(qoeObject);
```

## API da coleção de mídia

Inclua `media.qoe.bitrate` no objeto `params` de sua solicitação POST `bitrateChange`:

```json
{
  "playerTime": { "playhead": 90, "ts": 1699523820000 },
  "eventType": "bitrateChange",
  "params": {
    "media.qoe.bitrate": 3200
  }
}
```

Consulte a [Referência de eventos da API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) para obter a estrutura de solicitação completa.
