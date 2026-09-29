---
title: Pausar eventos
description: Conta cada pausa distinta que ocorreu durante uma sessão.
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
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.pauseCount`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feeds de dados | `event_list`, `post_event_list` (consulte a pesquisa de [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | N/D |
