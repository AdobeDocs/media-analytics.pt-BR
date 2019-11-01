---
title: Rastrear a qualidade da experiência no Android
description: Este tópico descreve como implementar o rastreamento de qualidade de experiência (QoE, QoS) usando o SDK de mídia no Android.
uuid: 81ff3939-48a6-45c1-8837-ddfa33490559
translation-type: tm+mt
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Rastrear a qualidade da experiência no Android{#track-quality-of-experience-on-android}

>[!IMPORTANT]
>
>As instruções a seguir fornecem orientação para a implementação em todos os SDKs 2.x. Se estiver implementando uma versão 1.x do SDK, você pode baixar os Guias dos desenvolvedores aqui: [Baixar SDKs.](/help/sdk-implement/download-sdks.md)

## Implementação de QoS

1. Identify when the bitrate changes during media playback and create the `MediaObject` instance using the QoS information.

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

   Criação do objeto de QoS:

   ```java
   MediaObject qosObject =  
     MediaHeartbeat.createQoSObject(<BITRATE>,  
                                    <STARTUP_TIME>,  
                                    <FPS>,  
                                    <DROPPED_FRAMES>);
   ```

1. Verifique se o método `getQoSObject()` retorna as informações de QoS mais atualizadas.
1. Quando a reprodução altera as taxas de bits, chame o evento `BitrateChange` na instância do Heartbeat de mídia:

   ```java
   public void onBitrateChange(Observable observable, Object data) {  
       _heartbeat.trackEvent(MediaHeartbeat.Event.BitrateChange, null, null); 
   } 
   ```

   >[!IMPORTANT]
   >
   >Atualize o objeto QoS e chame o evento de alteração da taxa de bits em cada alteração da taxa de bits. Isso fornece os dados de QoS mais precisos.

