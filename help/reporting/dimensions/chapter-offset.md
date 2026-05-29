---
title: Deslocamento de capítulo
description: Informa o deslocamento de cada capítulo dentro do conteúdo.
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 2%

---


# Deslocamento de capítulo

>[!BEGINSHADEBOX]

*Esta página cobre a dimensão de relatório **Deslocamento de capítulo**. Consulte [Deslocamento de capítulo](/help/implementation/variables/chapters/chapter-offset.md) para saber como coletar essa variável.*

>[!ENDSHADEBOX]

A dimensão **Deslocamento do capítulo** informa o deslocamento de cada capítulo dentro do conteúdo, medido em segundos desde o início.

## Como essa dimensão é preenchida

O deslocamento de capítulo é definido pelo reprodutor em cada evento de [início de capítulo](/help/implementation/events/chapters/chapter-start.md).

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics (regra de processamento) | Crie uma [Regra de processamento](https://experienceleague.adobe.com/pt-br/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) que mapeie `a.media.chapter.offset` para uma eVar. |
| Adobe Analytics (classificação) | Classificação da dimensão [Capítulo](chapter.md) — a Adobe cria automaticamente essa classificação quando **[[!UICONTROL Capítulos de mídia]](/help/reporting/media-reports-enable.md)** está habilitado para o conjunto de relatórios. Você é responsável por preencher e manter os valores de classificação. |
| Customer Journey Analytics | [`xdm.mediaReporting.chapterDetails.offset`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/chapter-details-reporting) |
| Feeds de dados (regra de processamento) | `evar1`-`evar250`, `post_evar1`-`post_evar250` (a eVar para a qual sua regra de processamento mapeia `a.media.chapter.offset`) |
| Feeds de dados (classificação) | N/D — Os feeds de dados não aceitam classificações. |
| Audience Manager | `c_contextdata.a.media.chapter.offset` |

## Abordagem de classificação

O Adobe cria automaticamente a estrutura de classificação de deslocamento de capítulo quando **[[!UICONTROL Capítulos de mídia]](/help/reporting/media-reports-enable.md)** está habilitado para o conjunto de relatórios. Você é responsável por preencher e manter a classificação usando [Conjuntos de classificações](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html).

Esta abordagem fornece uma relação 1:1 garantida entre cada ID de capítulo e seu deslocamento. As atualizações de classificação se aplicam retroativamente a todos os dados históricos dessa ID.

>[!IMPORTANT]
>
>Não altere o nome da classificação de deslocamento do capítulo. Renomeá-la pode fazer com que o Adobe recrie a classificação original, resultando em uma duplicata.

## Abordagem de regras de processamento

Crie uma [Regra de processamento](https://experienceleague.adobe.com/pt-br/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) que mapeie `a.media.chapter.offset` para uma eVar. Essa abordagem captura o deslocamento do capítulo como um valor por ocorrência sem exigir manutenção de classificação.

A compensação é que você perde a relação garantida 1:1 entre o deslocamento do capítulo e a dimensão pai [Capítulo](chapter.md). Se a sua implementação enviar valores inconsistentes para a mesma ID de capítulo em todos os eventos, vários deslocamentos poderão aparecer sob o mesmo capítulo. A atualização de um valor se aplica somente aos dados daquele ponto em diante.

## Itens de dimensão

Cada item é o valor de deslocamento inteiro, em segundos, relatado em [início do capítulo](/help/implementation/events/chapters/chapter-start.md).
