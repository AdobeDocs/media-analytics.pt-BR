---
title: Rastrear erros no Roku
description: Este tópico descreve como implementar o rastreamento de erros usando o SDK do Media no Roku.
uuid: 4e0165f9-9169-47ed-9f11-ea8a8778f663
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Rastrear erros no Roku {#track-errors-on-roku}

>[!IMPORTANT]
>
>As instruções a seguir fornecem orientação para a implementação em todos os SDKs 2.x. Se estiver implementando uma versão 1.x do SDK, você pode baixar os Guias dos desenvolvedores 1.x aqui: [Baixar SDKs.](/help/sdk-implement/download-sdks.md)

## Implementar o rastreamento de erros

1. Rastrear erros do reprodutor de mídia:

   ```
   ADBMobile().mediaTrackError(msg.GetMessage(), 
                               ADBMobile().ERROR_SOURCE_PLAYER)
   ```

>[!NOTE]
>
>O rastreamento de erros do reprodutor de mídia não interrompe a sessão de rastreamento de mídia. Se o reprodutor de mídia estiver impedindo o andamento da reprodução, certifique-se de que a sessão de monitoramento de mídia está fechada, chamando `trackSessionEnd` após chamar `trackError`.

