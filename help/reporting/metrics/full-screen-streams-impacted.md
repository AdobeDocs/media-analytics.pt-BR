---
title: Fluxos afetados pela tela cheia
description: Conta sessões em que o visualizador entrou em tela cheia pelo menos uma vez.
feature: Metrics
role: User, Admin
source-git-commit: 4c4f1cc9e1c49044474e4ff34207796b2a814553
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 8%

---


# Fluxos afetados pela tela cheia

>[!BEGINSHADEBOX]

*Esta página aborda os **Fluxos afetados pela métrica de relatório de tela cheia**. Consulte [Tela inteira](/help/implementation/variables/player-state/full-screen.md) para saber como coletar essa variável.*

>[!ENDSHADEBOX]

A métrica **Fluxos afetados pela tela cheia** conta sessões nas quais o visualizador entrou na tela cheia pelo menos uma vez. A métrica é booleana em nível de sessão — várias entradas de tela cheia na mesma contagem de sessão como um fluxo afetado. Para o volume total de entradas em tela cheia, use [Contagens de tela cheia](full-screen-count.md).

## Como essa métrica é calculada

O back-end de mídia define esse sinalizador na primeira vez que um evento de início de estado em tela cheia é recebido durante a sessão. A métrica é relatada na chamada de fechamento.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.states.fullscreen.set` quando o [[!UICONTROL Rastreamento do Estado do Player]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.states[]`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/media-reporting-details) entrada onde `name = "fullscreen"`, campo `isSet` |
| Feeds de dados | `event_list`, `post_event_list` (consulte a pesquisa de [`event.tsv`](https://experienceleague.adobe.com/pt-br/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.states.fullscreen.set` |
