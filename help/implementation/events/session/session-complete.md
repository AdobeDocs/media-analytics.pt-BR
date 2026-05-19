---
title: Sessão concluída
description: Sinal de que o visualizador atingiu o fim do conteúdo principal.
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '138'
ht-degree: 16%

---


# Sessão concluída

O evento de conclusão da sessão indica que o visualizador atingiu o fim do conteúdo principal. A sessão não é encerrada imediatamente; a sessão permanece aberta até expirar naturalmente. Se quiser fechar a sessão imediatamente, chame [Fim da sessão](session-end.md).

* **Pré-requisitos**: [Início da sessão](session-start.md)
* **Métrica associada**: [Conteúdo concluído](/help/reporting/metrics/content-completes.md)

## SDK da web

Chamar [`sendEvent`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/collection/js/commands/sendevent/overview) com `eventType: "media.sessionComplete"`:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionComplete",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 128
    }
  }
});
```

## SDK móvel

Chame `trackComplete` quando o reprodutor de mídia atingir o fim do conteúdo.

**iOS (Swift)**

```swift
tracker.trackComplete()
```

**Android (Kotlin)**

```kotlin
tracker.trackComplete()
```

## Roku (BrightScript)

Chamar `sendMediaEvent` com `eventType: "media.sessionComplete"`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.sessionComplete",
        "mediaCollection": {
            "playhead": 128
        }
    }
})
```

## API de borda de mídia

Chame o ponto de extremidade [sessionComplete](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessioncomplete):

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/sessionComplete?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.sessionComplete",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 128
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## SDK de mídia

Chame `trackComplete` quando o reprodutor de mídia atingir o fim do conteúdo:

```javascript
tracker.trackComplete();
```

## API da coleção de mídia

Enviar uma POSTAGEM `sessionComplete` para o [ponto de extremidade de eventos](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md):

```json
{
  "playerTime": { "playhead": 128, "ts": 1699523820000 },
  "eventType": "sessionComplete"
}
```
