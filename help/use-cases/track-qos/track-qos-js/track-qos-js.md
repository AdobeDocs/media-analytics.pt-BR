---
title: Saiba como rastrear a qualidade de experiência usando o JavaScript 2.x
description: Saiba mais sobre como implementar o rastreamento de qualidade de experiência (QoE, QoS) usando o Media SDK em aplicativos de navegador com o JavaScript 2.x.
uuid: 3bc762a2-9706-4b62-aa91-747f461dd13d
exl-id: 5924eba4-15a9-405b-9a05-8a7308ddec47
feature: Streaming Media
role: User, Admin, Developer
TQID: https://experienceleague.adobe.com/S4UPE2qnHPcqM0znf4PVJy0p98rzv8FVlBBYqjer-7s
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
feature_v2:
  - id: e9dbdbc5-3e52-40f0-a7bc-e18542967b7a
  - id: fd307ce7-56f5-4ee3-af68-a7833ff6e85e
subfeature_v2:
  - id: bcc784b7-4ade-4c84-96fa-2f7631b1e5fd
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
source-git-commit: 10026f71b2092be536340ba4a48d7fd71fbc7d8e
workflow-type: tm+mt
source-wordcount: 226
ht-degree: 90%

---

# Rastrear a qualidade de experiência usando o JavaScript 2.x{#track-quality-of-experience-on-javascript}

As instruções a seguir fornecem orientação para a implementação em todos os SDKs 2.x.

>[!IMPORTANT]
>
>Se estiver implementando uma versão 1.x do SDK, você pode baixar os Guias dos desenvolvedores 1.x aqui: [Baixar SDKs.](/help/getting-started/download-sdks.md)

## Implementar QOS

1. Identifique quando a taxa de bits for alterada durante a reprodução de mídia e crie a instância `MediaObject` usando as informações de QoS.

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
   >Atualize o objeto de QoS e chame o evento de alteração na taxa de bits em cada alteração na taxa de bits. Isso fornece os dados de QoS mais precisos.

1. Verifique se o método `getQoSObject()` retorna as informações de QoS mais atualizadas.
1. Quando o reprodutor de mídia encontra um erro e o evento de erro está disponível para a API do reprodutor, use `trackError()` para capturar as informações do erro. (Consulte [Visão geral](/help/use-cases/track-errors/track-errors-overview.md).)

   >[!TIP]
   >
   >O rastreamento de erros do reprodutor de mídia não interrompe a sessão de rastreamento de mídia. Se o erro do reprodutor de mídia estiver impedindo o andamento da reprodução, certifique-se de que a sessão de monitoramento de mídia está fechada, chamando `trackSessionEnd()` após chamar `trackError()`.
