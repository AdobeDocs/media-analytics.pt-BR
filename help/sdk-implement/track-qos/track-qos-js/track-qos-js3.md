---
title: Saiba como rastrear a qualidade da experiência usando o JavaScript 3.x
description: '"Saiba mais sobre como implementar o rastreamento de qualidade de experiência (QoE, QoS) usando o SDK do Media em aplicativos de navegador usando JavaScript 3x."'
exl-id: b5570e9c-8fb1-4458-bd1a-86ff6fce7813
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: b6df391016ab4b9095e3993808a877e3587f0a51
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 58%

---

# Rastrear a qualidade da experiência usando o JavaScript 3.x{#track-quality-of-experience-on-javascript}

>[!IMPORTANT]
>
>As instruções a seguir fornecem orientação para a implementação em todos os SDKs 3.x. Se estiver implementando uma versão anterior do SDK, você pode baixar os Guias dos desenvolvedores Anterior aqui: [Baixar SDKs.](/help/sdk-implement/download-sdks.md)

## Implementar QOE

1. Identifique quando a taxa de bits é alterada durante a reprodução de mídia e crie a instância `qoeObject` usando as informações de QoE.

   Variáveis de QoEObject:

   >[!TIP]
   >
   >Essas variáveis somente são necessárias se você estiver planejando rastrear QoS.

   | Variável | Tipo | Descrição |
   | --- | --- | --- |
   | `bitrate` | número | Taxa de bits atual |
   | `startupTime` | número | Tempo de inicialização |
   | `fps` | número | Valor do FPS |
   | `droppedFrames` | número | Número de quadros perdidos |

   Criação do objeto de QoE:

   ```js
   // Replace <bitrate>, <startuptime>, <fps> and
   // <droppeFrames> with the current playback QoE values.
   var qoeObject = ADB.Media.createQoEObject(<bitrate>,
                                                  <startuptime>,
                                                  <fps>,
                                                  <droppedFrames>);
   tracker.updateQoEObject(qoeObject);
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

1. Certifique-se de chamar o método `updateQoEObject()` para fornecer as informações de QoE mais atualizadas para o SDK.
1. Quando o reprodutor de mídia encontra um erro e o evento de erro está disponível para a API do reprodutor, use `trackError()` para capturar as informações do erro. (Consulte [Visão geral](/help/sdk-implement/track-errors/track-errors-overview.md).)

   >[!TIP]
   >
   >O rastreamento de erros do reprodutor de mídia não interrompe a sessão de rastreamento de mídia. Se o reprodutor de mídia estiver impedindo o andamento da reprodução, certifique-se de que a sessão de monitoramento de mídia está fechada, chamando `trackSessionEnd()` após chamar `trackError()`.
