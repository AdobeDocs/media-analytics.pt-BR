---
title: Ad break concluído
description: Sinal de que todos os anúncios em um ad break foram concluídos.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 9%

---


# Ad break concluído

O evento de ad break concluído sinaliza que todos os anúncios em um ad break foram concluídos (concluídos ou ignorados). Ele fecha o ad break aberto por [Ad break start](ad-break-start.md).

* **Pré-requisitos**: [Início da sessão](../session/session-start.md), [Início de quebra de anúncio](ad-break-start.md)
* **Métrica associada**: nenhuma

>[!IMPORTANT]
>
>Todo `adBreakStart` deve ter um `adBreakComplete` correspondente. Sem o finalizador de fechamento, os eventos de anúncio são ignorados e a duração do anúncio é atribuída ao conteúdo principal.

## Tipos de implementação recomendados

>[!BEGINTABS]

>[!TAB Web SDK]

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

>[!TAB iOS]

Chame `trackEvent` com o tipo de evento `AdBreakComplete`.

```swift
tracker.trackEvent(event: MediaEvent.AdBreakComplete, info: nil, metadata: nil)
```

>[!TAB Android]

Chame `trackEvent` com o tipo de evento `AdBreakComplete`.

```kotlin
tracker.trackEvent(Media.Event.AdBreakComplete, null, null)
```

>[!TAB Roku]

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

>[!TAB API do Media Edge]

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

>[!ENDTABS]

## Tipos de implementação herdada (somente Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Chamar `trackEvent` com o tipo de evento `AdBreakComplete`:

```javascript
tracker.trackEvent(ADB.Media.Event.AdBreakComplete, null, null);
```

>[!TAB Chromecast]

Chamar `trackEvent` com o tipo de evento `AdBreakComplete`:

```javascript
ADBMobile.media.trackEvent(ADBMobile.media.Event.AdBreakComplete);
```

>[!TAB API da coleção de mídia]

Enviar uma POSTAGEM `adBreakComplete` para o [ponto de extremidade de eventos](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md):

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "adBreakComplete"
}
```

>[!ENDTABS]
