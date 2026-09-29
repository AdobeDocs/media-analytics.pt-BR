---
title: Nome do player do anúncio
description: Relata qual player renderizou cada anúncio.
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
source-wordcount: '134'
ht-degree: 10%
---

# Nome do player do anúncio

>[!BEGINSHADEBOX]

*Esta página aborda a **Dimensão de relatório do**player do anúncio. Consulte [Nome do player do anúncio](/help/implementation/variables/ads/ad-player-name.md) para saber como coletar essa variável.*

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
