---
title: Rastrear erros no JavaScript
description: Este tópico descreve como implementar o rastreamento de erros usando o SDK do Media em aplicativos de navegador (JS).
uuid: 5a4fc5df-2677-4189-92af-5cd074847b39
translation-type: ht
source-git-commit: 7da115fae0a05548173e8ca3ec68fae250128775

---


# Rastrear erros no JavaScript {#track-errors-on-javascript}

>[!IMPORTANT]
>
>As instruções a seguir fornecem orientação para a implementação em todos os SDKs 2.x. Se estiver implementando uma versão 1.x do SDK, você pode baixar os Guias dos desenvolvedores 1.x aqui: [Baixar SDKs.](/help/sdk-implement/download-sdks.md)

## Implementar o rastreamento de erros

1. Rastrear erros do reprodutor de mídia:

   ```js
   onPlayerError = function() { 
       this._mediaHeartbeat.trackError("mediaErrorId"); 
   };
   ```

>[!NOTE]
>
>O rastreamento de erros do reprodutor de mídia não interrompe a sessão de rastreamento de mídia. Se o reprodutor de mídia estiver impedindo o andamento da reprodução, certifique-se de que a sessão de monitoramento de mídia está fechada, chamando `trackSessionEnd` após chamar `trackError`.

