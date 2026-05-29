---
title: Taxa de bits
description: Defina a taxa de bits de reprodução atual (em kbps) no objeto de QoE para que o back-end possa calcular métricas de taxa de bits.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '288'
ht-degree: 6%

---


# Taxa de bits

>[!BEGINSHADEBOX]

*Esta página aborda a coleta de dados da variável **Taxa de bits**. Consulte [[!UICONTROL Taxa média de bits] (dimensão)](/help/reporting/dimensions/average-bitrate.md) e [[!UICONTROL Taxa média de bits] (métrica)](/help/reporting/metrics/average-bitrate.md) para as variáveis de relatório correspondentes.*

>[!ENDSHADEBOX]

A variável bitrate é a taxa de bits de reprodução atual, em kilobits por segundo. Defina-o no objeto de QoE sempre que o player negociar uma taxa de bits e atualize o objeto de QoE quando a taxa de bits mudar. A infraestrutura usa valores de taxa de bits para calcular a [[!UICONTROL taxa de bits média]](/help/reporting/metrics/average-bitrate.md), a dimensão por bloco de taxa de bits e a métrica [[!UICONTROL alterações na taxa de bits]](/help/reporting/metrics/bitrate-changes.md).

| Propriedade | Valor |
| --- | --- |
| **Variável de dados de contexto** | `a.media.qoe.bitrateAverageBucket` |
| **Campo da coleção XDM** | [`xdm.mediaCollection.qoeDataDetails.bitrate`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-collection) |
| **Característica do Audience Manager** | `c_contextdata.a.media.qoe.bitrateAverageBucket` |
| **Obrigatório** | Não |
| **Enviado com** | Eventos de qualidade ([alteração na taxa de bits](/help/implementation/events/playback/bitrate-change.md), [início do buffer](/help/implementation/events/playback/buffer-start.md), [erro](/help/implementation/events/error.md)), fechamento da sessão |

## Tipos de implementação recomendados

>[!BEGINTABS]

>[!TAB Web SDK]

Defina `bitrate` dentro de `xdm.mediaCollection.qoeDataDetails` em `media.bitrateChange` (ou qualquer evento relacionado à qualidade) ao chamar [`sendEvent`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/collection/js/commands/sendevent/overview):

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

>[!TAB iOS]

Transmita a taxa de bits como o primeiro argumento para `createQoEObject`. Atualize o objeto de QoE no rastreador antes de qualquer evento de qualidade ser acionado.

```swift
let qoeObject = Media.createQoEObjectWith(bitrate: 3200,
                                       startupTime: 0,
                                               fps: 24,
                                     droppedFrames: 0)

tracker.updateQoEObject(qoe: qoeObject)
```

>[!TAB Android]

Transmita a taxa de bits como o primeiro argumento para `createQoEObject`. Atualize o objeto de QoE no rastreador antes de qualquer evento de qualidade ser acionado.

```kotlin
val qoeObject = Media.createQoEObject(3200L,
                                      0.0,
                                      24.0,
                                      0L)

tracker.updateQoEObject(qoeObject)
```

>[!TAB Roku]

Defina `bitrate` dentro de `xdm.mediaCollection.qoeDataDetails` ao chamar `sendMediaEvent` para eventos de qualidade como `media.bitrateChange`:

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

>[!TAB API do Media Edge]

Chame o ponto de extremidade [bitrateChange](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/bitratechange/#bitratechange) com `bitrate` dentro de `xdm.mediaCollection.qoeDataDetails`:

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

>[!ENDTABS]

## Tipos de implementação herdada (somente Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

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

>[!TAB Chromecast]

Transmita a taxa de bits em kbps como o primeiro argumento para `ADBMobile.media.createQoSObject` e atualize o rastreador:

```javascript
var qosInfo = ADBMobile.media.createQoSObject(
  3200,  // bitrate (kbps)
  0,     // startupTime
  24,    // fps
  0      // droppedFrames
);
ADBMobile.media.updateQoSObject(qosInfo);
```

>[!TAB API da coleção de mídia]

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

>[!ENDTABS]
