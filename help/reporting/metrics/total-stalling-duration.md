---
title: Duração total da paralisação
description: Relata o tempo de paralisação cumulativo para somas e médias entre sessões.
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 7%

---


# Duração total da paralisação

A métrica **Duração total da paralisação** relata o tempo de paralisação cumulativo entre sessões, adequado para somas, médias e acúmulos de percentil. Use a métrica para calcular o tempo total que os visualizadores gastaram aguardando a reprodução interrompida em um período de relatório.

No Customer Journey Analytics, `xdm.mediaReporting.qoeDataDetails.stallTime` pode ser usado como uma métrica ou uma dimensão sem um componente de dimensão separado.

## Como essa métrica é calculada

O back-end de mídia soma a duração de cada intervalo de paralisação, detectado quando nenhum movimento do indicador de reprodução é gravado no conteúdo principal por pelo menos três eventos consecutivos. A métrica é relatada na chamada de fechamento. O Analysis Workspace mostra o valor como `HH:MM:SS`; Feeds de dados, Data Warehouse e APIs de relatórios mostram o valor em segundos.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Crie uma [Regra de processamento](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) que mapeie `a.media.qoe.stallTime` para um evento personalizado. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.stallTime`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Feeds de dados | `event_list`, `post_event_list` (o evento personalizado para o qual sua regra de processamento mapeia `a.media.qoe.stallTime`; consulte a pesquisa de [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.qoe.stallTime` |
