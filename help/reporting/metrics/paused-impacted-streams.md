---
title: Fluxos afetados pausados
description: Conta sessões em que o visualizador foi pausado pelo menos uma vez.
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
source-wordcount: '152'
ht-degree: 11%
---

# Fluxos afetados pausados

A métrica **Fluxos afetados pausados** conta sessões nas quais o visualizador foi pausado pelo menos uma vez. É um booleano de nível de sessão. Várias pausas na mesma contagem de sessões que um fluxo afetado. Use-o para medir o compartilhamento de sessões que tiveram qualquer pausa; para o volume total de pausa, use [Pausar eventos](pause-events.md).

## Como essa métrica é calculada

O back-end de mídia define esse sinalizador na primeira vez que um evento [pause start](/help/implementation/events/playback/pause-start.md) é recebido durante a sessão. A métrica é relatada na chamada de fechamento.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.pause` quando [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.hasPauseImpactedStreams`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feeds de dados | `event_list`, `post_event_list` (consulte a pesquisa de [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | N/D |
