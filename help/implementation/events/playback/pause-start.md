---
title: Início da pausa
description: Sinal de que o usuário pausou a reprodução de mídia.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '140'
ht-degree: 10%

---


# Início da pausa

O evento de início de pausa indica que o usuário pausou a reprodução. Não há evento de retomada separado; envie um evento [Reproduzir](play.md) quando a reprodução for retomada.

* **Pré-requisitos**: [Início da sessão](../session/session-start.md)
* **Métrica associada**: [[!UICONTROL Pausar eventos]](/help/reporting/metrics/pause-events.md)

>[!NOTE]
>
>Não há um tipo de evento de retomada. Retomar é inferido quando você envia um evento [`play`](play.md) após `pauseStart`.

## Tipos de implementação recomendados

>[!BEGINTABS]

>[!TAB Web SDK]

Chamar [`sendEvent`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/collection/js/commands/sendevent/overview) com `eventType: "media.pauseStart"`:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.pauseStart",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 30
    }
  }
});
```

>[!TAB iOS]

Chame `trackPause` quando o usuário pausar a reprodução.

```swift
tracker.trackPause()
```

>[!TAB Android]

Chame `trackPause` quando o usuário pausar a reprodução.

```kotlin
tracker.trackPause()
```

>[!TAB Roku]

Chamar `sendMediaEvent` com `eventType: "media.pauseStart"`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.pauseStart",
        "mediaCollection": {
            "playhead": 30
        }
    }
})
```

>[!TAB API do Media Edge]

Chame o ponto de extremidade [pauseStart](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/pausestart/):

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/pauseStart?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.pauseStart",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 30
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

Chamar `trackPause` quando o usuário pausar a reprodução:

```javascript
tracker.trackPause();
```

>[!TAB Chromecast]

Chamar `trackPause` quando o usuário pausar a reprodução:

```javascript
ADBMobile.media.trackPause();
```

>[!TAB API da coleção de mídia]

Enviar uma POSTAGEM `pauseStart` para o [ponto de extremidade de eventos](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md):

```json
{
  "playerTime": { "playhead": 30, "ts": 1699523820000 },
  "eventType": "pauseStart"
}
```

>[!ENDTABS]
