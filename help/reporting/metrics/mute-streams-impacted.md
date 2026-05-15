---
title: Fluxos afetados pela função mudo
description: Conta sessões em que o visualizador ativou o áudio pelo menos uma vez.
feature: Metrics
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '169'
ht-degree: 8%

---


# Fluxos afetados pela função mudo

>[!BEGINSHADEBOX]

*Esta página aborda os **Fluxos afetados pela métrica de relatório de mudo**. Consulte [Mudo](/help/implementation/variables/player-state/mute.md) para saber como coletar essa variável.*

>[!ENDSHADEBOX]

A métrica **Fluxos afetados pela função mudo** conta sessões nas quais o visualizador desativou o áudio pelo menos uma vez. A métrica é booleana em nível de sessão — vários alternadores de mudo na mesma contagem de sessões que um fluxo afetado. Para o volume com mudo total, use [Contagens de mudo](mute-count.md).

## Como essa métrica é calculada

O back-end de mídia define o sinalizador `isSet` em `mediaReporting.states[]` para a entrada `mute` como `true` na primeira vez que um evento `media.statesUpdate` com `mute` em `statesStart` é recebido. A métrica é relatada na chamada de fechamento.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.states.mute.set` quando o [[!UICONTROL Rastreamento do Estado do Player]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details) entrada onde `name = "mute"`, campo `isSet` |
| Feeds de dados | `event_list`, `post_event_list` (consulte a pesquisa de [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.states.mute.set` |
