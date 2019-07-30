---
seo-title: Rastrear erros no Roku
title: Rastrear erros no Roku
uuid: 4 e 0165 f 9-9169-47 ed -9 f 11-ea 8 a 8778 f 663
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Rastrear erros no Roku{#track-errors-on-roku}

>[!IMPORTANT]
>
>As instruções a seguir fornecem orientação para a implementação em todos os SDKs 2.x. Se estiver implementando uma versão 1.x do SDK, você pode baixar os Guias dos desenvolvedores aqui: [Baixar SDKs.](/help/sdk-implement/download-sdks.md)

## Implementar o rastreamento de erros

1. Erros do player de mídia:

   ```
   ADBMobile().mediaTrackError(msg.GetMessage(), 
                               ADBMobile().ERROR_SOURCE_PLAYER)
   ```

>[!NOTE]
>
>Os erros do player de mídia não interromperem a sessão de rastreamento de mídia. If the media player error prevents the playback from continuing, make sure that the media tracking session is closed by calling `trackSessionEnd` after calling `trackError`.

