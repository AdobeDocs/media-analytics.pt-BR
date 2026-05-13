---
title: Tempo gasto com capítulo
description: Informa o total de segundos de reprodução ativa por capítulo.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 8%

---


# Tempo gasto com capítulo

A métrica **Tempo gasto com capítulo** relata o total de segundos de reprodução ativa por capítulo. Emparelhe-o com [Comprimento do capítulo](/help/reporting/dimensions/chapter-length.md) para calcular o compartilhamento de cada capítulo consumido.

## Como essa métrica é calculada

O back-end de mídia soma o tempo decorrido do relógio de parede entre os eventos enquanto o reprodutor está no estado `play` em um capítulo. O tempo durante pausas, buffering e paralisações é excluído. A métrica é relatada na chamada de fechamento do capítulo. O valor é mostrado como `HH:MM:SS` no Analysis Workspace e em segundos nos Feeds de dados, Data Warehouse e APIs de relatórios.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.chapter.timePlayed` quando [[!UICONTROL Capítulos de mídia]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.chapterDetails.timePlayed`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/chapter-details-reporting) |
| Feeds de dados | `event_list`, `post_event_list` (consulte a pesquisa de [`event.tsv`](https://experienceleague.adobe.com/pt-br/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
