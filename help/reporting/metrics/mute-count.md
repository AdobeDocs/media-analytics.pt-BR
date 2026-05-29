---
title: Contagens da função Mudo
description: Informa o número de vezes que o visualizador silenciou o áudio durante uma sessão.
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '158'
ht-degree: 9%

---


# Contagens da função Mudo

>[!BEGINSHADEBOX]

*Esta página aborda a métrica de relatório **Contagens da função Mudo**. Consulte [Mudo](/help/implementation/variables/player-state/mute.md) para saber como coletar essa variável.*

>[!ENDSHADEBOX]

A métrica **Contagens da função Mudo** informa o número de vezes que o visualizador ativou o áudio durante uma sessão. Cada evento de início de estado da função Mudo incrementa a contagem. Emparelhe com [Fluxos afetados pela função mudo](mute-streams-impacted.md) para rollups booleanos em nível de sessão e com [Duração total da função mudo](mute-total-duration.md) para obter o tempo total no estado.

## Como essa métrica é calculada

O back-end de mídia incrementa essa contagem em cada evento de início de estado de mudo. A métrica é relatada na chamada de fechamento.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.states.mute.count` quando o [[!UICONTROL Rastreamento do Estado do Player]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.states[]`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/media-reporting-details) entrada onde `name = "mute"`, campo `count` |
| Feeds de dados | `event_list`, `post_event_list` (consulte a pesquisa de [`event.tsv`](https://experienceleague.adobe.com/pt-br/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.states.mute.count` |
