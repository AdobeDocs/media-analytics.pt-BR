---
title: Posição do anúncio no pod
description: Relata a posição com índice zero de cada anúncio dentro do ad break principal.
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 7%

---


# Posição do anúncio no pod

>[!BEGINSHADEBOX]

*Esta página aborda a **Dimensão de relatório Anúncio na posição pod**. Consulte [Posição do anúncio no pod](/help/implementation/variables/ads/ad-in-pod-position.md) para saber como coletar essa variável.*

>[!ENDSHADEBOX]

A dimensão **Ad in pod position** relata a posição de índice zero de cada anúncio dentro de seu ad break principal. O primeiro anúncio em um pod é `0`, o segundo é `1` e assim por diante. Use a dimensão para comparar o envolvimento e a conclusão por posição em um ad break.

## Como essa dimensão é preenchida

A posição do anúncio no pod é definida pelo reprodutor a cada evento [início de anúncio](/help/implementation/events/ads/ad-start.md).

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.ad.podPosition` quando o [[!UICONTROL Media Ads]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.podPosition`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Feeds de dados | `videoadinpod`, `post_videoadinpod` |
| Audience Manager | `c_contextdata.a.media.ad.podPosition` |

## Itens de dimensão

Cada item é o valor de posição inteiro (`0`, `1`, `2`, ...) relatado em [início do anúncio](/help/implementation/events/ads/ad-start.md).
