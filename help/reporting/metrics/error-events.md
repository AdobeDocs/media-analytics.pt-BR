---
title: Eventos de erro
description: Conta eventos de erro para somas e médias entre sessões.
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
source-wordcount: '184'
ht-degree: 8%
---

# Eventos de erro

>[!BEGINSHADEBOX]

*Esta página abrange a métrica **Eventos de erro**. O Adobe Analytics preenche automaticamente uma [dimensão de erros](/help/reporting/dimensions/errors.md) emparelhada a partir da mesma variável de dados de contexto `a.media.qoe.errorCount`. O Customer Journey Analytics expõe um único campo `xdm.mediaReporting.qoeDataDetails.errorCount` que você pode usar como dimensão ou métrica.*

>[!ENDSHADEBOX]

A métrica **Eventos de erro** conta eventos de erro em todas as sessões, adequados para somas, médias e acúmulos de percentil. Use a métrica para calcular o volume total de erros em um período de relatório e comparar as taxas de erro entre o conteúdo, as redes ou os players.

## Como essa métrica é calculada

O back-end de mídia incrementa a contagem em cada erro relatado pelo reprodutor. A métrica é relatada na chamada de fechamento.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.qoe.errorCount` quando a [[!UICONTROL Qualidade de Mídia]](/help/reporting/setup/analytics-reporting.md) está habilitada. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.errorCount`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Feeds de dados | `event_list`, `post_event_list` (consulte a pesquisa de [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.qoe.errorCount` |

Para relatórios booleanos em nível de sessão (se algum erro ocorreu), use [Fluxos afetados por erros](error-impacted-streams.md).
