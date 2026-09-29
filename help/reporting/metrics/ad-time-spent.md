---
title: Tempo gasto com o anúncio
description: Informa o total de segundos de reprodução de anúncio ativa por sessão.
feature: Metrics
role: User, Admin
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
    internal-label: Metrics
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '174'
ht-degree: 8%
---

# Tempo gasto com o anúncio

A métrica **Tempo gasto com anúncio** relata o total de segundos de reprodução de anúncio ativa por sessão, excluindo pausas, buffering e interrupções. Combine-o com [Tempo gasto com conteúdo](/help/reporting/metrics/content-time-spent.md) para comparar o carregamento de anúncio com o envolvimento de conteúdo.

## Como essa métrica é calculada

O back-end de mídia soma o tempo decorrido do relógio de parede entre os eventos enquanto o reprodutor está no estado `play` em um anúncio. O tempo durante pausas, buffering e buscas é excluído, de forma consistente com a forma como o [Tempo gasto com o conteúdo](/help/reporting/metrics/content-time-spent.md) é calculado para o conteúdo principal. A métrica é relatada na chamada de fechamento de anúncio. O valor é mostrado como `HH:MM:SS` no Analysis Workspace e em segundos nos Feeds de dados, Data Warehouse e APIs de relatórios.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.ad.timePlayed` quando o [[!UICONTROL Media Ads]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.timePlayed`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Feeds de dados | `event_list`, `post_event_list` (consulte a pesquisa de [`event.tsv`](https://experienceleague.adobe.com/pt-br/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.ad.timePlayed` |
