---
title: Fluxos estimados
description: Aproxima o número de fluxos de áudio ou vídeo por sessão.
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
source-wordcount: '190'
ht-degree: 10%
---

# Fluxos estimados

A métrica **Fluxos estimados** aproxima o número de fluxos de áudio ou vídeo por sessão, com um fluxo contado para cada 30 minutos de reprodução total. Ele destina-se a contratos de sindicalização de conteúdo e alcança aproximações nas quais cada bloco de consumo de 30 minutos conta como um &quot;fluxo&quot; separado.

## Como essa métrica é calculada

O back-end de mídia calcula essa métrica como `FLOOR(totalTimePlayed / 1800) + 1`, em que `totalTimePlayed` é [Tempo gasto com a mídia](media-time-spent.md) em segundos. A métrica é relatada na chamada de fechamento.

| Tempo gasto com a mídia | Fluxos estimados |
| --- | --- |
| 0 a 29 min | 1 |
| 30 a 59 min | 2 |
| 60 a 89 min | 3 |
| 90+ min | 4+ |

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Crie uma [Regra de processamento](https://experienceleague.adobe.com/pt-br/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) que mapeie `a.media.estimatedStreams` para um evento personalizado. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.estimatedStreams`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feeds de dados | `event_list`, `post_event_list` (o evento personalizado para o qual sua regra de processamento mapeia `a.media.estimatedStreams`; consulte a pesquisa de [`event.tsv`](https://experienceleague.adobe.com/pt-br/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.estimatedStreams` |
