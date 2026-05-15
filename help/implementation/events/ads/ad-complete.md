---
title: Anúncio concluído
description: Sinal de que um anúncio individual terminou de ser reproduzido.
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 15%

---


# Anúncio concluído

O evento de conclusão do anúncio indica que um anúncio individual terminou de ser reproduzido. Enviá-lo depois que o anúncio for reproduzido até a conclusão. Se o visualizador ignorar o anúncio, envie [Ignorar anúncio](ad-skip.md).

* **Pré-requisitos**: [Início da sessão](../session/session-start.md), [Início de quebra de anúncio](ad-break-start.md), [Início de anúncio](ad-start.md)
* **Métrica associada**: [Anúncio concluído](/help/reporting/metrics/ad-completes.md)

>[!IMPORTANT]
>
>Este evento deve estar entre `adBreakStart` e `adBreakComplete` delimitadores, mesmo quando um único anúncio é reproduzido. Sem esses delimitadores, os eventos de anúncio são ignorados e a duração do anúncio é contada como a duração do conteúdo principal.

## SDK da web

Chamar [`sendEvent`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/collection/js/commands/sendevent/overview) com `eventType: "media.adComplete"`:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adComplete",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 15
    }
  }
});
```

## SDK móvel

Chame `trackEvent` com o tipo de evento `AdComplete`.

**iOS (Swift)**

```swift
tracker.trackEvent(event: MediaEvent.AdComplete, info: nil, metadata: nil)
```

**Android (Kotlin)**

```kotlin
tracker.trackEvent(Media.Event.AdComplete, null, null)
```

## Roku (BrightScript)

Chamar `sendMediaEvent` com `eventType: "media.adComplete"`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adComplete",
        "mediaCollection": {
            "playhead": 15
        }
    }
})
```

## API de borda de mídia

Chame o ponto de extremidade [adComplete](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adcomplete):

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/adComplete?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.adComplete",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 15
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## SDK de mídia

Chamar `trackEvent` com o tipo de evento `AdComplete`:

```javascript
tracker.trackEvent(ADB.Media.Event.AdComplete, null, null);
```

## API da coleção de mídia

Enviar uma POSTAGEM `adComplete` para o [ponto de extremidade de eventos](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md):

```json
{
  "playerTime": { "playhead": 15, "ts": 1699523820000 },
  "eventType": "adComplete"
}
```
