---
title: Rastrear a qualidade da experiência no Chromecast
description: Este tópico descreve como implementar o rastreamento de qualidade de experiência (QoE, QoS) usando o SDK do Media no Chromecast.
uuid: d0cdc8cd-4db0-45ef-9470-1cba3996305b
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Rastrear a qualidade da experiência no Chromecast {#track-quality-of-experience-on-chromecast}

>[!IMPORTANT]
>
>As instruções a seguir fornecem orientação para a implementação em todos os SDKs 2.x. Se estiver implementando uma versão 1.x do SDK, você pode baixar os Guias dos desenvolvedores 1.x aqui: [Baixar SDKs.](/help/sdk-implement/download-sdks.md)

## Visão geral {#overview}

O rastreamento da qualidade da experiência inclui qualidade do serviço (QoS) e rastreamento de erros; ambos são elementos opcionais e **não** são necessários para implementações de rastreamento de mídia principal. Você pode usar a API do reprodutor de mídia para identificar as variáveis relacionadas ao rastreamento de erros e QoS.

## Eventos do reprodutor {#player-events}

### Em todos os eventos de alteração da taxa de bits

* Criar/atualizar a instância do objeto QoS para a reprodução, `qosObject`
* Chame `trackEvent(Media.Heartbeat.Event.BitrateChange, qosObject);`

### Quando ocorrem erros no reprodutor

Chame `trackError(“media error id”);`

## Implementação {#implement}

1. Identifique quando a taxa de bits for alterada durante a reprodução de mídia e crie a instância `MediaObject` usando as informações de QoS.

   **Variáveis de QoSObject:**

   >[!TIP]
   >
   >Essas variáveis somente são necessárias se você estiver planejando rastrear QoS.

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
   >Atualize o objeto de QoS e chame o evento de alteração na taxa de bits em cada alteração na taxa de bits. Isso fornece os dados de QoS mais precisos.

1. Verifique se o método `getQoSObject()` retorna as informações de QoS mais atualizadas.
1. Quando o reprodutor de mídia encontra um erro e o evento de erro está disponível para a API do reprodutor, use `trackError()` para capturar as informações do erro. (Consulte [Visão geral](/help/sdk-implement/track-errors/track-errors-overview.md).)

   >[!TIP]
   >
   >O rastreamento de erros do reprodutor de mídia não interrompe a sessão de rastreamento de mídia. Se o reprodutor de mídia estiver impedindo o andamento da reprodução, certifique-se de que a sessão de monitoramento de mídia está fechada, chamando `trackSessionEnd()` após chamar `trackError()`.

