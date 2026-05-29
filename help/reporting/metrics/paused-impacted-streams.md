---
title: Fluxos afetados pausados
description: Conta sessões em que o visualizador foi pausado pelo menos uma vez.
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
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
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.pause` quando [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.hasPauseImpactedStreams`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feeds de dados | `event_list`, `post_event_list` (consulte a pesquisa de [`event.tsv`](https://experienceleague.adobe.com/pt-br/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | N/D |
