---
title: Capítulo
description: Relata cada capítulo exclusivo reproduzido, digitado por uma ID de capítulo gerada automaticamente.
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
source-wordcount: '196'
ht-degree: 9%
---

# Capítulo

A dimensão **Capítulo** relata cada capítulo exclusivo reproduzido, digitado por uma ID de capítulo gerada automaticamente. A ID é criada pela SDK ou pelo back-end a partir da ID de conteúdo, do índice do capítulo e da hora de início do capítulo, de modo que duas sessões do mesmo capítulo no mesmo conteúdo são acumuladas em um único item de linha. Use a dimensão como chave de junção para classificações no nível do capítulo, como Nome do capítulo, Comprimento do capítulo, Deslocamento do capítulo e Posição do capítulo.

## Como essa dimensão é preenchida

A ID do capítulo é gerada automaticamente quando um evento de [início de capítulo](/help/implementation/events/chapters/chapter-start.md) é acionado. O valor não é definido diretamente; ele é derivado da posição, deslocamento e ID de conteúdo do capítulo.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.chapter.name` quando [[!UICONTROL Capítulos de mídia]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.chapterDetails.ID`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/chapter-details-reporting) |
| Feeds de dados | `videochapter`, `post_videochapter` |
| Audience Manager | N/D |

## Itens de dimensão

Cada item é uma ID de capítulo exclusiva. A ID é opaca (normalmente um hash de ID de conteúdo + índice + deslocamento) e é mais útil como uma chave de agrupamento. Emparelhe com [Nome do capítulo](chapter-name.md) para obter um rótulo amigável.
