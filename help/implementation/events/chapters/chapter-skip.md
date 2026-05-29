---
title: Capítulo ignorado
description: Sinal de que o visualizador ignorou um capítulo.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 10%

---


# Capítulo ignorado

O capítulo ignora sinais de evento de que o visualizador ignorou um capítulo antes de terminar. Enviá-lo quando o visualizador navegar além do limite do capítulo sem observá-lo até a conclusão. Enviar [Capítulo concluído](chapter-complete.md) se o capítulo for reproduzido até o fim.

* **Pré-requisitos**: [Início da sessão](../session/session-start.md), [Início do capítulo](chapter-start.md)
* **Métrica associada**: nenhuma

## Tipos de implementação recomendados

>[!BEGINTABS]

>[!TAB Web SDK]

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

>[!TAB iOS]

Chame `trackEvent` com o tipo de evento `ChapterSkip`.

```swift
tracker.trackEvent(event: MediaEvent.ChapterSkip, info: nil, metadata: nil)
```

>[!TAB Android]

Chame `trackEvent` com o tipo de evento `ChapterSkip`.

```kotlin
tracker.trackEvent(Media.Event.ChapterSkip, null, null)
```

>[!TAB Roku]

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

>[!TAB API do Media Edge]

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

>[!ENDTABS]

## Tipos de implementação herdada (somente Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Chamar `trackEvent` com o tipo de evento `ChapterSkip`:

```javascript
tracker.trackEvent(ADB.Media.Event.ChapterSkip, null, null);
```

>[!TAB Chromecast]

Chamar `trackEvent` com o tipo de evento `ChapterSkip`:

```javascript
ADBMobile.media.trackEvent(ADBMobile.media.Event.ChapterSkip);
```

>[!TAB API da coleção de mídia]

Enviar uma POSTAGEM `chapterSkip` para o [ponto de extremidade de eventos](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md):

```json
{
  "playerTime": { "playhead": 60, "ts": 1699523820000 },
  "eventType": "chapterSkip"
}
```

>[!ENDTABS]
