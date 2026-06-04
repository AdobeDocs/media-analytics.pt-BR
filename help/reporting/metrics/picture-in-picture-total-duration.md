---
title: Duração total do Picture in picture
description: Relata os segundos cumulativos que o visualizador gastou em picture-in-picture durante uma sessão.
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 7%

---


# Duração total do Picture in picture

>[!BEGINSHADEBOX]

*Esta página aborda a métrica de relatório **Duração total do Picture in picture**. Consulte [Picture in picture](/help/implementation/variables/player-state/picture-in-picture.md) para saber como coletar essa variável.*

>[!ENDSHADEBOX]

A métrica **Duração total do Picture in picture** relata o tempo cumulativo, em segundos, que o visualizador gastou no picture in picture durante uma sessão. O back-end soma cada intervalo entre um início de estado de picture-in-picture e o evento de fim de estado correspondente.

## Como essa métrica é calculada

O back-end de mídia soma o tempo decorrido em todos os intervalos picture-in-picture durante a sessão. A métrica é relatada na chamada de fechamento. O Analysis Workspace mostra o valor como `HH:MM:SS`; Feeds de dados, Data Warehouse e APIs de relatórios mostram o valor em segundos.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.states.pictureinpicture.time` quando o [[!UICONTROL Rastreamento do Estado do Player]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.states[]`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/media-reporting-details) entrada onde `name = "pictureInPicture"`, campo `time` |
| Feeds de dados | `event_list`, `post_event_list` (consulte a pesquisa de [`event.tsv`](https://experienceleague.adobe.com/pt-br/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.states.pictureinpicture.time` |
