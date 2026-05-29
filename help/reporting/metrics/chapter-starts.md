---
title: Início do capítulo
description: Conta cada capítulo que começou a ser reproduzido durante uma sessão.
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 12%

---


# Início do capítulo

A métrica **Início do capítulo** conta todos os capítulos que começaram a ser executados durante uma sessão. Emparelhe-o com [Conclusões de capítulo](chapter-completes.md) para calcular a taxa de conclusão do capítulo.

## Como essa métrica é calculada

O back-end de mídia define esse sinalizador quando um evento [início de capítulo](/help/implementation/events/chapters/chapter-start.md) é recebido. A métrica é relatada na chamada de fechamento do capítulo.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.chapter.view` quando [[!UICONTROL Capítulos de mídia]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.chapterDetails.isStarted`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/chapter-details-reporting) |
| Feeds de dados | `event_list`, `post_event_list` (consulte a pesquisa de [`event.tsv`](https://experienceleague.adobe.com/pt-br/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.chapter.view` |
