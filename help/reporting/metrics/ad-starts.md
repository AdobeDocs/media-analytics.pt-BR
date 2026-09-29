---
title: Anúncio iniciado
description: Conta cada anúncio que começou a ser reproduzido durante uma sessão.
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
source-wordcount: '126'
ht-degree: 11%
---

# Anúncio iniciado

A métrica **Anúncio iniciado** conta todos os anúncios que começaram a ser reproduzidos durante a sessão. Emparelhe-o com [Anúncio concluído](ad-completes.md) para calcular a taxa de conclusão do anúncio, e com [Contagem de anúncios](/help/reporting/metrics/ad-count.md) para a distribuição equivalente em nível de sessão.

## Como essa métrica é calculada

O back-end de mídia define esse sinalizador quando um evento [ad start](/help/implementation/events/ads/ad-start.md) é recebido. A métrica é relatada na chamada de início do anúncio.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.ad.view` quando o [[!UICONTROL Media Ads]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.isStarted`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Feeds de dados | `event_list`, `post_event_list` (consulte a pesquisa de [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.ad.view` |
