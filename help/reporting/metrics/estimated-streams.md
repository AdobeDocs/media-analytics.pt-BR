---
title: Fluxos estimados
description: Aproxima o número de fluxos de áudio ou vídeo por sessão.
feature: Metrics
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 10%

---


# Fluxos estimados

A métrica **Fluxos estimados** aproxima o número de fluxos de áudio ou vídeo por sessão, com um fluxo contado para cada 30 minutos de reprodução total. Ele destina-se a contratos de sindicalização de conteúdo e alcança aproximações nas quais cada bloco de consumo de 30 minutos conta como um &quot;fluxo&quot; separado.

## Como essa métrica é calculada

O back-end de mídia computa `mediaReporting.sessionDetails.estimatedStreams = FLOOR(totalTimePlayed / 1800) + 1`, onde `totalTimePlayed` é [Tempo de mídia gasto](media-time-spent.md) em segundos. A métrica é relatada na chamada de fechamento.

| Tempo gasto com a mídia | Fluxos estimados |
| --- | --- |
| 0 a 29 min | 1 |
| 30 a 59 min | 2 |
| 60 a 89 min | 3 |
| 90+ min | 4+ |

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Crie uma [Regra de processamento](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) que mapeie `a.media.estimatedStreams` para um evento personalizado. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.estimatedStreams`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feeds de dados | `event_list`, `post_event_list` (o evento personalizado para o qual sua regra de processamento mapeia `a.media.estimatedStreams`; consulte a pesquisa de [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.estimatedStreams` |
