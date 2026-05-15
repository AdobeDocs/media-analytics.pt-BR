---
title: Início do conteúdo
description: Conta sessões em que o conteúdo principal realmente começou a ser reproduzido.
feature: Metrics
role: User, Admin
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 10%

---


# Início do conteúdo

A métrica **Início do conteúdo** conta as sessões em que o conteúdo principal realmente começou a ser reproduzido. Ao contrário do [Media starts](media-starts.md), ele exclui sessões que terminaram durante anúncios precedentes, buffering ou interrupções. Isso o torna o denominador correto para taxas de conclusão e engajamento.

## Como essa métrica é calculada

O back-end de mídia define `mediaReporting.sessionDetails.isPlayed = true` na primeira vez que um evento [play](/help/implementation/events/playback/play.md) para conteúdo principal é recebido. A métrica é acionada nesse evento de reprodução, mas relatada na chamada de fechamento. Para calcular a taxa de descarte antes da exibição, use `(Media starts − Content starts) / Media starts`.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.play` quando [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.isPlayed`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feeds de dados | `event_list`, `post_event_list` (consulte a pesquisa de [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.play` |
