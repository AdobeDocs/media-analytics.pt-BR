---
title: Comprimento do capítulo
description: Informa a duração de cada capítulo.
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
source-wordcount: '366'
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
| Adobe Analytics (classificação) | Classificação da dimensão [Capítulo](chapter.md). O Adobe cria automaticamente essa classificação quando **[[!UICONTROL Capítulos de mídia]](/help/reporting/setup/analytics-reporting.md)** está habilitado para o conjunto de relatórios. Você é responsável por preencher e manter os valores de classificação. |
| Customer Journey Analytics | [`xdm.mediaReporting.chapterDetails.length`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/chapter-details-reporting) |
| Feeds de dados (regra de processamento) | `evar1`-`evar250`, `post_evar1`-`post_evar250` (a eVar para a qual sua regra de processamento mapeia `a.media.chapter.length`) |
| Feeds de dados (classificação) | N/D — Os feeds de dados não aceitam classificações. |
| Audience Manager | `c_contextdata.a.media.chapter.length` |

## Abordagem de classificação

O Adobe cria automaticamente a estrutura de classificação de comprimento de capítulo quando **[[!UICONTROL Capítulos de mídia]](/help/reporting/setup/analytics-reporting.md)** está habilitado para o conjunto de relatórios. Você é responsável por preencher e manter a classificação usando [Conjuntos de classificações](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html).

Essa abordagem fornece uma relação 1:1 garantida entre cada ID de capítulo e seu comprimento. As atualizações de classificação se aplicam retroativamente a todos os dados históricos dessa ID.

>[!IMPORTANT]
>
>Não altere o nome de classificação Comprimento do capítulo. Renomeá-la pode fazer com que o Adobe recrie a classificação original, resultando em uma duplicata.

## Abordagem de regras de processamento

Crie uma [Regra de processamento](https://experienceleague.adobe.com/pt-br/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) que mapeie `a.media.chapter.length` para uma eVar. Essa abordagem captura o comprimento do capítulo como um valor por ocorrência sem exigir manutenção de classificação.

A compensação é que você perde a relação 1:1 garantida entre o comprimento do capítulo e a dimensão pai [Capítulo](chapter.md). Se a sua implementação enviar valores inconsistentes para a mesma ID de capítulo em todos os eventos, vários comprimentos poderão aparecer sob o mesmo capítulo. A atualização de um valor se aplica somente aos dados daquele ponto em diante.

## Itens de dimensão

Cada item é o valor de comprimento inteiro, em segundos, relatado em [início do capítulo](/help/implementation/events/chapters/chapter-start.md).
