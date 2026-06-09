---
title: Tipo de conteúdo
description: Defina o tipo de conteúdo para identificar o formato do fluxo (VOD, Ao vivo, Linear, podcast, música e assim por diante).
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 5%

---


# Tipo de conteúdo

>[!BEGINSHADEBOX]

*Esta página aborda a coleta de dados para a variável **Tipo de conteúdo**. Consulte [Tipo de conteúdo](/help/reporting/dimensions/content-type.md) para a dimensão de relatório correspondente.*

>[!ENDSHADEBOX]

A variável de tipo de conteúdo identifica o formato do fluxo (por exemplo, VOD, Live ou Linear para vídeo, podcast ou audiobook para áudio). É necessário para todas as implementações de mídia de transmissão e deve ser definido no início da sessão. Os valores definidos pelo Adobe preenchem os segmentos e relatórios integrados Tipo de conteúdo; cadeias de caracteres personalizadas também são aceitas, mas não corresponderão aos segmentos integrados. Se não for definido, o valor padrão será `missing_content_type`.

Valores recomendados:

* **Vídeo:** `vod`, `live`, `linear`, `ugc`, `dvod`
* **Áudio:** `song`, `podcast`, `audiobook`, `radio`

| Propriedade | Valor |
| --- | --- |
| **Variável de dados de contexto** | `a.contentType` |
| **Campo da coleção XDM** | [`xdm.mediaCollection.sessionDetails.contentType`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Característica do Audience Manager** | `c_contextdata.a.contentType` |
| **Obrigatório** | Sim |
| **Enviado com** | [Início da sessão](/help/implementation/events/session/session-start.md), fechamento da sessão |

## Tipos de implementação recomendados

>[!BEGINTABS]

>[!TAB Web SDK]

Definir `contentType` dentro de `xdm.mediaCollection.sessionDetails` ao chamar [`sendEvent`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/collection/js/commands/sendevent/overview):

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
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

Passe a constante de tipo de conteúdo como o argumento `streamType` para `createMediaObject`. Use valores de `MediaConstants.StreamType.*` como `VOD`, `LIVE`, `LINEAR`, `AOD`, `PODCAST`. Observação: no Mobile SDK, o argumento `streamType` controla o Tipo de conteúdo. A variável Tipo de Fluxo (áudio vs. vídeo) é o argumento `mediaType` separado.

```swift
let mediaObject = Media.createMediaObjectWith(name: "My Video",
                                                id: "video-123",
                                            length: 128,
                                        streamType: MediaConstants.StreamType.VOD,
                                         mediaType: MediaType.Video)

tracker.trackSessionStart(info: mediaObject, metadata: nil)
```

>[!TAB Android]

Passe a constante de tipo de conteúdo como o argumento `streamType` para `createMediaObject`. Use valores de `MediaConstants.StreamType.*` como `VOD`, `LIVE`, `LINEAR`, `AOD`, `PODCAST`. Observação: no Mobile SDK, o argumento `streamType` controla o Tipo de conteúdo. A variável Tipo de Fluxo (áudio vs. vídeo) é o argumento `mediaType` separado.

```kotlin
var mediaInfo = Media.createMediaObject("My Video",
                                        "video-123",
                                        128,
                                        MediaConstants.StreamType.VOD,
                                        Media.MediaType.Video)

tracker.trackSessionStart(mediaInfo, null)
```

>[!TAB Roku Edge]

Definir `contentType` dentro de `xdm.mediaCollection.sessionDetails` ao chamar `createMediaSession`:

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
            "playhead": 0
        }
    }
})
```

>[!TAB API do Media Edge]

Chame o ponto de extremidade [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) com `contentType` dentro de `xdm.mediaCollection.sessionDetails`:

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

Passe uma constante `ADB.Media.StreamType.*` como quarto argumento para `ADB.Media.createMediaObject`:

```javascript
var mediaInfo = ADB.Media.createMediaObject(
  "My Video",
  "video-123",
  128,
  ADB.Media.StreamType.VOD, // Content type — VOD, LIVE, LINEAR, etc.
  ADB.Media.MediaType.Video
);

tracker.trackSessionStart(mediaInfo, contextData);
```

>[!TAB Chromecast]

Passe uma constante `ADBMobile.media.StreamType.*` como quarto argumento para `ADBMobile.media.createMediaObject`:

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

Transmita uma constante `MEDIA_STREAM_TYPE_*` como o quarto argumento (`streamType`) para `adb_media_init_mediainfo`. No SDK do Roku 2.x, esse argumento carrega o tipo de conteúdo (`vod`, `live`, `linear`):

```brightscript
adb = ADBMobile()
mediaInfo = adb_media_init_mediainfo("My Video", "video-123", 128.0, adb.MEDIA_STREAM_TYPE_VOD, adb.MEDIA_TYPE_VIDEO)

adb.mediaTrackSessionStart(mediaInfo, invalid)
```

>[!TAB API da coleção de mídia]

Inclua `media.contentType` no objeto `params` de sua solicitação POST `sessionStart`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.contentType": "vod"
  }
}
```

Consulte a [Referência de sessões da API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md) para obter a estrutura de solicitação completa.

>[!ENDTABS]
