---
seo-title: Visão geral
title: Visão geral
uuid: 4d73c47f-d0a4-4228-9040-d6432311c9eb
translation-type: tm+mt
source-git-commit: 46710c621f00374aeb55a88e51d4b720dcb941a6

---


# Visão geral{#overview}

>[!IMPORTANT]
>
>As instruções a seguir fornecem orientação para a implementação em todos os SDKs 2.x. Se estiver implementando uma versão 1.x do SDK, você pode baixar os Guias dos desenvolvedores aqui: [Baixar SDKs.](/help/sdk-implement/download-sdks.md)

Quality of experience tracking includes quality of service (QoS) and error tracking, both are optional elements and are **not** required for core media tracking implementations. Você pode usar a API do player de mídia para identificar as variáveis relacionadas ao QoS e ao rastreamento de erros. Veja abaixo os principais elementos do rastreamento da qualidade da experiência:

## Player events {#player-events}

### Em qualquer alteração de métrica de QoS:

Crie ou atualize a instância do objeto QoS para a reprodução. [QoS API Reference](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createQoSObject)

### Em todos os eventos de alteração da taxa de bits

Chama `trackEvent(Media.Heartbeat.Event.BitrateChange);`

## Implementação do QOS

1. Identify when any of QOS metrics change during media playback, create the `MediaObject` using the QoS information, and update the new QoS information.

   Variáveis de QoSObject:

   >[!TIP]
   >
   >Essas variáveis só são necessárias se você estiver planejando rastrear QoS.

   | Variável | Descrição | Obrigatório |
   | --- | --- | :---: |
   | `bitrate` | Taxa de bits atual | Sim |
   | `startupTime` | Tempo de inicialização | Sim |
   | `fps` | Valor do FPS | Sim |
   | `droppedFrames` | Número de quadros perdidos | Sim |

1. Verifique se o método `getQoSObject()` retorna as informações de QoS mais atualizadas.
1. Quando a reprodução altera as taxas de bits, chame o evento `BitrateChange` na instância do Heartbeat de mídia.

   >[!IMPORTANT]
   >
   >Atualize o objeto QoS e chame o evento de alteração da taxa de bits em cada alteração da taxa de bits. Isso fornece os dados de QoS mais precisos.

The following sample code uses the JavaScript 2.x SDK for an HTML5 media player. Use esse código com o código principal de reprodução de mídia.

```js
var mediaDelegate = new MediaHeartbeatDelegate(); 
...  
 
// This is called periodically by MediaHeartbeat instance 
mediaDelegate.prototype.getQoSObject = function() { 
    return this.qosInfo; 
}; 
 
if (e.type == "qos_update") { 
    var qosInfo = MediaHeartbeat.createQoSObject(<BITRATE>,<STARTUP_TIME>,<FPS>,<DROPPED_FRAMES>); 
    mediaDelegate.qosInfo = qosInfo; 
}; 
 
if (e.type == "bitrate_change") { 
    this.mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BitrateChange, qosObject); 
};
```

