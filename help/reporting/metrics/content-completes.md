---
title: Conteúdo completo
description: Conta as sessões cujo indicador de reprodução atingiu o fim do conteúdo.
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
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
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.complete` quando [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.isCompleted`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feeds de dados | `event_list`, `post_event_list` (consulte a pesquisa de [`event.tsv`](https://experienceleague.adobe.com/pt-br/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.complete` |
