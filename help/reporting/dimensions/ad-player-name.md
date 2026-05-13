---
title: Nome do player do anúncio
description: Relata qual player renderizou cada anúncio.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 7%

---


# Nome do player do anúncio

>[!BEGINSHADEBOX]

*Esta página aborda a **Dimensão de relatório do**player do anúncio. Consulte [Nome do player do anúncio](/help/implementation/variables/ads/ad-player-name.md) para saber como coletar essa variável.*

>[!ENDSHADEBOX]

A dimensão **Nome do player de anúncio** informa qual player renderizou cada anúncio (por exemplo, `"Freewheel"`, `"Google IMA"`). O reprodutor de anúncios pode diferir do reprodutor de conteúdo principal quando os anúncios são compilados por um serviço de inserção de anúncios do lado do servidor.

## Como essa dimensão é preenchida

O nome do player do anúncio é definido pelo player em cada evento `media.adStart`.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.ad.playerName` quando o [[!UICONTROL Media Ads]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.playerName`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Feeds de dados | `videoadplayername, post_videoadplayername` |

## Itens de dimensão

Cada item é o nome literal do player de anúncio reportado em `media.adStart`.
