---
title: Primeira transmissão
description: Defina a data em que o conteúdo foi exibido na televisão pela primeira vez. A Adobe recomenda o formato AAAA-MM-DD.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 8%

---


# Primeira transmissão

>[!BEGINSHADEBOX]

*Esta página aborda a coleta de dados da variável **Primeira transmissão**. Consulte [Primeira transmissão](/help/reporting/dimensions/first-air-date.md) para a dimensão de relatório correspondente.*

>[!ENDSHADEBOX]

A primeira variável de data de exibição é a data em que o conteúdo foi exibido na televisão pela primeira vez. Qualquer formato de data é aceito, mas a Adobe recomenda `YYYY-MM-DD` para consistência. Use-o para comparar o engajamento em novas versões com o conteúdo do catálogo.

| Propriedade | Valor |
| --- | --- |
| **Variável de dados de contexto** | `a.media.airDate` |
| **Campo da coleção XDM** | [`xdm.mediaCollection.sessionDetails.firstAirDate`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Característica do Audience Manager** | `c_contextdata.a.media.airDate` |
| **Obrigatório** | Não |
| **Enviado com** | [Início da sessão](/help/implementation/events/session/session-start.md), fechamento da sessão |

## Tipos de implementação recomendados

>[!BEGINTABS]

>[!TAB Web SDK]

Definir `firstAirDate` dentro de `xdm.mediaCollection.sessionDetails` ao chamar [`sendEvent`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/collection/js/commands/sendevent/overview):

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        firstAirDate: "2016-01-25"
      },
      playhead: 0
    }
  }
});
```

>[!TAB iOS]

Transmita a primeira data como uma chave de metadados no argumento HashMap para `trackSessionStart`. Use `MediaConstants.VideoMetadataKeys.FIRST_AIR_DATE`.

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.FIRST_AIR_DATE] = "2016-01-25"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

>[!TAB Android]

Transmita a primeira data como uma chave de metadados no argumento HashMap para `trackSessionStart`. Use `MediaConstants.VideoMetadataKeys.FIRST_AIR_DATE`.

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.FIRST_AIR_DATE] = "2016-01-25"

tracker.trackSessionStart(mediaInfo, metadata)
```

>[!TAB Roku]

Use `createMediaSession` para definir `firstAirDate` dentro de `sessionDetails`:

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "firstAirDate": "2016-01-25"
            },
            "playhead": 0
        }
    }
})
```

>[!TAB API do Media Edge]

Chame o ponto de extremidade [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) com `firstAirDate` dentro de `xdm.mediaCollection.sessionDetails`:

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
          "firstAirDate": "2016-01-25"
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

Passar a primeira data de exibição no objeto `contextData` usando `ADB.Media.VideoMetadataKeys.FirstAirDate`:

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.FirstAirDate] = "2016-01-25";

tracker.trackSessionStart(mediaInfo, contextData);
```

>[!TAB Chromecast]

Use `ADBMobile.media.VideoMetadataKeys.FIRST_AIR_DATE` para definir a primeira data de transmissão na propriedade `StandardMediaMetadata` do objeto de mídia antes de chamar `trackSessionStart`:

```javascript
var mediaInfo = ADBMobile.media.createMediaObject("My Video", "video-123", 128,
  ADBMobile.media.StreamType.VOD, ADBMobile.media.MediaType.Video);
var standardMetadata = {};
standardMetadata[ADBMobile.media.VideoMetadataKeys.FIRST_AIR_DATE] = "2016-01-25";
mediaInfo[ADBMobile.media.MediaObjectKey.StandardMediaMetadata] = standardMetadata;
ADBMobile.media.trackSessionStart(mediaInfo, null);
```

>[!TAB API da coleção de mídia]

Incluir `media.firstAirDate` no objeto `params`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.firstAirDate": "2016-01-25"
  }
}
```

Consulte a [Referência de sessões da API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md) para obter a estrutura de solicitação completa.

>[!ENDTABS]
