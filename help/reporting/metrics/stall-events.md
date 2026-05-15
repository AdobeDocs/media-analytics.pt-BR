---
title: Eventos de parada
description: Conta eventos de paralisação para somas e médias entre sessões.
feature: Metrics
role: User, Admin
source-git-commit: 1278355e0bfc67c635250c426edaf865fb658c37
workflow-type: tm+mt
source-wordcount: '203'
ht-degree: 7%

---


# Eventos de parada

A métrica **Eventos de paralisação** conta eventos de paralisação entre sessões, adequados para somas, médias e acúmulos de percentil. Use a métrica para calcular o volume total de paralisações em um período do relatório e comparar a estabilidade de paralisações entre conteúdo, redes ou players.

No Customer Journey Analytics, `mediaReporting.qoeDataDetails.stallCount` pode ser usado como uma métrica ou uma dimensão sem um componente de dimensão separado.

## Como essa métrica é calculada

O back-end de mídia incrementa a contagem sempre que nenhum movimento do indicador de reprodução é gravado no conteúdo principal por pelo menos três eventos consecutivos. A métrica é relatada na chamada de fechamento.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Crie uma [Regra de processamento](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) que mapeie `a.media.qoe.stallCount` para um evento personalizado. |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.stallCount`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Feeds de dados | `event_list`, `post_event_list` (o evento personalizado para o qual sua regra de processamento mapeia `a.media.qoe.stallCount`; consulte a pesquisa de [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.qoe.stallCount` |

Para relatórios booleanos em nível de sessão (independentemente de ter ocorrido alguma paralisação), use [Fluxos afetados pela paralisação](stall-impacted-streams.md).
