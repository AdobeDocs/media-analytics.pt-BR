---
title: Rastrear a qualidade da experiência no Roku
description: Este tópico descreve como implementar o rastreamento de qualidade de experiência (QoE, QoS) usando o SDK do Media no Roku.
uuid: a8b242ab-da3c-4297-9eef-f0b9684ef56a
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Rastrear a qualidade da experiência no Roku {#track-quality-of-experience-on-roku}

>[!IMPORTANT]
>
>As instruções a seguir fornecem orientação para a implementação em todos os SDKs 2.x. Se estiver implementando uma versão 1.x do SDK, você pode baixar os Guias dos desenvolvedores 1.x aqui: [Baixar SDKs.](/help/sdk-implement/download-sdks.md)

## Implementação do QOS

1. Identifique quando a taxa de bits muda durante a reprodução da mídia e use a API de `mediaUpdateQoS` para atualizar as informações de QoS no SDK do Media.

   Variáveis de QoSObject:

   >[!TIP]
   >
   >Essas variáveis só são necessárias se você estiver rastreando QoS.

   | Variável | Descrição | Obrigatório |
   | --- | --- | :---: |
   | `bitrate` | Taxa de bits atual | Sim |
   | `startupTime` | Tempo de inicialização | Sim |
   | `fps` | Valor do FPS | Sim |
   | `droppedFrames` | Número de quadros perdidos | Sim |

   Por exemplo:

   ```
   bitrate = 200000
   fps = 0
   droppedFrames = 1
   startupTime = 2
   qosinfo = adb_media_init_qosinfo(bitrate, startupTime, fps, droppedFrames)
   
   ADBMobile().mediaUpdateQoS(qosinfo)
   ```

   <!--
    QoS object creation:
 
    ```
    qosInfo=adb_media_init_qosinfo()
    qosInfo.bitrate = 200000
    qosInfo.fps = 0
    qosInfo.droppedFrames = 1
    qosInfo.startupTime = 2
    ```
    -->

1. Quando a reprodução alterna as taxas de bits, chame `trackEvent(BitrateChange)` para notificar o SDK do Media de que a taxa de bits mudou.

   ```
   ADBMobile().mediaTrackEvent(ADBMobile().MEDIA_BITRATE_CHANGE)
   ```

   >[!NOTE]
   >
   >Você precisa chamar `updateQoSObject` com o valor atualizado da taxa de bits.

   <!--
    ```
    qosContextData = {}
    ADBMobile().mediaTrackEvent(MEDIA_BITRATE_CHANGE, qosInfo, qosContextData)
    ```
 
    >[!IMPORTANT]
    >
    >Update the QoS object and call the bitrate change event on every bitrate change. This provides the most accurate QoS data.
    -->

1. Quando o reprodutor de mídia encontra um erro e o evento de erro está disponível para a API do reprodutor, use `trackError()` para capturar as informações do erro. (Consulte [Visão geral](/help/sdk-implement/track-errors/track-errors-overview.md).)

   >[!TIP]
   >
   >O rastreamento de erros do reprodutor de mídia não interrompe a sessão de rastreamento de mídia. Se o reprodutor de mídia estiver impedindo o andamento da reprodução, certifique-se de que a sessão de monitoramento de mídia está fechada, chamando `trackSessionEnd()` após chamar `trackError()`.

