---
title: Enfileirar eventos quando a resposta das sessões é lenta
description: Saiba o que fazer quando a ID de sessão for retornada após o player disparar eventos.
uuid: 39ea59d9-89d3-4087-a806-48a43ecf0c98
exl-id: 2c23c378-c104-4256-b6e7-8eb6871f62da
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '205'
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
