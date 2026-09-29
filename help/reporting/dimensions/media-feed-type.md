---
title: Tipo de feed de mídia
description: Reporta o feed de transmissão (por exemplo, East-HD ou West-SD) quando o mesmo conteúdo é entregue por meio de vários feeds.
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
source-wordcount: '159'
ht-degree: 8%
---

# Tipo de feed de mídia

>[!BEGINSHADEBOX]

*Esta página abrange a **Tipo de feed de mídia**&#x200B;dimensão de relatório. Consulte [Tipo de feed de mídia](/help/implementation/variables/standard-metadata/media-feed-type.md) para saber como coletar essa variável.*

>[!ENDSHADEBOX]

A dimensão **Tipo de feed de mídia** informa o feed de difusão de cada sessão (por exemplo, `"East-HD"`, `"West-SD"` ou `"4K"`). Use-o quando o mesmo conteúdo for entregue por meio de vários feeds regionais ou de qualidade, e o engajamento precisar ser relatado por feed.

## Como essa dimensão é preenchida

O tipo de feed de mídia é definido pelo reprodutor no início da sessão.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.feed` quando os [[!UICONTROL Metadados de vídeo]](/help/reporting/setup/analytics-reporting.md) estão habilitados. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.feed`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feeds de dados | `videofeedtype`, `post_videofeedtype` |
| Audience Manager | `c_contextdata.a.media.feed` |

## Itens de dimensão

Cada item é o valor de feed literal relatado no início da sessão. Use um conjunto estável de identificadores de feed por divisão regional ou de qualidade.
