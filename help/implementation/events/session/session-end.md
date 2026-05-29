---
title: Fim da sessão
description: Feche imediatamente uma sessão de mídia quando o visualizador abandonar o conteúdo.
feature: Streaming Media
role: Developer
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '300'
ht-degree: 5%

---


# Fim da sessão

O evento de término de sessão fecha imediatamente e irreversivelmente uma sessão de rastreamento de mídia. O término da sessão é um encerramento permanente — uma vez enviada, a sessão é encerrada e nenhum outro evento pode ser rastreado nela. Use Sessão somente quando tiver certeza de que nenhum evento adicional acontecerá, como quando o reprodutor for destruído ou a página for descarregada. Na maioria dos casos, é mais seguro permitir que a sessão expire naturalmente, em vez de correr o risco de interromper eventos que ainda podem chegar. Se o visualizador terminar o conteúdo, chame [Sessão concluída](session-complete.md).

Sem um fim de sessão explícito, uma sessão é fechada automaticamente após 10 minutos sem eventos ou 30 minutos sem movimento do indicador de reprodução.

>[!NOTE]
>
>Você pode chamar com segurança o término de uma sessão mais de uma vez para a mesma sessão. O backend fecha a sessão no primeiro evento e descarta silenciosamente todos os eventos subsequentes dessa ID de sessão, incluindo um segundo fim de sessão. Você não precisa se proteger contra chamadas duplicadas em condições de corrida, como um tempo limite de 30 minutos expirando ao mesmo tempo em que o visualizador fecha o reprodutor.

* **Pré-requisitos**: [Início da sessão](session-start.md)
* **Métrica associada**: nenhuma

## Tipos de implementação recomendados

>[!BEGINTABS]

>[!TAB Web SDK]

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

>[!TAB iOS]

Chame `trackSessionEnd` quando o visualizador fechar o reprodutor ou sair.

```swift
tracker.trackSessionEnd()
```

>[!TAB Android]

Chame `trackSessionEnd` quando o visualizador fechar o reprodutor ou sair.

```kotlin
tracker.trackSessionEnd()
```

>[!TAB Roku]

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

>[!TAB API do Media Edge]

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

>[!ENDTABS]

## Tipos de implementação herdada (somente Analytics)

>[!BEGINTABS]

>[!TAB Media SDK JS 3.x]

Chame `trackSessionEnd` quando o visualizador fechar o reprodutor ou sair:

```javascript
tracker.trackSessionEnd();
```

>[!TAB Chromecast]

Chame `trackSessionEnd` quando o visualizador fechar o reprodutor ou sair:

```javascript
ADBMobile.media.trackSessionEnd();
```

>[!TAB API da coleção de mídia]

Enviar uma POSTAGEM `sessionEnd` para o [ponto de extremidade de eventos](/help/implementation/media-collection-api/mc-api-ref/mc-api-events-req.md):

```json
{
  "playerTime": { "playhead": 45, "ts": 1699523820000 },
  "eventType": "sessionEnd"
}
```

>[!ENDTABS]
