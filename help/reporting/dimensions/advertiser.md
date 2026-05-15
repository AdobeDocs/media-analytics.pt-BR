---
title: Anunciante
description: Informa a empresa ou marca em destaque em cada anúncio.
feature: Dimensions
role: User, Admin
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 12%

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
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.ad.advertiser` quando o [[!UICONTROL Media Ads]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.advertiser`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Feeds de dados | `videoadvertiser`, `post_videoadvertiser` |
| Audience Manager | `c_contextdata.a.media.ad.advertiser` |

## Itens de dimensão

Cada item é o nome literal do anunciante relatado em [início do anúncio](/help/implementation/events/ads/ad-start.md).
