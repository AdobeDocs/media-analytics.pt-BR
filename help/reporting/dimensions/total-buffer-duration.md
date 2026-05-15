---
title: Duração total do buffer (dimensão)
description: Relata os segundos cumulativos gastos no buffering por sessão.
feature: Dimensions
role: User, Admin
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 6%

---


# Duração total do buffer (dimensão)

>[!BEGINSHADEBOX]

*Esta página cobre a dimensão **Duração total do buffer**. O Adobe Analytics preenche automaticamente um par de [Duração total do buffer (métrica)](/help/reporting/metrics/total-buffer-duration.md) com a mesma variável de dados de contexto `a.media.qoe.bufferTime`. O Customer Journey Analytics expõe um único campo `mediaReporting.qoeDataDetails.bufferTime` que você pode usar como dimensão ou métrica.*

>[!ENDSHADEBOX]

A dimensão **Duração total do buffer** informa o tempo cumulativo, em segundos, que o player gastou em um estado de buffer durante uma sessão. Use a dimensão para separar o engajamento pelo valor exato da duração do buffer.

## Como essa dimensão é preenchida

O back-end de mídia soma a duração de cada intervalo de buffer (do [início do buffer](/help/implementation/events/playback/buffer-start.md) até a próxima alteração de estado). O valor é relatado na chamada de fechamento. O Analysis Workspace mostra o valor como `HH:MM:SS`; Feeds de dados, Data Warehouse e APIs de relatórios mostram o valor em segundos.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.qoe.bufferTime` quando a [[!UICONTROL Qualidade de Mídia]](/help/reporting/media-reports-enable.md) está habilitada. |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.bufferTime`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Feeds de dados | `videoqoebuffertimeevar`, `post_videoqoebuffertimeevar` |
| Audience Manager | `c_contextdata.a.media.qoe.bufferTime` |

## Itens de dimensão

Cada item é o valor de duração literal, em segundos, relatado na chamada de fechamento.
