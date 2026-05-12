---
title: Quadros soltos
description: Defina a contagem de quadros ignorados no objeto de QoE para que o back-end possa relatar a qualidade de queda de quadro.
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 12%

---


# Quadros soltos

>[!BEGINSHADEBOX]

*Esta página aborda a coleção de dados da variável **Quadros soltos**. Consulte [Quadros soltos](/help/reporting/dimensions/dropped-frames.md) para obter a dimensão e a métrica de relatório correspondentes.*

>[!ENDSHADEBOX]

A variável dropped frames é a contagem de quadros que o reprodutor derrubou durante a sessão. Defina-o no objeto de QoE e atualize o valor sempre que o reprodutor relatar novas quedas. O backend relata o valor mais recente no fechamento da sessão.

| Propriedade | Valor |
| --- | --- |
| **Variável de dados de contexto** | `a.media.qoe.droppedFrameCount` |
| **Campo da coleção XDM** | [`mediaCollection.qoeDataDetails.droppedFrames`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-collection) |
| **Obrigatório** | Não |
| **Enviado com** | Eventos de qualidade, fechamento de sessão |

## SDK da web

Definir `droppedFrames` dentro de `mediaCollection.qoeDataDetails` ao chamar [`sendEvent`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/collection/js/commands/sendevent/overview):

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.bitrateChange",
    mediaCollection: {
      qoeDataDetails: {
        bitrate: 3200,
        droppedFrames: 3
      },
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

## SDK móvel

Passar quadros ignorados como quarto argumento para `createQoEObject`. Atualize o rastreador antes de qualquer evento de qualidade ser acionado.

**iOS (Swift)**

```swift
let qoeObject = Media.createQoEObjectWith(bitrate: 3200,
                                       startupTime: 0,
                                               fps: 24,
                                     droppedFrames: 3)

tracker.updateQoEObject(qoe: qoeObject)
```

**Android (Kotlin)**

```kotlin
val qoeObject = Media.createQoEObject(3200L,
                                      0.0,
                                      24.0,
                                      3L)

tracker.updateQoEObject(qoeObject)
```

## Roku (BrightScript)

Definir `droppedFrames` dentro de `mediaCollection.qoeDataDetails` ao chamar `sendMediaEvent`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.bitrateChange",
        "mediaCollection": {
            "qoeDataDetails": {
                "bitrate": 3200,
                "droppedFrames": 3
            },
            "playhead": 90
        }
    }
})
```

## API de borda de mídia

Chame o ponto de extremidade [bitrateChange](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/bitratechange/#bitratechange) com `droppedFrames` dentro de `mediaCollection.qoeDataDetails`:

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.bitrateChange",
      "mediaCollection": {
        "qoeDataDetails": {
          "droppedFrames": 3
        },
        "sessionID": "{sid}",
        "playhead": 90
      }
    }
  }]
}
```

## SDK de mídia

Passar quadros ignorados como quarto argumento para `ADB.Media.createQoEObject`:

```javascript
var qoeObject = ADB.Media.createQoEObject(3200, 0, 24, 3);
tracker.updateQoEObject(qoeObject);
```

## API da coleção de mídia

Incluir `media.qoe.droppedFrames` no objeto `params`:

```json
{
  "playerTime": { "playhead": 90, "ts": 1699523820000 },
  "eventType": "bitrateChange",
  "params": {
    "media.qoe.droppedFrames": 3
  }
}
```

Consulte a [Referência de eventos da API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) para obter a estrutura de solicitação completa.
