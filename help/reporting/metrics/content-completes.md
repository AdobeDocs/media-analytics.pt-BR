---
title: Conteúdo completo
description: Conta as sessões cujo indicador de reprodução atingiu o fim do conteúdo.
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
source-wordcount: '142'
ht-degree: 10%
---

# Conteúdo completo

A métrica **Conteúdo concluído** conta as sessões cujo indicador de reprodução atingiu o fim do conteúdo. Emparelhe-o com [Início do conteúdo](content-starts.md) para calcular a taxa de conclusão; emparelhe com [Início da mídia](media-starts.md) para calcular a taxa de exibição de ponta a ponta.

## Como essa métrica é calculada

O back-end de mídia define esse sinalizador quando um evento [sessão concluída](/help/implementation/events/session/session-complete.md) é recebido. A métrica é relatada na chamada de fechamento. Uma sessão que atinge o tempo limite sem um `sessionComplete` explícito não conta como uma conclusão.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.complete` quando [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.isCompleted`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feeds de dados | `event_list`, `post_event_list` (consulte a pesquisa de [`event.tsv`](https://experienceleague.adobe.com/pt-br/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.complete` |
