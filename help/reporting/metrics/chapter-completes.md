---
title: Capítulo completo
description: Conta cada capítulo reproduzido até a conclusão.
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 12%

---


# Capítulo completo

A métrica **Capítulo concluído** conta todos os capítulos reproduzidos até a conclusão. Emparelhe-o com [Inícios de capítulo](chapter-starts.md) para calcular a taxa de conclusão do capítulo.

## Como essa métrica é calculada

O back-end de mídia define esse sinalizador quando um evento [chapter complete](/help/implementation/events/chapters/chapter-complete.md) é recebido. A métrica é relatada na chamada de fechamento do capítulo. Os capítulos ignorados ou abandonados no meio da reprodução não contam como conclusões.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.chapter.complete` quando [[!UICONTROL Capítulos de mídia]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.chapterDetails.isCompleted`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/chapter-details-reporting) |
| Feeds de dados | `event_list`, `post_event_list` (consulte a pesquisa de [`event.tsv`](https://experienceleague.adobe.com/pt-br/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.chapter.complete` |
