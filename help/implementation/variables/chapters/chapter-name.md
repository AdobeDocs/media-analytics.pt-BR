---
title: Nome do capítulo
description: Defina o nome amigável de cada capítulo para que o relatório de nível de capítulo possa ser dividido por título de capítulo.
feature: Streaming Media
role: Developer
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 13%

---


# Nome do capítulo

>[!BEGINSHADEBOX]

*Esta página aborda a coleta de dados da variável **Nome do capítulo**. Consulte [Nome do capítulo](/help/reporting/dimensions/chapter-name.md) para a dimensão de relatório correspondente.*

>[!ENDSHADEBOX]

A variável de nome de capítulo é o título legível de um capítulo (por exemplo, `"Pilot Episode - Opening"`). Defina-o em cada evento `media.chapterStart` cujo conteúdo esteja dividido em capítulos.

| Propriedade | Valor |
| --- | --- |
| **Variável de dados de contexto** | `a.media.chapter.friendlyName` |
| **Campo da coleção XDM** | [`mediaCollection.chapterDetails.friendlyName`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/chapter-details-collection) |
| **Característica do Audience Manager** | `c_contextdata.a.media.chapter.friendlyName` |
| **Obrigatório** | Não |
| **Enviado com** | [Início do capítulo](/help/implementation/events/chapters/chapter-start.md), fechamento do capítulo |

## SDK da web

Definir `friendlyName` dentro de `mediaCollection.chapterDetails` ao chamar [`sendEvent`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/collection/js/commands/sendevent/overview):

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.chapterStart",
    mediaCollection: {
      chapterDetails: {
        friendlyName: "Pilot Episode - Opening",
        index: 1,
        offset: 0,
        length: 240
      },
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

## SDK móvel

Passar o nome do capítulo como o primeiro argumento (`name`) para `createChapterObject`.

**iOS (Swift)**

```swift
let chapterObject = Media.createChapterObjectWith(name: "Pilot Episode - Opening",
                                              position: 1,
                                                length: 240,
                                             startTime: 0)

tracker.trackEvent(event: MediaEvent.ChapterStart, info: chapterObject, metadata: nil)
```

**Android (Kotlin)**

```kotlin
val chapterObject = Media.createChapterObject("Pilot Episode - Opening",
                                              1L,
                                              240.0,
                                              0.0)

tracker.trackEvent(Media.Event.ChapterStart, chapterObject, null)
```

## Roku (BrightScript)

Definir `friendlyName` dentro de `mediaCollection.chapterDetails` ao chamar `sendMediaEvent` para `media.chapterStart`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.chapterStart",
        "mediaCollection": {
            "chapterDetails": {
                "friendlyName": "Pilot Episode - Opening",
                "index": 1,
                "offset": 0,
                "length": 240
            },
            "playhead": 0
        }
    }
})
```

## API de borda de mídia

Chame o ponto de extremidade [chapterStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/chapters/#chapterstart) com `friendlyName` dentro de `mediaCollection.chapterDetails`:

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.chapterStart",
      "mediaCollection": {
        "chapterDetails": {
          "friendlyName": "Pilot Episode - Opening",
          "index": 1,
          "offset": 0,
          "length": 240
        },
        "sessionID": "{sid}",
        "playhead": 0
      }
    }
  }]
}
```

## SDK de mídia

Passar o nome do capítulo como o primeiro argumento para `ADB.Media.createChapterObject`:

```javascript
var chapterInfo = ADB.Media.createChapterObject(
  "Pilot Episode - Opening",  // name
  1,                          // position
  240,                        // length (seconds)
  0                           // start time (seconds)
);

tracker.trackEvent(ADB.Media.Event.ChapterStart, chapterInfo, contextData);
```

## API da coleção de mídia

Inclua `media.chapter.friendlyName` no objeto `params` de sua solicitação POST `chapterStart`:

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "chapterStart",
  "params": {
    "media.chapter.friendlyName": "Pilot Episode - Opening"
  }
}
```

Consulte a [Referência de eventos da API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) para obter a estrutura de solicitação completa.
