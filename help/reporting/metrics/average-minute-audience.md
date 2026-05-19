---
title: Público-alvo médio a cada minuto
description: Relata o número médio de visualizadores assistindo a qualquer minuto no tempo de execução do conteúdo.
feature: Metrics
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 12%

---


# Público-alvo médio a cada minuto

A métrica **Audiência média por minuto** informa o número médio de visualizadores assistindo a qualquer minuto, durante o tempo de execução do conteúdo. É a medida padrão &quot;AMA&quot; usada para comparar o alcance da mídia em conteúdo de diferentes tamanhos.

## Como essa métrica é calculada

O back-end de mídia calcula a Audiência média por minuto por sessão como `Content time spent / Content length`. Quando somado entre as sessões, o total representa o tamanho médio do público-alvo em cada minuto do conteúdo. A métrica é relatada na chamada de fechamento.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.averageMinuteAudience` quando [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.averageMinuteAudience`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feeds de dados | `event_list`, `post_event_list` (consulte a pesquisa de [`event.tsv`](https://experienceleague.adobe.com/pt-br/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.averageMinuteAudience` |

>[!IMPORTANT]
>
>A Audiência média por minuto requer um [Tamanho do conteúdo](/help/reporting/dimensions/content-length.md) diferente de zero. Se a duração do conteúdo for indefinida ou zero, essa métrica não será produzida para a sessão.
