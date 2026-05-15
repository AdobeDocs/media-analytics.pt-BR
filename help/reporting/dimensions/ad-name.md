---
title: Nome do anúncio
description: Informa o título legível de cada anúncio.
feature: Dimensions
role: User, Admin
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 6%

---


# Nome do anúncio

>[!BEGINSHADEBOX]

*Esta página abrange a dimensão de relatório **Nome do anúncio**. Consulte [Nome do anúncio](/help/implementation/variables/ads/ad-name.md) para saber como coletar essa variável.*

>[!ENDSHADEBOX]

A dimensão **Nome do anúncio** informa o título legível de cada anúncio.

## Como essa dimensão é preenchida

O nome do anúncio é definido pelo reprodutor em cada evento [início de anúncio](/help/implementation/events/ads/ad-start.md).

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.ad.friendlyName` quando o [[!UICONTROL Media Ads]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.friendlyName`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Feeds de dados | `videoadname`, `post_videoadname` |
| Audience Manager | `c_contextdata.a.media.ad.friendlyName` |

No Adobe Analytics, essa dimensão aparece de duas maneiras: como **Nome do anúncio (variável)** (coletado diretamente de `a.media.ad.friendlyName`) e como **Nome do anúncio** (uma classificação derivada da dimensão [Anúncio](ad.md)). Se você usar a classificação, será responsável por preencher e manter seus valores usando [Conjuntos de classificações](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html). O uso do **Nome do anúncio (variável)** não requer manutenção de classificação, mas você perde a relação 1:1 garantida entre o nome do anúncio e a dimensão [Anúncio](ad.md) principal. Use qualquer componente que seja compatível com seu fluxo de trabalho de implementação.

## Itens de dimensão

Cada item é o título de anúncio literal relatado em [início do anúncio](/help/implementation/events/ads/ad-start.md) (por exemplo, `"Ford F-150"`).
