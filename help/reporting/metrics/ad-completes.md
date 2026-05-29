---
title: Anúncio completo
description: Conta cada anúncio reproduzido até a conclusão.
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '123'
ht-degree: 12%

---


# Anúncio completo

A métrica **Anúncio concluído** conta todos os anúncios reproduzidos até a conclusão. Emparelhe-o com [Inícios do anúncio](ad-starts.md) para calcular a taxa de conclusão do anúncio.

## Como essa métrica é calculada

O back-end de mídia define esse sinalizador quando um evento [anúncio concluído](/help/implementation/events/ads/ad-complete.md) é recebido. A métrica é relatada na chamada de fechamento de anúncio. Os anúncios ignorados ou abandonados não contam como conclusões.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.ad.complete` quando o [[!UICONTROL Media Ads]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.isCompleted`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Feeds de dados | `event_list`, `post_event_list` (consulte a pesquisa de [`event.tsv`](https://experienceleague.adobe.com/pt-br/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.ad.complete` |
