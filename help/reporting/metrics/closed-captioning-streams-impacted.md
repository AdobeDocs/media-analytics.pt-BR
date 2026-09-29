---
title: Fluxos afetados pelas legendas ocultas
description: Conta sessões nas quais o visualizador ativou legendas pelo menos uma vez.
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
source-wordcount: '176'
ht-degree: 8%
---

# Fluxos afetados pelas legendas ocultas

>[!BEGINSHADEBOX]

*Esta página aborda os **Fluxos afetados pelas legendas ocultas**. Consulte [Legendas ocultas](/help/implementation/variables/player-state/closed-captioning.md) para saber como coletar essa variável.*

>[!ENDSHADEBOX]

A métrica **Fluxos afetados pelas legendas ocultas** conta sessões nas quais o visualizador ativou legendas pelo menos uma vez. A métrica é um booleano em nível de sessão; várias alternâncias de legenda na mesma contagem de sessão como um fluxo afetado. Para o volume total habilitado para legenda, use [Contagens de legendas ocultas](closed-captioning-count.md).

## Como essa métrica é calculada

O back-end de mídia define esse sinalizador na primeira vez que um evento de início de estado habilitado para legenda é recebido durante a sessão. A métrica é relatada na chamada de fechamento.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.states.closedcaptioning.set` quando o [[!UICONTROL Rastreamento do Estado do Player]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.states[]`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/media-reporting-details) entrada onde `name = "closedCaptioning"`, campo `isSet` |
| Feeds de dados | `event_list`, `post_event_list` (consulte a pesquisa de [`event.tsv`](https://experienceleague.adobe.com/pt-br/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.states.closedcaptioning.set` |
