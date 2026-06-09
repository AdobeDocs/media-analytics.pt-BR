---
title: Quadros por segundo
description: Defina a taxa de quadros atual no objeto de QoE para que o back-end tenha contexto de taxa de quadros para os relatórios de qualidade.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 7%

---


# Quadros por segundo

A variável frames por segundo é a taxa de quadros atual do fluxo. Defina-o no objeto de QoE ao lado da taxa de bits e dos quadros soltos, para que o back-end tenha um contexto de qualidade total para cada sessão de reprodução. O Adobe Analytics não cria automaticamente uma variável de relatório para a taxa de quadros; crie uma regra de processamento personalizada se desejar que ela apareça como um relatório.

| Propriedade | Valor |
| --- | --- |
| **Variável de dados de contexto** | Nenhum (o Adobe Analytics não atribui uma chave de dados de contexto reservada para a taxa de quadros) |
| **Campo da coleção XDM** | [`xdm.mediaCollection.qoeDataDetails.framesPerSecond`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-collection) |
| **Característica do Audience Manager** | N/D |
| **Obrigatório** | Não |
| **Enviado com** | Eventos de qualidade ([alteração na taxa de bits](/help/implementation/events/playback/bitrate-change.md), [início do buffer](/help/implementation/events/playback/buffer-start.md), [erro](/help/implementation/events/error.md)), fechamento da sessão |

## Tipos de implementação recomendados

>[!BEGINTABS]

>[!TAB Web SDK]

Definir `framesPerSecond` dentro de `xdm.mediaCollection.qoeDataDetails` ao chamar [`sendEvent`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/collection/js/commands/sendevent/overview):

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

>[!TAB iOS]

Transmita a taxa de quadros como o terceiro argumento (`fps`) para `createQoEObject`.

```swift
let qoeObject = Media.createQoEObjectWith(bitrate: 3200,
                                       startupTime: 0,
                                               fps: 24,
                                     droppedFrames: 0)

tracker.updateQoEObject(qoe: qoeObject)
```

>[!TAB Android]

Transmita a taxa de quadros como o terceiro argumento (`fps`) para `createQoEObject`.

```kotlin
val qoeObject = Media.createQoEObject(3200L,
                                      0.0,
                                      24.0,
                                      0L)

tracker.updateQoEObject(qoeObject)
```

>[!TAB Roku Edge]

Definir `framesPerSecond` dentro de `xdm.mediaCollection.qoeDataDetails` ao chamar `sendMediaEvent`:

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

>[!TAB API do Media Edge]

Chame o ponto de extremidade [bitrateChange](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/bitratechange/#bitratechange) com `framesPerSecond` dentro de `xdm.mediaCollection.qoeDataDetails`:

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

>[!ENDTABS]

## Tipos de implementação herdada (somente Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Transmita a taxa de quadros como o terceiro argumento para `ADB.Media.createQoEObject`:

```javascript
var qoeObject = ADB.Media.createQoEObject(3200, 0, 24, 0);
tracker.updateQoEObject(qoeObject);
```

>[!TAB Chromecast]

Transmita a taxa de quadros como o terceiro argumento (`fps`) para `ADBMobile.media.createQoSObject` e atualize o rastreador:

```javascript
var qosInfo = ADBMobile.media.createQoSObject(
  3200,  // bitrate
  0,     // startupTime
  24,    // fps
  0      // droppedFrames
);
ADBMobile.media.updateQoSObject(qosInfo);
```

>[!TAB Roku 2.x]

Passe a taxa de quadros como o terceiro argumento (`fps`) para `adb_media_init_qosinfo` e atualize o rastreador com `mediaUpdateQoS`:

```brightscript
adb = ADBMobile()
qosInfo = adb_media_init_qosinfo(3200.0, 0.0, 24.0, 0.0)  ' bitrate, startupTime, fps, droppedFrames

adb.mediaUpdateQoS(qosInfo)
```

>[!TAB API da coleção de mídia]

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

>[!ENDTABS]
