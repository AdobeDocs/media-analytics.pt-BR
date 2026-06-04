---
title: Alterações na taxa de bits (métrica)
description: Conta eventos de alteração de taxa de bits para somas e médias entre sessões.
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 7%

---


# Alterações na taxa de bits (métrica)

>[!BEGINSHADEBOX]

*Esta página aborda a métrica **Alterações na taxa de bits**. O Adobe Analytics preenche automaticamente um par de [alterações na taxa de bits (dimensão)](/help/reporting/dimensions/bitrate-changes.md) da mesma variável de dados de contexto `a.media.qoe.bitrateChangeCount`. O Customer Journey Analytics expõe um único campo `xdm.mediaReporting.qoeDataDetails.bitrateChangeCount` que você pode usar como dimensão ou métrica. Consulte [Alteração na taxa de bits](/help/implementation/variables/quality/bitrate-change.md) para saber como acionar eventos de alteração na taxa de bits.*

>[!ENDSHADEBOX]

A métrica **Alterações na taxa de bits** conta eventos de alteração na taxa de bits entre sessões, adequados para somas, médias e acúmulos de percentil. Use a métrica para calcular o volume total de alterações da taxa de bits em um período do relatório e comparar a estabilidade da taxa de bits em conteúdo, redes ou players.

## Como essa métrica é calculada

O back-end de mídia incrementa a contagem em cada evento de [alteração de taxa de bits](/help/implementation/events/playback/bitrate-change.md) recebido durante a sessão. A métrica é relatada na chamada de fechamento.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.qoe.bitrateChangeCount` quando a [[!UICONTROL Qualidade de Mídia]](/help/reporting/setup/analytics-reporting.md) está habilitada. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.bitrateChangeCount`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Feeds de dados | `event_list`, `post_event_list` (consulte a pesquisa de [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.qoe.bitrateChangeCount` |

Para relatórios booleanos em nível de sessão (se a sessão sofreu alguma alteração na taxa de bits), use [Fluxos afetados pela alteração na taxa de bits](bitrate-change-impacted-streams.md).
