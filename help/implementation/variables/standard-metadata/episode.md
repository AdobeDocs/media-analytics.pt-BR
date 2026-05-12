---
title: Episódio
description: Defina o número do episódio para o conteúdo episódico, de modo que episódios individuais possam ser relatados separadamente.
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '179'
ht-degree: 16%

---


# Episódio

>[!BEGINSHADEBOX]

*Esta página aborda a coleta de dados da variável **Episódio**. Consulte [Episódio](/help/reporting/dimensions/episode.md) para a dimensão de relatório correspondente.*

>[!ENDSHADEBOX]

A variável episode é o número do episódio na temporada (normalmente um inteiro como `"13"`). Emparelhe com [Programa](/help/implementation/variables/standard-metadata/show.md) e [Temporada](/help/implementation/variables/standard-metadata/season.md) para que o engajamento possa ser dividido por episódio individual.

| Propriedade | Valor |
| --- | --- |
| **Variável de dados de contexto** | `a.media.episode` |
| **Campo da coleção XDM** | [`mediaCollection.sessionDetails.episode`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Obrigatório** | Não |
| **Enviado com** | Início da sessão, fechamento da sessão |

## SDK da web

Definir `episode` dentro de `mediaCollection.sessionDetails` ao chamar [`sendEvent`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/collection/js/commands/sendevent/overview):

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        episode: "13"
      },
      playhead: 0
    }
  }
});
```

## SDK móvel

Passe o número do episódio como uma chave de metadados no argumento de HashMap para `trackSessionStart`. Use `MediaConstants.VideoMetadataKeys.EPISODE`.

**iOS (Swift)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.EPISODE] = "13"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

**Android (Kotlin)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.EPISODE] = "13"

tracker.trackSessionStart(mediaInfo, metadata)
```

## Roku (BrightScript)

Use `createMediaSession` para definir `episode` dentro de `sessionDetails`:

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "episode": "13"
            },
            "playhead": 0
        }
    }
})
```

## API de borda de mídia

Chame o ponto de extremidade [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) com `episode` dentro de `mediaCollection.sessionDetails`:

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
          "episode": "13"
        },
        "playhead": 0
      }
    }
  }]
}
```

## SDK de mídia

Passar o episódio no objeto `contextData` usando `ADB.Media.VideoMetadataKeys.Episode`:

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.Episode] = "13";

tracker.trackSessionStart(mediaInfo, contextData);
```

## API da coleção de mídia

Incluir `media.episode` no objeto `params`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.episode": "13"
  }
}
```

Consulte a [Referência de sessões da API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md) para obter a estrutura de solicitação completa.
