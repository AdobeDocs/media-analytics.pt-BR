---
title: Posição do capítulo
description: Informa o índice de cada capítulo dentro do conteúdo.
feature: Dimensions
role: User, Admin
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '366'
ht-degree: 2%

---


# Posição do capítulo

>[!BEGINSHADEBOX]

*Esta página aborda a **Posição do capítulo**&#x200B;da dimensão de relatório. Consulte [Posição do capítulo](/help/implementation/variables/chapters/chapter-position.md) para saber como coletar essa variável.*

>[!ENDSHADEBOX]

A dimensão **Posição do capítulo** informa o índice de cada capítulo dentro do conteúdo.

## Como essa dimensão é preenchida

A posição do capítulo é definida pelo reprodutor em cada evento de [início de capítulo](/help/implementation/events/chapters/chapter-start.md).

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics (regra de processamento) | Crie uma [Regra de processamento](https://experienceleague.adobe.com/pt-br/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) que mapeie `a.media.chapter.position` para uma eVar. |
| Adobe Analytics (classificação) | Classificação da dimensão [Capítulo](chapter.md) — a Adobe cria automaticamente essa classificação quando **[[!UICONTROL Capítulos de mídia]](/help/reporting/media-reports-enable.md)** está habilitado para o conjunto de relatórios. Você é responsável por preencher e manter os valores de classificação. |
| Customer Journey Analytics | [`mediaReporting.chapterDetails.index`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/chapter-details-reporting) |
| Feeds de dados (regra de processamento) | `evar1`-`evar250`, `post_evar1`-`post_evar250` (a eVar para a qual sua regra de processamento mapeia `a.media.chapter.position`) |
| Feeds de dados (classificação) | N/D — Os feeds de dados não aceitam classificações. |
| Audience Manager | `c_contextdata.a.media.chapter.position` |

## Abordagem de classificação

O Adobe cria a estrutura de classificação de posição de capítulo automaticamente quando **[[!UICONTROL Capítulos de mídia]](/help/reporting/media-reports-enable.md)** está habilitado para o conjunto de relatórios. Você é responsável por preencher e manter a classificação usando [Conjuntos de classificações](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html).

Esta abordagem fornece uma relação garantida de :1 entre cada ID de capítulo e sua posição. As atualizações de classificação se aplicam retroativamente a todos os dados históricos dessa ID.

>[!IMPORTANT]
>
>Não altere o nome de classificação da posição do capítulo. Renomeá-la pode fazer com que o Adobe recrie a classificação original, resultando em uma duplicata.

## Abordagem de regras de processamento

Crie uma [Regra de processamento](https://experienceleague.adobe.com/pt-br/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) que mapeie `a.media.chapter.position` para uma eVar. Essa abordagem captura a posição do capítulo como um valor por ocorrência sem exigir manutenção de classificação.

A compensação é que você perde a relação garantida 1:1 entre a posição do capítulo e a dimensão pai [Capítulo](chapter.md). Se a sua implementação enviar valores inconsistentes para a mesma ID de capítulo entre eventos, várias posições poderão aparecer sob o mesmo capítulo. A atualização de um valor se aplica somente aos dados daquele ponto em diante.

## Itens de dimensão

Cada item é o valor de posição inteiro relatado em [início do capítulo](/help/implementation/events/chapters/chapter-start.md).
