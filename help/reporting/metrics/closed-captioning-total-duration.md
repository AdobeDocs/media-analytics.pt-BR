---
title: Duração total das legendas ocultas
description: Relata que as legendas de segundos cumulativos foram habilitadas durante uma sessão.
feature: Metrics
role: User, Admin
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
    internal-label: Metrics
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '174'
ht-degree: 8%
---

# Duração total das legendas ocultas

>[!BEGINSHADEBOX]

*Esta página aborda a **Duração total da legenda oculta**. Consulte [Legendas ocultas](/help/implementation/variables/player-state/closed-captioning.md) para saber como coletar essa variável.*

>[!ENDSHADEBOX]

A métrica **Duração total das legendas ocultas** relata o tempo cumulativo, em segundos, em que as legendas foram habilitadas durante uma sessão. O backend soma cada intervalo entre um início de estado habilitado para legenda e o evento de fim de estado correspondente.

## Como essa métrica é calculada

As somas de tempo decorrido do back-end de mídia em todos os intervalos habilitados para legenda durante a sessão. A métrica é relatada na chamada de fechamento. O Analysis Workspace mostra o valor como `HH:MM:SS`; Feeds de dados, Data Warehouse e APIs de relatórios mostram o valor em segundos.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.states.closedcaptioning.time` quando o [[!UICONTROL Rastreamento do Estado do Player]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.states[]`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/media-reporting-details) entrada onde `name = "closedCaptioning"`, campo `time` |
| Feeds de dados | `event_list`, `post_event_list` (consulte a pesquisa de [`event.tsv`](https://experienceleague.adobe.com/pt-br/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.states.closedcaptioning.time` |
