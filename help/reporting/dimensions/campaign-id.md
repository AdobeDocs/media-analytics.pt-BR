---
title: ID da campanha
description: Relata a campanha à qual cada anúncio pertence.
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
source-wordcount: '122'
ht-degree: 14%
---

# ID da campanha

>[!BEGINSHADEBOX]

*Esta página aborda a **ID da campanha**dimensão de relatório. Consulte [ID da campanha](/help/implementation/variables/ads/campaign-id.md) para saber como coletar essa variável.*

>[!ENDSHADEBOX]

A dimensão **ID da campanha** informa a campanha publicitária à qual cada criativo de anúncio pertence. Use a dimensão para acumular engajamento em várias criações que compartilham uma campanha.

## Como essa dimensão é preenchida

A ID da campanha é definida pelo reprodutor em cada evento [ad start](/help/implementation/events/ads/ad-start.md).

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.ad.campaign` quando o [[!UICONTROL Media Ads]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.campaignID`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Feeds de dados | `videocampaign`, `post_videocampaign` |
| Audience Manager | `c_contextdata.a.media.ad.campaign` |

## Itens de dimensão

Cada item é o valor literal da campanha reportado em [início do anúncio](/help/implementation/events/ads/ad-start.md).
