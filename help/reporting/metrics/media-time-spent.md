---
title: Tempo gasto com a mídia
description: Informa o total de segundos de reprodução ativa por sessão, incluindo anúncios.
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '182'
ht-degree: 8%

---


# Tempo gasto com a mídia

A métrica **Tempo gasto com a mídia** relata o total de segundos de reprodução ativa por sessão, incluindo o conteúdo principal e anúncios, mas excluindo pausas, buffering e paralisações. Use-o para medir o tempo total que o visualizador esteve ativamente envolvido com o reprodutor. Para conteúdo principal apenas, use [Tempo gasto com conteúdo](content-time-spent.md).

## Como essa métrica é calculada

O back-end de mídia soma o tempo decorrido do relógio de parede entre os eventos enquanto o reprodutor está no estado `play`, no conteúdo principal ou nos anúncios. O tempo durante pausas, eventos de buffer e interrupções é excluído. A métrica é relatada na chamada de fechamento. O valor é mostrado como `HH:MM:SS` no Analysis Workspace e em segundos nos Feeds de dados, Data Warehouse e APIs de relatórios.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.totalTimePlayed` quando [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.totalTimePlayed`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feeds de dados | `event_list`, `post_event_list` (consulte a pesquisa de [`event.tsv`](https://experienceleague.adobe.com/pt-br/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.totalTimePlayed` |
