---
title: Início da mídia
description: Conta todas as sessões de mídia iniciadas, incluindo sessões que terminaram em anúncios precedentes ou buffering.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 7%

---


# Início da mídia

A métrica **Início da mídia** conta todas as sessões de mídia iniciadas. Ele é incrementado assim que o back-end recebe um evento `media.sessionStart`, mesmo se o visualizador sair durante anúncios precedentes, buffering ou antes de qualquer conteúdo principal ser reproduzido. Use-a como a mais ampla métrica top-of-funnel para relatórios de mídia; combine-a com [Inícios do conteúdo](content-starts.md) para medir a queda de anúncio e buffer.

## Como essa métrica é calculada

O back-end de mídia define `mediaReporting.sessionDetails.isViewed = true` quando um evento `media.sessionStart` é recebido. A métrica relatada é `1` por sessão. Inícios de mídia são relatados na chamada de início, não na chamada de fechamento. É a única métrica da Fase 1 que não espera pelo fechamento da sessão.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.view` quando [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.isViewed`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feeds de dados | `event_list`, `post_event_list` (consulte a pesquisa de [`event.tsv`](https://experienceleague.adobe.com/pt-br/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
