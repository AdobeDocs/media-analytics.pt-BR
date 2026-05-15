---
title: Reproduzir
description: Sinal de que o reprodutor de mídia entrou no estado de reprodução.
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 17%

---


# Reproduzir

O evento de reprodução indica que o reprodutor de mídia mudou de estado para reproduzido. Enviá-lo no início do conteúdo, na reprodução automática e sempre que o reprodutor for retomado após uma pausa ou buffer. Não há evento de retomada separado; um evento de reprodução após [Início da pausa](pause-start.md) ou [Início do buffer](buffer-start.md) serve como retomada.

* **Pré-requisitos**: [Início da sessão](../session/session-start.md)
* **Métrica associada**: [Início do conteúdo](/help/reporting/metrics/content-starts.md)

## SDK da web

Chamar [`sendEvent`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/collection/js/commands/sendevent/overview) com `eventType: "media.play"`:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.play",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

## SDK móvel

Chame `trackPlay` quando o reprodutor de mídia iniciar ou retomar a reprodução.

**iOS (Swift)**

```swift
tracker.trackPlay()
```

**Android (Kotlin)**

```kotlin
tracker.trackPlay()
```

## Roku (BrightScript)

Chamar `sendMediaEvent` com `eventType: "media.play"`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.play",
        "mediaCollection": {
            "playhead": 0
        }
    }
})
```

## API de borda de mídia

Chame o ponto de extremidade [play](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/play/):

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/play?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.play",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 0
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## SDK de mídia

Chame `trackPlay` quando o reprodutor de mídia iniciar ou retomar a reprodução:

```javascript
tracker.trackPlay();
```

## API da coleção de mídia

Enviar uma POSTAGEM `play` para o [ponto de extremidade de eventos](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md):

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "play"
}
```
