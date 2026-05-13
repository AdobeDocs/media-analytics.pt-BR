---
title: Início do capítulo
description: Conta cada capítulo que começou a ser reproduzido durante uma sessão.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 11%

---


# Início do capítulo

A métrica **Início do capítulo** conta todos os capítulos que começaram a ser executados durante uma sessão. Emparelhe-o com [Conclusões de capítulo](chapter-completes.md) para calcular a taxa de conclusão do capítulo.

## Como essa métrica é calculada

O back-end de mídia define `mediaReporting.chapterDetails.isStarted = true` quando um evento `media.chapterStart` é recebido. A métrica é relatada na chamada de fechamento do capítulo.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.chapter.view` quando [[!UICONTROL Capítulos de mídia]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.chapterDetails.isStarted`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/chapter-details-reporting) |
| Feeds de dados | `event_list`, `post_event_list` (consulte a pesquisa de [`event.tsv`](https://experienceleague.adobe.com/pt-br/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
