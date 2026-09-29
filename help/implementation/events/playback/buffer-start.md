---
title: Início do buffer
description: Sinal de que o reprodutor de mídia entrou em um estado de buffering.
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
source-wordcount: '205'
ht-degree: 7%
---

# Início do buffer

O evento de início de buffer indica que o reprodutor de mídia entrou em um estado de buffering.

* **Pré-requisitos**: [Início da sessão](../session/session-start.md)
* **Métrica associada**: [[!UICONTROL Eventos de buffer]](/help/reporting/metrics/buffer-events.md)

>[!NOTE]
>
>**APIs baseadas em XDM (Web SDK, Roku, API do Media Edge, API da Coleção de Mídia):** Não há tipo de evento de retomada de buffer; o fim do buffer é inferido quando você envia um evento [`play`](play.md) após `bufferStart`.
>
>**SDK móvel:** Chame `trackEvent(BufferComplete)` quando o player sair do buffering e, em seguida, chame `trackPlay()` para retomar a reprodução.

## Tipos de implementação recomendados

>[!BEGINTABS]

>[!TAB Web SDK]

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

>[!TAB iOS]

Chame `trackEvent` com `BufferStart` quando o player entrar em um estado de buffering e `BufferComplete` quando ele sair.

```swift
// Buffer starts
tracker.trackEvent(event: MediaEvent.BufferStart, info: nil, metadata: nil)

// Buffer ends
tracker.trackEvent(event: MediaEvent.BufferComplete, info: nil, metadata: nil)
```

>[!TAB Android]

Chame `trackEvent` com `BufferStart` quando o player entrar em um estado de buffering e `BufferComplete` quando ele sair.

```kotlin
// Buffer starts
tracker.trackEvent(Media.Event.BufferStart, null, null)

// Buffer ends
tracker.trackEvent(Media.Event.BufferComplete, null, null)
```

>[!TAB Roku Edge]

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

>[!TAB API do Media Edge]

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

>[!ENDTABS]

## Tipos de implementação herdada (somente Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Chamar `trackEvent` com o tipo de evento `BufferStart`:

```javascript
tracker.trackEvent(ADB.Media.Event.BufferStart, null, null);
```

>[!TAB Chromecast]

Chame `trackEvent` com `BufferStart` quando o player entrar em um estado de buffering e `BufferComplete` quando ele sair:

```javascript
// Buffer starts
ADBMobile.media.trackEvent(ADBMobile.media.Event.BufferStart);

// Buffer ends
ADBMobile.media.trackEvent(ADBMobile.media.Event.BufferComplete);
```

>[!TAB Roku 2.x]

Chame `mediaTrackEvent` com `MEDIA_BUFFER_START` quando o player entrar em um estado de buffering e `MEDIA_BUFFER_COMPLETE` quando ele sair:

```brightscript
adb = ADBMobile()

' Buffer starts
adb.mediaTrackEvent(adb.MEDIA_BUFFER_START)

' Buffer ends
adb.mediaTrackEvent(adb.MEDIA_BUFFER_COMPLETE)
```

>[!TAB API da coleção de mídia]

Enviar uma POSTAGEM `bufferStart` para o [ponto de extremidade de eventos](https://developer.adobe.com/analytics-collection-apis/methods/media-collection/events):

```json
{
  "playerTime": { "playhead": 45, "ts": 1699523820000 },
  "eventType": "bufferStart"
}
```

>[!ENDTABS]
