---
title: Segmento de conteúdo
description: Informa o intervalo do indicador de reprodução exibido durante a sessão, em minutos.
feature: Dimensions
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '200'
ht-degree: 6%

---


# Segmento de conteúdo

A dimensão **Segmento de conteúdo** relata o intervalo do indicador de reprodução exibido durante uma sessão, em minutos (por exemplo, `[0-5]` para os minutos de 0 a 5). O back-end calcula o segmento a partir dos valores mínimos e máximos do indicador de reprodução relatados durante a reprodução. Use-a junto com a métrica [Visualizações do segmento de conteúdo](/help/reporting/metrics/content-segment-views.md) para analisar quais partes do conteúdo de forma longa os visualizadores realmente consomem.

## Como essa dimensão é preenchida

O segmento de conteúdo é calculado pelo back-end de mídia a partir dos valores do indicador de reprodução relatados nos eventos da sessão. Ele não é definido pelo cliente. O valor relatado é derivado dos valores do indicador de reprodução vistos durante a reprodução.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.segment` quando [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.segment`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feeds de dados | `videosegment`, `post_videosegment` |
| Audience Manager | `c_contextdata.a.media.segment` |

>[!IMPORTANT]
>
>Se o indicador de reprodução não for relatado corretamente durante a sessão, o segmento calculado pode ser impreciso. Para fluxos ao vivo, o segmento é calculado a partir dos valores relativos do indicador de reprodução vistos durante a sessão.

## Itens de dimensão

Cada item é um intervalo de cadeia de caracteres que abrange os valores do indicador de reprodução vistos durante uma sessão (por exemplo, `[0-5]`, `[5-10]`, `[10-15]`). A granularidade é fixa em cinco minutos.
