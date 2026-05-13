---
title: Contagens de Picture in picture
description: Informa o número de vezes que o visualizador entrou no picture-in-picture durante uma sessão.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 7%

---


# Contagens de Picture in picture

>[!BEGINSHADEBOX]

*Esta página aborda a **métrica de relatórios de contagem de imagens**&#x200B;do Picture in picture. Consulte [Picture in picture](/help/implementation/variables/player-state/picture-in-picture.md) para saber como coletar essa variável.*

>[!ENDSHADEBOX]

A métrica **Picture in picture count** relata o número de vezes que o visualizador inseriu a reprodução picture-in-picture durante uma sessão. Cada evento de início de estado de picture-in-picture incrementa a contagem. Emparelhe com [Fluxos afetados pela imagem na imagem](picture-in-picture-streams-impacted.md) para rollups booleanos em nível de sessão e com [Duração total da imagem na imagem](picture-in-picture-total-duration.md) para tempo total no estado.

## Como essa métrica é calculada

O back-end de mídia incrementa o campo `count` na entrada `pictureInPicture` de `mediaReporting.states[]` em cada evento de início de estado de picture-in-picture. A métrica é relatada na chamada de fechamento.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.states.pictureinpicture.count` quando o [[!UICONTROL Rastreamento do Estado do Player]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.states[]`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/media-reporting-details) entrada onde `name = "pictureInPicture"`, campo `count` |
| Feeds de dados | `event_list`, `post_event_list` (consulte a pesquisa de [`event.tsv`](https://experienceleague.adobe.com/pt-br/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
