---
title: Contagem de capítulo
description: Informa o número de capítulos iniciados durante uma sessão.
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 9%

---


# Contagem de capítulo

A métrica **Contagem de capítulos** informa o número de capítulos iniciados durante uma sessão. Use-o para comparar o consumo de capítulo entre o conteúdo. Para contagens de início de capítulo giradas por dimensões de capítulo (nome do capítulo, posição), use a métrica de inícios de capítulo disponível quando a categoria de variável Capítulos estiver ativada.

## Como essa métrica é calculada

O back-end de mídia incrementa essa contagem em cada evento de [início de capítulo](/help/implementation/events/chapters/chapter-start.md) recebido durante a sessão. A métrica é relatada na chamada de fechamento.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Crie uma [Regra de processamento](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) que mapeie `a.media.chapterCount` para um evento personalizado. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.chapterCount`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feeds de dados | `event_list`, `post_event_list` (o evento personalizado para o qual sua regra de processamento mapeia `a.media.chapterCount`; consulte a pesquisa de [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | N/D |
