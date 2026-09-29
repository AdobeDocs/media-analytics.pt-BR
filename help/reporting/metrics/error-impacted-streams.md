---
title: Fluxos afetados pelo erro
description: Conta sessões em que ocorreu pelo menos um erro.
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
source-wordcount: '143'
ht-degree: 10%
---

# Fluxos afetados pelo erro

A métrica **Fluxos afetados por erro** conta sessões nas quais pelo menos um erro ocorreu (`trackError` foi chamado ou um evento [erro](/help/implementation/events/error.md) foi acionado). A métrica é um booleano em nível de sessão; vários erros na mesma contagem de sessão que um fluxo afetado. Para o volume de erros total, use [Erros](/help/reporting/dimensions/errors.md).

## Como essa métrica é calculada

O back-end de mídia define esse sinalizador na primeira vez que um evento [error](/help/implementation/events/error.md) é recebido durante a sessão. A métrica é relatada na chamada de fechamento.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.qoe.error` quando a [[!UICONTROL Qualidade de Mídia]](/help/reporting/setup/analytics-reporting.md) está habilitada. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.hasErrorImpactedStreams`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Feeds de dados | `event_list`, `post_event_list` (consulte a pesquisa de [`event.tsv`](https://experienceleague.adobe.com/pt-br/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.qoe.error` |
