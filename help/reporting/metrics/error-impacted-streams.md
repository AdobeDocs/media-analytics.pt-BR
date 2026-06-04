---
title: Fluxos afetados pelo erro
description: Conta sessões em que ocorreu pelo menos um erro.
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 10%

---


# Fluxos afetados pelo erro

A métrica **Fluxos afetados por erro** conta sessões nas quais pelo menos um erro ocorreu (`trackError` foi chamado ou um evento [erro](/help/implementation/events/error.md) foi acionado). A métrica é booleana em nível de sessão — vários erros na mesma contagem de sessão que um fluxo afetado. Para o volume de erros total, use [Erros](/help/reporting/dimensions/errors.md).

## Como essa métrica é calculada

O back-end de mídia define esse sinalizador na primeira vez que um evento [error](/help/implementation/events/error.md) é recebido durante a sessão. A métrica é relatada na chamada de fechamento.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.qoe.error` quando a [[!UICONTROL Qualidade de Mídia]](/help/reporting/setup/analytics-reporting.md) está habilitada. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.hasErrorImpactedStreams`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Feeds de dados | `event_list`, `post_event_list` (consulte a pesquisa de [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.qoe.error` |
