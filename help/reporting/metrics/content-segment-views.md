---
title: Visualizações do segmento de conteúdo
description: Conta segmentos nos quais ocorreu a reprodução do conteúdo principal ativo.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '176'
ht-degree: 7%

---


# Visualizações do segmento de conteúdo

A métrica **Visualizações de segmento de conteúdo** conta segmentos de conteúdo de cinco minutos nos quais ocorreu a reprodução do conteúdo principal ativo. A métrica confirma que o visualizador reproduziu o conteúdo nesse segmento, em vez de apenas carregar ou armazenar em buffer. Emparelhe-a com a dimensão [Segmento de conteúdo](/help/reporting/dimensions/content-segment.md) para detalhar quais partes dos visualizadores de conteúdo de formulário longo realmente consumiram.

## Como essa métrica é calculada

O back-end de mídia define `mediaReporting.sessionDetails.hasSegmentView = true` para qualquer chamada de fechamento que cubra um segmento no qual pelo menos um evento `media.play` para conteúdo principal foi recebido. A métrica é relatada na chamada de fechamento. No caminho da API do Media Edge, as visualizações de segmento são acionadas nas mesmas condições que os inícios de conteúdo. Ambos exigem um `media.play` sobre o conteúdo principal.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.segmentView` quando [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.hasSegmentView`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feeds de dados | `event_list`, `post_event_list` (consulte a pesquisa de [`event.tsv`](https://experienceleague.adobe.com/pt-br/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
