---
title: Mostrar tipo
description: Reporta o formato do conteúdo (episódio completo, pré-visualização, clipe ou outro).
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '143'
ht-degree: 10%

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
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.type` quando os [[!UICONTROL Metadados de vídeo]](/help/reporting/media-reports-enable.md) estão habilitados. |
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
