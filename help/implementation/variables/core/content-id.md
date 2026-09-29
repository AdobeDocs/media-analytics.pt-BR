---
title: ID de conteúdo
description: Identifique exclusivamente um conteúdo de mídia.
feature: Streaming Media
role: Developer
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: c153fd90-23e1-4614-81d3-3cc7571227f7
    internal-label: Analysis Workspace
subfeature_v2:
  - id: c9bb7ea6-c04f-4262-b69c-fbb8d91e3559
    internal-label: Streaming Media
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 9%
---

# ID de conteúdo

>[!BEGINSHADEBOX]

*Esta página aborda a coleta de dados da variável **ID de Conteúdo**. Consulte [Conteúdo](/help/reporting/dimensions/content.md) para a dimensão de relatório correspondente.*

>[!ENDSHADEBOX]

A variável de ID de conteúdo identifica exclusivamente cada parte do conteúdo de mídia. Ela é necessária para todas as implementações de mídia de transmissão e é a chave primária para a dimensão de relatório Conteúdo. Defina-o no início da sessão e mantenha-o estável em todas as sessões para o mesmo ativo.

| Propriedade | Valor |
| --- | --- |
| **Variável de dados de contexto** | `a.media.name` |
| **Campo da coleção XDM** | [`xdm.mediaCollection.sessionDetails.name`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Característica do Audience Manager** | `c_contextdata.a.media.name` |
| **Obrigatório** | Sim |
| **Enviado com** | [Início da sessão](/help/implementation/events/session/session-start.md), fechamento da sessão |

## Tipos de implementação recomendados

>[!BEGINTABS]

>[!TAB Web SDK]

Definir `name` dentro de `xdm.mediaCollection.sessionDetails` ao chamar [`sendEvent`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/collection/js/commands/sendevent/overview):

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        name: "video-123",
        friendlyName: "My Video",
        length: 128,
        contentType: "vod",
        playerName: "HTML5 Player",
        channel: "Sports",
        streamType: "video"
      },
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

Passar a ID de conteúdo como o argumento `mediaId` para `createMediaObject`.

```swift
let mediaObject = Media.createMediaObjectWith(name: "My Video",
                                                id: "video-123",
                                            length: 128,
                                        streamType: MediaConstants.StreamType.VOD,
                                         mediaType: MediaType.Video)

tracker.trackSessionStart(info: mediaObject, metadata: nil)
```

>[!TAB Android]

Passar a ID de conteúdo como o argumento `mediaId` para `createMediaObject`.

```kotlin
var mediaInfo = Media.createMediaObject("My Video",
                                        "video-123",
                                        128,
                                        MediaConstants.StreamType.VOD,
                                        Media.MediaType.Video)

tracker.trackSessionStart(mediaInfo, null)
```

>[!TAB Roku Edge]

Definir `name` dentro de `xdm.mediaCollection.sessionDetails` ao chamar `createMediaSession`:

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "name": "video-123",
                "friendlyName": "My Video",
                "length": 128,
                "contentType": "vod",
                "playerName": "Roku Player",
                "channel": "Sports",
                "streamType": "video"
            },
            "playhead": 0
        }
    }
})
```

>[!TAB API do Media Edge]

Chame o ponto de extremidade [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) com `name` (a ID de Conteúdo) dentro de `xdm.mediaCollection.sessionDetails`:

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

Passe a ID de conteúdo como segundo argumento para `ADB.Media.createMediaObject`:

```javascript
var mediaInfo = ADB.Media.createMediaObject(
  "My Video",               // name (friendly name)
  "video-123",              // media ID — Content ID
  128,                      // length (seconds)
  ADB.Media.StreamType.VOD,
  ADB.Media.MediaType.Video
);

tracker.trackSessionStart(mediaInfo, contextData);
```

>[!TAB Chromecast]

Passe a ID de conteúdo como segundo argumento para `ADBMobile.media.createMediaObject`:

```javascript
var mediaInfo = ADBMobile.media.createMediaObject(
  "My Video",
  "video-123",
  128,
  ADBMobile.media.StreamType.VOD,
  ADBMobile.media.MediaType.Video
);
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB Roku 2.x]

Passe a ID de conteúdo como segundo argumento para `adb_media_init_mediainfo`:

```brightscript
adb = ADBMobile()
mediaInfo = adb_media_init_mediainfo("My Video", "video-123", 128.0, adb.MEDIA_STREAM_TYPE_VOD, adb.MEDIA_TYPE_VIDEO)

adb.mediaTrackSessionStart(mediaInfo, invalid)
```

>[!TAB API da coleção de mídia]

Inclua `media.id` no objeto `params` de sua solicitação POST `sessionStart`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.id": "video-123"
  }
}
```

Consulte a [Referência de sessões da API Media Collection](https://developer.adobe.com/analytics-collection-apis/methods/media-collection/sessions) para obter a estrutura de solicitação completa.

>[!ENDTABS]
