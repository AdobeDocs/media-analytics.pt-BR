---
title: Duração total da pausa
description: Relata os segundos cumulativos que o visualizador gastou pausados durante uma sessão.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '151'
ht-degree: 8%

---


# Duração total da pausa

A métrica **Duração total da pausa** relata os segundos cumulativos que o visualizador gastou pausados durante uma sessão. A métrica é a soma de todos os intervalos entre cada `media.pauseStart` e o `media.play` subsequente. Várias pausas são adicionadas. Emparelhe com [Eventos de pausa](pause-events.md) para derivar o comprimento médio da pausa.

## Como essa métrica é calculada

O back-end de mídia soma o tempo decorrido do relógio de parede entre cada `media.pauseStart` e o evento `media.play` correspondente. A métrica é relatada na chamada de fechamento. O valor é mostrado como `HH:MM:SS` no Analysis Workspace e em segundos em outro lugar.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.pauseTime` quando [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.pauseTime`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feeds de dados | `event_list`, `post_event_list` (consulte a pesquisa de [`event.tsv`](https://experienceleague.adobe.com/pt-br/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
