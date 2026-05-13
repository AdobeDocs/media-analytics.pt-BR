---
source-git-commit: c06ecd16f417c9584fb87181074d1c2bee487e0b
workflow-type: tm+mt
source-wordcount: '267'
ht-degree: 5%

---
﻿---
title: Métricas calculadas
description: Métricas calculadas personalizadas para relatórios de mídia de transmissão no Adobe Analytics e no Customer Journey Analytics.
feature: Metrics
role: User, Admin
---

# Métricas calculadas

As métricas calculadas para os serviços de streaming de mídia da Adobe são métricas personalizadas criadas a partir das métricas de streaming de mídia padrão, que permitem obter taxas como tempo médio de anúncio gasto ou taxa de conclusão de mídia sem alterar a implementação.

Para criar essas métricas calculadas no Analysis Workspace, consulte a respectiva visão geral em [Adobe Analytics](https://experienceleague.adobe.com/en/docs/analytics/components/calculated-metrics/cm-overview) ou [Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/cja-calcmetrics/calc-metr-overview).

| Métrica calculada | Descrição | Fórmula |
| --- | --- | --- |
| Média anúncios por fluxo de mídia | Anúncio iniciado por mídia iniciada | [`Ad Starts`](/help/reporting/metrics/ad-starts.md) / [`Media Starts`](/help/reporting/metrics/media-starts.md) |
| Média capítulos por fluxo de mídia | Início do capítulo por mídia iniciada | [`Chapter Starts`](/help/reporting/metrics/chapter-starts.md) / [`Media Starts`](/help/reporting/metrics/media-starts.md) |
| Média tempo gasto com a mídia | Tempo total gasto por inicializações de mídia (`HH:MM:SS`) | [`Media Time Spent`](/help/reporting/metrics/media-time-spent.md) / [`Media Starts`](/help/reporting/metrics/media-starts.md) |
| Média tempo gasto com o conteúdo | Tempo gasto no conteúdo por inicializações de conteúdo (`HH:MM:SS`) | [`Content Time Spent`](/help/reporting/metrics/content-time-spent.md) / [`Content Starts`](/help/reporting/metrics/content-starts.md) |
| Média tempo gasto com o anúncio | Tempo gasto no anúncio por inicializações de anúncio (`HH:MM:SS`) | [`Ad Time Spent`](/help/reporting/metrics/ad-time-spent.md) / [`Ad Starts`](/help/reporting/metrics/ad-starts.md) |
| Média tempo gasto com capítulo | Tempo gasto no capítulo por inicializações do capítulo (`HH:MM:SS`) | [`Chapter Time Spent`](/help/reporting/metrics/chapter-time-spent.md) / [`Chapter Starts`](/help/reporting/metrics/chapter-starts.md) |
| Taxa de conclusão da mídia | Taxa de conteúdo concluído vs. mídia iniciada | [`Content Completes`](/help/reporting/metrics/content-completes.md) / [`Media Starts`](/help/reporting/metrics/media-starts.md) |
| Taxa de conclusão do conteúdo | Taxa de conteúdo concluído vs. inícios de conteúdo | [`Content Completes`](/help/reporting/metrics/content-completes.md) / [`Content Starts`](/help/reporting/metrics/content-starts.md) |
| Taxa de conclusão do anúncio | Taxa de conclusões de anúncios vs. inícios de anúncios | [`Ad Completes`](/help/reporting/metrics/ad-completes.md) / [`Ad Starts`](/help/reporting/metrics/ad-starts.md) |
| Taxa de conclusão do capítulo | Taxa de conclusões de capítulo vs. inícios de capítulo | [`Chapter Completes`](/help/reporting/metrics/chapter-completes.md) / [`Chapter Starts`](/help/reporting/metrics/chapter-starts.md) |
| Soltar antes da taxa inicial | Taxa de quedas antes do início vs. início da mídia | [`Drops Before Start`](/help/reporting/metrics/drops-before-start.md) / [`Media Starts`](/help/reporting/metrics/media-starts.md) |
| Taxa de duração da pausa do conteúdo | Taxa de duração total da pausa vs. tempo gasto com conteúdo | [`Total Pause Duration`](/help/reporting/metrics/total-pause-duration.md) / [`Content Time Spent`](/help/reporting/metrics/content-time-spent.md) |
| Taxa de duração do buffer de conteúdo | Taxa de duração total do buffer vs. tempo gasto com conteúdo | [`Total Buffer Duration`](/help/reporting/metrics/total-buffer-duration.md) / [`Content Time Spent`](/help/reporting/metrics/content-time-spent.md) |
| Taxa de tempo para início do conteúdo | Taxa de tempo para iniciar vs. tempo gasto com conteúdo | [`Time to Start`](/help/reporting/metrics/time-to-start.md) / [`Content Time Spent`](/help/reporting/metrics/content-time-spent.md) |
| Taxa de tempo gasto com anúncio | Taxa de tempo gasto com anúncio vs. tempo gasto com conteúdo | [`Ad Time Spent`](/help/reporting/metrics/ad-time-spent.md) / [`Content Time Spent`](/help/reporting/metrics/content-time-spent.md) |
