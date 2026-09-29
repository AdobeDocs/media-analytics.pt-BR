---
title: Tipo de carregamento de anúncio
description: Defina o tipo de carregamento do anúncio para a sessão de streaming.
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
source-wordcount: '278'
ht-degree: 3%
---

# Tipo de carregamento de anúncio

>[!BEGINSHADEBOX]

*Esta página aborda a coleta de dados para a variável **Tipo de carregamento de anúncio**. Consulte [Carregamentos de anúncios](/help/reporting/dimensions/ad-load-type.md) para a dimensão de relatório correspondente.*

>[!ENDSHADEBOX]

A variável de tipo de carregamento de anúncio identifica o tipo de anúncio carregado no início da sessão. Esse valor é definido pelo sistema interno de entrega de anúncios da organização e não está restrito a uma lista discriminada padrão. Você pode usar qualquer cadeia de caracteres significativa para sua implementação, como `"linear"`, `"dynamic"` ou `"programmatic"`.

| Propriedade | Valor |
| --- | --- |
| **Variável de dados de contexto** | `a.media.adLoad` |
| **Campo da coleção XDM** | [`xdm.mediaCollection.sessionDetails.adLoad`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Característica do Audience Manager** | `c_contextdata.a.media.adLoad` |
| **Obrigatório** | Não |
| **Enviado com** | [Início da sessão](/help/implementation/events/session/session-start.md), fechamento da sessão |

## Tipos de implementação recomendados

>[!BEGINTABS]

>[!TAB Web SDK]

Definir `adLoad` dentro de `xdm.mediaCollection.sessionDetails` ao chamar [`createMediaSession`](https://experienceleague.adobe.com/en/docs/experience-platform/collection/js/commands/createmediasession):

```javascript
alloy("createMediaSession", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        name: "video-123",
        friendlyName: "My Video",
        length: 300,
        contentType: "vod",
        playerName: "HTML5 Player",
        channel: "Sports",
        adLoad: "linear"
      },
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

Passe o tipo de carregamento de anúncio como uma chave de metadados no argumento de dicionário para `trackSessionStart`. Use `MediaConstants.VideoMetadataKeys.AD_LOAD`.

```swift
var videoMetadata: [String: String] = [:]
videoMetadata[MediaConstants.VideoMetadataKeys.AD_LOAD] = "linear"

tracker.trackSessionStart(info: mediaObject, metadata: videoMetadata)
```

>[!TAB Android]

Passe o tipo de carregamento de anúncio como uma chave de metadados no argumento HashMap para `trackSessionStart`. Use `MediaConstants.VideoMetadataKeys.AD_LOAD`.

```kotlin
val videoMetadata = HashMap<String, String>()
videoMetadata[MediaConstants.VideoMetadataKeys.AD_LOAD] = "linear"

tracker.trackSessionStart(mediaInfo, videoMetadata)
```

>[!TAB Roku Edge]

Use `createMediaSession` para definir `adLoad` dentro de `sessionDetails`:

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "adLoad": "linear"
            },
            "playhead": 0
        }
    }
})
```

>[!TAB API do Media Edge]

Chame o ponto de extremidade [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) com `adLoad` dentro de `xdm.mediaCollection.sessionDetails`:

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.sessionStart",
      "mediaCollection": {
        "sessionDetails": {
          "name": "video-123",
          "length": 300,
          "contentType": "vod",
          "playerName": "HTML5 Player",
          "channel": "Sports",
          "adLoad": "linear"
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

Passar o tipo de carregamento de anúncio no objeto `contextData` usando `ADB.Media.VideoMetadataKeys.AdLoad`:

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.AdLoad] = "linear";

tracker.trackSessionStart(mediaInfo, contextData);
```

>[!TAB Chromecast]

Use `ADBMobile.media.VideoMetadataKeys.AD_LOAD` para definir o tipo de carregamento de anúncio na propriedade `StandardMediaMetadata` do objeto de mídia antes de chamar `trackSessionStart`:

```javascript
var mediaInfo = ADBMobile.media.createMediaObject("My Video", "video-123", 300,
  ADBMobile.media.StreamType.VOD, ADBMobile.media.MediaType.Video);
var standardMetadata = {};
standardMetadata[ADBMobile.media.VideoMetadataKeys.AD_LOAD] = "linear";
mediaInfo[ADBMobile.media.MediaObjectKey.StandardMediaMetadata] = standardMetadata;
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB Roku 2.x]

Use `MEDIA_VideoMetadataKeyAD_LOAD` para definir o tipo de carregamento de anúncio nos metadados padrão do objeto de mídia antes de chamar `mediaTrackSessionStart`:

```brightscript
adb = ADBMobile()
mediaInfo = adb_media_init_mediainfo("My Video", "video-123", 128.0, adb.MEDIA_STREAM_TYPE_VOD, adb.MEDIA_TYPE_VIDEO)

standardMetadata = {}
standardMetadata[adb.MEDIA_VideoMetadataKeyAD_LOAD] = "linear"
mediaInfo[adb.MEDIA_STANDARD_MEDIA_METADATA] = standardMetadata

adb.mediaTrackSessionStart(mediaInfo, invalid)
```

>[!TAB API da coleção de mídia]

Inclua `media.adLoad` no objeto `params` de sua solicitação POST `sessionStart`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.adLoad": "linear"
  }
}
```

Consulte a [Referência de sessões da API Media Collection](https://developer.adobe.com/analytics-collection-apis/methods/media-collection/sessions) para obter a estrutura de solicitação completa.

>[!ENDTABS]
