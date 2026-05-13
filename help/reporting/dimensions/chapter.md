---
title: Capítulo
description: Relata cada capítulo exclusivo reproduzido, digitado por uma ID de capítulo gerada automaticamente.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 6%

---


# Capítulo

A dimensão **Capítulo** relata cada capítulo exclusivo reproduzido, digitado por uma ID de capítulo gerada automaticamente. A ID é criada pela SDK ou pelo back-end a partir da ID de conteúdo, do índice do capítulo e da hora de início do capítulo, de modo que duas sessões do mesmo capítulo no mesmo conteúdo são acumuladas em um único item de linha. Use a dimensão como chave de junção para classificações no nível do capítulo, como Nome do capítulo, Comprimento do capítulo, Deslocamento do capítulo e Posição do capítulo.

## Como essa dimensão é preenchida

A ID do capítulo é gerada automaticamente quando `media.chapterStart` é acionado. O valor não é definido diretamente; ele é derivado da posição, deslocamento e ID de conteúdo do capítulo.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.chapter.name` quando [[!UICONTROL Capítulos de mídia]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.chapterDetails.ID`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/chapter-details-reporting) |
| Feeds de dados | `videochapter, post_videochapter` |

## Itens de dimensão

Cada item é uma ID de capítulo exclusiva. A ID é opaca (normalmente um hash de ID de conteúdo + índice + deslocamento) e é mais útil como uma chave de agrupamento. Emparelhe com [Nome do capítulo](chapter-name.md) para obter um rótulo amigável.
