---
title: Autor
description: Relata o autor do conteúdo. Usado principalmente para audiolivros.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '117'
ht-degree: 10%

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

## Itens de dimensão

Cada item é o nome literal do autor relatado no início da sessão.
