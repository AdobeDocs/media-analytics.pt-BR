---
title: Álbum
description: Defina o nome do álbum para o conteúdo de áudio.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 9%

---


# Álbum

>[!BEGINSHADEBOX]

*Esta página aborda a coleção de dados da variável **Álbum**. Consulte [Álbum](/help/reporting/dimensions/album.md) para obter a dimensão de relatório correspondente.*

>[!ENDSHADEBOX]

A variável do álbum é o nome do álbum ao qual a faixa de áudio pertence (por exemplo, `"Pinegrove"`). Use-o para acumular engajamento entre faixas do mesmo álbum.

| Propriedade | Valor |
| --- | --- |
| **Variável de dados de contexto** | `a.media.album` |
| **Campo da coleção XDM** | [`xdm.mediaCollection.sessionDetails.album`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Característica do Audience Manager** | `c_contextdata.a.media.album` |
| **Obrigatório** | Não |
| **Enviado com** | [Início da sessão](/help/implementation/events/session/session-start.md), fechamento da sessão |

## Tipos de implementação recomendados

>[!BEGINTABS]

>[!TAB Web SDK]

Definir `album` dentro de `xdm.mediaCollection.sessionDetails` ao chamar [`sendEvent`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/collection/js/commands/sendevent/overview):

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        album: "Pinegrove"
      },
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

Passe o álbum como uma chave de metadados no argumento HashMap para `trackSessionStart`. Use `MediaConstants.AudioMetadataKeys.ALBUM`.

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.AudioMetadataKeys.ALBUM] = "Pinegrove"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

>[!TAB Android]

Passe o álbum como uma chave de metadados no argumento HashMap para `trackSessionStart`. Use `MediaConstants.AudioMetadataKeys.ALBUM`.

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.AudioMetadataKeys.ALBUM] = "Pinegrove"

tracker.trackSessionStart(mediaInfo, metadata)
```

>[!TAB Roku Edge]

Use `createMediaSession` para definir `album` dentro de `sessionDetails`:

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "album": "Pinegrove"
            },
            "playhead": 0
        }
    }
})
```

>[!TAB API do Media Edge]

Chame o ponto de extremidade [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) com `album` dentro de `xdm.mediaCollection.sessionDetails`:

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
          "channel": "Sports",
          "album": "Pinegrove"
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

Passar o álbum no objeto `contextData` usando `ADB.Media.AudioMetadataKeys.Album`:

```javascript
var contextData = {};
contextData[ADB.Media.AudioMetadataKeys.Album] = "Pinegrove";

tracker.trackSessionStart(mediaInfo, contextData);
```

>[!TAB Chromecast]

Use `ADBMobile.media.AudioMetadataKeys.ALBUM` para definir o álbum na propriedade `StandardMediaMetadata` do objeto de mídia antes de chamar `trackSessionStart`:

```javascript
var mediaInfo = ADBMobile.media.createMediaObject("My Track", "audio-123", 240,
  ADBMobile.media.StreamType.AOD, ADBMobile.media.MediaType.Audio);
var standardMetadata = {};
standardMetadata[ADBMobile.media.AudioMetadataKeys.ALBUM] = "Pinegrove";
mediaInfo[ADBMobile.media.MediaObjectKey.StandardMediaMetadata] = standardMetadata;
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB Roku 2.x]

Use `MEDIA_AudioMetadataKeyALBUM` para definir o álbum nos metadados padrão do objeto de mídia antes de chamar `mediaTrackSessionStart`:

```brightscript
adb = ADBMobile()
mediaInfo = adb_media_init_mediainfo("My Track", "audio-123", 240.0, adb.MEDIA_STREAM_TYPE_AOD, adb.MEDIA_TYPE_AUDIO)

standardMetadata = {}
standardMetadata[adb.MEDIA_AudioMetadataKeyALBUM] = "Pinegrove"
mediaInfo[adb.MEDIA_STANDARD_MEDIA_METADATA] = standardMetadata

adb.mediaTrackSessionStart(mediaInfo, invalid)
```

>[!TAB API da coleção de mídia]

Incluir `media.album` no objeto `params`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.album": "Pinegrove"
  }
}
```

Consulte a [Referência de sessões da API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md) para obter a estrutura de solicitação completa.

>[!ENDTABS]
