---
title: Classificação de conteúdo
description: Defina a classificação de conteúdo conforme definido pelas Diretrizes de controle parental da TV ou pelo seu sistema de classificação regional.
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 14%

---


# Classificação de conteúdo

>[!BEGINSHADEBOX]

*Esta página aborda a coleta de dados para a variável **Classificação de conteúdo**. Consulte [Classificação de conteúdo](/help/reporting/dimensions/content-rating.md) para a dimensão de relatório correspondente.*

>[!ENDSHADEBOX]

A variável de classificação de conteúdo é a classificação de público-alvo conforme definido pelas Diretrizes de controle parental da TV (`"TVY"`, `"TVG"`, `"TVPG"`, `"TVMA"`) ou qualquer sistema de classificação regional que você usar. Use-a para comparar o engajamento e a carga de anúncios entre os níveis de classificação.

| Propriedade | Valor |
| --- | --- |
| **Variável de dados de contexto** | `a.media.rating` |
| **Campo da coleção XDM** | [`mediaCollection.sessionDetails.rating`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Obrigatório** | Não |
| **Enviado com** | Início da sessão, fechamento da sessão |

## SDK da web

Definir `rating` dentro de `mediaCollection.sessionDetails` ao chamar [`sendEvent`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/collection/js/commands/sendevent/overview):

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        rating: "TVPG"
      },
      playhead: 0
    }
  }
});
```

## SDK móvel

Passe a classificação como uma chave de metadados no argumento HashMap para `trackSessionStart`. Use `MediaConstants.VideoMetadataKeys.RATING`.

**iOS (Swift)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.RATING] = "TVPG"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

**Android (Kotlin)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.RATING] = "TVPG"

tracker.trackSessionStart(mediaInfo, metadata)
```

## Roku (BrightScript)

Use `createMediaSession` para definir `rating` dentro de `sessionDetails`:

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "rating": "TVPG"
            },
            "playhead": 0
        }
    }
})
```

## API de borda de mídia

Chame o ponto de extremidade [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) com `rating` dentro de `mediaCollection.sessionDetails`:

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
          "rating": "TVPG"
        },
        "playhead": 0
      }
    }
  }]
}
```

## SDK de mídia

Passar a classificação no objeto `contextData` usando `ADB.Media.VideoMetadataKeys.Rating`:

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.Rating] = "TVPG";

tracker.trackSessionStart(mediaInfo, contextData);
```

## API da coleção de mídia

Incluir `media.rating` no objeto `params`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.rating": "TVPG"
  }
}
```

Consulte a [Referência de sessões da API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md) para obter a estrutura de solicitação completa.
