---
title: Contagens da função Em foco
description: Relata o número de vezes que o reprodutor ganhou foco durante uma sessão.
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
source-wordcount: '165'
ht-degree: 9%
---

# Contagens da função Em foco

>[!BEGINSHADEBOX]

*Esta página aborda a métrica de relatório **Contagens de foco**. Consulte [Em foco](/help/implementation/variables/player-state/in-focus.md) para saber como coletar essa variável.*

>[!ENDSHADEBOX]

A métrica **Em contagens de foco** informa o número de vezes que o player ganhou foco durante uma sessão. Cada evento de início de estado de foco aumenta a contagem. Emparelhe com [Fluxos afetados pela função em foco](in-focus-streams-impacted.md) para rollups booleanos em nível de sessão e com [Duração total da função em foco](in-focus-total-duration.md) para o tempo total em estado.

## Como essa métrica é calculada

O back-end de mídia incrementa essa contagem em cada evento de início de estado de foco. A métrica é relatada na chamada de fechamento.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.states.infocus.count` quando o [[!UICONTROL Rastreamento do Estado do Player]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details) entrada onde `name = "inFocus"`, campo `count` |
| Feeds de dados | `event_list`, `post_event_list` (consulte a pesquisa de [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.states.infocus.count` |
