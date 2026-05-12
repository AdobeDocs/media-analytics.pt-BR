---
title: Deslocamento de capítulo
description: Defina o deslocamento do capítulo dentro do conteúdo, em segundos desde o início.
feature: Streaming Media
role: Developer
source-git-commit: 97cae4771558fc3f4d9719074b2fcf3ba661f1cc
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 12%

---


# Deslocamento de capítulo

>[!BEGINSHADEBOX]

*Esta página aborda a coleta de dados da variável **Deslocamento de capítulo**. Consulte [Deslocamento de capítulo](/help/reporting/dimensions/chapter-offset.md) para a dimensão de relatório correspondente.*

>[!ENDSHADEBOX]

A variável de deslocamento do capítulo é o deslocamento do capítulo dentro do conteúdo, medido em segundos desde o início. O primeiro capítulo normalmente tem o deslocamento `0`; os capítulos subsequentes têm deslocamentos que correspondem à hora de início do indicador de reprodução.

| Propriedade | Valor |
| --- | --- |
| **Variável de dados de contexto** | `a.media.chapter.offset` |
| **Campo da coleção XDM** | [`mediaCollection.chapterDetails.offset`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/chapter-details-collection) |
| **Obrigatório** | Não (Mobile SDK); Sim (Edge, API Media Collection) |
| **Enviado com** | Início do capítulo, fechamento do capítulo |

## SDK da web

Definir `offset` dentro de `mediaCollection.chapterDetails` ao chamar [`sendEvent`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/collection/js/commands/sendevent/overview):

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.chapterStart",
    mediaCollection: {
      chapterDetails: {
        friendlyName: "Act II",
        index: 2,
        offset: 240,
        length: 360
      },
      sessionID: "{sid}",
      playhead: 240
    }
  }
});
```

## SDK móvel

Transmita o deslocamento em segundos como o quarto argumento (`startTime`) para `createChapterObject`.

**iOS (Swift)**

```swift
let chapterObject = Media.createChapterObjectWith(name: "Act II",
                                              position: 2,
                                                length: 360,
                                             startTime: 240)

tracker.trackEvent(event: MediaEvent.ChapterStart, info: chapterObject, metadata: nil)
```

**Android (Kotlin)**

```kotlin
val chapterObject = Media.createChapterObject("Act II",
                                              2L,
                                              360.0,
                                              240.0)

tracker.trackEvent(Media.Event.ChapterStart, chapterObject, null)
```

## Roku (BrightScript)

Definir `offset` dentro de `mediaCollection.chapterDetails` ao chamar `sendMediaEvent` para `media.chapterStart`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.chapterStart",
        "mediaCollection": {
            "chapterDetails": {
                "friendlyName": "Act II",
                "index": 2,
                "offset": 240,
                "length": 360
            },
            "playhead": 240
        }
    }
})
```

## API de borda de mídia

Chame o ponto de extremidade [chapterStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/chapters/#chapterstart) com `offset` dentro de `mediaCollection.chapterDetails`:

```json
{
  "events": [{
    "xdm": {
      "eventType": "media.chapterStart",
      "mediaCollection": {
        "chapterDetails": {
          "index": 2,
          "offset": 240,
          "length": 360
        },
        "sessionID": "{sid}",
        "playhead": 240
      }
    }
  }]
}
```

## SDK de mídia

Passar o deslocamento como quarto argumento para `ADB.Media.createChapterObject`:

```javascript
var chapterInfo = ADB.Media.createChapterObject(
  "Act II",
  2,
  360,
  240
);

tracker.trackEvent(ADB.Media.Event.ChapterStart, chapterInfo, contextData);
```

## API da coleção de mídia

Inclua `media.chapter.offset` no objeto `params` de sua solicitação POST `chapterStart`:

```json
{
  "playerTime": { "playhead": 240, "ts": 1699523820000 },
  "eventType": "chapterStart",
  "params": {
    "media.chapter.offset": 240
  }
}
```

Consulte a [Referência de eventos da API Media Collection](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) para obter a estrutura de solicitação completa.
