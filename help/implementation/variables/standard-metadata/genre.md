---
title: Gênero
description: Defina o gênero de conteúdo como uma string delimitada por vírgulas. O conteúdo multigênero é dividido entre itens de linha nos relatórios.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 8%

---


# Gênero

>[!BEGINSHADEBOX]

*Esta página aborda a coleta de dados para a variável **Gênero**. Consulte [Gênero](/help/reporting/dimensions/genre.md) para a dimensão de relatório correspondente.*

>[!ENDSHADEBOX]

A variável de gênero é o gênero de conteúdo conforme definido pelo produtor (por exemplo, `"Drama"`, `"Comedy"` ou `"Drama,Action"`). Delimite por vírgulas vários valores quando o conteúdo se ajustar a mais de um gênero. Nos relatórios, a variável de lista divide cada valor em um item de linha separado, com cada item de linha recebendo peso de métrica igual.

>[!NOTE]
>
>No pipeline de relatórios, o valor do gênero é exposto como `xdm.mediaReporting.sessionDetails.genreList` (um campo de lista). O caminho `xdm.mediaReporting.sessionDetails.genre` mais antigo permanece funcional, mas `genreList` é recomendado.

| Propriedade | Valor |
| --- | --- |
| **Variável de dados de contexto** | `a.media.genre` |
| **Campo da coleção XDM** | [`xdm.mediaCollection.sessionDetails.genre`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Característica do Audience Manager** | `c_contextdata.a.media.genre` |
| **Obrigatório** | Não |
| **Enviado com** | [Início da sessão](/help/implementation/events/session/session-start.md), fechamento da sessão |

## Tipos de implementação recomendados

>[!BEGINTABS]

>[!TAB Web SDK]

Definir `genre` dentro de `xdm.mediaCollection.sessionDetails` ao chamar [`sendEvent`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/collection/js/commands/sendevent/overview):

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

>[!TAB iOS]

Passe a cadeia de caracteres do gênero como uma chave de metadados no argumento HashMap para `trackSessionStart`. Use `MediaConstants.VideoMetadataKeys.GENRE`.

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.GENRE] = "Drama,Action"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

>[!TAB Android]

Passe a cadeia de caracteres do gênero como uma chave de metadados no argumento HashMap para `trackSessionStart`. Use `MediaConstants.VideoMetadataKeys.GENRE`.

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.GENRE] = "Drama,Action"

tracker.trackSessionStart(mediaInfo, metadata)
```

>[!TAB Roku]

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

>[!TAB API do Media Edge]

Chame o ponto de extremidade [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) com `genre` dentro de `xdm.mediaCollection.sessionDetails`:

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

>[!ENDTABS]

## Tipos de implementação herdada (somente Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Passar o gênero no objeto `contextData` usando `ADB.Media.VideoMetadataKeys.Genre`:

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.Genre] = "Drama,Action";

tracker.trackSessionStart(mediaInfo, contextData);
```

>[!TAB Chromecast]

Use `ADBMobile.media.VideoMetadataKeys.GENRE` para definir o gênero na propriedade `StandardMediaMetadata` do objeto de mídia antes de chamar `trackSessionStart`:

```javascript
var mediaInfo = ADBMobile.media.createMediaObject("My Video", "video-123", 128,
  ADBMobile.media.StreamType.VOD, ADBMobile.media.MediaType.Video);
var standardMetadata = {};
standardMetadata[ADBMobile.media.VideoMetadataKeys.GENRE] = "Drama,Action";
mediaInfo[ADBMobile.media.MediaObjectKey.StandardMediaMetadata] = standardMetadata;
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB API da coleção de mídia]

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

>[!ENDTABS]
