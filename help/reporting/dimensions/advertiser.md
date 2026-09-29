---
title: Anunciante
description: Informa a empresa ou marca em destaque em cada anúncio.
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
source-wordcount: '117'
ht-degree: 13%
---

# Anunciante

>[!BEGINSHADEBOX]

*Esta página abrange a dimensão de relatório **Anunciante**. Consulte [Anunciante](/help/implementation/variables/ads/advertiser.md) para saber como coletar essa variável.*

>[!ENDSHADEBOX]

A dimensão **Anunciante** informa a empresa ou marca em destaque em cada anúncio (por exemplo, `"Ford"` ou `"Coca-Cola"`). Use a dimensão para romper o engajamento e a conclusão pelo anunciante.

## Como essa dimensão é preenchida

O anunciante é definido pelo reprodutor em cada evento [ad start](/help/implementation/events/ads/ad-start.md).

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.ad.advertiser` quando o [[!UICONTROL Media Ads]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.advertiser`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Feeds de dados | `videoadvertiser`, `post_videoadvertiser` |
| Audience Manager | `c_contextdata.a.media.ad.advertiser` |

## Itens de dimensão

Cada item é o nome literal do anunciante relatado em [início do anúncio](/help/implementation/events/ads/ad-start.md).
