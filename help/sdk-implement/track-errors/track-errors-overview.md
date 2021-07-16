---
title: Explicação dos erros de rastreamento
description: Saiba mais sobre o rastreamento de erros usando o SDK do Media.
uuid: d71429e6-ef8b-4ea2-8491-ff3cdbf4357f
exl-id: 61c5f835-d66c-4621-a0af-2e4f47a922ac
feature: Media Analytics
role: User, Admin, Data Engineer
source-git-commit: 8e0f5d012e1404623e3a0a460a9391303e2ab4e0
workflow-type: tm+mt
source-wordcount: '95'
ht-degree: 87%

---

# Visão geral{#overview}

As instruções a seguir fornecem orientação para a implementação em todos os SDKs 2.x.

>[!IMPORTANT]
>
>Se estiver implementando uma versão 1.x do SDK, você pode baixar os Guias dos desenvolvedores 1.x aqui: [Baixar SDKs.](/help/sdk-implement/download-sdks.md)

## Implementar o rastreamento de erros

1. Rastrear erros do reprodutor de mídia.

   Em eventos de erro, chame `trackError` com informações sobre o erro.

>[!NOTE]
>
>O rastreamento de erros do reprodutor de mídia não interrompe a sessão de rastreamento de mídia. Se o reprodutor de mídia estiver impedindo o andamento da reprodução, certifique-se de que a sessão de monitoramento de mídia está fechada, chamando `trackSessionEnd` após chamar `trackError`.
