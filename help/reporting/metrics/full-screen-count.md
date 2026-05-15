---
title: Contagens de tela inteira
description: Relata o número de vezes que o visualizador entrou em tela cheia durante uma sessão.
feature: Metrics
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '173'
ht-degree: 8%

---


# Contagens de tela inteira

>[!BEGINSHADEBOX]

*Esta página aborda a **contagem de tela cheia**métrica de relatório. Consulte [Tela inteira](/help/implementation/variables/player-state/full-screen.md) para saber como coletar essa variável.*

>[!ENDSHADEBOX]

A métrica **Contagens de tela cheia** informa o número de vezes que o visualizador entrou em tela cheia durante uma sessão. Cada evento de início de estado de tela cheia incrementa a contagem. Emparelhe com [Fluxos afetados pela tela cheia](full-screen-streams-impacted.md) para rollups booleanos em nível de sessão e com [Duração total da tela cheia](full-screen-total-duration.md) para o tempo total no estado.

## Como essa métrica é calculada

O back-end de mídia incrementa o campo `count` na entrada `fullscreen` de `mediaReporting.states[]` em cada evento de início de estado de tela cheia. A métrica é relatada na chamada de fechamento.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.states.fullscreen.count` quando o [[!UICONTROL Rastreamento do Estado do Player]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details) entrada onde `name = "fullscreen"`, campo `count` |
| Feeds de dados | `event_list`, `post_event_list` (consulte a pesquisa de [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.states.fullscreen.count` |
