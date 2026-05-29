---
title: Anúncio iniciado
description: Conta cada anúncio que começou a ser reproduzido durante uma sessão.
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
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
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.ad.view` quando o [[!UICONTROL Media Ads]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.isStarted`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Feeds de dados | `event_list`, `post_event_list` (consulte a pesquisa de [`event.tsv`](https://experienceleague.adobe.com/pt-br/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.ad.view` |
