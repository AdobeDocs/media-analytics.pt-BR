---
title: Quedas antes do início
description: Conta sessões em que o visualizador saiu antes de qualquer conteúdo principal renderizado.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 8%

---


# Quedas antes do início

A métrica **Desistências antes do início** conta sessões em que o visualizador foi encerrado antes da renderização de qualquer conteúdo principal. A métrica sinaliza o abandono de pré-conteúdo independentemente do comportamento do anúncio, de modo que seja a melhor medida de descarte de pré-conteúdo puro. Emparelhe-o com [Inícios da mídia](/help/reporting/metrics/media-starts.md) e [Inícios do conteúdo](/help/reporting/metrics/content-starts.md) para calcular o compartilhamento de sessões que nunca produziram um quadro de conteúdo.

## Como essa métrica é calculada

O back-end de mídia define `mediaReporting.qoeDataDetails.isDroppedBeforeStart = true` para sessões que se fecham sem nunca produzir um evento `media.play` no conteúdo principal. A métrica é relatada na chamada de fechamento.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.qoe.dropBeforeStart` quando a [[!UICONTROL Qualidade de Mídia]](/help/reporting/media-reports-enable.md) está habilitada. |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.isDroppedBeforeStart`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Feeds de dados | `event_list`, `post_event_list` (consulte a pesquisa de [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
