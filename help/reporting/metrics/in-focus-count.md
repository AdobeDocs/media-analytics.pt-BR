---
title: Contagens da função Em foco
description: Relata o número de vezes que o reprodutor ganhou foco durante uma sessão.
feature: Metrics
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 7%

---


# Contagens da função Em foco

>[!BEGINSHADEBOX]

*Esta página aborda a métrica de relatório **Contagens de foco**. Consulte [Em foco](/help/implementation/variables/player-state/in-focus.md) para saber como coletar essa variável.*

>[!ENDSHADEBOX]

A métrica **Em contagens de foco** informa o número de vezes que o player ganhou foco durante uma sessão. Cada evento de início de estado de foco aumenta a contagem. Emparelhe com [Fluxos afetados pela função em foco](in-focus-streams-impacted.md) para rollups booleanos em nível de sessão e com [Duração total da função em foco](in-focus-total-duration.md) para o tempo total em estado.

## Como essa métrica é calculada

O back-end de mídia incrementa o campo `count` na entrada `inFocus` de `mediaReporting.states[]` em cada evento de início de estado de foco. A métrica é relatada na chamada de fechamento.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.states.infocus.count` quando o [[!UICONTROL Rastreamento do Estado do Player]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.states[]`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/media-reporting-details) entrada onde `name = "inFocus"`, campo `count` |
| Feeds de dados | `event_list`, `post_event_list` (consulte a pesquisa de [`event.tsv`](https://experienceleague.adobe.com/pt-br/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
