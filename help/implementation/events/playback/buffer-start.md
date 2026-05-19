---
title: Início do buffer
description: Sinal de que o reprodutor de mídia entrou em um estado de buffering.
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 15%

---


# Início do buffer

O evento de início de buffer indica que o reprodutor de mídia entrou em um estado de buffering.

* **Pré-requisitos**: [Início da sessão](../session/session-start.md)
* **Métrica associada**: [Eventos de buffer](/help/reporting/metrics/buffer-events.md)

>[!NOTE]
>
>**APIs baseadas em XDM (Web SDK, Roku, API do Media Edge, API da Coleção de Mídia):** Não há tipo de evento de retomada de buffer; o fim do buffer é inferido quando você envia um evento [`play`](play.md) após `bufferStart`.
>
>**SDK móvel:** Chame `trackEvent(BufferComplete)` quando o player sair do buffering e, em seguida, chame `trackPlay()` para retomar a reprodução.

## SDK da web

Chamar [`sendEvent`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/collection/js/commands/sendevent/overview) com `eventType: "media.bufferStart"`:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.bufferStart",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 45
    }
  }
});
```

## SDK móvel

Chame `trackEvent` com `BufferStart` quando o player entrar em um estado de buffering e `BufferComplete` quando ele sair.

**iOS (Swift)**

```swift
// Buffer starts
tracker.trackEvent(event: MediaEvent.BufferStart, info: nil, metadata: nil)

// Buffer ends
tracker.trackEvent(event: MediaEvent.BufferComplete, info: nil, metadata: nil)
```

**Android (Kotlin)**

```kotlin
// Buffer starts
tracker.trackEvent(Media.Event.BufferStart, null, null)

// Buffer ends
tracker.trackEvent(Media.Event.BufferComplete, null, null)
```

## Roku (BrightScript)

Chamar `sendMediaEvent` com `eventType: "media.bufferStart"`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.bufferStart",
        "mediaCollection": {
            "playhead": 45
        }
    }
})
```

## API de borda de mídia

Chame o ponto de extremidade [bufferStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/bufferstart/):

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/bufferStart?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.bufferStart",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 45
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## SDK de mídia

Chamar `trackEvent` com o tipo de evento `BufferStart`:

```javascript
tracker.trackEvent(ADB.Media.Event.BufferStart, null, null);
```

## API da coleção de mídia

Enviar uma POSTAGEM `bufferStart` para o [ponto de extremidade de eventos](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md):

```json
{
  "playerTime": { "playhead": 45, "ts": 1699523820000 },
  "eventType": "bufferStart"
}
```
