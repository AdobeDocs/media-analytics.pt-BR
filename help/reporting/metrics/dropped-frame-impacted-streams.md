---
title: Fluxos afetados por quedas de quadros
description: Conta sessões em que pelo menos um quadro foi descartado.
feature: Metrics
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '133'
ht-degree: 11%

---


# Fluxos afetados por quedas de quadros

A métrica **Queda de quadro afetou os fluxos** ao contar sessões em que pelo menos um quadro foi descartado. A métrica é um booleano em nível de sessão — várias quedas na mesma contagem de sessão como um fluxo afetado. Para o volume total de descarte, use [Quadros descartados](dropped-frames.md).

## Como essa métrica é calculada

O back-end de mídia define `mediaReporting.qoeDataDetails.hasDroppedFrameImpactedStreams = true` se o valor `droppedFrames` do objeto de QoE for maior que zero no fechamento da sessão.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.qoe.droppedFrames` quando a [[!UICONTROL Qualidade de Mídia]](/help/reporting/media-reports-enable.md) está habilitada. |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.hasDroppedFrameImpactedStreams`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Feeds de dados | `event_list`, `post_event_list` (consulte a pesquisa de [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.qoe.droppedFrames` |
