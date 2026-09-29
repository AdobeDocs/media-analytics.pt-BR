---
title: Temporada
description: Reporta o número da temporada do conteúdo episódico.
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
source-wordcount: '140'
ht-degree: 11%
---

# Temporada

>[!BEGINSHADEBOX]

*Esta página aborda a dimensão de relatório **Temporada**. Consulte [Temporada](/help/implementation/variables/standard-metadata/season.md) para saber como coletar essa variável.*

>[!ENDSHADEBOX]

A dimensão **Temporada** informa o número da temporada do conteúdo episódico. Use-o junto com o [Programa](show.md) e o [Episódio](episode.md) para fazer detalhamentos episódicos completos.

## Como essa dimensão é preenchida

A temporada é definida pelo reprodutor no início da sessão quando o conteúdo faz parte de uma série.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.season` quando os [[!UICONTROL Metadados de vídeo]](/help/reporting/setup/analytics-reporting.md) estão habilitados. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.season`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feeds de dados | `videoseason`, `post_videoseason` |
| Audience Manager | `c_contextdata.a.media.season` |

## Itens de dimensão

Cada item é o valor literal de temporada relatado no início da sessão (normalmente um número inteiro como `"1"`, `"2"`). Seja consistente em todos os episódios do mesmo programa; a dimensão não normaliza `"1"` e `"01"` para o mesmo item de linha.
