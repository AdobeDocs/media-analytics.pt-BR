---
title: Autor
description: Relata o autor do conteúdo. Usado principalmente para audiolivros.
feature: Dimensions
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '119'
ht-degree: 11%

---


# Autor

>[!BEGINSHADEBOX]

*Esta página cobre a dimensão de relatório **Autor**. Consulte [Autor](/help/implementation/variables/standard-metadata/author.md) para saber como coletar essa variável.*

>[!ENDSHADEBOX]

A dimensão **Autor** informa o autor do conteúdo (por exemplo, `"Eleanor Clementine"`). Usado principalmente para audiolivros, mas também válido para podcasts cujo host ou produtor é a atribuição relevante.

## Como essa dimensão é preenchida

O autor é definido pelo reprodutor no início da sessão para conteúdo de áudio.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.author` quando os [[!UICONTROL Metadados de áudio]](/help/reporting/media-reports-enable.md) estão habilitados. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.author`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feeds de dados | `videoaudioauthor` |
| Audience Manager | `c_contextdata.a.media.author` |

## Itens de dimensão

Cada item é o nome literal do autor relatado no início da sessão.
