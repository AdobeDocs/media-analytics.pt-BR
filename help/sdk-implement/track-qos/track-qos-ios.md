---
seo-title: Rastrear a qualidade da experiência no iOS
title: Rastrear a qualidade da experiência no iOS
uuid: cae 2 c 142-ed 39-4234-a 711-765 dcabc 5415
translation-type: tm+mt
source-git-commit: ed200520b9bed990460a444dabdcf956980362ca

---


# Rastrear a qualidade da experiência no iOS{#track-quality-of-experience-on-ios}

>[!IMPORTANT]
>
>As instruções a seguir fornecem orientação para a implementação em todos os SDKs 2.x. Se estiver implementando uma versão 1.x do SDK, você pode baixar os Guias dos desenvolvedores aqui: [Baixar SDKs.](../../sdk-implement/download-sdks.md)

## Proemement QOS

1. Identify when the bitrate changes during media playback and create the `MediaObject` instance using the QoS information.

   Variáveis de QoSObject:

   | Variável | Descrição | Obrigatório |
   | --- | --- | :---: |
   | `bitrate` | Taxa de bits atual | Sim |
   | `startupTime` | Tempo de inicialização | Sim |
   | `fps` | Valor do FPS | Sim |
   | `droppedFrames` | Número de quadros perdidos | Sim |

   >[!TIP]
   >
   >Essas variáveis só serão necessárias se você estiver planejando o rastreamento de qos.

   Criação do objeto de QoS:

   ```
   id qosObject = [ADBMediaHeartbeat createQoSObjectWithBitrate:[BITRATE] 
                                     startupTime:[STARTUP_TIME]  
                                     fps:[FPS]  
                                     droppedFrames:[DROPPED_FRAMES]];
   ```

1. Verifique se o método `getQoSObject` retorna as informações de QoS mais atualizadas.
1. Quando a reprodução altera as taxas de bits, chame o evento `BitrateChange` na instância do Heartbeat de mídia:

   ```
   - (void)onBitrateChange:(NSNotification *)notification { 
       [_mediaHeartbeat trackEvent:ADBMediaHeartbeatEventBitrateChange  
                        mediaObject:nil  
                        data:nil]; 
   }
   ```

   >[!IMPORTANT]
   >
   >Atualize o objeto qos e chame o evento de alteração da taxa de bits em cada alteração de taxa de bits. Isso fornece os dados de QoS mais precisos.

