---
title: Duração total do buffer (métrica)
description: Relata o tempo de buffer cumulativo para somas e médias entre sessões.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 6%

---


# Duração total do buffer (métrica)

>[!BEGINSHADEBOX]

*Esta página abrange a métrica **Duração total do buffer**. O Adobe Analytics preenche automaticamente uma [Duração total do buffer (dimensão)](/help/reporting/dimensions/total-buffer-duration.md) emparelhada a partir da mesma variável de dados de contexto `a.media.qoe.bufferTime`. O Customer Journey Analytics expõe um único campo `mediaReporting.qoeDataDetails.bufferTime` que você pode usar como dimensão ou métrica.*

>[!ENDSHADEBOX]

A métrica **Duração total do buffer** relata o tempo de buffer cumulativo entre sessões, adequado para somas, médias e acúmulos de percentil. Use a métrica para calcular o tempo total que os clientes gastaram aguardando buffers em um período de relatório.

## Como essa métrica é calculada

O back-end de mídia soma a duração de cada intervalo de buffer (de `media.bufferStart` até a próxima alteração de estado). A métrica é relatada na chamada de fechamento. O Analysis Workspace mostra o valor como `HH:MM:SS`; Feeds de dados, Data Warehouse e APIs de relatórios mostram o valor em segundos.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.qoe.bufferTime` quando a [[!UICONTROL Qualidade de Mídia]](/help/reporting/media-reports-enable.md) está habilitada. |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.bufferTime`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Feeds de dados | `event_list`, `post_event_list` (consulte a pesquisa de [`event.tsv`](https://experienceleague.adobe.com/pt-br/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
