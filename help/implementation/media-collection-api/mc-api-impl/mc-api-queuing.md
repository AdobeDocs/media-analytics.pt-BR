---
title: Enfileirar eventos quando a resposta das sessões é lenta
description: Saiba o que fazer quando a ID de sessão for retornada após o player disparar eventos.
uuid: 39ea59d9-89d3-4087-a806-48a43ecf0c98
exl-id: 2c23c378-c104-4256-b6e7-8eb6871f62da
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/maOCcXZJkPef7edi3UtaSIJKa-4x9byaH6Qzt2eDR2Y
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 205
ht-degree: 80%

---

# Enfileirar eventos quando a resposta das sessões é lenta{#queueing-events-when-sessions-response-is-slow}

A API Media Collection é RESTful: ou seja, você faz uma solicitação HTTP e espera pela resposta. Isso é importante somente quando você faz uma [Solicitação de sessões](../mc-api-ref/mc-api-sessions-req.md) para obter uma ID de sessão no início da reprodução do vídeo. Isso é importante porque a ID da sessão é necessária para todas as chamadas de rastreamento subsequentes.

O reprodutor pode disparar eventos _antes da resposta das sessões ser retornada_ (com o parâmetro da ID de sessão) do back-end. Se isso ocorrer, o aplicativo deve colocar em fila todos os eventos de rastreamento que chegam entre a [Solicitação de sessões](../mc-api-ref/mc-api-sessions-req.md) e a resposta. Quando a resposta das sessões for recebida, primeiro você deve processar todos os [eventos](../mc-api-ref/mc-api-events-req.md) na fila, e depois começar a processar os eventos _em tempo real_ com as chamadas de [eventos.](../mc-api-ref/mc-api-events-req.md)

>[!NOTE]
>
>A [Solicitação de eventos](../mc-api-ref/mc-api-events-req.md) não retorna dados ao cliente além de um código de resposta HTTP.

Verifique o reprodutor de referência na distribuição para saber como processar eventos antes de receber uma ID de sessão. Por exemplo:

```js
var eventData = {};            // JSON payload 
eventData.playerTime = getPlayerTime(); // Required 
eventData.eventType = "play";           // Required 
eventData.params = {};                  // Optional for events 
 
VideoPlayer.prototype._collectEvent =  
  function(eventData) { 
 
    // If we don't have a Session ID yet,  
    // queue the event and return... 
    if (!sessionStarted) { 
        console.log("[Player] Queueing event "); 
        _pendingEvents.push(eventData); 
        return; 
    } 
 
    // If we DO have a Session ID, process the 
    // tracking event...     
    apiClient.request({ 
        "baseUrl": "{endpoint}", 
        "path": "api/v1/{sid}/events", // events request 
        "method": "POST", 
        "data": eventData 
    }).then((response) => {   
        […] 
    } 
} 
 
VideoPlayer.prototype.collectEvent =  
  function (eventType, eventParams) { 
         
    if (typeof eventParams === 'undefined') {   
        eventParams = {}; 
    } 
 
    this._collectEvent({                   
        eventType: eventType,            // Required 
        playerTime: getPlayerTime(),     // Required 
        params: eventParams              // Optional  
    });                                    
}; 
 
VideoPlayer.prototype.getPlayerTime = function() { 
    return { 
        playhead: this.getPlayhead(),    // playhead value in seconds 
        ts: this.getCurrentTimestamp()   // timestamp value in milliseconds 
    }; 
};
```

**Processar todos os eventos em fila -** O reprodutor de referência processa os eventos em fila da seguinte maneira:

```js
    […] 
    this._processPendingEvents();    // Once you have a Session ID, 
    […]                              // process any queued events 
 
VideoPlayer.prototype._processPendingEvents =  
  function() { 
    this._pendingEvents.forEach((eventData) => { 
        this._collectEvent(eventData); 
    }); 
 
    this._pendingEvents = []; 
}
```

Continue a processar os eventos de rastreamento à medida que eles ocorrerem.
