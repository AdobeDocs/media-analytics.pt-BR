---
title: Comprimento do capítulo
description: Informa a duração de cada capítulo.
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 2%

---


# Comprimento do capítulo

>[!BEGINSHADEBOX]

*Esta página cobre a dimensão de relatório **Comprimento do capítulo**. Consulte [Comprimento do capítulo](/help/implementation/variables/chapters/chapter-length.md) para saber como coletar essa variável.*

>[!ENDSHADEBOX]

A dimensão **Comprimento do capítulo** informa a duração de cada capítulo, em segundos.

## Como essa dimensão é preenchida

O comprimento do capítulo é definido pelo reprodutor a cada evento de [início de capítulo](/help/implementation/events/chapters/chapter-start.md).

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics (regra de processamento) | Crie uma [Regra de processamento](https://experienceleague.adobe.com/pt-br/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) que mapeie `a.media.chapter.length` para uma eVar. |
| Adobe Analytics (classificação) | Classificação da dimensão [Capítulo](chapter.md) — a Adobe cria automaticamente essa classificação quando **[[!UICONTROL Capítulos de mídia]](/help/reporting/media-reports-enable.md)** está habilitado para o conjunto de relatórios. Você é responsável por preencher e manter os valores de classificação. |
| Customer Journey Analytics | [`xdm.mediaReporting.chapterDetails.length`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/chapter-details-reporting) |
| Feeds de dados (regra de processamento) | `evar1`-`evar250`, `post_evar1`-`post_evar250` (a eVar para a qual sua regra de processamento mapeia `a.media.chapter.length`) |
| Feeds de dados (classificação) | N/D — Os feeds de dados não aceitam classificações. |
| Audience Manager | `c_contextdata.a.media.chapter.length` |

## Abordagem de classificação

O Adobe cria automaticamente a estrutura de classificação de comprimento de capítulo quando **[[!UICONTROL Capítulos de mídia]](/help/reporting/media-reports-enable.md)** está habilitado para o conjunto de relatórios. Você é responsável por preencher e manter a classificação usando [Conjuntos de classificações](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html).

Esta abordagem fornece uma relação 1:1 garantida entre cada ID de capítulo e seu comprimento. As atualizações de classificação se aplicam retroativamente a todos os dados históricos dessa ID.

>[!IMPORTANT]
>
>Não altere o nome de classificação Comprimento do capítulo. Renomeá-la pode fazer com que o Adobe recrie a classificação original, resultando em uma duplicata.

## Abordagem de regras de processamento

Crie uma [Regra de processamento](https://experienceleague.adobe.com/pt-br/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) que mapeie `a.media.chapter.length` para uma eVar. Essa abordagem captura o comprimento do capítulo como um valor por ocorrência sem exigir manutenção de classificação.

A compensação é que você perde a relação garantida 1:1 entre o comprimento do capítulo e a dimensão pai [Capítulo](chapter.md). Se a sua implementação enviar valores inconsistentes para a mesma ID de capítulo em todos os eventos, vários comprimentos poderão aparecer sob o mesmo capítulo. A atualização de um valor se aplica somente aos dados daquele ponto em diante.

## Itens de dimensão

Cada item é o valor de comprimento inteiro, em segundos, relatado em [início do capítulo](/help/implementation/events/chapters/chapter-start.md).
