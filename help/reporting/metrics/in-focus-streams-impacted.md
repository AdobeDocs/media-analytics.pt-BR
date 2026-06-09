---
title: Fluxos afetados pela função em foco
description: Conta sessões em que o player estava em foco pelo menos uma vez.
feature: Metrics
role: User, Admin
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 8%

---


# Fluxos afetados pela função em foco

>[!BEGINSHADEBOX]

*Esta página aborda a métrica de relatório **Fluxos afetados pela função em foco**. Consulte [Em foco](/help/implementation/variables/player-state/in-focus.md) para saber como coletar essa variável.*

>[!ENDSHADEBOX]

A métrica **Fluxos afetados pela métrica em foco** conta sessões nas quais o player estava em foco pelo menos uma vez. A métrica é um booleano em nível de sessão; vários eventos de foco na mesma contagem de sessão como um fluxo afetado. Para o volume de evento de foco total, use [Contagens de foco](in-focus-count.md).

## Como essa métrica é calculada

O back-end de mídia define esse sinalizador na primeira vez que um evento de início de estado de foco é recebido durante a sessão. A métrica é relatada na chamada de fechamento.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.states.infocus.set` quando o [[!UICONTROL Rastreamento do Estado do Player]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.states[]`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/media-reporting-details) entrada onde `name = "inFocus"`, campo `isSet` |
| Feeds de dados | `event_list`, `post_event_list` (consulte a pesquisa de [`event.tsv`](https://experienceleague.adobe.com/pt-br/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.states.infocus.set` |
