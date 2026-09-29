---
title: Contagem de anúncios
description: Relata o número de anúncios iniciados durante uma sessão.
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
source-wordcount: '176'
ht-degree: 9%
---

# Contagem de anúncios

A métrica **Contagem de anúncios** informa o número de anúncios iniciados durante uma sessão. Use-o para entender a carga do anúncio por conteúdo, canal ou tipo de fluxo. Para contagens de início de anúncios giradas por dimensões de anúncio (anunciante, campanha, criativo), use a métrica Inícios de anúncio disponível quando a categoria de variável Anúncios estiver habilitada.

## Como essa métrica é calculada

O back-end de mídia incrementa essa contagem a cada evento [ad start](/help/implementation/events/ads/ad-start.md) recebido durante a sessão. A métrica é relatada na chamada de fechamento.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Crie uma [Regra de processamento](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) que mapeie `a.media.adCount` para um evento personalizado. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.adCount`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feeds de dados | `event_list`, `post_event_list` (o evento personalizado para o qual sua regra de processamento mapeia `a.media.adCount`; consulte a pesquisa de [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | N/D |
