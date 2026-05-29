---
title: IDs de erro externo
description: Relata identificadores de erro exclusivos de fontes externas, como erros de CDN.
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '155'
ht-degree: 7%

---


# IDs de erro externo

A dimensão **IDs de erro externo** relata identificadores de erro exclusivos de qualquer origem fora do SDK do player (por exemplo, erros de CDN). O reprodutor deve fornecer os códigos ou IDs no momento da implementação por meio da API de rastreamento de erros. Há suporte para diversas IDs de erro por sessão.

## Como essa dimensão é preenchida

O reprodutor passa IDs de erro externo para o rastreador em eventos [error](/help/implementation/events/error.md). O back-end coleta IDs exclusivas na sessão e as relata na chamada de fechamento.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.qoe.externalErrors` quando a [[!UICONTROL Qualidade de Mídia]](/help/reporting/media-reports-enable.md) está habilitada. |
| Customer Journey Analytics | [`xdm.mediaReporting.qoeDataDetails.externalErrors`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/qoe-data-details-reporting) |
| Feeds de dados | `videoqoeextneralerrors` |
| Audience Manager | `c_contextdata.a.media.qoe.externalErrors` |

## Itens de dimensão

Cada item é um código de erro ou uma ID fornecida pelo reprodutor. Use uma taxonomia estável em todas as implementações para que as IDs de erro sejam acumuladas corretamente nas sessões.
