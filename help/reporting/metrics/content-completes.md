---
title: Conteúdo completo
description: Conta as sessões cujo indicador de reprodução atingiu o fim do conteúdo.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 9%

---


# Conteúdo completo

A métrica **Conteúdo concluído** conta as sessões cujo indicador de reprodução atingiu o fim do conteúdo. Emparelhe-o com [Início do conteúdo](content-starts.md) para calcular a taxa de conclusão; emparelhe com [Início da mídia](media-starts.md) para calcular a taxa de exibição de ponta a ponta.

## Como essa métrica é calculada

O back-end de mídia define `mediaReporting.sessionDetails.isCompleted = true` quando um evento `media.sessionComplete` é recebido. A métrica é relatada na chamada de fechamento. Uma sessão que atinge o tempo limite sem um `sessionComplete` explícito não conta como uma conclusão.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.complete` quando [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.isCompleted`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feeds de dados | `event_list`, `post_event_list` (consulte a pesquisa de [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
