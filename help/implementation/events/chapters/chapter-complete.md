---
title: Capítulo concluído
description: Sinal de que um segmento de capítulo terminou de ser reproduzido.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 10%

---


# Capítulo concluído

O evento de conclusão de capítulo indica que um capítulo terminou de ser reproduzido. Enviá-lo quando o visualizador atingir o final de um capítulo. Se o visualizador ignorar o capítulo, envie [Chapter skip](chapter-skip.md).

* **Pré-requisitos**: [Início da sessão](../session/session-start.md), [Início do capítulo](chapter-start.md)
* **Métrica associada**: [[!UICONTROL Capítulo concluído]](/help/reporting/metrics/chapter-completes.md)

## Tipos de implementação recomendados

>[!BEGINTABS]

>[!TAB Web SDK]

Chamar [`sendEvent`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/collection/js/commands/sendevent/overview) com `eventType: "media.chapterComplete"`:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.chapterComplete",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 240
    }
  }
});
```

>[!TAB iOS]

Chame `trackEvent` com o tipo de evento `ChapterComplete`.

```swift
tracker.trackEvent(event: MediaEvent.ChapterComplete, info: nil, metadata: nil)
```

>[!TAB Android]

Chame `trackEvent` com o tipo de evento `ChapterComplete`.

```kotlin
tracker.trackEvent(Media.Event.ChapterComplete, null, null)
```

>[!TAB Roku Edge]

Chamar `sendMediaEvent` com `eventType: "media.chapterComplete"`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.chapterComplete",
        "mediaCollection": {
            "playhead": 240
        }
    }
})
```

>[!TAB API do Media Edge]

Chame o ponto de extremidade [chapterComplete](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/chapters/#chaptercomplete):

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/chapterComplete?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.chapterComplete",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 240
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

>[!ENDTABS]

## Tipos de implementação herdada (somente Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Chamar `trackEvent` com o tipo de evento `ChapterComplete`:

```javascript
tracker.trackEvent(ADB.Media.Event.ChapterComplete, null, null);
```

>[!TAB Chromecast]

Chamar `trackEvent` com o tipo de evento `ChapterComplete`:

```javascript
ADBMobile.media.trackEvent(ADBMobile.media.Event.ChapterComplete);
```

>[!TAB Roku 2.x]

Chamar `mediaTrackEvent` com o tipo de evento `MEDIA_CHAPTER_COMPLETE`:

```brightscript
adb = ADBMobile()
adb.mediaTrackEvent(adb.MEDIA_CHAPTER_COMPLETE)
```

>[!TAB API da coleção de mídia]

Enviar uma POSTAGEM `chapterComplete` para o [ponto de extremidade de eventos](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md):

```json
{
  "playerTime": { "playhead": 240, "ts": 1699523820000 },
  "eventType": "chapterComplete"
}
```

>[!ENDTABS]
