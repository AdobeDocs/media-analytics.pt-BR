---
title: Caminho da mídia
description: Registra a ID de conteúdo como uma variável de tráfego para análise de caminho.
feature: Dimensions
role: User, Admin
source-git-commit: 7b5232f25f3aa26e8566783557163f316af3fe57
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 5%

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
