---
title: Contagem de capítulo
description: Informa o número de capítulos iniciados durante uma sessão.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 7%

---


# Contagem de capítulo

A métrica **Contagem de capítulos** informa o número de capítulos iniciados durante uma sessão. Use-o para comparar o consumo de capítulo entre o conteúdo. Para contagens de início de capítulo giradas por dimensões de capítulo (nome do capítulo, posição), use a métrica de inícios de capítulo disponível quando a categoria de variável Capítulos estiver ativada.

## Como essa métrica é calculada

O back-end de mídia incrementa `mediaReporting.sessionDetails.chapterCount` em cada evento `media.chapterStart` recebido durante a sessão. A métrica é relatada na chamada de fechamento.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Crie uma [Regra de processamento](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) que mapeie `a.media.chapterCount` para um evento personalizado. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.chapterCount`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feeds de dados | `event_list`, `post_event_list` (o evento personalizado para o qual sua regra de processamento mapeia `a.media.chapterCount`; consulte a pesquisa de [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
