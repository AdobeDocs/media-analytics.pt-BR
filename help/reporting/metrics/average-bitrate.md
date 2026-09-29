---
title: Taxa média de bits (métrica)
description: Informa a taxa de bits média ponderada bruta de cada sessão, em kbps.
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
source-wordcount: '175'
ht-degree: 8%
---

# Taxa média de bits (métrica)

>[!BEGINSHADEBOX]

*Esta página aborda a métrica de evento **Taxa média de bits**, que relata a taxa de bits média ponderada bruta por sessão. Consulte [Taxa média de bits (dimensão)](/help/reporting/dimensions/average-bitrate.md) para a dimensão classificada. Consulte [Taxa de bits](/help/implementation/variables/quality/bitrate.md) para saber como coletar essa variável.*

>[!ENDSHADEBOX]

A métrica **Taxa de bits média** informa a taxa de bits média ponderada bruta de reprodução, em kbps, para cada sessão. Ao contrário da [dimensão segmentada](/help/reporting/dimensions/average-bitrate.md), a métrica é um valor numérico contínuo adequado para somas, médias e rollups de percentil entre sessões.

## Como essa métrica é calculada

O back-end de mídia calcula uma média ponderada de todos os valores de taxa de bits relatados durante a sessão, ponderada pela duração em que cada taxa de bits estava ativa. A métrica é relatada na chamada de fechamento.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.qoe.bitrateAverage` quando a [[!UICONTROL Qualidade de Mídia]](/help/reporting/setup/analytics-reporting.md) está habilitada. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.bitrateAverage`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Feeds de dados | `event_list`, `post_event_list` (consulte a pesquisa de [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.qoe.bitrateAverage` |
