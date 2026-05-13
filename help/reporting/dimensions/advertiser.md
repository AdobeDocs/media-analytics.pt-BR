---
title: Anunciante
description: Informa a empresa ou marca em destaque em cada anúncio.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '109'
ht-degree: 11%

---


# Anunciante

>[!BEGINSHADEBOX]

*Esta página abrange a dimensão de relatório **Anunciante**. Consulte [Anunciante](/help/implementation/variables/ads/advertiser.md) para saber como coletar essa variável.*

>[!ENDSHADEBOX]

A dimensão **Anunciante** informa a empresa ou marca em destaque em cada anúncio (por exemplo, `"Ford"` ou `"Coca-Cola"`). Use a dimensão para romper o engajamento e a conclusão pelo anunciante.

## Como essa dimensão é preenchida

O anunciante é definido pelo reprodutor em cada evento `media.adStart`.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.ad.advertiser` quando o [[!UICONTROL Media Ads]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.advertiser`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Feeds de dados | `videoadvertiser, post_videoadvertiser` |

## Itens de dimensão

Cada item é o nome literal do anunciante relatado em `media.adStart`.
