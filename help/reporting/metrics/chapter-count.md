---
title: Contagem de capítulo
description: Informa o número de capítulos iniciados durante uma sessão.
feature: Metrics
role: User, Admin
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
    internal-label: Metrics
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
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
