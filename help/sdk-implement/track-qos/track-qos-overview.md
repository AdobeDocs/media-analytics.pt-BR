---
seo-title: Visão geral
title: Visão geral
uuid: 4 d 73 c 47 f-d 0 a 4-4228-9040-d 6432311 c 9 eb
translation-type: tm+mt
source-git-commit: 46710c621f00374aeb55a88e51d4b720dcb941a6

---


# Visão geral{#overview}

>[!IMPORTANT]
>
>As instruções a seguir fornecem orientação para a implementação em todos os SDKs 2.x. Se estiver implementando uma versão 1.x do SDK, você pode baixar os Guias dos desenvolvedores aqui: [Baixar SDKs.](/help/sdk-implement/download-sdks.md)

Quality of experience tracking includes quality of service (QoS) and error tracking, both are optional elements and are **not** required for core media tracking implementations. Você pode usar a API do player de mídia para identificar as variáveis relacionadas a qos e rastreamento de erros. Veja abaixo os principais elementos do rastreamento da qualidade da experiência:

## Eventos do player {#player-events}

### Em qualquer alteração de métrica de QoS:

Crie ou atualize a instância do objeto QoS para a reprodução. [Referência da API de qos](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createQoSObject)

### Em todos os eventos de alteração da taxa de bits

Chama `trackEvent(Media.Heartbeat.Event.BitrateChange);`

## Proemement QOS

1. Identify when any of QOS metrics change during media playback, create the `MediaObject` using the QoS information, and update the new QoS information.

   Variáveis de QoSObject:

   >[!TIP]
   >
   >Essas variáveis só serão necessárias se você estiver planejando o rastreamento de qos.

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
   >Atualize o objeto qos e chame o evento de alteração da taxa de bits em cada alteração de taxa de bits. Isso fornece os dados de QoS mais precisos.

O código de exemplo a seguir usa o SDK do javascript 2. x para um player de mídia HTML 5. Você deve usar este código com o código de reprodução de mídia principal.

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

