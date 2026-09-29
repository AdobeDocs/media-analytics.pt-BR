---
title: Episódio
description: Reporta o número do episódio em uma temporada.
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
source-wordcount: '132'
ht-degree: 12%
---

# Episódio

>[!BEGINSHADEBOX]

*Esta página cobre a dimensão de relatório **Episódio**. Consulte [Episódio](/help/implementation/variables/standard-metadata/episode.md) para saber como coletar essa variável.*

>[!ENDSHADEBOX]

A dimensão **Episódio** informa o número do episódio em uma temporada. Use-o junto com o [Show](show.md) e a [Temporada](season.md) para cancelar o engajamento no nível de episódio individual.

## Como essa dimensão é preenchida

O episódio é definido pelo reprodutor no início da sessão.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.episode` quando os [[!UICONTROL Metadados de vídeo]](/help/reporting/setup/analytics-reporting.md) estão habilitados. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.episode`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feeds de dados | `videoepisode`, `post_videoepisode` |
| Audience Manager | `c_contextdata.a.media.episode` |

## Itens de dimensão

Cada item é o valor literal do episódio relatado no início da sessão (normalmente um número inteiro como `"13"`). Os números de episódio por si só não são únicos em todas as estações; emparelhe com Temporada para separações inequívocas.
