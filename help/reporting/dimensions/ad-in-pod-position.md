---
title: Posição do anúncio no pod
description: Relata a posição com índice zero de cada anúncio dentro do ad break principal.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 6%

---


# Posição do anúncio no pod

>[!BEGINSHADEBOX]

*Esta página aborda a **Dimensão de relatório Anúncio na posição pod**. Consulte [Posição do anúncio no pod](/help/implementation/variables/ads/ad-in-pod-position.md) para saber como coletar essa variável.*

>[!ENDSHADEBOX]

A dimensão **Ad in pod position** relata a posição de índice zero de cada anúncio dentro de seu ad break principal. O primeiro anúncio em um pod é `0`, o segundo é `1` e assim por diante. Use a dimensão para comparar o envolvimento e a conclusão por posição em um ad break.

## Como essa dimensão é preenchida

A posição do anúncio no pod é definida pelo reprodutor em cada evento `media.adStart`.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.ad.podPosition` quando o [[!UICONTROL Media Ads]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.podPosition`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Feeds de dados | `videoadinpod, post_videoadinpod` |

## Itens de dimensão

Cada item é o valor de posição inteiro (`0`, `1`, `2`, ...) reportado em `media.adStart`.
