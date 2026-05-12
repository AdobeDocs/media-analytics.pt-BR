---
title: Alteração da taxa de bits
description: Acione um evento de alteração de taxa de bits sempre que o reprodutor alternar para uma taxa de bits diferente.
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 11%

---


# Alteração da taxa de bits

>[!BEGINSHADEBOX]

*Esta página aborda como implementar eventos de alteração na taxa de bits. Consulte [Alterações na taxa de bits (dimensão)](/help/reporting/dimensions/bitrate-changes.md) e [Alterações na taxa de bits (métrica)](/help/reporting/metrics/bitrate-changes.md) para as variáveis de relatório correspondentes.*

>[!ENDSHADEBOX]

O evento de alteração da taxa de bits indica que o reprodutor mudou para uma taxa de bits diferente. Atualize primeiro o valor [Bitrate](/help/implementation/variables/quality/bitrate.md) no objeto de QoE e, em seguida, acione o evento de alteração de taxa de bits. O back-end usa a contagem desses eventos para calcular a dimensão e a métrica de alterações na taxa de bits, e os valores de taxa de bits resultantes alimentam a taxa de bits média.

| Propriedade | Valor |
| --- | --- |
| **Variável de dados de contexto** | (nenhum — contado pelo back-end) |
| **Tipo de evento XDM** | `media.bitrateChange` |
| **Obrigatório** | Não |
| **Enviado com** | Sempre que o reprodutor altera a taxa de bits |

## SDK da web

Use [`sendEvent`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/collection/js/commands/sendevent/overview) para enviar um evento `media.bitrateChange` com a nova taxa de bits:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.bitrateChange",
    mediaCollection: {
      qoeDataDetails: {
        bitrate: 4500,
        droppedFrames: 0,
        framesPerSecond: 24,
        timeToStart: 0
      },
      sessionID: "{sid}",
      playhead: 120
    }
  }
});
```

## SDK móvel

Atualize o objeto de QoE com a nova taxa de bits e acione o evento de alteração da taxa de bits.

**iOS (Swift)**

```swift
let qoeObject = Media.createQoEObjectWith(bitrate: 4500,
                                       startupTime: 0,
                                               fps: 24,
                                     droppedFrames: 0)
tracker.updateQoEObject(qoe: qoeObject)
tracker.trackEvent(event: MediaEvent.BitrateChange, info: nil, metadata: nil)
```

**Android (Kotlin)**

```kotlin
val qoeObject = Media.createQoEObject(4500L, 0.0, 24.0, 0L)
tracker.updateQoEObject(qoeObject)
tracker.trackEvent(Media.Event.BitrateChange, null, null)
```

## Roku (BrightScript)

Use `sendMediaEvent` com `media.bitrateChange` para sinalizar uma alteração na taxa de bits. Incluir a nova taxa de bits em `qoeDataDetails`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.bitrateChange",
        "mediaCollection": {
            "qoeDataDetails": {
                "bitrate": 4500,
                "droppedFrames": 0,
                "framesPerSecond": 24,
                "timeToStart": 0
            },
            "playhead": 120
        }
    }
})
```

## API de borda de mídia

Chame o ponto de extremidade [bitrateChange](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/bitratechange/#bitratechange) com o `qoeDataDetails` atualizado:

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.bitrateChange",
      "mediaCollection": {
        "qoeDataDetails": {
          "bitrate": 4500
        },
        "sessionID": "{sid}",
        "playhead": 120
      }
    }
  }]
}
```

## SDK de mídia

Atualize o objeto de QoE e acione o evento:

```javascript
var qoeObject = ADB.Media.createQoEObject(4500, 0, 24, 0);
tracker.updateQoEObject(qoeObject);
tracker.trackEvent(ADB.Media.Event.BitrateChange);
```

## API da coleção de mídia

Enviar uma solicitação POST `bitrateChange` com a nova taxa de bits:

```json
{
  "playerTime": { "playhead": 120, "ts": 1699523820000 },
  "eventType": "bitrateChange",
  "params": {
    "media.qoe.bitrate": 4500
  }
}
```

Consulte a [Referência de eventos da API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) para obter a estrutura de solicitação completa.
