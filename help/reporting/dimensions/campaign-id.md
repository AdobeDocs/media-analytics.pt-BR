---
title: ID da campanha
description: Relata a campanha à qual cada anúncio pertence.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 12%

---


# ID da campanha

>[!BEGINSHADEBOX]

*Esta página aborda a **ID da campanha**dimensão de relatório. Consulte [ID da campanha](/help/implementation/variables/ads/campaign-id.md) para saber como coletar essa variável.*

>[!ENDSHADEBOX]

A dimensão **ID da campanha** informa a campanha publicitária à qual cada criativo de anúncio pertence. Use a dimensão para acumular engajamento em várias criações que compartilham uma campanha.

## Como essa dimensão é preenchida

A ID da campanha é definida pelo reprodutor em cada evento `media.adStart`.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.ad.campaign` quando o [[!UICONTROL Media Ads]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.campaignID`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Feeds de dados | `videocampaign, post_videocampaign` |

## Itens de dimensão

Cada item é o valor literal da campanha reportado em `media.adStart`.
