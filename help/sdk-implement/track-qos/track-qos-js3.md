---
title: Acompanhar a qualidade da experiência usando o JavaScript 3.x
description: Este tópico descreve como implementar o rastreamento de qualidade de experiência (QoE, QoS) usando o SDK de mídia em aplicativos de navegador usando o JavaScript 3x.
translation-type: tm+mt
source-git-commit: b165c9d133637fd0f1c529a98a936f8f31b72465
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 49%

---


# Acompanhar a qualidade da experiência usando o JavaScript 3.x{#track-quality-of-experience-on-javascript}

>[!IMPORTANT]
>
>As instruções a seguir fornecem orientação para a implementação em todos os SDKs 3.x. If you are implementing any previous versions of the SDK, you can download the Developers Guides here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

## Implementar QOE

1. Identify when the bitrate changes during media playback and create the `qoeObject` instance using the QoE information.

   Variáveis QoEObject:

   >[!TIP]
   >
   >Essas variáveis somente são necessárias se você estiver planejando rastrear QoS.

   | Variável | Tipo | Descrição |
   | --- | --- | --- |
   | `bitrate` | número | Taxa de bits atual |
   | `startupTime` | número | Tempo de inicialização |
   | `fps` | número | Valor do FPS |
   | `droppedFrames` | número | Número de quadros perdidos |

   Criação de objetos QoE:

   ```js
   // Replace <bitrate>, <startuptime>, <fps> and
   // <droppeFrames> with the current playback QoE values.
   var qoeObject = ADB.Media.createQoEObject(<bitrate>,
                                                  <startuptime>,
                                                  <fps>,
                                                  <droppedFrames>);
   ```

1. Quando a reprodução altera as taxas de bits, chame o evento `BitrateChange` na instância do Heartbeat de mídia:

   ```js
   _onBitrateChange = function() {
       // If the new bitrate value is available provide it to the tracker.
       var qoeObject = ADB.Media.createQoEObject(1000000, 2.4, 25, 10);
       tracker.updateQoEObject(qoeObject);
   
       tracker.trackEvent(ADB.Media.Event.BitrateChange);
   };
   ```

   >[!IMPORTANT]
   >
   >Atualize o objeto QoE e chame o evento de alteração da taxa de bits em cada alteração da taxa de bits. Isso fornece os dados de QoE mais precisos.

1. Certifique-se de chamar o `updateQoEObject()` método para fornecer as informações de QoE mais atualizadas para o SDK.
1. Quando o reprodutor de mídia encontra um erro e o evento de erro está disponível para a API do reprodutor, use `trackError()` para capturar as informações do erro. (Consulte [Visão geral](/help/sdk-implement/track-errors/track-errors-overview.md).)

   >[!TIP]
   >
   >O rastreamento de erros do reprodutor de mídia não interrompe a sessão de rastreamento de mídia. Se o reprodutor de mídia estiver impedindo o andamento da reprodução, certifique-se de que a sessão de monitoramento de mídia está fechada, chamando `trackSessionEnd()` após chamar `trackError()`.
