---
title: Primeira data digital
description: Defina a data em que o conteúdo foi exibido em uma plataforma digital pela primeira vez. A Adobe recomenda o formato AAAA-MM-DD.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '206'
ht-degree: 13%

---


# Primeira data digital

>[!BEGINSHADEBOX]

*Esta página aborda a coleta de dados da variável **Primeira data digital**. Consulte [Primeira data digital](/help/reporting/dimensions/first-digital-date.md) para a dimensão de relatório correspondente.*

>[!ENDSHADEBOX]

A primeira variável de data digital é a data em que o conteúdo foi exibido em qualquer plataforma digital pela primeira vez. Qualquer formato de data é aceito, mas a Adobe recomenda `YYYY-MM-DD` para consistência. Use juntamente com a [Primeira data de transmissão](/help/implementation/variables/standard-metadata/first-air-date.md) para comparar o tempo de lançamento digital com a transmissão original.

| Propriedade | Valor |
| --- | --- |
| **Variável de dados de contexto** | `a.media.digitalDate` |
| **Campo da coleção XDM** | [`mediaCollection.sessionDetails.firstDigitalDate`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-collection) |
| **Característica do Audience Manager** | `c_contextdata.a.media.digitalDate` |
| **Obrigatório** | Não |
| **Enviado com** | [Início da sessão](/help/implementation/events/session/session-start.md), fechamento da sessão |

## SDK da web

Definir `firstDigitalDate` dentro de `mediaCollection.sessionDetails` ao chamar [`sendEvent`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/collection/js/commands/sendevent/overview):

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionStart",
    mediaCollection: {
      sessionDetails: {
        firstDigitalDate: "2016-01-25"
      },
      playhead: 0
    }
  }
});
```

## SDK móvel

Passe a primeira data digital como uma chave de metadados no argumento HashMap para `trackSessionStart`. Use `MediaConstants.VideoMetadataKeys.FIRST_DIGITAL_DATE`.

**iOS (Swift)**

```swift
var metadata: [String: String] = [:]
metadata[MediaConstants.VideoMetadataKeys.FIRST_DIGITAL_DATE] = "2016-01-25"

tracker.trackSessionStart(info: mediaObject, metadata: metadata)
```

**Android (Kotlin)**

```kotlin
val metadata = HashMap<String, String>()
metadata[MediaConstants.VideoMetadataKeys.FIRST_DIGITAL_DATE] = "2016-01-25"

tracker.trackSessionStart(mediaInfo, metadata)
```

## Roku (BrightScript)

Use `createMediaSession` para definir `firstDigitalDate` dentro de `sessionDetails`:

```brightscript
m.aepSdk.createMediaSession({
    "xdm": {
        "eventType": "media.sessionStart",
        "mediaCollection": {
            "sessionDetails": {
                "firstDigitalDate": "2016-01-25"
            },
            "playhead": 0
        }
    }
})
```

## API de borda de mídia

Chame o ponto de extremidade [sessionStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionstart) com `firstDigitalDate` dentro de `mediaCollection.sessionDetails`:

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
          "firstDigitalDate": "2016-01-25"
        },
        "playhead": 0
      }
    }
  }]
}
```

## SDK de mídia

Passar a primeira data digital no objeto `contextData` usando `ADB.Media.VideoMetadataKeys.FirstDigitalDate`:

```javascript
var contextData = {};
contextData[ADB.Media.VideoMetadataKeys.FirstDigitalDate] = "2016-01-25";

tracker.trackSessionStart(mediaInfo, contextData);
```

## API da coleção de mídia

Incluir `media.firstDigitalDate` no objeto `params`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "sessionStart",
  "params": {
    "media.firstDigitalDate": "2016-01-25"
  }
}
```

Consulte a [Referência de sessões da API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-sessions-req.md) para obter a estrutura de solicitação completa.
