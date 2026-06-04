---
title: ID da campanha
description: Relata a campanha à qual cada anúncio pertence.
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '120'
ht-degree: 13%

---


# ID da campanha

>[!BEGINSHADEBOX]

*Esta página aborda a **ID da campanha**&#x200B;dimensão de relatório. Consulte [ID da campanha](/help/implementation/variables/ads/campaign-id.md) para saber como coletar essa variável.*

>[!ENDSHADEBOX]

A dimensão **ID da campanha** informa a campanha publicitária à qual cada criativo de anúncio pertence. Use a dimensão para acumular engajamento em várias criações que compartilham uma campanha.

## Como essa dimensão é preenchida

A ID da campanha é definida pelo reprodutor em cada evento [ad start](/help/implementation/events/ads/ad-start.md).

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.ad.campaign` quando o [[!UICONTROL Media Ads]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.campaignID`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Feeds de dados | `videocampaign`, `post_videocampaign` |
| Audience Manager | `c_contextdata.a.media.ad.campaign` |

## Itens de dimensão

Cada item é o valor literal da campanha reportado em [início do anúncio](/help/implementation/events/ads/ad-start.md).
