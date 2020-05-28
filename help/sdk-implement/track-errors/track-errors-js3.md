---
title: Rastrear erros usando o JavaScript 3.x
description: Este tópico descreve como implementar o rastreamento de erros usando o SDK do Media em aplicativos de navegador (JS).
translation-type: tm+mt
source-git-commit: 5f274452b9ff5770908f7e2e450935be572a22ea
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 69%

---


# Rastrear erros usando o JavaScript 3.x{#track-errors-on-javascript}

>[!IMPORTANT]
>
>As instruções a seguir fornecem orientação para a implementação em todos os SDKs 3.x. If you are implementing any previous versions of the SDK, you can download the Developers Guides here: [Download SDKs.](/help/sdk-implement/download-sdks.md)

## Implementar o rastreamento de erros

1. Rastrear erros do reprodutor de mídia:

   ```js
   onPlayerError = function() {
       tracker.trackError("errorId");
   };
   ```

>[!NOTE]
>
>O rastreamento de erros do reprodutor de mídia não interrompe a sessão de rastreamento de mídia. Se o reprodutor de mídia estiver impedindo o andamento da reprodução, certifique-se de que a sessão de monitoramento de mídia está fechada, chamando `trackSessionEnd` após chamar `trackError`.
