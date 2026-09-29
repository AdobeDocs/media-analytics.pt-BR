---
title: Alterações na taxa de bits (métrica)
description: Conta eventos de alteração de taxa de bits para somas e médias entre sessões.
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
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.bitrateChangeCount`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Feeds de dados | `event_list`, `post_event_list` (consulte a pesquisa de [`event.tsv`](https://experienceleague.adobe.com/pt-br/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.qoe.bitrateChangeCount` |

Para relatórios booleanos em nível de sessão (se a sessão sofreu alguma alteração na taxa de bits), use [Fluxos afetados pela alteração na taxa de bits](bitrate-change-impacted-streams.md).
