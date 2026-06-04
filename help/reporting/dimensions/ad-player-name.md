---
title: Nome do player do anúncio
description: Relata qual player renderizou cada anúncio.
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '132'
ht-degree: 9%

---


# Nome do player do anúncio

>[!BEGINSHADEBOX]

*Esta página aborda a **Dimensão de relatório do**&#x200B;player do anúncio. Consulte [Nome do player do anúncio](/help/implementation/variables/ads/ad-player-name.md) para saber como coletar essa variável.*

>[!ENDSHADEBOX]

A dimensão **Nome do player de anúncio** informa qual player renderizou cada anúncio (por exemplo, `"Freewheel"`, `"Google IMA"`). O reprodutor de anúncios pode diferir do reprodutor de conteúdo principal quando os anúncios são compilados por um serviço de inserção de anúncios do lado do servidor.

## Como essa dimensão é preenchida

O nome do player do anúncio é definido pelo player em cada evento [início de anúncio](/help/implementation/events/ads/ad-start.md).

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.ad.playerName` quando o [[!UICONTROL Media Ads]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.playerName`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Feeds de dados | `videoadplayername`, `post_videoadplayername` |
| Audience Manager | `c_contextdata.a.media.ad.playerName` |

## Itens de dimensão

Cada item é o nome literal do player de anúncio reportado em [início do anúncio](/help/implementation/events/ads/ad-start.md).
