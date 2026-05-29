---
title: Contagens de Picture in picture
description: Informa o número de vezes que o visualizador entrou no picture-in-picture durante uma sessão.
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 8%

---


# Contagens de Picture in picture

>[!BEGINSHADEBOX]

*Esta página aborda a **métrica de relatórios de contagem de imagens**do Picture in picture. Consulte [Picture in picture](/help/implementation/variables/player-state/picture-in-picture.md) para saber como coletar essa variável.*

>[!ENDSHADEBOX]

A métrica **Picture in picture count** relata o número de vezes que o visualizador inseriu a reprodução picture-in-picture durante uma sessão. Cada evento de início de estado de picture-in-picture incrementa a contagem. Emparelhe com [Fluxos afetados pela imagem na imagem](picture-in-picture-streams-impacted.md) para rollups booleanos em nível de sessão e com [Duração total da imagem na imagem](picture-in-picture-total-duration.md) para tempo total no estado.

## Como essa métrica é calculada

O back-end de mídia incrementa essa contagem em cada evento de início de estado de picture-in-picture. A métrica é relatada na chamada de fechamento.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.states.pictureinpicture.count` quando o [[!UICONTROL Rastreamento do Estado do Player]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details) entrada onde `name = "pictureInPicture"`, campo `count` |
| Feeds de dados | `event_list`, `post_event_list` (consulte a pesquisa de [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.states.pictureinpicture.count` |
