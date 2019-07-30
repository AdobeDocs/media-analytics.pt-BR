---
seo-title: Visão geral
title: Visão geral
uuid: d 71429 e 6-ef 8 b -4 ea 2-8491-ff 3 cdbf 4357 f
translation-type: tm+mt
source-git-commit: e89620ce60a37aa4ba0207e8f5a4f43c76026dcd

---


# Visão geral{#overview}

>[!IMPORTANT]
>
>As instruções a seguir fornecem orientação para a implementação em todos os SDKs 2.x. Se estiver implementando uma versão 1.x do SDK, você pode baixar os Guias dos desenvolvedores aqui: [Baixar SDKs.](/help/sdk-implement/download-sdks.md)

## Implementar o rastreamento de erros

1. Rastrear erros do player de mídia.

   Em eventos de erro, chame `trackError` com informações sobre o erro.

>[!NOTE]
>
>Os erros do player de mídia não interromperem a sessão de rastreamento de mídia. If the media player error prevents the playback from continuing, make sure that the media tracking session is closed by calling `trackSessionEnd` after calling `trackError`.

