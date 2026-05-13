---
title: Duração total da função Em foco
description: Relata os segundos cumulativos em que o player esteve em foco durante uma sessão.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 7%

---


# Duração total da função Em foco

>[!BEGINSHADEBOX]

*Esta página aborda a métrica de relatório **Duração total do foco**. Consulte [Em foco](/help/implementation/variables/player-state/in-focus.md) para saber como coletar essa variável.*

>[!ENDSHADEBOX]

A métrica **Duração total do foco** informa o tempo cumulativo, em segundos, que o player esteve em foco durante uma sessão. O backend soma cada intervalo entre um início de estado de foco e o evento de fim de estado correspondente.

## Como essa métrica é calculada

As somas de tempo decorrido do back-end de mídia em todos os intervalos em foco durante a sessão. A métrica é relatada na chamada de fechamento. O Analysis Workspace mostra o valor como `HH:MM:SS`; Feeds de dados, Data Warehouse e APIs de relatórios mostram o valor em segundos.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.states.infocus.time` quando o [[!UICONTROL Rastreamento do Estado do Player]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.states[]`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/media-reporting-details) entrada onde `name = "inFocus"`, campo `time` |
| Feeds de dados | `event_list`, `post_event_list` (consulte a pesquisa de [`event.tsv`](https://experienceleague.adobe.com/pt-br/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
