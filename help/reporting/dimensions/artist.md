---
title: Artista
description: Informa o artista performático sobre o conteúdo de áudio.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '126'
ht-degree: 9%

---


# Artista

>[!BEGINSHADEBOX]

*Esta página aborda a dimensão de relatório **Artista**. Consulte [Artista](/help/implementation/variables/standard-metadata/artist.md) para saber como coletar essa variável.*

>[!ENDSHADEBOX]

A dimensão **Artista** informa o artista executante sobre o conteúdo de áudio (por exemplo, `"Crested Larks"`). Use-o para romper o engajamento em catálogos de música ou podcast por artista.

## Como essa dimensão é preenchida

Artista é definido pelo reprodutor no início da sessão para conteúdo de áudio.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.artist` quando os [[!UICONTROL Metadados de áudio]](/help/reporting/media-reports-enable.md) estão habilitados. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.artist`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feeds de dados | `videoaudioartist` |

## Itens de dimensão

Cada item é o nome literal do artista relatado no início da sessão. Use um nome estável e canônico por artista para que os dados não sejam fragmentados em variantes de formatação.
