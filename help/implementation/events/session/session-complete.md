---
title: Sessão concluída
description: Sinal de que o visualizador atingiu o fim do conteúdo principal.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '165'
ht-degree: 9%

---


# Sessão concluída

O evento de conclusão da sessão indica que o visualizador atingiu o fim do conteúdo principal. A sessão não é encerrada imediatamente; a sessão permanece aberta até expirar naturalmente. Se quiser fechar a sessão imediatamente, chame [Fim da sessão](session-end.md).

* **Pré-requisitos**: [Início da sessão](session-start.md)
* **Métrica associada**: [[!UICONTROL Conteúdo concluído]](/help/reporting/metrics/content-completes.md)

## Tipos de implementação recomendados

>[!BEGINTABS]

>[!TAB Web SDK]

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

>[!TAB iOS]

Chame `trackComplete` quando o reprodutor de mídia atingir o fim do conteúdo.

```swift
tracker.trackComplete()
```

>[!TAB Android]

Chame `trackComplete` quando o reprodutor de mídia atingir o fim do conteúdo.

```kotlin
tracker.trackComplete()
```

>[!TAB Roku]

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

>[!TAB API do Media Edge]

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

>[!ENDTABS]

## Tipos de implementação herdada (somente Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Chame `trackComplete` quando o reprodutor de mídia atingir o fim do conteúdo:

```javascript
tracker.trackComplete();
```

>[!TAB Chromecast]

Chame `trackComplete` quando o reprodutor de mídia atingir o fim do conteúdo:

```javascript
ADBMobile.media.trackComplete();
```

>[!TAB API da coleção de mídia]

Enviar uma POSTAGEM `sessionComplete` para o [ponto de extremidade de eventos](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md):

```json
{
  "playerTime": { "playhead": 128, "ts": 1699523820000 },
  "eventType": "sessionComplete"
}
```

>[!ENDTABS]
