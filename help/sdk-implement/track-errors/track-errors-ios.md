---
title: Rastrear erros no iOS
description: Este tópico descreve como implementar o rastreamento de erros usando o SDK do Media no iOS.
uuid: 18ea93d3-5948-4375-bcdb-72309268e38d
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Rastrear erros no iOS {#track-errors-on-ios}

>[!IMPORTANT]
>
>As instruções a seguir fornecem orientação para a implementação em todos os SDKs 2.x. Se estiver implementando uma versão 1.x do SDK, você pode baixar os Guias dos desenvolvedores 1.x aqui: [Baixar SDKs.](/help/sdk-implement/download-sdks.md)

## Implementar o rastreamento de erros

1. Rastrear erros do reprodutor de mídia:

   ```
   - (void)onPlayerError:(NSNotification *)notification { 
       [_mediaHeartbeat trackError:@"mediaoErrorId"]; 
   }
   ```

>[!NOTE]
>
>O rastreamento de erros do reprodutor de mídia não interrompe a sessão de rastreamento de mídia. Se o reprodutor de mídia estiver impedindo o andamento da reprodução, certifique-se de que a sessão de monitoramento de mídia está fechada, chamando `trackSessionEnd` após chamar `trackError`.

