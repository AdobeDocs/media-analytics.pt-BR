---
title: Tempo gasto com o anúncio
description: Informa o total de segundos de reprodução de anúncio ativa por sessão.
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
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
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.timePlayed`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Feeds de dados | `event_list`, `post_event_list` (consulte a pesquisa de [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.ad.timePlayed` |
