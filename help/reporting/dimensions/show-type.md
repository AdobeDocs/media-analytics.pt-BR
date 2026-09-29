---
title: Mostrar tipo
description: Reporta o formato do conteúdo (episódio completo, pré-visualização, clipe ou outro).
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
source-wordcount: '145'
ht-degree: 11%
---

# Mostrar tipo

>[!BEGINSHADEBOX]

*Esta página cobre a dimensão de relatório **Mostrar tipo**. Consulte [Mostrar tipo](/help/implementation/variables/standard-metadata/show-type.md) para saber como coletar essa variável.*

>[!ENDSHADEBOX]

A dimensão **Mostrar tipo** informa o formato do conteúdo usando um código inteiro de cadeia de caracteres. Use-a para separar a visualização completa de programas do conteúdo curto, como trailers e clipes, ao medir o engajamento.

## Como essa dimensão é preenchida

O tipo de programa é definido pelo reprodutor no início da sessão.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.type` quando os [[!UICONTROL Metadados de vídeo]](/help/reporting/setup/analytics-reporting.md) estão habilitados. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.showType`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feeds de dados | `videoshowtype`, `post_videoshowtype` |
| Audience Manager | `c_contextdata.a.media.type` |

## Itens de dimensão

| Valor | Descrição |
| --- | --- |
| `0` | Episódio completo |
| `1` | Pré-visualização ou trailer |
| `2` | Clip |
| `3` | Outro |

Os valores são relatados como cadeias de caracteres. Valores personalizados são aceitos, mas não serão acumulados nos quatro compartimentos incorporados.
