---
title: Quadros soltos (métrica)
description: Relata os quadros ignorados cumulativos para somas e médias entre sessões.
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 7%

---


# Quadros soltos (métrica)

>[!BEGINSHADEBOX]

*Esta página cobre a métrica **Quadros soltos**. O Adobe Analytics preenche automaticamente um par de [Quadros ignorados (dimensão)](/help/reporting/dimensions/dropped-frames.md) da mesma variável de dados de contexto `a.media.qoe.droppedFrameCount`. O Customer Journey Analytics expõe um único campo `xdm.mediaReporting.qoeDataDetails.droppedFrames` que você pode usar como dimensão ou métrica. Consulte [Quadros soltos](/help/implementation/variables/quality/dropped-frames.md) para saber como coletar essa variável.*

>[!ENDSHADEBOX]

A métrica **Quadros soltos** relata os quadros soltos cumulativos nas sessões, adequados para somas, médias e acúmulos de percentil. Use a métrica para calcular o volume total de quedas em um período de relatório e comparar a qualidade de renderização de quadros entre o conteúdo, as redes ou os players.

## Como essa métrica é calculada

O reprodutor atualiza o valor `droppedFrames` do objeto de QoE à medida que as quedas se acumulam. O backend relata o valor mais recente na chamada de fechamento.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.qoe.droppedFrameCount` quando a [[!UICONTROL Qualidade de Mídia]](/help/reporting/media-reports-enable.md) está habilitada. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.droppedFrames`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Feeds de dados | `event_list`, `post_event_list` (consulte a pesquisa de [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.qoe.droppedFrameCount` |

Para relatórios booleanos em nível de sessão (se algum quadro foi descartado), use [Fluxos afetados pelo quadro descartado](dropped-frame-impacted-streams.md).
