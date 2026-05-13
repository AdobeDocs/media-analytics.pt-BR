---
title: Fluxos afetados pelo picture in picture
description: Conta as sessões em que o visualizador entrou no picture-in-picture pelo menos uma vez.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '189'
ht-degree: 6%

---


# Fluxos afetados pelo picture in picture

>[!BEGINSHADEBOX]

*Esta página aborda a métrica de relatório **Fluxos afetados pela imagem na imagem**. Consulte [Picture in picture](/help/implementation/variables/player-state/picture-in-picture.md) para saber como coletar essa variável.*

>[!ENDSHADEBOX]

A métrica **Fluxos afetados pela métrica picture in picture** conta sessões em que o visualizador inseriu a reprodução picture in picture pelo menos uma vez. A métrica é booleana em nível de sessão — várias entradas picture-in-picture na mesma contagem de sessão de um fluxo afetado. Para o volume total de entrada picture-in-picture, use [contagem de picture-in-picture](picture-in-picture-count.md).

## Como essa métrica é calculada

O back-end de mídia define o sinalizador `isSet` em `mediaReporting.states[]` para a entrada `pictureInPicture` como `true` na primeira vez que um evento `media.statesUpdate` com `pictureInPicture` em `statesStart` é recebido. A métrica é relatada na chamada de fechamento.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.states.pictureinpicture.set` quando o [[!UICONTROL Rastreamento do Estado do Player]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.states[]`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/media-reporting-details) entrada onde `name = "pictureInPicture"`, campo `isSet` |
| Feeds de dados | `event_list`, `post_event_list` (consulte a pesquisa de [`event.tsv`](https://experienceleague.adobe.com/pt-br/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
