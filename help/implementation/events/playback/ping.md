---
title: Ping
description: Envie um heartbeat para manter a sessão de mídia ativa e rastrear o progresso da reprodução em intervalos regulares.
feature: Streaming Media
role: Developer
source-git-commit: b75e50f626b85992575961ea267d0f74eda09f0a
workflow-type: tm+mt
source-wordcount: '198'
ht-degree: 6%

---


# Ping

O evento ping é um heartbeat que mantém a sessão ativa e rastreia o progresso da reprodução. Enviá-lo em um cronômetro durante toda a reprodução.

* **Conteúdo principal**: primeiro ping 10 segundos após o início da reprodução, depois a cada 10 segundos
* **Conteúdo do anúncio**: a cada 1 segundo durante o rastreamento do anúncio

Não inclua um objeto `params` no corpo da solicitação de ping.

* **Pré-requisitos**: [Início da sessão](../session/session-start.md)
* **Métrica associada**: nenhuma

## SDK da web

Agendar uma chamada recorrente de `sendEvent` com `eventType: "media.ping"`. Atualize `playhead` para a posição de reprodução atual em cada chamada:

```javascript
alloy("sendEvent", {
  xdm: {
    eventType: "media.ping",
    mediaCollection: {
      sessionID: "{sid}",
      playhead: 10
    }
  }
});
```

## SDK móvel

O Mobile SDK envia eventos de ping automaticamente. Nenhuma chamada explícita é necessária.

## Roku (BrightScript)

Agendar uma chamada recorrente de `sendMediaEvent` com `eventType: "media.ping"`. Atualize `playhead` para a posição de reprodução atual em cada chamada:

```brightscript
m.aepSdk.sendMediaEvent({
    "xdm": {
        "eventType": "media.ping",
        "mediaCollection": {
            "playhead": 10
        }
    }
})
```

## API de borda de mídia

Chame o ponto de extremidade [ping](https://developer.adobe.com/data-collection-apis/docs/endpoints/media/ping/) em um timer. A Adobe recomenda que o primeiro ping seja executado 10 segundos após o início da reprodução principal, a cada 10 segundos após e a cada 1 segundo durante o rastreamento de anúncios:

```sh
curl -X POST "https://edge.adobedc.net/ee/va/v1/ping?configId={datastreamID}" \
--header 'Content-Type: application/json' \
--data '{
  "events": [{
    "xdm": {
      "eventType": "media.ping",
      "mediaCollection": {
        "sessionID": "{sid}",
        "playhead": 10
      },
      "timestamp": "YYYY-08-20T22:41:40+00:00"
    }
  }]
}'
```

## SDK de mídia

O Media SDK envia eventos de ping automaticamente. Nenhuma chamada explícita é necessária.

## API da coleção de mídia

Envie uma POSTAGEM `ping` para o [ponto de extremidade de eventos](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) em um timer. Não inclua um objeto `params`:

```json
{
  "playerTime": { "playhead": 10, "ts": 1699523820000 },
  "eventType": "ping"
}
```
