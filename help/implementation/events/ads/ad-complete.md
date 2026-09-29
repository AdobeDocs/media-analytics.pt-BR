---
title: Anúncio concluído
description: Sinal de que um anúncio individual terminou de ser reproduzido.
feature: Streaming Media
role: Developer
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: c153fd90-23e1-4614-81d3-3cc7571227f7
    internal-label: Analysis Workspace
subfeature_v2:
  - id: c9bb7ea6-c04f-4262-b69c-fbb8d91e3559
    internal-label: Streaming Media
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 8%
---

# Anúncio concluído

O evento de conclusão do anúncio indica que um anúncio individual terminou de ser reproduzido. Enviá-lo depois que o anúncio for reproduzido até a conclusão. Se o visualizador ignorar o anúncio, envie [Ignorar anúncio](ad-skip.md).

* **Pré-requisitos**: [Início da sessão](../session/session-start.md), [Início de quebra de anúncio](ad-break-start.md), [Início de anúncio](ad-start.md)
* **Métrica associada**: [[!UICONTROL Anúncio concluído]](/help/reporting/metrics/ad-completes.md)

>[!IMPORTANT]
>
>Este evento deve estar entre `adBreakStart` e `adBreakComplete` delimitadores, mesmo quando um único anúncio é reproduzido. Sem esses delimitadores, os eventos de anúncio são ignorados e a duração do anúncio é contada como a duração do conteúdo principal.

## Tipos de implementação recomendados

>[!BEGINTABS]

>[!TAB Web SDK]

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

>[!TAB iOS]

Chame `trackEvent` com o tipo de evento `AdComplete`.

```swift
tracker.trackEvent(event: MediaEvent.AdComplete, info: nil, metadata: nil)
```

>[!TAB Android]

Chame `trackEvent` com o tipo de evento `AdComplete`.

```kotlin
tracker.trackEvent(Media.Event.AdComplete, null, null)
```

>[!TAB Roku Edge]

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

>[!TAB API do Media Edge]

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

>[!ENDTABS]

## Tipos de implementação herdada (somente Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Chamar `trackEvent` com o tipo de evento `AdComplete`:

```javascript
tracker.trackEvent(ADB.Media.Event.AdComplete, null, null);
```

>[!TAB Chromecast]

Chamar `trackEvent` com o tipo de evento `AdComplete`:

```javascript
ADBMobile.media.trackEvent(ADBMobile.media.Event.AdComplete);
```

>[!TAB Roku 2.x]

Chamar `mediaTrackEvent` com o tipo de evento `MEDIA_AD_COMPLETE`:

```brightscript
adb = ADBMobile()
adb.mediaTrackEvent(adb.MEDIA_AD_COMPLETE)
```

>[!TAB API da coleção de mídia]

Enviar uma POSTAGEM `adComplete` para o [ponto de extremidade de eventos](https://developer.adobe.com/analytics-collection-apis/methods/media-collection/events):

```json
{
  "playerTime": { "playhead": 15, "ts": 1699523820000 },
  "eventType": "adComplete"
}
```

>[!ENDTABS]
