---
title: Capítulo ignorado
description: Sinal de que o visualizador ignorou um capítulo.
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 18%

---


# Capítulo ignorado

O capítulo ignora sinais de evento de que o visualizador ignorou um capítulo antes de terminar. Enviá-lo quando o visualizador navegar além do limite do capítulo sem observá-lo até a conclusão. Enviar [Capítulo concluído](chapter-complete.md) se o capítulo for reproduzido até o fim.

* **Pré-requisitos**: [Início da sessão](../session/session-start.md), [Início do capítulo](chapter-start.md)
* **Métrica associada**: nenhuma

## SDK da web

Chamar [`sendEvent`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/collection/js/commands/sendevent/overview) com `eventType: "media.chapterSkip"`:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.chapterSkip",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 60
    }
  }
});
```

## SDK móvel

Chame `trackEvent` com o tipo de evento `ChapterSkip`.

**iOS (Swift)**

```swift
tracker.trackEvent(event: MediaEvent.ChapterSkip, info: nil, metadata: nil)
```

**Android (Kotlin)**

```kotlin
tracker.trackEvent(Media.Event.ChapterSkip, null, null)
```

## Roku (BrightScript)

Chamar `sendMediaEvent` com `eventType: "media.chapterSkip"`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.chapterSkip",
        "mediaCollection": {
            "playhead": 60
        }
    }
})
```

## API de borda de mídia

Chame o ponto de extremidade [chapterSkip](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/chapters/#chapterskip):

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/chapterSkip?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.chapterSkip",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 60
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## SDK de mídia

Chamar `trackEvent` com o tipo de evento `ChapterSkip`:

```javascript
tracker.trackEvent(ADB.Media.Event.ChapterSkip, null, null);
```

## API da coleção de mídia

Enviar uma POSTAGEM `chapterSkip` para o [ponto de extremidade de eventos](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md):

```json
{
  "playerTime": { "playhead": 60, "ts": 1699523820000 },
  "eventType": "chapterSkip"
}
```
