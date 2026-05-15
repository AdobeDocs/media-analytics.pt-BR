---
title: Editor
description: Relata o editor do conteúdo de áudio.
feature: Dimensions
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '114'
ht-degree: 12%

---


# Editor

>[!BEGINSHADEBOX]

*Esta página abrange a dimensão de relatório **Publicador**. Consulte [Publicador](/help/implementation/variables/standard-metadata/publisher.md) para saber como coletar essa variável.*

>[!ENDSHADEBOX]

A dimensão **Editor** informa o editor de conteúdo de áudio (por exemplo, uma rede de podcast ou editor de audiobook). Use-a para comparar o engajamento entre editores em um catálogo de áudio com curadoria.

## Como essa dimensão é preenchida

O editor é definido pelo reprodutor no início da sessão para conteúdo de áudio.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.publisher` quando os [[!UICONTROL Metadados de áudio]](/help/reporting/media-reports-enable.md) estão habilitados. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.publisher`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feeds de dados | `videoaudiopublisher` |
| Audience Manager | `c_contextdata.a.media.publisher` |

## Itens de dimensão

Cada item é o nome literal do editor relatado no início da sessão.
