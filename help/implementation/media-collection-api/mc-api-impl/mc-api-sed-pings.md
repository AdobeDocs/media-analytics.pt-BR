---
title: Enviar eventos de ping
description: Os eventos de ping são a pulsação dos serviços de streaming de mídia da Adobe. Saiba como enviar um ping programado para o conteúdo principal ou o rastreamento de anúncios.
uuid: c92c1a92-3af6-4474-9e42-ffb8f6c94b33
exl-id: 0a645363-26d5-41e7-aa16-c775253e2b1d
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/EJ6R7DILB56bcHgAki-Lvto3yYbuhf-wYfklvPElDeM
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
source-wordcount: 110
ht-degree: 50%

---

# Enviar eventos de ping{#sending-ping-events}

**Você deve acionar eventos de ping a cada 10 segundos, começando após 10 segundos de reprodução, independentemente dos outros eventos de API enviados. Isso se aplica ao conteúdo principal e ao rastreamento de anúncios.**

Os eventos de ping são o &quot;heartbeat&quot; dos serviços de mídia de transmissão da Adobe. Os únicos parâmetros necessários para uma chamada de ping são `eventType: ping`, juntamente com o objeto `playerTime` (posição do indicador de reprodução e carimbo de data e hora).

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
