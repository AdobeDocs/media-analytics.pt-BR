---
title: Duração total da tela inteira
description: Relata os segundos cumulativos que o visualizador gastou em tela inteira durante uma sessão.
feature: Metrics
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 8%

---


# Duração total da tela inteira

>[!BEGINSHADEBOX]

*Esta página aborda a **duração total da tela cheia**&#x200B;da métrica de relatório. Consulte [Tela inteira](/help/implementation/variables/player-state/full-screen.md) para saber como coletar essa variável.*

>[!ENDSHADEBOX]

A métrica **Duração total da tela cheia** informa o tempo cumulativo, em segundos, que o visualizador gastou em tela cheia durante uma sessão. O backend soma cada intervalo entre um início de estado em tela cheia e o evento de fim de estado correspondente.

## Como essa métrica é calculada

O back-end de mídia soma o tempo decorrido em todos os intervalos de tela cheia durante a sessão. A métrica é relatada na chamada de fechamento. O Analysis Workspace mostra o valor como `HH:MM:SS`; Feeds de dados, Data Warehouse e APIs de relatórios mostram o valor em segundos.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.states.fullscreen.time` quando o [[!UICONTROL Rastreamento do Estado do Player]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.states[]`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/media-reporting-details) entrada onde `name = "fullscreen"`, campo `time` |
| Feeds de dados | `event_list`, `post_event_list` (consulte a pesquisa de [`event.tsv`](https://experienceleague.adobe.com/pt-br/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.states.fullscreen.time` |
