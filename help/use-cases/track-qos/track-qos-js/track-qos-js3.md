---
title: Saiba como rastrear a qualidade da experiência usando o JavaScript 3.x
description: “Saiba como implementar o rastreamento da qualidade da experiência (QoE, QoS) usando o SDK de mídia em aplicativos de navegador que utilizam o JavaScript 3.x.”
exl-id: b5570e9c-8fb1-4458-bd1a-86ff6fce7813
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 2ce09eafeb8def909ae2a8ae7cc09a88b2f663af
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 99%

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
   >O rastreamento de erros do reprodutor de mídia não interrompe a sessão de rastreamento de mídia. Se o reprodutor de mídia estiver impedindo o andamento da reprodução, certifique-se de que a sessão de monitoramento de mídia está fechada, chamando `trackSessionEnd()` após chamar `trackError()`.
