---
title: Álbum
description: Defina o nome do álbum para o conteúdo de áudio.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 16%

---


# Álbum

>[!BEGINSHADEBOX]

*Esta página aborda a coleção de dados da variável **Álbum**. Consulte [Álbum](/help/reporting/dimensions/album.md) para obter a dimensão de relatório correspondente.*

>[!ENDSHADEBOX]

A variável do álbum é o nome do álbum ao qual a faixa de áudio pertence (por exemplo, `"Pinegrove"`). Use-o para acumular engajamento entre faixas do mesmo álbum.

| Propriedade | Valor |
| --- | --- |
| **Variável de dados de contexto** | `a.media.album` |
| **Campo da coleção XDM** | [`mediaCollection.sessionDetails.album`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Característica do Audience Manager** | `c_contextdata.a.media.album` |
| **Obrigatório** | Não |
| **Enviado com** | [Início da sessão](/help/implementation/events/session/session-start.md), fechamento da sessão |

## SDK da web

Definir `album` dentro de `mediaCollection.sessionDetails` ao chamar [`sendEvent`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/collection/js/commands/sendevent/overview):

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

## SDK móvel

Passe o álbum como uma chave de metadados no argumento HashMap para `trackSessionStart`. Use `MediaConstants.AudioMetadataKeys.ALBUM`.

**iOS (Swift)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.AudioMetadataKeys.ALBUM] = "Pinegrove"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

**Android (Kotlin)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.AudioMetadataKeys.ALBUM] = "Pinegrove"

tracker.trackSessionStart(mediaInfo, metadata)
```

## Roku (BrightScript)

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

## API de borda de mídia

Chame o ponto de extremidade [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) com `album` dentro de `mediaCollection.sessionDetails`:

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

## SDK de mídia

Passar o álbum no objeto `contextData` usando `ADB.Media.AudioMetadataKeys.Album`:

```javascript
var contextData = {};
contextData[ADB.Media.AudioMetadataKeys.Album] = "Pinegrove";

tracker.trackSessionStart(mediaInfo, contextData);
```

## API da coleção de mídia

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
