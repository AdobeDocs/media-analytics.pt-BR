---
title: Pausar eventos
description: Conta cada pausa distinta que ocorreu durante uma sessão.
feature: Metrics
role: User, Admin
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 12%

---


# Pausar eventos

A métrica **Pausar eventos** conta todos os eventos [de início de pausa](/help/implementation/events/playback/pause-start.md) distintos recebidos durante uma sessão, incluindo várias pausas na mesma sessão. Emparelhe-a com [Duração total da pausa](total-pause-duration.md) para derivar a duração média da pausa e com [Fluxos afetados pela pausa](paused-impacted-streams.md) para contar sessões que foram pausadas pelo menos uma vez.

## Como essa métrica é calculada

O back-end de mídia incrementa `mediaReporting.sessionDetails.pauseCount` a cada evento de [início de pausa](/help/implementation/events/playback/pause-start.md). A métrica é relatada na chamada de fechamento.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.pauseCount` quando [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.pauseCount`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feeds de dados | `event_list`, `post_event_list` (consulte a pesquisa de [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | N/D |
