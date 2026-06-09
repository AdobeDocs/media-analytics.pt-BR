---
title: Erro
description: Sinal de que o reprodutor de mídia encontrou um erro.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 9%

---


# Erro

O evento de erro indica que o reprodutor de mídia encontrou um erro. O rastreamento de um erro não encerra a sessão. Se o erro impedir que a reprodução continue, chame [Fim da sessão](session/session-end.md) após o evento de erro.

* **Pré-requisitos**: [Início da sessão](session/session-start.md)
* **Métrica associada**: [[!UICONTROL Fluxos afetados pelo erro]](/help/reporting/metrics/error-impacted-streams.md)

A propriedade `errorDetails.source` aceita apenas dois valores: `player` (erros originados no reprodutor de mídia) e `external` (erros de uma fonte externa, como um CDN ou uma rede).

## Tipos de implementação recomendados

>[!BEGINTABS]

>[!TAB Web SDK]

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

>[!TAB iOS]

Chame `trackError` com uma cadeia de caracteres de ID de erro.

```swift
tracker.trackError(errorId: "media-error-001")
```

>[!TAB Android]

Chame `trackError` com uma cadeia de caracteres de ID de erro.

```kotlin
tracker.trackError("media-error-001")
```

>[!TAB Roku Edge]

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

>[!TAB API do Media Edge]

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

>[!ENDTABS]

## Tipos de implementação herdada (somente Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Chame `trackError` com uma cadeia de caracteres de ID de erro:

```javascript
tracker.trackError("media-error-001");
```

>[!TAB Chromecast]

Chame `trackError` com uma cadeia de caracteres de ID de erro:

```javascript
ADBMobile.media.trackError("media-error-001");
```

>[!TAB Roku 2.x]

Chame `mediaTrackError` com uma ID de erro e a origem do erro. Usar a constante `ERROR_SOURCE_PLAYER` para erros do player:

```brightscript
adb = ADBMobile()
adb.mediaTrackError("media-error-001", adb.ERROR_SOURCE_PLAYER)
```

>[!TAB API da coleção de mídia]

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

>[!ENDTABS]
