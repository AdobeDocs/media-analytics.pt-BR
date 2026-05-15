---
title: Pod de anúncio
description: Informa cada ad break exclusivo, digitado por uma ID de pod gerada automaticamente.
feature: Dimensions
role: User, Admin
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 7%

---


# Pod de anúncio

A dimensão **Pod de anúncio** relata cada ad break exclusivo, digitado por uma ID de pod gerada automaticamente. Cada anúncio em uma sessão pertence a um pod de anúncio principal, e o pod agrupa vários anúncios reproduzidos simultaneamente. Use a dimensão para separar o envolvimento por ad break e como chave de junção para as classificações [Nome do pod](pod-name.md) e [Posição do pod](pod-position.md).

## Como essa dimensão é preenchida

A ID do pod de anúncio é gerada automaticamente pela SDK quando um evento [ad break start](/help/implementation/events/ads/ad-break-start.md) é acionado. As implementações de API direta o constroem a partir do índice de quebra e da hora de início ou fornecem uma ID de pod personalizada.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.ad.pod` quando o [[!UICONTROL Media Ads]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.advertisingPodDetails.ID`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-pod-details-reporting) |
| Feeds de dados | `videoadpod`, `post_videoadpod` |
| Audience Manager | N/D |

## Itens de dimensão

Cada item é uma ID de pod de anúncio exclusiva. A ID é opaca (geralmente um hash de ID de sessão, ID de conteúdo e índice de interrupção) e é mais útil como uma chave de agrupamento quando combinada com [Nome do pod](pod-name.md) para o rótulo amigável.
