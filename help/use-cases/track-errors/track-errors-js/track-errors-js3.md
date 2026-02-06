---
title: Saiba como rastrear erros usando o JavaScript 3.x
description: Saiba como implementar o rastreamento de erros usando o SDK de mídia em aplicativos de navegador (JS).
exl-id: 3769fc47-fbc4-4498-9d2a-04c88cdd0e83
feature: Streaming Media
role: User, Admin, Developer
source-git-commit: afc22870fc69d8319acbff91aafc66b66ec9bdf9
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 100%

---

# Rastrear erros usando o JavaScript 3.x{#track-errors-on-javascript}

As instruções a seguir fornecem orientação para a implementação em todos os SDKs 2.x.

>[!IMPORTANT]
>
>Se estiver implementando uma versão anterior do SDK, você pode baixar os Guias dos desenvolvedores aqui: [Baixar SDKs.](/help/getting-started/download-sdks.md)

## Implementar o rastreamento de erros

1. Rastrear erros do reprodutor de mídia:

   ```js
   onPlayerError = function() {
       tracker.trackError("errorId");
   };
   ```

>[!NOTE]
>
>O rastreamento de erros do reprodutor de mídia não interrompe a sessão de rastreamento de mídia. Se o erro do reprodutor de mídia estiver impedindo o andamento da reprodução, certifique-se de que a sessão de monitoramento de mídia está fechada, chamando `trackSessionEnd` após chamar `trackError`.
