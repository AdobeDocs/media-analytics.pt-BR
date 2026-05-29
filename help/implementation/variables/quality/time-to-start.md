---
title: Hora de início
description: Defina o tempo de inicialização do reprodutor, em milissegundos, para que o back-end possa relatar a qualidade do tempo até o primeiro quadro.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 6%

---


# Hora de início

>[!BEGINSHADEBOX]

*Esta página aborda a coleta de dados da variável **Hora de início**. Consulte [[!UICONTROL Hora de início]](/help/reporting/dimensions/time-to-start.md) para obter a dimensão e a métrica de relatório correspondentes.*

>[!ENDSHADEBOX]

O tempo para iniciar a variável é o tempo decorrido, em milissegundos, entre o reprodutor iniciar a reprodução e a renderização do primeiro quadro. Defina-o no objeto QoE antes do acionamento do evento de início da sessão. O Adobe armazena e relata o valor em segundos; passa milissegundos e o Adobe converte ao assimilar.

>[!IMPORTANT]
>
>Assim que o player começar a renderizar quadros de conteúdo, pare a atualização de `timeToStart`. O valor pode aumentar durante a fase inicial de buffering ou carregamento, mas deve ser tratado como fixo a partir do momento em que a reprodução começa. Continuar a atualizá-la após a renderização do primeiro quadro produz uma métrica [[!UICONTROL Hora de início]](/help/reporting/metrics/time-to-start.md) inflada ou incorreta.

| Propriedade | Valor |
| --- | --- |
| **Variável de dados de contexto** | `a.media.qoe.timeToStart` |
| **Campo da coleção XDM** | [`xdm.mediaCollection.qoeDataDetails.timeToStart`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-collection) |
| **Característica do Audience Manager** | `c_contextdata.a.media.qoe.timeToStart` |
| **Obrigatório** | Não |
| **Enviado com** | [Início da sessão](/help/implementation/events/session/session-start.md), fechamento da sessão |

## Tipos de implementação recomendados

>[!BEGINTABS]

>[!TAB Web SDK]

Definir `timeToStart` dentro de `xdm.mediaCollection.qoeDataDetails` em `media.sessionStart` ao chamar [`sendEvent`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/collection/js/commands/sendevent/overview):

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

>[!TAB iOS]

Passa o tempo de inicialização como segundo argumento (`startupTime`) para `createQoEObject`.

```swift
let qoeObject = Media.createQoEObjectWith(bitrate: 3200,
                                       startupTime: 30000,
                                               fps: 24,
                                     droppedFrames: 0)

tracker.updateQoEObject(qoe: qoeObject)
```

>[!TAB Android]

Passa o tempo de inicialização como segundo argumento (`startupTime`) para `createQoEObject`.

```kotlin
val qoeObject = Media.createQoEObject(3200L,
                                      30000.0,
                                      24.0,
                                      0L)

tracker.updateQoEObject(qoeObject)
```

>[!TAB Roku]

Definir `timeToStart` dentro de `xdm.mediaCollection.qoeDataDetails` em `media.sessionStart` ao chamar `createMediaSession`:

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

>[!TAB API do Media Edge]

Chame o ponto de extremidade [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) com `timeToStart` dentro de `xdm.mediaCollection.qoeDataDetails`:

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

>[!ENDTABS]

## Tipos de implementação herdada (somente Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Passar o tempo para iniciar como segundo argumento para `ADB.Media.createQoEObject`:

```javascript
var qoeObject = ADB.Media.createQoEObject(3200, 30000, 24, 0);
tracker.updateQoEObject(qoeObject);
```

>[!TAB Chromecast]

Passe o tempo de inicialização em milissegundos como segundo argumento (`startupTime`) para `ADBMobile.media.createQoSObject` e atualize o rastreador:

```javascript
var qosInfo = ADBMobile.media.createQoSObject(
  3200,   // bitrate
  0,      // startupTime (ms)
  24,     // fps
  0       // droppedFrames
);
ADBMobile.media.updateQoSObject(qosInfo);
```

>[!TAB API da coleção de mídia]

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

>[!ENDTABS]
