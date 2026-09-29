---
title: Artista
description: Informa o artista performático sobre o conteúdo de áudio.
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
source-wordcount: '128'
ht-degree: 10%
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
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.artist` quando os [[!UICONTROL Metadados de áudio]](/help/reporting/setup/analytics-reporting.md) estão habilitados. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.artist`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feeds de dados | `videoaudioartist` |
| Audience Manager | `c_contextdata.a.media.artist` |

## Itens de dimensão

Cada item é o nome literal do artista relatado no início da sessão. Use um nome estável e canônico por artista para que os dados não sejam fragmentados em variantes de formatação.
