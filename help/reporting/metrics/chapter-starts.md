---
title: Início do capítulo
description: Conta cada capítulo que começou a ser reproduzido durante uma sessão.
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
source-wordcount: '116'
ht-degree: 12%
---

# Início do capítulo

A métrica **Início do capítulo** conta todos os capítulos que começaram a ser executados durante uma sessão. Emparelhe-o com [Conclusões de capítulo](chapter-completes.md) para calcular a taxa de conclusão do capítulo.

## Como essa métrica é calculada

O back-end de mídia define esse sinalizador quando um evento [início de capítulo](/help/implementation/events/chapters/chapter-start.md) é recebido. A métrica é relatada na chamada de fechamento do capítulo.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.chapter.view` quando [[!UICONTROL Capítulos de mídia]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.chapterDetails.isStarted`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/chapter-details-reporting) |
| Feeds de dados | `event_list`, `post_event_list` (consulte a pesquisa de [`event.tsv`](https://experienceleague.adobe.com/pt-br/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.chapter.view` |
