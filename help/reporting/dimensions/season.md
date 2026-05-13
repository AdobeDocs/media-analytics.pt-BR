---
title: Temporada
description: Reporta o número da temporada do conteúdo episódico.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '136'
ht-degree: 8%

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
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.season` quando os [[!UICONTROL Metadados de vídeo]](/help/reporting/media-reports-enable.md) estão habilitados. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.season`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feeds de dados | `videoseason, post_videoseason` |

## Itens de dimensão

Cada item é o valor literal de temporada relatado no início da sessão (normalmente um número inteiro como `"1"`, `"2"`). Seja consistente em todos os episódios do mesmo programa; a dimensão não normaliza `"1"` e `"01"` para o mesmo item de linha.
