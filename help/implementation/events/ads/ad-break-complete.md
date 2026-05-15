---
title: Ad break concluído
description: Sinal de que todos os anúncios em um ad break foram concluídos.
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 16%

---


# Ad break concluído

O evento de ad break concluído sinaliza que todos os anúncios em um ad break foram concluídos (concluídos ou ignorados). Ele fecha o ad break aberto por [Ad break start](ad-break-start.md).

* **Pré-requisitos**: [Início da sessão](../session/session-start.md), [Início de quebra de anúncio](ad-break-start.md)
* **Métrica associada**: nenhuma

>[!IMPORTANT]
>
>Todo `adBreakStart` deve ter um `adBreakComplete` correspondente. Sem o finalizador de fechamento, os eventos de anúncio são ignorados e a duração do anúncio é atribuída ao conteúdo principal.

## SDK da web

Chamar [`sendEvent`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/collection/js/commands/sendevent/overview) com `eventType: "media.adBreakComplete"`:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adBreakComplete",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 0
    }
  }
});
```

## SDK móvel

Chame `trackEvent` com o tipo de evento `AdBreakComplete`.

**iOS (Swift)**

```swift
tracker.trackEvent(event: MediaEvent.AdBreakComplete, info: nil, metadata: nil)
```

**Android (Kotlin)**

```kotlin
tracker.trackEvent(Media.Event.AdBreakComplete, null, null)
```

## Roku (BrightScript)

Chamar `sendMediaEvent` com `eventType: "media.adBreakComplete"`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adBreakComplete",
        "mediaCollection": {
            "playhead": 0
        }
    }
})
```

## API de borda de mídia

Chame o ponto de extremidade [adBreakComplete](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adbreakcomplete):

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/adBreakComplete?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.adBreakComplete",
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

Chamar `trackEvent` com o tipo de evento `AdBreakComplete`:

```javascript
tracker.trackEvent(ADB.Media.Event.AdBreakComplete, null, null);
```

## API da coleção de mídia

Enviar uma POSTAGEM `adBreakComplete` para o [ponto de extremidade de eventos](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md):

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adBreakComplete"
}
```
