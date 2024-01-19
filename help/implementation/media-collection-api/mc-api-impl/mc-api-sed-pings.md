---
title: Enviar eventos de ping
description: Os eventos de ping são a pulsação da Análise de mídia de transmissão. Saiba como enviar um ping programado para o conteúdo principal ou o rastreamento de anúncios.
uuid: c92c1a92-3af6-4474-9e42-ffb8f6c94b33
exl-id: 0a645363-26d5-41e7-aa16-c775253e2b1d
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: e84864164adf056f47f24d65f0400c89d53d1630
workflow-type: tm+mt
source-wordcount: '107'
ht-degree: 70%

---

# Enviar eventos de ping{#sending-ping-events}

**Você deve acionar eventos de ping a cada 10 segundos, começando após 10 segundos de reprodução, independentemente dos outros eventos de API enviados. Isso se aplica ao conteúdo principal e ao rastreamento de anúncios.**

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
