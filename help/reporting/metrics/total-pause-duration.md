---
title: Duração total da pausa
description: Relata os segundos cumulativos que o visualizador gastou pausados durante uma sessão.
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
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.pauseTime`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feeds de dados | `event_list`, `post_event_list` (consulte a pesquisa de [`event.tsv`](https://experienceleague.adobe.com/pt-br/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | N/D |
