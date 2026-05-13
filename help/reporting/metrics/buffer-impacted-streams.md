---
title: Fluxos afetados pelo buffer
description: Conta sessões em que o player entrou em um estado de buffer pelo menos uma vez.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 9%

---


# Fluxos afetados pelo buffer

A métrica **Fluxos afetados pelo buffer** conta sessões nas quais o player entrou em um estado de buffer pelo menos uma vez. A métrica é booleana em nível de sessão — vários eventos de buffer na mesma contagem de sessão que um fluxo afetado. Para o volume de buffer total, use [Eventos de buffer](buffer-events.md).

## Como essa métrica é calculada

O back-end de mídia define `mediaReporting.qoeDataDetails.hasBufferImpactedStreams = true` na primeira vez que um evento `media.bufferStart` é recebido durante a sessão. A métrica é relatada na chamada de fechamento.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.qoe.buffer` quando a [[!UICONTROL Qualidade de Mídia]](/help/reporting/media-reports-enable.md) está habilitada. |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.hasBufferImpactedStreams`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Feeds de dados | `event_list`, `post_event_list` (consulte a pesquisa de [`event.tsv`](https://experienceleague.adobe.com/pt-br/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
