---
title: Métricas calculadas
description: Métricas calculadas personalizadas para relatórios de mídia de transmissão no Adobe Analytics e no Customer Journey Analytics.
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
source-wordcount: '269'
ht-degree: 4%
---
# Métricas calculadas de streaming de mídia

As métricas calculadas para os serviços de streaming de mídia da Adobe são métricas personalizadas criadas a partir das métricas de streaming de mídia padrão, que permitem obter taxas como tempo médio de anúncio gasto ou taxa de conclusão de mídia sem alterar a implementação.

Para criar essas métricas calculadas no Analysis Workspace, consulte a respectiva visão geral em [Adobe Analytics](https://experienceleague.adobe.com/en/docs/analytics/components/calculated-metrics/cm-overview) ou [Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-components/cja-calcmetrics/calc-metr-overview).

| Métrica calculada | Descrição | Fórmula |
| --- | --- | --- |
| Média anúncios por fluxo de mídia | [[!UICONTROL Início do anúncio]](/help/reporting/metrics/ad-starts.md) por [[!UICONTROL Início da mídia]](/help/reporting/metrics/media-starts.md) | `[Ad starts] / [Media starts]` |
| Média capítulos por fluxo de mídia | [[!UICONTROL Início do capítulo]](/help/reporting/metrics/chapter-starts.md) por [[!UICONTROL Início da mídia]](/help/reporting/metrics/media-starts.md) | `[Chapter starts] / [Media starts]` |
| Média tempo gasto com a mídia | [[!UICONTROL Tempo gasto com a mídia]](/help/reporting/metrics/media-time-spent.md) por [[!UICONTROL Inícios da mídia]](/help/reporting/metrics/media-starts.md) (`HH:MM:SS`) | `[Media time spent] / [Media starts]` |
| Média tempo gasto com o conteúdo | [[!UICONTROL Tempo gasto do conteúdo]](/help/reporting/metrics/content-time-spent.md) por [[!UICONTROL Inícios do conteúdo]](/help/reporting/metrics/content-starts.md) (`HH:MM:SS`) | `[Content time spent] / [Content starts]` |
| Média tempo gasto com o anúncio | [[!UICONTROL Tempo gasto com anúncio]](/help/reporting/metrics/ad-time-spent.md) por [[!UICONTROL Início do anúncio]](/help/reporting/metrics/ad-starts.md) (`HH:MM:SS`) | `[Ad time spent] / [Ad starts]` |
| Média tempo gasto com capítulo | [[!UICONTROL Tempo gasto com capítulo]](/help/reporting/metrics/chapter-time-spent.md) por [[!UICONTROL Inícios de capítulo]](/help/reporting/metrics/chapter-starts.md) (`HH:MM:SS`) | `[Chapter time spent] / [Chapter starts]` |
| Taxa de conclusão da mídia | Taxa de [[!UICONTROL Conclusões de conteúdo]](/help/reporting/metrics/content-completes.md) vs. [[!UICONTROL Inícios da mídia]](/help/reporting/metrics/media-starts.md) | `[Content completes] / [Media starts]` |
| Taxa de conclusão do conteúdo | Taxa de [[!UICONTROL Conclusões de conteúdo]](/help/reporting/metrics/content-completes.md) vs. [[!UICONTROL Inícios de conteúdo]](/help/reporting/metrics/content-starts.md) | `[Content completes] / [Content starts]` |
| Taxa de conclusão do anúncio | Taxa de [[!UICONTROL Anúncio concluído]](/help/reporting/metrics/ad-completes.md) vs. [[!UICONTROL Anúncio iniciado]](/help/reporting/metrics/ad-starts.md) | `[Ad completes] / [Ad starts]` |
| Taxa de conclusão do capítulo | Taxa de [[!UICONTROL Conclusões de capítulo]](/help/reporting/metrics/chapter-completes.md) vs. [[!UICONTROL Inícios de capítulo]](/help/reporting/metrics/chapter-starts.md) | `[Chapter completes] / [Chapter starts]` |
| Soltar antes da taxa inicial | Taxa de [[!UICONTROL Desistências antes do início]](/help/reporting/metrics/drops-before-start.md) vs. [[!UICONTROL Início da mídia]](/help/reporting/metrics/media-starts.md) | `[Drops before start] / [Media starts]` |
| Taxa de duração da pausa do conteúdo | Taxa de [[!UICONTROL Duração total da pausa]](/help/reporting/metrics/total-pause-duration.md) vs. [[!UICONTROL Tempo gasto com conteúdo]](/help/reporting/metrics/content-time-spent.md) | `[Total pause duration] / [Content time spent]` |
| Taxa de duração do buffer de conteúdo | Taxa de [[!UICONTROL Duração total do buffer]](/help/reporting/metrics/total-buffer-duration.md) vs. [[!UICONTROL Tempo gasto com o conteúdo]](/help/reporting/metrics/content-time-spent.md) | `[Total buffer duration] / [Content time spent]` |
| Taxa de tempo para início do conteúdo | Taxa de [[!UICONTROL Tempo para iniciar]](/help/reporting/metrics/time-to-start.md) vs. [[!UICONTROL Tempo gasto com o conteúdo]](/help/reporting/metrics/content-time-spent.md) | `[Time to start] / [Content time spent]` |
| Taxa de tempo gasto com anúncio | Taxa de [[!UICONTROL Tempo gasto com anúncio]](/help/reporting/metrics/ad-time-spent.md) vs. [[!UICONTROL Tempo gasto com conteúdo]](/help/reporting/metrics/content-time-spent.md) | `[Ad time spent] / [Content time spent]` |

