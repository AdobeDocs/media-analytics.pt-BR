---
title: Eventos de buffer (dimensão)
description: Relata a contagem de eventos de buffer por sessão.
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
source-wordcount: '175'
ht-degree: 8%
---

# Eventos de buffer (dimensão)

>[!BEGINSHADEBOX]

*Esta página abrange a dimensão **Eventos de buffer**. O Adobe Analytics preenche automaticamente um par de [Eventos de buffer (métrica)](/help/reporting/metrics/buffer-events.md) da mesma variável de dados de contexto `a.media.qoe.bufferCount`. O Customer Journey Analytics expõe um único campo `xdm.mediaReporting.qoeDataDetails.bufferCount` que você pode usar como dimensão ou métrica.*

>[!ENDSHADEBOX]

A dimensão **Eventos de buffer** relata a contagem de eventos de buffer que ocorreram durante uma sessão. Use a dimensão para dividir o engajamento por contagem exata de buffer.

## Como essa dimensão é preenchida

O back-end de mídia incrementa a contagem toda vez que o player entra em um estado `buffer`. O valor é relatado na chamada de fechamento.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.qoe.bufferCount` quando a [[!UICONTROL Qualidade de Mídia]](/help/reporting/setup/analytics-reporting.md) está habilitada. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.bufferCount`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Feeds de dados | `videoqoebuffercountevar`, `post_videoqoebuffercountevar` |
| Audience Manager | `c_contextdata.a.media.qoe.bufferCount` |

## Itens de dimensão

Cada item é o valor literal de contagem de buffer relatado na chamada de fechamento. Para relatórios booleanos em nível de sessão (se a sessão passou por algum buffer), use [Fluxos afetados pelo buffer](/help/reporting/metrics/buffer-impacted-streams.md).
