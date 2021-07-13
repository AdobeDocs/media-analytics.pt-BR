---
title: Saiba como rastrear a qualidade da experiência no iOS
description: '"Saiba mais sobre como implementar o rastreamento de qualidade de experiência (QoE, QoS) usando o SDK do Media no iOS."'
uuid: cae2c142-ed39-4234-a711-765dcabc5415
exl-id: 7f01e6eb-95bd-4e3d-93d0-8a2e68323313
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '158'
ht-degree: 84%

---

# Rastrear a qualidade da experiência no iOS{#track-quality-of-experience-on-ios}

>[!IMPORTANT]
>
>As instruções a seguir fornecem orientação para a implementação em todos os SDKs 2.x. Se estiver implementando uma versão 1.x do SDK, você pode baixar os Guias dos desenvolvedores 1.x aqui: [Baixar SDKs.](/help/sdk-implement/download-sdks.md)

## Implementação do QOS

1. Identifique quando a taxa de bits for alterada durante a reprodução de mídia e crie a instância `MediaObject` usando as informações de QoS.

   Variáveis de QoSObject:

   | Variável | Descrição | Obrigatório |
   | --- | --- | :---: |
   | `bitrate` | Taxa de bits atual | Sim |
   | `startupTime` | Tempo de inicialização | Sim |
   | `fps` | Valor do FPS | Sim |
   | `droppedFrames` | Número de quadros perdidos | Sim |

   >[!TIP]
   >
   >Essas variáveis somente são necessárias se você estiver planejando rastrear QoS.

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
   >Atualize o objeto de QoS e chame o evento de alteração na taxa de bits em cada alteração na taxa de bits. Isso fornece os dados de QoS mais precisos.
