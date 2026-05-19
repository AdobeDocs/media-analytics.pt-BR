---
title: Quadros por segundo
description: Defina a taxa de quadros atual no objeto de QoE para que o back-end tenha contexto de taxa de quadros para os relatórios de qualidade.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 12%

---


# Quadros por segundo

A variável frames por segundo é a taxa de quadros atual do fluxo. Defina-o no objeto de QoE ao lado da taxa de bits e dos quadros soltos, para que o back-end tenha um contexto de qualidade total para cada sessão de reprodução. O Adobe Analytics não cria automaticamente uma variável de relatório para a taxa de quadros; crie uma regra de processamento personalizada se desejar que ela apareça como um relatório.

| Propriedade | Valor |
| --- | --- |
| **Variável de dados de contexto** | Nenhum (o Adobe Analytics não atribui uma chave de dados de contexto reservada para a taxa de quadros) |
| **Campo da coleção XDM** | [`mediaCollection.qoeDataDetails.framesPerSecond`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/qoe-data-details-collection) |
| **Característica do Audience Manager** | N/D |
| **Obrigatório** | Não |
| **Enviado com** | Eventos de qualidade ([alteração na taxa de bits](/help/implementation/events/playback/bitrate-change.md), [início do buffer](/help/implementation/events/playback/buffer-start.md), [erro](/help/implementation/events/error.md)), fechamento da sessão |

## SDK da web

Definir `framesPerSecond` dentro de `mediaCollection.qoeDataDetails` ao chamar [`sendEvent`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/collection/js/commands/sendevent/overview):

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.bitrateChange",
    mediaCollection: {
      qoeDataDetails: {
        bitrate: 3200,
        framesPerSecond: 24
      },
      sessionID: "{sid}",
      playhead: 90
    }
  }
});
```

## SDK móvel

Transmita a taxa de quadros como o terceiro argumento (`fps`) para `createQoEObject`.

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

Definir `framesPerSecond` dentro de `mediaCollection.qoeDataDetails` ao chamar `sendMediaEvent`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.bitrateChange",
        "mediaCollection": {
            "qoeDataDetails": {
                "bitrate": 3200,
                "framesPerSecond": 24
            },
            "playhead": 90
        }
    }
})
```

## API de borda de mídia

Chame o ponto de extremidade [bitrateChange](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/bitratechange/#bitratechange) com `framesPerSecond` dentro de `mediaCollection.qoeDataDetails`:

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.bitrateChange",
      "mediaCollection": {
        "qoeDataDetails": {
          "framesPerSecond": 24
        },
        "sessionID": "{sid}",
        "playhead": 90
      }
    }
  }]
}
```

## SDK de mídia

Transmita a taxa de quadros como o terceiro argumento para `ADB.Media.createQoEObject`:

```javascript
var qoeObject = ADB.Media.createQoEObject(3200, 0, 24, 0);
tracker.updateQoEObject(qoeObject);
```

## API da coleção de mídia

Incluir `media.qoe.framesPerSecond` no objeto `params`:

```json
{
  "playerTime": { "playhead": 90, "ts": 1699523820000 },
  "eventType": "bitrateChange",
  "params": {
    "media.qoe.framesPerSecond": 24
  }
}
```

Consulte a [Referência de eventos da API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) para obter a estrutura de solicitação completa.
