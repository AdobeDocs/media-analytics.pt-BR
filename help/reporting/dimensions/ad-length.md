---
title: Comprimento do anúncio
description: Relata a duração em segundos de cada anúncio.
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
source-wordcount: '195'
ht-degree: 7%
---

# Comprimento do anúncio

>[!BEGINSHADEBOX]

*Esta página abrange a **Comprimento do anúncio**dimensão de relatório. Consulte [Comprimento do anúncio](/help/implementation/variables/ads/ad-length.md) para saber como coletar essa variável.*

>[!ENDSHADEBOX]

A dimensão **Comprimento do anúncio** informa a duração em segundos de cada anúncio.

## Como essa dimensão é preenchida

O comprimento do anúncio é definido pelo reprodutor a cada evento [início de anúncio](/help/implementation/events/ads/ad-start.md).

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.ad.length` quando o [[!UICONTROL Media Ads]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.length`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Feeds de dados | `videoadlength`, `post_videoadlength` |
| Audience Manager | `c_contextdata.a.media.ad.length` |

No Adobe Analytics, essa dimensão aparece de duas maneiras: como **Comprimento do anúncio (variável)** (coletado diretamente de `a.media.ad.length`) e como **Comprimento do anúncio** (uma classificação derivada da dimensão [Anúncio](ad.md)). Se você usar a classificação, será responsável por preencher e manter seus valores usando [Conjuntos de classificações](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html). O uso de **Comprimento do anúncio (variável)** não requer manutenção de classificação, mas você perde a relação 1:1 garantida entre o comprimento do anúncio e a dimensão [Anúncio](ad.md) principal. Use qualquer componente que seja compatível com seu fluxo de trabalho de implementação.

## Itens de dimensão

Cada item é o valor literal de comprimento do anúncio, em segundos, reportado no [início do anúncio](/help/implementation/events/ads/ad-start.md).
