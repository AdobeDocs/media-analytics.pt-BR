---
title: Primeira transmissão
description: Defina a data em que o conteúdo foi exibido na televisão pela primeira vez. A Adobe recomenda o formato AAAA-MM-DD.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 13%

---


# Primeira transmissão

>[!BEGINSHADEBOX]

*Esta página aborda a coleta de dados da variável **Primeira transmissão**. Consulte [Primeira transmissão](/help/reporting/dimensions/first-air-date.md) para a dimensão de relatório correspondente.*

>[!ENDSHADEBOX]

A primeira variável de data de exibição é a data em que o conteúdo foi exibido na televisão pela primeira vez. Qualquer formato de data é aceito, mas a Adobe recomenda `YYYY-MM-DD` para consistência. Use-o para comparar o engajamento em novas versões com o conteúdo do catálogo.

| Propriedade | Valor |
| --- | --- |
| **Variável de dados de contexto** | `a.media.airDate` |
| **Campo da coleção XDM** | [`mediaCollection.sessionDetails.firstAirDate`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Característica do Audience Manager** | `c_contextdata.a.media.airDate` |
| **Obrigatório** | Não |
| **Enviado com** | [Início da sessão](/help/implementation/events/session/session-start.md), fechamento da sessão |

## SDK da web

Definir `firstAirDate` dentro de `mediaCollection.sessionDetails` ao chamar [`sendEvent`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/collection/js/commands/sendevent/overview):

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

## SDK móvel

Transmita a primeira data como uma chave de metadados no argumento HashMap para `trackSessionStart`. Use `MediaConstants.VideoMetadataKeys.FIRST_AIR_DATE`.

**iOS (Swift)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.FIRST_AIR_DATE] = "2016-01-25"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

**Android (Kotlin)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.FIRST_AIR_DATE] = "2016-01-25"

tracker.trackSessionStart(mediaInfo, metadata)
```

## Roku (BrightScript)

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

## API de borda de mídia

Chame o ponto de extremidade [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) com `firstAirDate` dentro de `mediaCollection.sessionDetails`:

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

## SDK de mídia

Passar a primeira data de exibição no objeto `contextData` usando `ADB.Media.VideoMetadataKeys.FirstAirDate`:

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.FirstAirDate] = "2016-01-25";

tracker.trackSessionStart(mediaInfo, contextData);
```

## API da coleção de mídia

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
