---
title: Saiba como rastrear a qualidade da experiência usando o JavaScript 3.x
description: Saiba mais sobre como implementar o rastreamento de qualidade de experiência (QoE, QoS) usando o Media SDK em aplicativos de navegador com o JavaScript 3x.
exl-id: b5570e9c-8fb1-4458-bd1a-86ff6fce7813
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/aR7oVHv3n2xQnrMGHowhLFCYxhRyP1vyIrlXbKHEa5A
product_v2: id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2: id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 227
ht-degree: 90%

---

# Rastrear a qualidade da experiência usando o JavaScript 3.x{#track-quality-of-experience-on-javascript}

As instruções a seguir fornecem orientação para a implementação em todos os SDKs 2.x.

>[!IMPORTANT]
>
>Se estiver implementando uma versão anterior do SDK, você pode baixar os Guias dos desenvolvedores aqui: [Baixar SDKs.](/help/getting-started/download-sdks.md)

## Implementar QOE

1. Identifique quando a taxa de bits for alterada durante a reprodução de mídia e crie a instância `qoeObject` usando as informações de QoE.

   Variáveis de QoEObject:

   >[!TIP]
   >
   >Essas variáveis somente são necessárias se você estiver planejando rastrear QoS.

   | Variável | Tipo | Descrição |
   | --- | --- | --- |
   | `bitrate` | number | Taxa de bits atual |
   | `startupTime` | number | Tempo de inicialização |
   | `fps` | number | Valor do FPS |
   | `droppedFrames` | number | Número de quadros perdidos |

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

1. Quando a reprodução alterar as taxas de bits, chame o evento `BitrateChange` na instância do heartbeat de mídia:

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
   >Atualize o objeto de QoE e chame o evento de alteração da taxa de bits a cada alteração. Isto fornece os dados de QoE mais precisos.

1. Certifique-se de chamar o método `updateQoEObject()` para fornecer as informações de QoE mais atualizadas para o SDK.
1. Quando o reprodutor de mídia encontra um erro e o evento de erro está disponível para a API do reprodutor, use `trackError()` para capturar as informações do erro. (Consulte [Visão geral](/help/use-cases/track-errors/track-errors-overview.md).)

   >[!TIP]
   >
   >O rastreamento de erros do reprodutor de mídia não interrompe a sessão de rastreamento de mídia. Se o erro do reprodutor de mídia estiver impedindo o andamento da reprodução, certifique-se de que a sessão de monitoramento de mídia está fechada, chamando `trackSessionEnd()` após chamar `trackError()`.
