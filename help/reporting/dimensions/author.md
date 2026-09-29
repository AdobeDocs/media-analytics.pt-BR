---
title: Autor
description: Relata o autor do conteúdo. Usado principalmente para audiolivros.
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
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.author` quando os [[!UICONTROL Metadados de áudio]](/help/reporting/setup/analytics-reporting.md) estão habilitados. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.author`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feeds de dados | `videoaudioauthor` |
| Audience Manager | `c_contextdata.a.media.author` |

## Itens de dimensão

Cada item é o nome literal do autor relatado no início da sessão.
