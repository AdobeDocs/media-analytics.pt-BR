---
title: Público-alvo médio a cada minuto
description: Relata o número médio de visualizadores assistindo a qualquer minuto no tempo de execução do conteúdo.
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
source-wordcount: '173'
ht-degree: 12%
---

# Público-alvo médio a cada minuto

A métrica **Audiência média por minuto** informa o número médio de visualizadores assistindo a qualquer minuto, durante o tempo de execução do conteúdo. É a medida padrão &quot;AMA&quot; usada para comparar o alcance da mídia em conteúdo de diferentes tamanhos.

## Como essa métrica é calculada

O back-end de mídia calcula a Audiência média por minuto por sessão como `Content time spent / Content length`. Quando somado entre as sessões, o total representa o tamanho médio do público-alvo em cada minuto do conteúdo. A métrica é relatada na chamada de fechamento.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.averageMinuteAudience` quando [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.averageMinuteAudience`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feeds de dados | `event_list`, `post_event_list` (consulte a pesquisa de [`event.tsv`](https://experienceleague.adobe.com/pt-br/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.averageMinuteAudience` |

>[!IMPORTANT]
>
>A Audiência média por minuto requer um [Tamanho do conteúdo](/help/reporting/dimensions/content-length.md) diferente de zero. Se a duração do conteúdo for indefinida ou zero, essa métrica não será produzida para a sessão.
