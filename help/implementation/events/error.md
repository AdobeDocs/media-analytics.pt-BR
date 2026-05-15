---
title: Erro
description: Sinal de que o reprodutor de mídia encontrou um erro.
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 16%

---


# Erro

O evento de erro indica que o reprodutor de mídia encontrou um erro. O rastreamento de um erro não encerra a sessão. Se o erro impedir que a reprodução continue, chame [Fim da sessão](session/session-end.md) após o evento de erro.

* **Pré-requisitos**: [Início da sessão](session/session-start.md)
* **Métrica associada**: [Fluxos afetados pelo erro](/help/reporting/metrics/error-impacted-streams.md)

A propriedade `errorDetails.source` aceita apenas dois valores: `player` (erros originados no reprodutor de mídia) e `external` (erros de uma fonte externa, como um CDN ou uma rede).

## SDK da web

Chame [`sendEvent`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/collection/js/commands/sendevent/overview) com `eventType: "media.error"` e o `errorDetails` necessário:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.error",
    mediaCollection: {
      errorDetails: {
        name: "media-error-001",
        source: "player"
      },
      sessionID: "{sid}",
      playhead: 45
    }
  }
});
```

## SDK móvel

Chame `trackError` com uma cadeia de caracteres de ID de erro.

**iOS (Swift)**

```swift
tracker.trackError(errorId: "media-error-001")
```

**Android (Kotlin)**

```kotlin
tracker.trackError("media-error-001")
```

## Roku (BrightScript)

Chame `sendMediaEvent` com `eventType: "media.error"` e o(a) `errorDetails` necessário(a):

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.error",
        "mediaCollection": {
            "errorDetails": {
                "name": "media-error-001",
                "source": "player"
            },
            "playhead": 45
        }
    }
})
```

## API de borda de mídia

Chame o ponto de extremidade [erro](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/error/) com o `errorDetails` necessário:

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/error?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.error",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 45,
        "errorDetails": {
          "name": "media-error-001",
          "source": "player"
        }
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## SDK de mídia

Chame `trackError` com uma cadeia de caracteres de ID de erro:

```javascript
tracker.trackError("media-error-001");
```

## API da coleção de mídia

Enviar uma POSTAGEM `error` para o [ponto de extremidade de eventos](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md):

```json
{
  "playerTime": { "playhead": 45, "ts": 1699523820000 },
  "eventType": "error",
  "params": {
    "media.errorId": "media-error-001",
    "media.errorSource": "player"
  }
}
```
