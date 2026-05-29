---
title: Duração total da função Mudo
description: Relata que o áudio de segundos cumulativos foi silenciado durante uma sessão.
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 8%

---


# Duração total da função Mudo

>[!BEGINSHADEBOX]

*Esta página abrange a métrica de relatório **Duração total da função Mudo**. Consulte [Mudo](/help/implementation/variables/player-state/mute.md) para saber como coletar essa variável.*

>[!ENDSHADEBOX]

A métrica **Duração total da função Mudo** informa o tempo cumulativo, em segundos, em que o áudio foi desativado durante uma sessão. O back-end soma cada intervalo entre um início de estado mudo e o evento de fim de estado correspondente.

## Como essa métrica é calculada

As somas de tempo decorrido do back-end de mídia em todos os intervalos de mudo durante a sessão. A métrica é relatada na chamada de fechamento. O Analysis Workspace mostra o valor como `HH:MM:SS`; Feeds de dados, Data Warehouse e APIs de relatórios mostram o valor em segundos.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.states.mute.time` quando o [[!UICONTROL Rastreamento do Estado do Player]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.states[]`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/media-reporting-details) entrada onde `name = "mute"`, campo `time` |
| Feeds de dados | `event_list`, `post_event_list` (consulte a pesquisa de [`event.tsv`](https://experienceleague.adobe.com/pt-br/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.states.mute.time` |
