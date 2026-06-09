---
title: Ping
description: Envie um heartbeat para manter a sessão de mídia ativa e rastrear o progresso da reprodução em intervalos regulares.
feature: Streaming Media
role: Developer
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '283'
ht-degree: 1%

---


# Ping

O evento ping é um heartbeat que mantém a sessão ativa e rastreia o progresso da reprodução. Enviá-lo em um cronômetro durante toda a reprodução. Nos SDKs móveis, os pings são enviados automaticamente; em todas as outras plataformas, eles devem ser enviados manualmente no intervalo especificado.

* **Conteúdo principal**: primeiro ping 10 segundos após o início da reprodução, depois a cada 10 segundos
* **Conteúdo do anúncio**: a cada 1 segundo durante o rastreamento do anúncio

Não inclua um objeto `params` no corpo da solicitação de ping.

* **Pré-requisitos**: [Início da sessão](../session/session-start.md)
* **Métrica associada**: nenhuma

## Tipos de implementação recomendados

>[!BEGINTABS]

>[!TAB Web SDK]

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

>[!TAB iOS]

O Mobile SDK envia eventos de ping automaticamente. Nenhuma chamada explícita é necessária.

>[!TAB Android]

O Mobile SDK envia eventos de ping automaticamente. Nenhuma chamada explícita é necessária.

>[!TAB Roku Edge]

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

>[!TAB API do Media Edge]

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

>[!ENDTABS]

## Tipos de implementação herdada (somente Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

O Media SDK envia eventos de ping automaticamente. Nenhuma chamada explícita é necessária.

>[!TAB Chromecast]

O SDK do Chromecast envia eventos de ping automaticamente. Nenhuma chamada explícita é necessária.

>[!TAB Roku 2.x]

O Media SDK envia eventos de ping automaticamente, desde que você chame `processMediaMessages` no loop do evento. Atualize o indicador de reprodução para que cada ping reporte a posição atual:

```brightscript
ADBMobile().mediaUpdatePlayhead(10)
```

>[!TAB API da coleção de mídia]

Envie uma POSTAGEM `ping` para o [ponto de extremidade de eventos](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md) em um timer. Não inclua um objeto `params`:

```json
{
  "playerTime": { "playhead": 10, "ts": 1699523820000 },
  "eventType": "ping"
}
```

>[!ENDTABS]
