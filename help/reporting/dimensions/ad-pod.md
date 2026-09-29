---
title: Pod de anúncio
description: Informa cada ad break exclusivo, digitado por uma ID de pod gerada automaticamente.
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
source-wordcount: '197'
ht-degree: 8%
---

# Pod de anúncio

A dimensão **Pod de anúncio** relata cada ad break exclusivo, digitado por uma ID de pod gerada automaticamente. Cada anúncio em uma sessão pertence a um pod de anúncio principal, e o pod agrupa vários anúncios reproduzidos simultaneamente. Use a dimensão para separar o envolvimento por ad break e como chave de junção para as classificações [Nome do pod](pod-name.md) e [Posição do pod](pod-position.md).

## Como essa dimensão é preenchida

A ID do pod de anúncio é gerada automaticamente pela SDK quando um evento [ad break start](/help/implementation/events/ads/ad-break-start.md) é acionado. As implementações de API direta o constroem a partir do índice de quebra e da hora de início ou fornecem uma ID de pod personalizada.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.ad.pod` quando o [[!UICONTROL Media Ads]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingPodDetails.ID`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-pod-details-reporting) |
| Feeds de dados | `videoadpod`, `post_videoadpod` |
| Audience Manager | N/D |

## Itens de dimensão

Cada item é uma ID de pod de anúncio exclusiva. A ID é opaca (geralmente um hash de ID de sessão, ID de conteúdo e índice de interrupção) e é mais útil como uma chave de agrupamento quando combinada com [Nome do pod](pod-name.md) para o rótulo amigável.
