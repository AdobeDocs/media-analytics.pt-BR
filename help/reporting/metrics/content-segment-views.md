---
title: Visualizações do segmento de conteúdo
description: Conta segmentos nos quais ocorreu a reprodução do conteúdo principal ativo.
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
source-wordcount: '185'
ht-degree: 9%
---

# Visualizações do segmento de conteúdo

A métrica **Visualizações de segmento de conteúdo** conta segmentos de conteúdo de cinco minutos nos quais ocorreu a reprodução do conteúdo principal ativo. A métrica confirma que o visualizador reproduziu o conteúdo nesse segmento, em vez de apenas carregar ou armazenar em buffer. Emparelhe-a com a dimensão [Segmento de conteúdo](/help/reporting/dimensions/content-segment.md) para detalhar quais partes dos visualizadores de conteúdo de formulário longo realmente consumiram.

## Como essa métrica é calculada

O back-end de mídia define esse sinalizador para qualquer chamada de fechamento que cubra um segmento no qual pelo menos um evento [play](/help/implementation/events/playback/play.md) para conteúdo principal foi recebido. A métrica é relatada na chamada de fechamento. No caminho da API do Media Edge, as visualizações de segmento são acionadas nas mesmas condições que os inícios de conteúdo. Ambos exigem um evento [play](/help/implementation/events/playback/play.md) no conteúdo principal.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.segmentView` quando [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.hasSegmentView`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feeds de dados | `event_list`, `post_event_list` (consulte a pesquisa de [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | N/D |
