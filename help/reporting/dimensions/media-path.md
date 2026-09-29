---
title: Caminho da mídia
description: Registra a ID de conteúdo como uma variável de tráfego para análise de caminho.
feature: Dimensions
role: User, Admin
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: b8734a57-d5fb-44a8-8ee1-65225cecaeae
    internal-label: Data configuration and collection
subfeature_v2:
  - id: b22bc0f7-b089-4966-95a1-31e7b3b69b79
    internal-label: Dimensions
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 6%
---

# Caminho da mídia

A dimensão **Caminho da mídia** captura a ID de conteúdo como uma variável de tráfego (prop) para que ela possa ser usada na análise de definição de caminho (por exemplo, os relatórios de fluxo de conteúdo seguinte e conteúdo anterior). É exclusivo do Adobe Analytics: o Customer Journey Analytics não armazena variáveis de tráfego e a definição de caminho é executada diretamente na dimensão Conteúdo (ID).

## Como essa dimensão é preenchida

O caminho da mídia é derivado automaticamente da ID de conteúdo definida no início da sessão. Não há nenhuma variável separada para definir; a coluna de feed de dados `videopath` é preenchida sempre que a ID (Conteúdo) é preenchida.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletada automaticamente dos dados de contexto `a.media.name` como uma variável de tráfego (prop) quando o [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | N/D — use [Conteúdo](content.md) para análise de caminho. |
| Feeds de dados | `videopath`, `post_videopath` |
| Audience Manager | `c_contextdata.a.media.name` |

>[!NOTE]
>
>As props do Adobe Analytics têm um limite de 100 bytes. Valores maiores que 100 bytes são truncados.

>[!IMPORTANT]
>
>Os relatórios de definição de caminho comparam o valor da prop entre ocorrências na mesma visita. Se o Conteúdo (ID) for alterado em uma visita (por exemplo, quando um visualizador muda de um conteúdo para outro), o relatório de caminho mostrará esse fluxo.

## Itens de dimensão

Cada item é uma ID de conteúdo relatada durante uma visita. Você pode usar painéis de Fluxo para exibir caminhos de navegação de conteúdo para conteúdo.
