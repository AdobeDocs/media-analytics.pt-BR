---
title: Duração total da pausa
description: Relata os segundos cumulativos que o visualizador gastou pausados durante uma sessão.
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 10%

---


# Duração total da pausa

A métrica **Duração total da pausa** relata os segundos cumulativos que o visualizador gastou pausados durante uma sessão. A métrica é a soma de todos os intervalos entre cada evento [pausar início](/help/implementation/events/playback/pause-start.md) e o evento [reproduzir](/help/implementation/events/playback/play.md) subsequente. Várias pausas são adicionadas. Emparelhe com [Eventos de pausa](pause-events.md) para derivar o comprimento médio da pausa.

## Como essa métrica é calculada

O back-end de mídia soma o tempo decorrido do relógio de parede entre cada evento de [início de pausa](/help/implementation/events/playback/pause-start.md) e o evento [reprodução](/help/implementation/events/playback/play.md) correspondente. A métrica é relatada na chamada de fechamento. O valor é mostrado como `HH:MM:SS` no Analysis Workspace e em segundos em outro lugar.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.pauseTime` quando [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.pauseTime`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feeds de dados | `event_list`, `post_event_list` (consulte a pesquisa de [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | N/D |
