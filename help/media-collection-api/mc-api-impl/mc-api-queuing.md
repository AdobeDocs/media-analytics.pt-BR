---
title: Enfileirar eventos quando a resposta das sessões é lenta
description: 'Saiba o que fazer quando a ID de sessão for retornada após o reprodutor disparar eventos. '
uuid: 39ea59d9-89d3-4087-a806-48a43ecf0c98
exl-id: 2c23c378-c104-4256-b6e7-8eb6871f62da
feature: Media Analytics
role: Business Practitioner, Administrator, Data Engineer
source-git-commit: c96532bb032a4c9aaf9eed28d97fbd33ceb1516f
workflow-type: tm+mt
source-wordcount: '207'
ht-degree: 92%

---

# Enfileirar eventos quando a resposta das sessões for lenta{#queueing-events-when-sessions-response-is-slow}

A API Media Collection é RESTful: ou seja, você faz uma solicitação HTTP e espera pela resposta. Isso é importante somente quando você faz uma [Solicitação de sessões](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) para obter uma ID de sessão no início da reprodução do vídeo. Isso é importante porque a ID da sessão é necessária para todas as chamadas de rastreamento subsequentes.

O reprodutor pode disparar eventos _antes da resposta das sessões ser retornada_ (com o parâmetro da ID de sessão) do back-end. Se isso ocorrer, o aplicativo deve colocar em fila todos os eventos de rastreamento que chegam entre a [Solicitação de sessões](/help/media-collection-api/mc-api-ref/mc-api-sessions-req.md) e a resposta. Quando a resposta das sessões for recebida, primeiro você deve processar todos os [eventos](/help/media-collection-api/mc-api-ref/mc-api-events-req.md) na fila, e depois começar a processar os eventos _em tempo real_ com as chamadas de [eventos.](/help/media-collection-api/mc-api-ref/mc-api-events-req.md)

>[!NOTE]
>
>A [Solicitação de eventos](/help/media-collection-api/mc-api-ref/mc-api-events-req.md) não retorna dados ao cliente além de um código de resposta HTTP.

Verifique o Reprodutor de referência na sua distribuição para obter uma maneira de processar eventos antes de receber uma ID de sessão. Por exemplo:

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

**Processar eventos enfileirados -** O reprodutor de referência processa eventos enfileirados da seguinte forma:

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

Continue a processar os eventos de rastreamento conforme ocorrerem.
