---
title: Ignorar anúncio
description: Sinal de que o visualizador ignorou um anúncio.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 8%

---


# Ignorar anúncio

O evento de anúncio ignorado indica que o visualizador ignorou um anúncio antes de terminar. Enviá-lo quando o visualizador selecionar o botão Ignorar. Envie [Anúncio concluído](ad-complete.md) se o anúncio for reproduzido até o fim.

* **Pré-requisitos**: [Início da sessão](../session/session-start.md), [Início de quebra de anúncio](ad-break-start.md), [Início de anúncio](ad-start.md)
* **Métrica associada**: nenhuma

>[!IMPORTANT]
>
>Este evento deve estar entre `adBreakStart` e `adBreakComplete` delimitadores, mesmo quando um único anúncio é reproduzido. Sem esses delimitadores, os eventos de anúncio são ignorados e a duração do anúncio é contada como a duração do conteúdo principal.

## Tipos de implementação recomendados

>[!BEGINTABS]

>[!TAB Web SDK]

Chamar [`sendEvent`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/collection/js/commands/sendevent/overview) com `eventType: "media.adSkip"`:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.adSkip",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 5
    }
  }
});
```

>[!TAB iOS]

Chame `trackEvent` com o tipo de evento `AdSkip`.

```swift
tracker.trackEvent(event: MediaEvent.AdSkip, info: nil, metadata: nil)
```

>[!TAB Android]

Chame `trackEvent` com o tipo de evento `AdSkip`.

```kotlin
tracker.trackEvent(Media.Event.AdSkip, null, null)
```

>[!TAB Roku Edge]

Chamar `sendMediaEvent` com `eventType: "media.adSkip"`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.adSkip",
        "mediaCollection": {
            "playhead": 5
        }
    }
})
```

>[!TAB API do Media Edge]

Chame o ponto de extremidade [adSkip](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ads/#adskip):

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/adSkip?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.adSkip",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 5
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

Chamar `trackEvent` com o tipo de evento `AdSkip`:

```javascript
tracker.trackEvent(ADB.Media.Event.AdSkip, null, null);
```

>[!TAB Chromecast]

Chamar `trackEvent` com o tipo de evento `AdSkip`:

```javascript
ADBMobile.media.trackEvent(ADBMobile.media.Event.AdSkip);
```

>[!TAB Roku 2.x]

Chamar `mediaTrackEvent` com o tipo de evento `MEDIA_AD_SKIP`:

```brightscript
adb = ADBMobile()
adb.mediaTrackEvent(adb.MEDIA_AD_SKIP)
```

>[!TAB API da coleção de mídia]

Enviar uma POSTAGEM `adSkip` para o [ponto de extremidade de eventos](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md):

```json
{
  "playerTime": { "playhead": 5, "ts": 1699523820000 },
  "eventType": "adSkip"
}
```

>[!ENDTABS]
