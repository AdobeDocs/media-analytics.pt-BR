---
title: IDs de erro do Player SDK
description: Relata identificadores de erro exclusivos gerados pelo SDK do reprodutor de conteúdo.
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
source-wordcount: '159'
ht-degree: 8%
---

# IDs de erro do Player SDK

A dimensão **IDs de erro do Player SDK** relata identificadores de erro exclusivos gerados pelo SDK do player de conteúdo durante uma sessão. O reprodutor deve fornecer os códigos ou IDs no momento da implementação por meio da API de rastreamento de erros. Há suporte para diversas IDs de erro por sessão.

## Como essa dimensão é preenchida

O reprodutor passa IDs de erro de SDK do reprodutor para o rastreador em eventos de [erro](/help/implementation/events/error.md). O back-end coleta IDs exclusivas na sessão e as relata na chamada de fechamento.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.qoe.playerSdkErrors` quando a [[!UICONTROL Qualidade de Mídia]](/help/reporting/setup/analytics-reporting.md) está habilitada. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.playerSdkErrors`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Feeds de dados | `videoqoeplayersdkerrors`, `post_videoqoeplayersdkerrors` |
| Audience Manager | `c_contextdata.a.media.qoe.playerSdkErrors` |

## Itens de dimensão

Cada item é um código de erro ou uma ID gerada pelo SDK do reprodutor. Use uma taxonomia estável em todas as implementações para que as IDs de erro sejam acumuladas corretamente nas sessões.
