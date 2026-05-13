---
title: Capítulo completo
description: Conta cada capítulo reproduzido até a conclusão.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 11%

---


# Capítulo completo

A métrica **Capítulo concluído** conta todos os capítulos reproduzidos até a conclusão. Emparelhe-o com [Inícios de capítulo](chapter-starts.md) para calcular a taxa de conclusão do capítulo.

## Como essa métrica é calculada

O back-end de mídia define `mediaReporting.chapterDetails.isCompleted = true` quando um evento `media.chapterComplete` é recebido. A métrica é relatada na chamada de fechamento do capítulo. Os capítulos ignorados ou abandonados no meio da reprodução não contam como conclusões.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.chapter.complete` quando [[!UICONTROL Capítulos de mídia]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.chapterDetails.isCompleted`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/chapter-details-reporting) |
| Feeds de dados | `event_list`, `post_event_list` (consulte a pesquisa de [`event.tsv`](https://experienceleague.adobe.com/pt-br/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
