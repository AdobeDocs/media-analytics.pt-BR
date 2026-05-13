---
title: Taxa média de bits (dimensão)
description: Informa a taxa média de bits de cada sessão em intervalos de 100 kbps.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '166'
ht-degree: 6%

---


# Taxa média de bits (dimensão)

>[!BEGINSHADEBOX]

*Esta página aborda a dimensão **Taxa média de bits**, que relata a taxa de bits classificada de cada sessão. Consulte [Taxa média de bits (métrica)](/help/reporting/metrics/average-bitrate.md) para obter a métrica média ponderada bruta. Consulte [Taxa de bits](/help/implementation/variables/quality/bitrate.md) para saber como coletar essa variável.*

>[!ENDSHADEBOX]

A dimensão **Taxa média de bits** informa a taxa média de bits de reprodução por sessão, classificada em intervalos de 100 kbps. O back-end calcula o valor como uma média ponderada de todos os valores de taxa de bits na sessão e o atribui a um intervalo. Use a dimensão para dividir o engajamento e a qualidade por nível de taxa de bits.

## Como essa dimensão é preenchida

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.qoe.bitrateAverageBucket` quando a [[!UICONTROL Qualidade de Mídia]](/help/reporting/media-reports-enable.md) está habilitada. |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.bitrateAverageBucket`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Feeds de dados | `videoqoebitrateaverageevar, post_videoqoebitrateaverageevar` |

## Itens de dimensão

Cada item é um rótulo de bloco de taxa de bits (por exemplo, `800-899`, `3200-3299`). Use a [Taxa média de bits (métrica)](/help/reporting/metrics/average-bitrate.md) para um valor médio ponderado bruto em vez de uma dimensão classificada.
