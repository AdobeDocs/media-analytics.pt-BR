---
title: Duração total do buffer (dimensão)
description: Relata os segundos cumulativos gastos no buffering por sessão.
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
source-wordcount: '194'
ht-degree: 7%
---

# Duração total do buffer (dimensão)

>[!BEGINSHADEBOX]

*Esta página cobre a dimensão **Duração total do buffer**. O Adobe Analytics preenche automaticamente um par de [Duração total do buffer (métrica)](/help/reporting/metrics/total-buffer-duration.md) com a mesma variável de dados de contexto `a.media.qoe.bufferTime`. O Customer Journey Analytics expõe um único campo `xdm.mediaReporting.qoeDataDetails.bufferTime` que você pode usar como dimensão ou métrica.*

>[!ENDSHADEBOX]

A dimensão **Duração total do buffer** informa o tempo cumulativo, em segundos, que o player gastou em um estado de buffer durante uma sessão. Use a dimensão para separar o engajamento pelo valor exato da duração do buffer.

## Como essa dimensão é preenchida

O back-end de mídia soma a duração de cada intervalo de buffer (do [início do buffer](/help/implementation/events/playback/buffer-start.md) até a próxima alteração de estado). O valor é relatado na chamada de fechamento. O Analysis Workspace mostra o valor como `HH:MM:SS`; Feeds de dados, Data Warehouse e APIs de relatórios mostram o valor em segundos.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.qoe.bufferTime` quando a [[!UICONTROL Qualidade de Mídia]](/help/reporting/setup/analytics-reporting.md) está habilitada. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.bufferTime`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Feeds de dados | `videoqoebuffertimeevar`, `post_videoqoebuffertimeevar` |
| Audience Manager | `c_contextdata.a.media.qoe.bufferTime` |

## Itens de dimensão

Cada item é o valor de duração literal, em segundos, relatado na chamada de fechamento.
