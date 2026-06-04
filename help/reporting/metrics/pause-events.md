---
title: Pausar eventos
description: Conta cada pausa distinta que ocorreu durante uma sessão.
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 10%

---


# Pausar eventos

A métrica **Pausar eventos** conta todos os eventos [de início de pausa](/help/implementation/events/playback/pause-start.md) distintos recebidos durante uma sessão, incluindo várias pausas na mesma sessão. Emparelhe-a com [Duração total da pausa](total-pause-duration.md) para derivar a duração média da pausa e com [Fluxos afetados pela pausa](paused-impacted-streams.md) para contar sessões que foram pausadas pelo menos uma vez.

## Como essa métrica é calculada

O back-end de mídia incrementa essa contagem a cada evento de [início de pausa](/help/implementation/events/playback/pause-start.md). Uma única pausa contínua gera um incremento independentemente de sua duração. Heartbeat [pings](/help/implementation/events/playback/ping.md) enviados enquanto o player permanece pausado, todos pertencem ao mesmo período de pausa e não incrementam a contagem novamente. A métrica é relatada na chamada de fechamento.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.pauseCount` quando [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.pauseCount`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feeds de dados | `event_list`, `post_event_list` (consulte a pesquisa de [`event.tsv`](https://experienceleague.adobe.com/pt-br/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | N/D |
