---
title: Deslocamento de capítulo
description: Defina o deslocamento do capítulo dentro do conteúdo, em segundos desde o início.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 7%

---


# Deslocamento de capítulo

>[!BEGINSHADEBOX]

*Esta página aborda a coleta de dados da variável **Deslocamento de capítulo**. Consulte [Deslocamento de capítulo](/help/reporting/dimensions/chapter-offset.md) para a dimensão de relatório correspondente.*

>[!ENDSHADEBOX]

A variável de deslocamento do capítulo é o deslocamento do capítulo dentro do conteúdo, medido em segundos desde o início. O primeiro capítulo normalmente tem o deslocamento `0`; os capítulos subsequentes têm deslocamentos que correspondem à hora de início do indicador de reprodução.

| Propriedade | Valor |
| --- | --- |
| **Variável de dados de contexto** | `a.media.chapter.offset` |
| **Campo da coleção XDM** | [`xdm.mediaCollection.chapterDetails.offset`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/chapter-details-collection) |
| **Característica do Audience Manager** | `c_contextdata.a.media.chapter.offset` |
| **Obrigatório** | Não (Mobile SDK); Sim (Edge, API Media Collection) |
| **Enviado com** | [Início do capítulo](/help/implementation/events/chapters/chapter-start.md), fechamento do capítulo |

## Tipos de implementação recomendados

>[!BEGINTABS]

>[!TAB Web SDK]

Definir `offset` dentro de `xdm.mediaCollection.chapterDetails` ao chamar [`sendEvent`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/collection/js/commands/sendevent/overview):

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

>[!TAB iOS]

Transmita o deslocamento em segundos como o quarto argumento (`startTime`) para `createChapterObject`.

```swift
let chapterObject = Media.createChapterObjectWith(name: "Act II",
                                              position: 2,
                                                length: 360,
                                             startTime: 240)

tracker.trackEvent(event: MediaEvent.ChapterStart, info: chapterObject, metadata: nil)
```

>[!TAB Android]

Transmita o deslocamento em segundos como o quarto argumento (`startTime`) para `createChapterObject`.

```kotlin
val chapterObject = Media.createChapterObject("Act II",
                                              2L,
                                              360.0,
                                              240.0)

tracker.trackEvent(Media.Event.ChapterStart, chapterObject, null)
```

>[!TAB Roku]

Definir `offset` dentro de `xdm.mediaCollection.chapterDetails` ao chamar `sendMediaEvent` para `media.chapterStart`:

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

>[!TAB API do Media Edge]

Chame o ponto de extremidade [chapterStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/chapters/#chapterstart) com `offset` dentro de `xdm.mediaCollection.chapterDetails`:

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

>[!ENDTABS]

## Tipos de implementação herdada (somente Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

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

>[!TAB Chromecast]

Transmita o deslocamento do capítulo em segundos como o quarto argumento (`startTime`) para `ADBMobile.media.createChapterObject`:

```javascript
var chapterInfo = ADBMobile.media.createChapterObject(
  "Pilot Episode - Opening",  // name
  1,                          // position
  240,                        // length
  0                           // startTime (seconds from content start)
);
ADBMobile.media.trackEvent(ADBMobile.media.Event.ChapterStart, chapterInfo, null);
```

>[!TAB API da coleção de mídia]

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

>[!ENDTABS]
