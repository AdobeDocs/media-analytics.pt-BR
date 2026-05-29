---
title: Fluxos afetados pela paralisação
description: Conta sessões em que pelo menos uma paralisação ocorreu durante a reprodução.
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 8%

---


# Fluxos afetados pela paralisação

A métrica **Fluxos afetados pela paralisação** conta sessões em que pelo menos uma paralisação ocorreu durante a reprodução. A métrica é booleana em nível de sessão — várias paralisações na mesma contagem de sessões que um fluxo afetado. Para o volume de paralisação total, use [Eventos de paralisação](stall-events.md).

## Como essa métrica é calculada

O back-end de mídia define esse sinalizador quando nenhum movimento do indicador de reprodução é gravado no conteúdo principal por pelo menos três eventos consecutivos durante a sessão. A métrica é relatada na chamada de fechamento.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Crie uma [Regra de processamento](https://experienceleague.adobe.com/pt-br/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) que mapeie `a.media.qoe.stall` para um evento personalizado. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.hasStallImpactedStreams`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Feeds de dados | `event_list`, `post_event_list` (o evento personalizado para o qual sua regra de processamento mapeia `a.media.qoe.stall`; consulte a pesquisa de [`event.tsv`](https://experienceleague.adobe.com/pt-br/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.qoe.stall` |
