---
title: Tempo de reprodução exclusivo
description: Relata os segundos de conteúdo distinto visualizado durante uma sessão, desduplicando repetições de busca de retorno.
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 8%

---


# Tempo de reprodução exclusivo

A métrica **Tempo de reprodução exclusivo** relata os segundos de conteúdo distinto visualizado durante uma sessão, desduplicando segmentos que foram repetidos via retorno. Comparado com o [Tempo gasto com o conteúdo](content-time-spent.md), o tempo de reprodução exclusivo é menor quando um visualizador observa uma parte do mesmo conteúdo na mesma sessão.

## Como essa métrica é calculada

O back-end de mídia rastreia quais intervalos de indicador de reprodução foram visualizados durante a sessão e soma sua união. Reproduzir o mesmo segmento de cinco segundos duas vezes ainda conta como cinco segundos. A métrica é relatada na chamada de fechamento. O valor é mostrado como `HH:MM:SS` no Analysis Workspace e em segundos nos Feeds de dados, Data Warehouse e APIs de relatórios.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.uniqueTimePlayed` quando [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.uniqueTimePlayed`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feeds de dados | `event_list`, `post_event_list` (consulte a pesquisa de [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.uniqueTimePlayed` |
