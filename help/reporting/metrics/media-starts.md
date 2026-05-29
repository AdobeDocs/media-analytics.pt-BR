---
title: Início da mídia
description: Conta todas as sessões de mídia iniciadas, incluindo sessões que terminaram em anúncios precedentes ou buffering.
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '228'
ht-degree: 6%

---


# Início da mídia

A métrica **Início da mídia** conta todas as sessões de mídia iniciadas. Ele é incrementado assim que o back-end recebe um evento de [início de sessão](/help/implementation/events/session/session-start.md), mesmo que o visualizador saia durante anúncios precedentes, buffering ou antes de qualquer conteúdo principal ser reproduzido. Use-a como a mais ampla métrica top-of-funnel para relatórios de mídia; combine-a com [Inícios do conteúdo](content-starts.md) para medir a queda de anúncio e buffer.

## Como essa métrica é calculada

O back-end de mídia define esse sinalizador quando um evento [início de sessão](/help/implementation/events/session/session-start.md) é recebido. A métrica relatada é `1` por sessão. Os inícios da mídia são relatados na chamada de início, não na chamada de fechamento; é a única métrica que não espera pelo fechamento da sessão. Todas as outras métricas de mídia, incluindo [Inícios do conteúdo](/help/reporting/metrics/content-starts.md), [Tempo gasto com o conteúdo](/help/reporting/metrics/content-time-spent.md) e [Marcadores de progresso](/help/reporting/metrics/progress-markers.md), são relatadas na chamada de fechamento e não estão disponíveis em tempo real durante a reprodução. [Início do anúncio](/help/reporting/metrics/ad-starts.md) é a única métrica adicional relatada em seu evento de acionamento, em vez de no fechamento.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.view` quando [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.isViewed`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feeds de dados | `event_list`, `post_event_list` (consulte a pesquisa de [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.view` |
