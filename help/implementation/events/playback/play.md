---
title: Reproduzir
description: Sinal de que o reprodutor de mídia entrou no estado de reprodução.
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
source-wordcount: '187'
ht-degree: 9%
---

# Reproduzir

O evento de reprodução indica que o reprodutor de mídia mudou de estado para reproduzido. Enviá-lo no início do conteúdo, na reprodução automática e sempre que o reprodutor for retomado após uma pausa ou buffer. Não há evento de retomada separado; um evento de reprodução após [Início da pausa](pause-start.md) ou [Início do buffer](buffer-start.md) serve como retomada.

* **Pré-requisitos**: [Início da sessão](../session/session-start.md)
* **Métrica associada**: [[!UICONTROL Início do conteúdo]](/help/reporting/metrics/content-starts.md)

## Tipos de implementação recomendados

>[!BEGINTABS]

>[!TAB Web SDK]

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

>[!TAB iOS]

Chame `trackPlay` quando o reprodutor de mídia iniciar ou retomar a reprodução.

```swift
tracker.trackPlay()
```

>[!TAB Android]

Chame `trackPlay` quando o reprodutor de mídia iniciar ou retomar a reprodução.

```kotlin
tracker.trackPlay()
```

>[!TAB Roku Edge]

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

>[!TAB API do Media Edge]

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

>[!ENDTABS]

## Tipos de implementação herdada (somente Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Chame `trackPlay` quando o reprodutor de mídia iniciar ou retomar a reprodução:

```javascript
tracker.trackPlay();
```

>[!TAB Chromecast]

Chame `trackPlay` quando o reprodutor de mídia iniciar ou retomar a reprodução:

```javascript
ADBMobile.media.trackPlay();
```

>[!TAB Roku 2.x]

Chame `mediaTrackPlay` quando o reprodutor de mídia iniciar ou retomar a reprodução:

```brightscript
ADBMobile().mediaTrackPlay()
```

>[!TAB API da coleção de mídia]

Enviar uma POSTAGEM `play` para o [ponto de extremidade de eventos](https://developer.adobe.com/analytics-collection-apis/methods/media-collection/events):

```json
{
  "playerTime": { "playhead": 0, "ts": 1699523820000 },
  "eventType": "play"
}
```

>[!ENDTABS]
