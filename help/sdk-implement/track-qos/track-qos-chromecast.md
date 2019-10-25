---
seo-title: Rastrear a qualidade da experiência no Chromecast
title: Rastrear a qualidade da experiência no Chromecast
uuid: d0cdc8cd-4db0-45ef-9470-1cba3996305b
translation-type: tm+mt
source-git-commit: 8938e324d570b7e3e2c3c3e971c00ade7e6be8b6

---


# Rastrear a qualidade da experiência no Chromecast{#track-quality-of-experience-on-chromecast}

>[!IMPORTANT]
>
>As instruções a seguir fornecem orientação para a implementação em todos os SDKs 2.x. Se estiver implementando uma versão 1.x do SDK, você pode baixar os Guias dos desenvolvedores aqui: [Baixar SDKs.](/help/sdk-implement/download-sdks.md)

## Visão geral {#overview}

Quality of experience tracking includes quality of service (QoS) and error tracking, both are optional elements and are **not** required for core media tracking implementations. Você pode usar a API do player de mídia para identificar as variáveis relacionadas ao QoS e ao rastreamento de erros.

## Eventos do player {#player-events}

### Em todos os eventos de alteração da taxa de bits

* Criar/atualizar a instância do objeto QoS para a reprodução, `qosObject`
* Chama `trackEvent(Media.Heartbeat.Event.BitrateChange, qosObject);`

### Quando ocorrem erros no reprodutor

Chama `trackError(“media error id”);`

## Implementação {#implement}

1. Identify when the bitrate changes during media playback and create the `MediaObject` instance using the QoS information.

   **Variáveis de QoSObject:**

   >[!TIP]
   >
   >Essas variáveis só são necessárias se você estiver planejando rastrear QoS.

   | Variável | Descrição | Obrigatório |
   | --- | --- | :---: |
   | `bitrate` | Taxa de bits atual | Sim |
   | `startupTime` | Tempo de inicialização | Sim |
   | `fps` | Valor do FPS | Sim |
   | `droppedFrames` | Número de quadros perdidos | Sim |

   **Criação do objeto de QoS:** [createQoSObject](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.createQoSObject)

   ```
   qosInfo = ADBMobile.media.createQoSObject(50000, 0, 24, 10); 
   ```

1. Quando a reprodução altera as taxas de bits, chame o evento `BitrateChange` na instância do Heartbeat de mídia: [trackEvent](https://adobe-marketing-cloud.github.io/media-sdks/reference/chromecast/ADBMobile.media.html#.trackEvent)

   ```
   ADBMobile.media.trackEvent(ADBMobile.media.Event.BitrateChange); 
   ```

   >[!IMPORTANT]
   >
   >Atualize o objeto QoS e chame o evento de alteração da taxa de bits em cada alteração da taxa de bits. Isso fornece os dados de QoS mais precisos.

1. Verifique se o método `getQoSObject()` retorna as informações de QoS mais atualizadas.
1. When the media player encounters an error, and the error event is available to the player API, use `trackError()` to capture the error information. (Consulte [Visão geral](/help/sdk-implement/track-errors/track-errors-overview.md).)

   >[!TIP]
   >
   >O rastreamento de erros do player de mídia não interrompe a sessão de rastreamento de mídia. If the media player error prevents the playback from continuing, make sure that the media tracking session is closed by calling `trackSessionEnd()` after calling `trackError()`.

