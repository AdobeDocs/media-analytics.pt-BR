---
title: Autor
description: Defina o autor do conteúdo. Usado principalmente para audiolivros.
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 16%

---


# Autor

>[!BEGINSHADEBOX]

*Esta página aborda a coleta de dados da variável **Author**. Consulte [Autor](/help/reporting/dimensions/author.md) para obter a dimensão de relatório correspondente.*

>[!ENDSHADEBOX]

A variável do autor é o autor do conteúdo (por exemplo, `"Eleanor Clementine"`). Usado principalmente para audiolivros, mas também aceitável para podcasts cujo host ou produtor é a atribuição relevante.

| Propriedade | Valor |
| --- | --- |
| **Variável de dados de contexto** | `a.media.author` |
| **Campo da coleção XDM** | [`mediaCollection.sessionDetails.author`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Obrigatório** | Não |
| **Enviado com** | Início da sessão, fechamento da sessão |

## SDK da web

Definir `author` dentro de `mediaCollection.sessionDetails` ao chamar [`sendEvent`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/collection/js/commands/sendevent/overview):

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        author: "Eleanor Clementine"
      },
      playhead: 0
    }
  }
});
```

## SDK móvel

Passe o autor como uma chave de metadados no argumento HashMap para `trackSessionStart`. Use `MediaConstants.AudioMetadataKeys.AUTHOR`.

**iOS (Swift)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.AudioMetadataKeys.AUTHOR] = "Eleanor Clementine"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

**Android (Kotlin)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.AudioMetadataKeys.AUTHOR] = "Eleanor Clementine"

tracker.trackSessionStart(mediaInfo, metadata)
```

## Roku (BrightScript)

Use `createMediaSession` para definir `author` dentro de `sessionDetails`:

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "author": "Eleanor Clementine"
            },
            "playhead": 0
        }
    }
})
```

## API de borda de mídia

Chame o ponto de extremidade [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) com `author` dentro de `mediaCollection.sessionDetails`:

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
          "author": "Eleanor Clementine"
        },
        "playhead": 0
      }
    }
  }]
}
```

## SDK de mídia

Passar o autor no objeto `contextData` usando `ADB.Media.AudioMetadataKeys.Author`:

```javascript
var contextData = {};
contextData[ADB.Media.AudioMetadataKeys.Author] = "Eleanor Clementine";

tracker.trackSessionStart(mediaInfo, contextData);
```

## API da coleção de mídia

Incluir `media.author` no objeto `params`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.author": "Eleanor Clementine"
  }
}
```

Consulte a [Referência de sessões da API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md) para obter a estrutura de solicitação completa.
