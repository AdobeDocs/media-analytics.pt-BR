---
title: Tipo de feed de mídia
description: Identifique o tipo de feed de transmissão (por exemplo, East-HD ou West-SD) para o conteúdo que varia por região ou qualidade.
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 13%

---


# Tipo de feed de mídia

>[!BEGINSHADEBOX]

*Esta página aborda a coleta de dados para a variável **Tipo de feed de mídia**. Consulte [Tipo de feed de mídia](/help/reporting/dimensions/media-feed-type.md) para a dimensão de relatório correspondente.*

>[!ENDSHADEBOX]

A variável de tipo de feed de mídia identifica o feed de difusão (por exemplo, `"East-HD"`, `"West-SD"` ou `"4K"`). Use-o quando o mesmo conteúdo for entregue por meio de vários feeds regionais ou de qualidade e o engajamento precisar ser dividido por feed.

| Propriedade | Valor |
| --- | --- |
| **Variável de dados de contexto** | `a.media.feed` |
| **Campo da coleção XDM** | [`mediaCollection.sessionDetails.feed`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Obrigatório** | Não |
| **Enviado com** | Início da sessão, fechamento da sessão |

## SDK da web

Definir `feed` dentro de `mediaCollection.sessionDetails` ao chamar [`sendEvent`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/collection/js/commands/sendevent/overview):

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        feed: "East-HD"
      },
      playhead: 0
    }
  }
});
```

## SDK móvel

Passe o tipo de feed como uma chave de metadados no argumento HashMap para `trackSessionStart`. Use `MediaConstants.VideoMetadataKeys.MEDIA_FEED`.

**iOS (Swift)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.MEDIA_FEED] = "East-HD"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

**Android (Kotlin)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.MEDIA_FEED] = "East-HD"

tracker.trackSessionStart(mediaInfo, metadata)
```

## Roku (BrightScript)

Use `createMediaSession` para definir `feed` dentro de `sessionDetails`:

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "feed": "East-HD"
            },
            "playhead": 0
        }
    }
})
```

## API de borda de mídia

Chame o ponto de extremidade [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) com `feed` dentro de `mediaCollection.sessionDetails`:

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
          "feed": "East-HD"
        },
        "playhead": 0
      }
    }
  }]
}
```

## SDK de mídia

Passar o feed no objeto `contextData` usando `ADB.Media.VideoMetadataKeys.Feed`:

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.Feed] = "East-HD";

tracker.trackSessionStart(mediaInfo, contextData);
```

## API da coleção de mídia

Incluir `media.feed` no objeto `params`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.feed": "East-HD"
  }
}
```

Consulte a [Referência de sessões da API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md) para obter a estrutura de solicitação completa.
