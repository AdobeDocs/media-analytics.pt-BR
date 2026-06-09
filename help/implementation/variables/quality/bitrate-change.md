---
title: Alteração da taxa de bits
description: Acione um evento de alteração de taxa de bits sempre que o reprodutor alternar para uma taxa de bits diferente.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '278'
ht-degree: 6%

---


# Alteração da taxa de bits

>[!BEGINSHADEBOX]

*Esta página aborda como implementar eventos de alteração na taxa de bits. Consulte [[!UICONTROL Alterações na taxa de bits] (dimensão)](/help/reporting/dimensions/bitrate-changes.md) e [[!UICONTROL Alterações na taxa de bits] (métrica)](/help/reporting/metrics/bitrate-changes.md) para as variáveis de relatório correspondentes.*

>[!ENDSHADEBOX]

O evento de alteração da taxa de bits indica que o reprodutor mudou para uma taxa de bits diferente. Atualize primeiro o valor [Bitrate](/help/implementation/variables/quality/bitrate.md) no objeto de QoE e, em seguida, acione o evento de alteração de taxa de bits. O back-end usa a contagem desses eventos para calcular a dimensão [[!UICONTROL Alterações na taxa de bits]](/help/reporting/dimensions/bitrate-changes.md) e a métrica [[!UICONTROL Alterações na taxa de bits]](/help/reporting/metrics/bitrate-changes.md), e os valores de taxa de bits resultantes alimentam a [[!UICONTROL Taxa de bits média]](/help/reporting/metrics/average-bitrate.md).

| Propriedade | Valor |
| --- | --- |
| **Variável de dados de contexto** | (nenhum — contado pelo back-end) |
| **Tipo de evento XDM** | `media.bitrateChange` |
| **Característica do Audience Manager** | `c_contextdata.a.media.qoe.bitrateChangeCount` |
| **Obrigatório** | Não |
| **Enviado com** | [Alteração na taxa de bits](/help/implementation/events/playback/bitrate-change.md) |

## Tipos de implementação recomendados

>[!BEGINTABS]

>[!TAB Web SDK]

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

>[!TAB iOS]

Atualize o objeto de QoE com a nova taxa de bits e acione o evento de alteração da taxa de bits.

```swift
let qoeObject = Media.createQoEObjectWith(bitrate: 4500,
                                       startupTime: 0,
                                               fps: 24,
                                     droppedFrames: 0)
tracker.updateQoEObject(qoe: qoeObject)
tracker.trackEvent(event: MediaEvent.BitrateChange, info: nil, metadata: nil)
```

>[!TAB Android]

Atualize o objeto de QoE com a nova taxa de bits e acione o evento de alteração da taxa de bits.

```kotlin
val qoeObject = Media.createQoEObject(4500L, 0.0, 24.0, 0L)
tracker.updateQoEObject(qoeObject)
tracker.trackEvent(Media.Event.BitrateChange, null, null)
```

>[!TAB Roku Edge]

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

>[!TAB API do Media Edge]

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

>[!ENDTABS]

## Tipos de implementação herdada (somente Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Atualize o objeto de QoE e acione o evento:

```javascript
var qoeObject = ADB.Media.createQoEObject(4500, 0, 24, 0);
tracker.updateQoEObject(qoeObject);
tracker.trackEvent(ADB.Media.Event.BitrateChange);
```

>[!TAB Chromecast]

Atualize o objeto de QoS com a nova taxa de bits e acione o evento de alteração da taxa de bits:

```javascript
var qosInfo = ADBMobile.media.createQoSObject(
  4500,  // bitrate (kbps)
  0,     // startupTime
  24,    // fps
  0      // droppedFrames
);
ADBMobile.media.updateQoSObject(qosInfo);
ADBMobile.media.trackEvent(ADBMobile.media.Event.BitrateChange);
```

>[!TAB Roku 2.x]

Atualize o objeto de QoS com a nova taxa de bits e acione o evento de alteração da taxa de bits:

```brightscript
adb = ADBMobile()
qosInfo = adb_media_init_qosinfo(4500.0, 0.0, 24.0, 0.0)  ' bitrate, startupTime, fps, droppedFrames

adb.mediaUpdateQoS(qosInfo)
adb.mediaTrackEvent(adb.MEDIA_BITRATE_CHANGE)
```

>[!TAB API da coleção de mídia]

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

>[!ENDTABS]
