---
title: Fim da sessão
description: Feche imediatamente uma sessão de mídia quando o visualizador abandonar o conteúdo.
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 14%

---


# Fim da sessão

O evento de fim de sessão fecha imediatamente uma sessão de rastreamento de mídia. Use-a quando o visualizador abandonar o conteúdo antes de atingir o fim e você não quiser que os eventos subsequentes sejam rastreados na mesma sessão. Se o visualizador terminar o conteúdo, chame [Sessão concluída](session-complete.md).

Sem um fim de sessão explícito, uma sessão é fechada automaticamente após 10 minutos sem eventos ou 30 minutos sem movimento do indicador de reprodução.

* **Pré-requisitos**: [Início da sessão](session-start.md)
* **Métrica associada**: nenhuma

## SDK da web

Chamar [`sendEvent`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/collection/js/commands/sendevent/overview) com `eventType: "media.sessionEnd"`:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.sessionEnd",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 45
    }
  }
});
```

## SDK móvel

Chame `trackSessionEnd` quando o visualizador fechar o reprodutor ou sair.

**iOS (Swift)**

```swift
tracker.trackSessionEnd()
```

**Android (Kotlin)**

```kotlin
tracker.trackSessionEnd()
```

## Roku (BrightScript)

Chamar `sendMediaEvent` com `eventType: "media.sessionEnd"`:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.sessionEnd",
        "mediaCollection": {
            "playhead": 45
        }
    }
})
```

## API de borda de mídia

Chame o ponto de extremidade [sessionEnd](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/sessions/#sessionend):

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/sessionEnd?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.sessionEnd",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 45
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## SDK de mídia

Chame `trackSessionEnd` quando o visualizador fechar o reprodutor ou sair:

```javascript
tracker.trackSessionEnd();
```

## API da coleção de mídia

Enviar uma POSTAGEM `sessionEnd` para o [ponto de extremidade de eventos](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md):

```json
{
  "playerTime": { "playhead": 45, "ts": 1699523820000 },
  "eventType": "sessionEnd"
}
```
