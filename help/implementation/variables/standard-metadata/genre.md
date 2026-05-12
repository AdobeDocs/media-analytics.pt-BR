---
title: Gênero
description: Defina o gênero de conteúdo como uma string delimitada por vírgulas. O conteúdo multigênero é dividido entre itens de linha nos relatórios.
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 13%

---


# Gênero

>[!BEGINSHADEBOX]

*Esta página aborda a coleta de dados para a variável **Gênero**. Consulte [Gênero](/help/reporting/dimensions/genre.md) para a dimensão de relatório correspondente.*

>[!ENDSHADEBOX]

A variável de gênero é o gênero de conteúdo conforme definido pelo produtor (por exemplo, `"Drama"`, `"Comedy"` ou `"Drama,Action"`). Delimite por vírgulas vários valores quando o conteúdo se ajustar a mais de um gênero. Nos relatórios, a variável de lista divide cada valor em um item de linha separado, com cada item de linha recebendo peso de métrica igual.

>[!NOTE]
>
>No pipeline de relatórios, o valor do gênero é exposto como `mediaReporting.sessionDetails.genreList` (um campo de lista). O caminho `mediaReporting.sessionDetails.genre` mais antigo permanece funcional, mas `genreList` é recomendado.

| Propriedade | Valor |
| --- | --- |
| **Variável de dados de contexto** | `a.media.genre` |
| **Campo da coleção XDM** | [`mediaCollection.sessionDetails.genre`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Obrigatório** | Não |
| **Enviado com** | Início da sessão, fechamento da sessão |

## SDK da web

Definir `genre` dentro de `mediaCollection.sessionDetails` ao chamar [`sendEvent`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/collection/js/commands/sendevent/overview):

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        genre: "Drama,Action"
      },
      playhead: 0
    }
  }
});
```

## SDK móvel

Passe a cadeia de caracteres do gênero como uma chave de metadados no argumento HashMap para `trackSessionStart`. Use `MediaConstants.VideoMetadataKeys.GENRE`.

**iOS (Swift)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.GENRE] = "Drama,Action"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

**Android (Kotlin)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.GENRE] = "Drama,Action"

tracker.trackSessionStart(mediaInfo, metadata)
```

## Roku (BrightScript)

Use `createMediaSession` para definir `genre` dentro de `sessionDetails`:

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "genre": "Drama,Action"
            },
            "playhead": 0
        }
    }
})
```

## API de borda de mídia

Chame o ponto de extremidade [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) com `genre` dentro de `mediaCollection.sessionDetails`:

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
          "genre": "Drama,Action"
        },
        "playhead": 0
      }
    }
  }]
}
```

## SDK de mídia

Passar o gênero no objeto `contextData` usando `ADB.Media.VideoMetadataKeys.Genre`:

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.Genre] = "Drama,Action";

tracker.trackSessionStart(mediaInfo, contextData);
```

## API da coleção de mídia

Incluir `media.genre` no objeto `params`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.genre": "Drama,Action"
  }
}
```

Consulte a [Referência de sessões da API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md) para obter a estrutura de solicitação completa.
