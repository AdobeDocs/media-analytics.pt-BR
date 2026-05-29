---
title: Sinalizador de mídia baixada
description: Marque uma sessão como reprodução offline baixada para que ela seja relatada separadamente das sessões transmitidas.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '273'
ht-degree: 6%

---


# Sinalizador de mídia baixada

>[!BEGINSHADEBOX]

*Esta página aborda a coleta de dados da variável **Sinalizador de mídia baixada**. Consulte [Mídia baixada](/help/reporting/dimensions/media-downloaded-flag.md) para a dimensão de relatório correspondente.*

>[!ENDSHADEBOX]

O sinalizador de mídia baixada indica que uma sessão é a reprodução de conteúdo offline baixado anteriormente, em vez de um stream ao vivo da Internet. Defina-o ao inicializar o rastreador (Mobile SDK) ou inclua-o na carga `sessionStart` (Edge / API Media Collection). Use esse sinalizador para separar a reprodução offline das sessões transmitidas nos relatórios.

| Propriedade | Valor |
| --- | --- |
| **Variável de dados de contexto** | `a.media.downloaded` |
| **Campo da coleção XDM** | [`xdm.mediaCollection.sessionDetails.isDownloaded`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Característica do Audience Manager** | `c_contextdata.a.media.downloaded` |
| **Obrigatório** | Não |
| **Enviado com** | [Início da sessão](/help/implementation/events/session/session-start.md), fechamento da sessão |

## Tipos de implementação recomendados

>[!BEGINTABS]

>[!TAB Web SDK]

Definir `isDownloaded` como `true` dentro de `xdm.mediaCollection.sessionDetails` ao chamar [`sendEvent`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/collection/js/commands/sendevent/overview):

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
        streamType: "video",
        isDownloaded: true
      },
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

Defina o sinalizador de conteúdo baixado na configuração do rastreador ao criar o rastreador, usando `MediaConstants.TrackerConfig.DOWNLOADED_CONTENT`.

```swift
var config: [String: Any] = [:]
config[MediaConstants.TrackerConfig.PLAYER_NAME] = "HTML5 Player"
config[MediaConstants.TrackerConfig.CHANNEL] = "Sports"
config[MediaConstants.TrackerConfig.DOWNLOADED_CONTENT] = true

Media.createTrackerWith(config: config) { tracker in
    self.tracker = tracker
}
```

>[!TAB Android]

Defina o sinalizador de conteúdo baixado na configuração do rastreador ao criar o rastreador, usando `MediaConstants.TrackerConfig.DOWNLOADED_CONTENT`.

```kotlin
val config = HashMap<String, Any>()
config[MediaConstants.TrackerConfig.PLAYER_NAME] = "HTML5 Player"
config[MediaConstants.TrackerConfig.CHANNEL] = "Sports"
config[MediaConstants.TrackerConfig.DOWNLOADED_CONTENT] = true

val tracker = Media.createTracker(config)
```

>[!TAB Roku]

Definir `isDownloaded` como `true` dentro de `xdm.mediaCollection.sessionDetails` ao chamar `createMediaSession`:

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
                "streamType": "video",
                "isDownloaded": true
            },
            "playhead": 0
        }
    }
})
```

>[!TAB API do Media Edge]

Chame o ponto de extremidade [baixado](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/downloaded/#downloaded) depois que o dispositivo voltar ao modo online, agrupando a sessão offline completa dentro de `mediaDownloadedEvents`. O Adobe define automaticamente `isDownloaded` como `true` e atribui uma ID de sessão; não inclua nenhuma das duas na carga.

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.downloaded",
      "mediaDownloadedEvents": [
        {
          "mediaEventTimestamp": "YYYY-09-26T15:52:24+00:00",
          "mediaEventType": "media.sessionStart",
          "mediaCollection": {
            "sessionDetails": {
              "name": "video-123",
              "length": 128,
              "contentType": "vod",
              "playerName": "HTML5 Player",
              "channel": "Sports"
            },
            "playhead": 0
          }
        },
        {
          "mediaEventTimestamp": "YYYY-09-26T15:54:32+00:00",
          "mediaEventType": "media.sessionComplete",
          "mediaCollection": {
            "playhead": 128
          }
        }
      ]
    }
  }]
}
```

>[!ENDTABS]

## Tipos de implementação herdada (somente Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Defina `downloadedContent` em `ADB.MediaConfig` antes de criar o rastreador:

```javascript
var mediaConfig = new ADB.MediaConfig();
mediaConfig.trackingServer = "your.tracking.server";
mediaConfig.playerName = "HTML5 Player";
mediaConfig.channel = "Sports";
mediaConfig.downloadedContent = true;

var tracker = ADB.Media.getInstance(mediaConfig);
```

>[!TAB Chromecast]

Defina `MediaDownloaded` no objeto de informações de mídia antes de chamar `trackSessionStart`:

```javascript
var mediaInfo = ADBMobile.media.createMediaObject("My Video", "video-123", 128,
  ADBMobile.media.StreamType.VOD, ADBMobile.media.MediaType.Video);
mediaInfo[ADBMobile.media.MediaObjectKey.MediaDownloaded] = true;
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB API da coleção de mídia]

Inclua `media.downloaded` no objeto `params` de sua solicitação POST `sessionStart`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.downloaded": true
  }
}
```

Consulte a [Referência de sessões da API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md) para obter a estrutura de solicitação completa.

>[!ENDTABS]
