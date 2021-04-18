---
title: Enviar eventos de ping
description: Enviar eventos de ping
uuid: c92c1a92-3af6-4474-9e42-ffb8f6c94b33
exl-id: 0a645363-26d5-41e7-aa16-c775253e2b1d
translation-type: tm+mt
source-git-commit: d4491dfec33d8729f40bcef1d57622467443bdbb
workflow-type: tm+mt
source-wordcount: '88'
ht-degree: 100%

---

# Enviar eventos de ping {#sending-ping-events}

**Para o conteúdo principal, você deve acionar eventos de ping a cada 10 segundos, começando após 10 segundos de reprodução, independentemente dos outros eventos de API enviados. Para o rastreamento de anúncios, você deve disparar os eventos de ping a cada 1 segundo.**

Os eventos de ping são literalmente o &quot;heartbeat&quot; do Media Analytics. Os únicos parâmetros necessários para uma chamada de ping são `eventType: ping`, juntamente com o objeto `playerTime` (posição do indicador de reprodução e carimbo de data e hora).

O fragmento de código a seguir mostra uma maneira de implementar um mecanismo de ping temporizado para o conteúdo principal (intervalo de 10 segundos):

```js
... 
Pinger.init(10000); 
... 
Pinger.kill();

var Pinger = { 
    init: function(interval) { 
        this._timer = window.setInterval(function() { 
                $.event.trigger({type: "onPing", _data: ""}); 
            }, interval); 
    }, 
     
    kill: function() { 
        window.clearInterval(this._timer); 
    } 
}
```
