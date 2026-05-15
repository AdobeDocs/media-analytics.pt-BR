---
title: Tipo de feed de mídia
description: Reporta o feed de transmissão (por exemplo, East-HD ou West-SD) quando o mesmo conteúdo é entregue por meio de vários feeds.
feature: Dimensions
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '157'
ht-degree: 7%

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
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.feed` quando os [[!UICONTROL Metadados de vídeo]](/help/reporting/media-reports-enable.md) estão habilitados. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.feed`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feeds de dados | `videofeedtype`, `post_videofeedtype` |
| Audience Manager | `c_contextdata.a.media.feed` |

## Itens de dimensão

Cada item é o valor de feed literal relatado no início da sessão. Use um conjunto estável de identificadores de feed por divisão regional ou de qualidade.
