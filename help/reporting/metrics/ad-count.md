---
title: Contagem de anúncios
description: Relata o número de anúncios iniciados durante uma sessão.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 7%

---


# Contagem de anúncios

A métrica **Contagem de anúncios** informa o número de anúncios iniciados durante uma sessão. Use-o para entender a carga do anúncio por conteúdo, canal ou tipo de fluxo. Para contagens de início de anúncios giradas por dimensões de anúncio (anunciante, campanha, criativo), use a métrica Inícios de anúncio disponível quando a categoria de variável Anúncios estiver habilitada.

## Como essa métrica é calculada

O back-end de mídia incrementa `mediaReporting.sessionDetails.adCount` em cada evento `media.adStart` recebido durante a sessão. A métrica é relatada na chamada de fechamento.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Crie uma [Regra de processamento](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) que mapeie `a.media.adCount` para um evento personalizado. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.adCount`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feeds de dados | `event_list`, `post_event_list` (o evento personalizado para o qual sua regra de processamento mapeia `a.media.adCount`; consulte a pesquisa de [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
