---
title: Quedas antes do início
description: Conta sessões em que o visualizador saiu antes de qualquer conteúdo principal renderizado.
feature: Metrics
role: User, Admin
source-git-commit: a2c91ef63fa9320a0e47f338ce4d53b9b8e977e3
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 7%

---


# Quedas antes do início

A métrica **Desistências antes do início** conta sessões em que o visualizador foi encerrado antes da renderização de qualquer conteúdo principal. A métrica sinaliza o abandono de pré-conteúdo independentemente do comportamento do anúncio, de modo que seja a melhor medida de descarte de pré-conteúdo puro. Emparelhe-o com [Inícios da mídia](/help/reporting/metrics/media-starts.md) e [Inícios do conteúdo](/help/reporting/metrics/content-starts.md) para calcular o compartilhamento de sessões que nunca produziram um quadro de conteúdo.

## Como essa métrica é calculada

O back-end de mídia define esse sinalizador para sessões que se fecham sem nunca produzir um evento [play](/help/implementation/events/playback/play.md) no conteúdo principal. A métrica é relatada na chamada de fechamento. Cenários comuns incluem: o visualizador sai durante um anúncio precedente, o reprodutor é interrompido indefinidamente na fase inicial de buffer ou um erro é acionado antes do primeiro evento de reprodução do conteúdo principal. Em todos esses casos, a sessão registra um [Início da mídia](/help/reporting/metrics/media-starts.md), mas nenhum [Início do conteúdo](/help/reporting/metrics/content-starts.md) e nenhum [Marcador de progresso](/help/reporting/metrics/progress-markers.md) foram registrados.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.qoe.dropBeforeStart` quando a [[!UICONTROL Qualidade de Mídia]](/help/reporting/media-reports-enable.md) está habilitada. |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.isDroppedBeforeStart`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Feeds de dados | `event_list`, `post_event_list` (consulte a pesquisa de [`event.tsv`](https://experienceleague.adobe.com/pt-br/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.qoe.dropBeforeStart` |
