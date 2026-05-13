---
title: IDs de erro do Player SDK
description: Relata identificadores de erro exclusivos gerados pelo SDK do reprodutor de conteúdo.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 6%

---


# IDs de erro do Player SDK

A dimensão **IDs de erro do Player SDK** relata identificadores de erro exclusivos gerados pelo SDK do player de conteúdo durante uma sessão. O reprodutor deve fornecer os códigos ou IDs no momento da implementação por meio da API de rastreamento de erros. Há suporte para diversas IDs de erro por sessão.

## Como essa dimensão é preenchida

O reprodutor passa IDs de erro de SDK do reprodutor para o rastreador em `media.error` eventos. O back-end coleta IDs exclusivas na sessão e as relata na chamada de fechamento.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.qoe.playerSdkErrors` quando a [[!UICONTROL Qualidade de Mídia]](/help/reporting/media-reports-enable.md) está habilitada. |
| Customer Journey Analytics | [`mediaReporting.qoeDataDetails.playerSdkErrors`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Feeds de dados | `videoqoeplayersdkerrors, post_videoqoeplayersdkerrors` |

## Itens de dimensão

Cada item é um código de erro ou uma ID gerada pelo SDK do reprodutor. Use uma taxonomia estável em todas as implementações para que as IDs de erro sejam acumuladas corretamente nas sessões.
