---
title: Contagens de legendas ocultas
description: Informa o número de vezes que o visualizador ativou legendas durante uma sessão.
feature: Metrics
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 8%

---


# Contagens de legendas ocultas

>[!BEGINSHADEBOX]

*Esta página aborda a **métrica de relatórios de contagens de legendas ocultas**. Consulte [Legendas ocultas](/help/implementation/variables/player-state/closed-captioning.md) para saber como coletar essa variável.*

>[!ENDSHADEBOX]

A métrica **Contagens de legendas ocultas** informa o número de vezes que o visualizador ativou legendas durante uma sessão. Cada evento de início de estado habilitado para legenda aumenta a contagem. Emparelhe com [Fluxos afetados pelas legendas ocultas](closed-captioning-streams-impacted.md) para rollups booleanos em nível de sessão e com [Duração total das legendas ocultas](closed-captioning-total-duration.md) para tempo total no estado.

## Como essa métrica é calculada

O back-end de mídia incrementa o campo `count` na entrada `closedCaptioning` de `mediaReporting.states[]` em cada evento de início de estado habilitado para legenda. A métrica é relatada na chamada de fechamento.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.states.closedcaptioning.count` quando o [[!UICONTROL Rastreamento do Estado do Player]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.states[]`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/media-reporting-details) entrada onde `name = "closedCaptioning"`, campo `count` |
| Feeds de dados | `event_list`, `post_event_list` (consulte a pesquisa de [`event.tsv`](https://experienceleague.adobe.com/pt-br/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.states.closedcaptioning.count` |
