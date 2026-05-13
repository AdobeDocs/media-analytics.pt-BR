---
title: Fluxos afetados pela alteração na taxa de bits
description: Conta sessões em que ocorreu pelo menos uma alteração de taxa de bits.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 9%

---


# Fluxos afetados pela alteração na taxa de bits

A métrica **Alteração na taxa de bits impactou os fluxos** ao contar sessões em que ocorreu pelo menos uma alteração na taxa de bits. A métrica é booleana em nível de sessão — várias alterações na taxa de bits na mesma contagem de sessão que um fluxo afetado. Para o volume total de alteração da taxa de bits, use [alterações da taxa de bits](/help/reporting/dimensions/bitrate-changes.md).

## Como essa métrica é calculada

O back-end de mídia define `mediaReporting.qoeDataDetails.hasBitrateChangeImpactedStreams = true` na primeira vez que um evento `media.bitrateChange` é recebido durante a sessão. A métrica é relatada na chamada de fechamento.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.qoe.bitrateChange` quando a [[!UICONTROL Qualidade de Mídia]](/help/reporting/media-reports-enable.md) está habilitada. |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.hasBitrateChangeImpactedStreams`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Feeds de dados | `event_list`, `post_event_list` (consulte a pesquisa de [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
