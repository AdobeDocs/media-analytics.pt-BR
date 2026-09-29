---
title: Quadros soltos (dimensão)
description: Informa a contagem cumulativa de quadros ignorados por sessão.
feature: Dimensions
role: User, Admin
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: b8734a57-d5fb-44a8-8ee1-65225cecaeae
    internal-label: Data configuration and collection
subfeature_v2:
  - id: b22bc0f7-b089-4966-95a1-31e7b3b69b79
    internal-label: Dimensions
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 7%
---

# Quadros soltos (dimensão)

>[!BEGINSHADEBOX]

*Esta página cobre a dimensão **Quadros soltos**. O Adobe Analytics preenche automaticamente um par de [Quadros ignorados (métrica)](/help/reporting/metrics/dropped-frames.md) da mesma variável de dados de contexto `a.media.qoe.droppedFrameCount`. O Customer Journey Analytics expõe um único campo `xdm.mediaReporting.qoeDataDetails.droppedFrames` que você pode usar como dimensão ou métrica. Consulte [Quadros soltos](/help/implementation/variables/quality/dropped-frames.md) para saber como coletar essa variável.*

>[!ENDSHADEBOX]

A dimensão **Quadros soltos** relata a contagem cumulativa de quadros soltos durante uma sessão. Use a dimensão para dividir o engajamento por contagem exata de quedas.

## Como essa dimensão é preenchida

O reprodutor atualiza o valor `droppedFrames` do objeto de QoE à medida que acumula quedas. O backend relata o valor mais recente na chamada de fechamento.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.qoe.droppedFrameCount` quando a [[!UICONTROL Qualidade de Mídia]](/help/reporting/setup/analytics-reporting.md) está habilitada. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.droppedFrames`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Feeds de dados | `videoqoedroppedframecountevar`, `post_videoqoedroppedframecountevar` |
| Audience Manager | `c_contextdata.a.media.qoe.droppedFrameCount` |

## Itens de dimensão

Cada item é o valor literal de contagem de queda relatado na chamada de fechamento. Para relatórios booleanos em nível de sessão (se algum quadro foi descartado), use [Fluxos afetados pelo quadro descartado](/help/reporting/metrics/dropped-frame-impacted-streams.md).
