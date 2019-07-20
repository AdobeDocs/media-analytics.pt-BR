---
seo-title: Enviar eventos de ping
title: Enviar eventos de ping
uuid: c 92 c 1 a 92-3 af 6-4474-9 e 42-ffb 8 f 6 c 94 b 33
translation-type: tm+mt
source-git-commit: 6468ace2e30db1a427a3d7f1b080ab42c578351a

---


# Enviar eventos de ping{#sending-ping-events}

**Para o conteúdo principal, você deve acionar eventos de ping a cada 10 segundos, começando após 10 segundos de reprodução, independentemente dos outros eventos de API enviados. For Ad tracking, you must fire ping events every 1 second.**

Os eventos ping são literalmente a "pulsação" do Media Analytics. Os únicos parâmetros necessários para uma chamada de ping são `eventType: ping`, juntamente com o objeto `playerTime` (posição do indicador de reprodução e carimbo de data e hora).

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

