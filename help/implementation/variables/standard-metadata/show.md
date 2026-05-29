---
title: Programa
description: Defina o nome do programa para o conteúdo de vídeo que faz parte de uma série, de modo que os episódios sejam agrupados em um único programa nos relatórios.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 8%

---


# Programa

>[!BEGINSHADEBOX]

*Esta página aborda a coleta de dados da variável **Mostrar**. Consulte [Mostrar](/help/reporting/dimensions/show.md) para a dimensão de relatório correspondente.*

>[!ENDSHADEBOX]

A variável show é o nome do programa ou da série (por exemplo, `"Blinding Light"` ou `"Coastline Mysteries"`). Defina-o em cada sessão cujo conteúdo pertença a uma série para que os episódios em várias temporadas sejam acumulados em um único item de linha na dimensão Programa. Deixe essa opção desmarcada para conteúdo único que não faz parte de uma série.

| Propriedade | Valor |
| --- | --- |
| **Variável de dados de contexto** | `a.media.show` |
| **Campo da coleção XDM** | [`xdm.mediaCollection.sessionDetails.show`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Característica do Audience Manager** | `c_contextdata.a.media.show` |
| **Obrigatório** | Não |
| **Enviado com** | [Início da sessão](/help/implementation/events/session/session-start.md), fechamento da sessão |

## Tipos de implementação recomendados

>[!BEGINTABS]

>[!TAB Web SDK]

Definir `show` dentro de `xdm.mediaCollection.sessionDetails` ao chamar [`sendEvent`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/collection/js/commands/sendevent/overview):

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        show: "Blinding Light"
      },
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

Passe o nome de exibição como uma chave de metadados no argumento HashMap para `trackSessionStart`. Use `MediaConstants.VideoMetadataKeys.SHOW`.

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.SHOW] = "Blinding Light"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

>[!TAB Android]

Passe o nome de exibição como uma chave de metadados no argumento HashMap para `trackSessionStart`. Use `MediaConstants.VideoMetadataKeys.SHOW`.

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.SHOW] = "Blinding Light"

tracker.trackSessionStart(mediaInfo, metadata)
```

>[!TAB Roku]

Use `createMediaSession` para definir `show` dentro de `sessionDetails`:

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "show": "Blinding Light"
            },
            "playhead": 0
        }
    }
})
```

>[!TAB API do Media Edge]

Chame o ponto de extremidade [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) com `show` dentro de `xdm.mediaCollection.sessionDetails`:

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
          "show": "Blinding Light"
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

Passar o nome de exibição no objeto `contextData` usando `ADB.Media.VideoMetadataKeys.Show`:

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.Show] = "Blinding Light";

tracker.trackSessionStart(mediaInfo, contextData);
```

>[!TAB Chromecast]

Use `ADBMobile.media.VideoMetadataKeys.SHOW` para definir o nome de exibição na propriedade `StandardMediaMetadata` do objeto de mídia antes de chamar `trackSessionStart`:

```javascript
var mediaInfo = ADBMobile.media.createMediaObject("My Video", "video-123", 128,
  ADBMobile.media.StreamType.VOD, ADBMobile.media.MediaType.Video);
var standardMetadata = {};
standardMetadata[ADBMobile.media.VideoMetadataKeys.SHOW] = "Blinding Light";
mediaInfo[ADBMobile.media.MediaObjectKey.StandardMediaMetadata] = standardMetadata;
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB API da coleção de mídia]

Inclua `media.show` no objeto `params` de sua solicitação POST `sessionStart`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.show": "Blinding Light"
  }
}
```

Consulte a [Referência de sessões da API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md) para obter a estrutura de solicitação completa.

>[!ENDTABS]
