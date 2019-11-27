---
title: Visão geral
description: Uma visão geral da qualidade de rastreamento da experiência (QoE, QoS) usando o SDK do Media.
uuid: 4d73c47f-d0a4-4228-9040-d6432311c9eb
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Visão geral {#overview}

>[!IMPORTANT]
>
>As instruções a seguir fornecem orientação para a implementação em todos os SDKs 2.x. Se estiver implementando uma versão 1.x do SDK, você pode baixar os Guias dos desenvolvedores 1.x aqui: [Baixar SDKs.](/help/sdk-implement/download-sdks.md)

O rastreamento da qualidade da experiência inclui qualidade do serviço (QoS) e rastreamento de erros; ambos são elementos opcionais e **não** são necessários para implementações de rastreamento de mídia principal. Você pode usar a API do reprodutor de mídia para identificar as variáveis relacionadas ao rastreamento de erros e QoS. Veja abaixo os principais elementos do rastreamento da qualidade da experiência:

## Eventos do reprodutor {#player-events}

### Em qualquer alteração de métrica de QoS:

Crie ou atualize a instância do objeto QoS para a reprodução. [Referência da API QoS](https://adobe-marketing-cloud.github.io/media-sdks/reference/javascript/MediaHeartbeat.html#.createQoSObject)

### Em todos os eventos de alteração da taxa de bits

Chame `trackEvent(Media.Heartbeat.Event.BitrateChange);`

## Implementação do QOS

1. Identifique quando qualquer uma das métricas de QOS for alterada durante a reprodução da mídia, crie o `MediaObject` usando as informações de QoS e atualize as novas informações.

   Variáveis de QoSObject:

   >[!TIP]
   >
   >Essas variáveis somente são necessárias se você estiver planejando rastrear QoS.

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
   >Atualize o objeto de QoS e chame o evento de alteração na taxa de bits em cada alteração na taxa de bits. Isso fornece os dados de QoS mais precisos.

O código de exemplo a seguir usa o SDK 2.x do JavaScript para um reprodutor de mídia HTML5. Você deve usar esse código com o código de reprodução de mídia principal.

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

