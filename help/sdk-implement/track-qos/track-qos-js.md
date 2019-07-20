---
seo-title: Rastrear a qualidade da experiência no JavaScript
title: Rastrear a qualidade da experiência no JavaScript
uuid: 3 bc 762 a 2-9706-4 b 62-aa 91-747 f 461 dd 13 d
translation-type: tm+mt
source-git-commit: ed200520b9bed990460a444dabdcf956980362ca

---


# Rastrear a qualidade da experiência no JavaScript{#track-quality-of-experience-on-javascript}

>[!IMPORTANT]
>
>As instruções a seguir fornecem orientação para a implementação em todos os SDKs 2.x. Se estiver implementando uma versão 1.x do SDK, você pode baixar os Guias dos desenvolvedores aqui: [Baixar SDKs.](../../sdk-implement/download-sdks.md)

## Proemement QOS

1. Identify when the bitrate changes during media playback and create the `MediaObject` instance using the QoS information.

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

   Criação do objeto de QoS:

   ```js
   // Replace <bitrate>, <startuptime>, <fps> and  
   // <droppeFrames> with the current playback QoS values.  
   var qosObject = MediaHeartbeat.createQoSObject(<bitrate>,  
                                                  <startuptime>,  
                                                  <fps>,  
                                                  <droppedFrames>); 
   ```

1. Quando a reprodução altera as taxas de bits, chame o evento `BitrateChange` na instância do Heartbeat de mídia:

   ```js
   _onBitrateChange = function() { 
       this._mediaHeartbeat.trackEvent(MediaHeartbeat.Event.BitrateChange, qosObject); 
   };
   ```

   >[!IMPORTANT]
   >
   >Atualize o objeto qos e chame o evento de alteração da taxa de bits em cada alteração de taxa de bits. Isso fornece os dados de QoS mais precisos.

1. Verifique se o método `getQoSObject()` retorna as informações de QoS mais atualizadas.
1. When the media player encounters an error, and the error event is available to the player API, use `trackError()` to capture the error information. (See [Overview](../../sdk-implement/track-errors/track-errors-overview.md).)

   >[!TIP]
   >
   >Os erros do player de mídia não interromperem a sessão de rastreamento de mídia. If the media player error prevents the playback from continuing, make sure that the media tracking session is closed by calling `trackSessionEnd()` after calling `trackError()`.

