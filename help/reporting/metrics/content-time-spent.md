---
title: Tempo gasto com o conteúdo
description: Informa o total de segundos de reprodução do conteúdo principal ativo por sessão.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 7%

---


# Tempo gasto com o conteúdo

A métrica **Tempo gasto com conteúdo** relata o total de segundos de reprodução do conteúdo principal ativo por sessão, excluindo anúncios, pausas, buffering e interrupções. Use-a como métrica de envolvimento para exibição de conteúdo; para o tempo gasto incluindo anúncios, consulte [Tempo gasto com a mídia](media-time-spent.md).

## Como essa métrica é calculada

O back-end de mídia soma o tempo decorrido do relógio de parede entre os eventos enquanto o reprodutor está no estado `play` no conteúdo principal. O tempo durante anúncios, pausas, eventos de buffer e interrupções é excluído. A métrica é relatada na chamada de fechamento. O valor é mostrado como `HH:MM:SS` no Analysis Workspace e em segundos nos Feeds de dados, Data Warehouse e APIs de relatórios.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.timePlayed` quando [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.timePlayed`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feeds de dados | `event_list`, `post_event_list` (consulte a pesquisa de [`event.tsv`](https://experienceleague.adobe.com/pt-br/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
