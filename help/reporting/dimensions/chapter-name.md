---
title: Nome do capítulo
description: Exibe o título do capítulo legível.
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 2%

---


# Nome do capítulo

>[!BEGINSHADEBOX]

*Esta página aborda a dimensão de relatório **Nome do capítulo**. Consulte [Nome do capítulo](/help/implementation/variables/chapters/chapter-name.md) para saber como coletar essa variável.*

>[!ENDSHADEBOX]

A dimensão **Nome do capítulo** exibe o título legível de cada capítulo (por exemplo, `"Pilot Episode - Opening"`).

## Como essa dimensão é preenchida

O nome do capítulo é definido pelo reprodutor em cada evento de [início de capítulo](/help/implementation/events/chapters/chapter-start.md).

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics (regra de processamento) | Crie uma [Regra de processamento](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) que mapeie `a.media.chapter.friendlyName` para uma eVar. |
| Adobe Analytics (classificação) | Classificação da dimensão [Capítulo](chapter.md) — a Adobe cria automaticamente essa classificação quando **[[!UICONTROL Capítulos de mídia]](/help/reporting/setup/analytics-reporting.md)** está habilitado para o conjunto de relatórios. Você é responsável por preencher e manter os valores de classificação. |
| Customer Journey Analytics | [`xdm.mediaReporting.chapterDetails.friendlyName`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/chapter-details-reporting) |
| Feeds de dados (regra de processamento) | `evar1`-`evar250`, `post_evar1`-`post_evar250` (a eVar para a qual sua regra de processamento mapeia `a.media.chapter.friendlyName`) |
| Feeds de dados (classificação) | N/D — Os feeds de dados não aceitam classificações. |
| Audience Manager | `c_contextdata.a.media.chapter.friendlyName` |

## Abordagem de classificação

O Adobe cria a estrutura de classificação de nome de capítulo automaticamente quando **[[!UICONTROL Capítulos de mídia]](/help/reporting/setup/analytics-reporting.md)** está habilitado para o conjunto de relatórios. Você é responsável por preencher e manter a classificação usando [Conjuntos de classificações](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html).

Esta abordagem fornece uma relação 1:1 garantida entre cada ID de capítulo e seu nome amigável. As atualizações de classificação se aplicam retroativamente a todos os dados históricos dessa ID.

>[!IMPORTANT]
>
>Não altere o nome de classificação do nome do capítulo. Renomeá-la pode fazer com que o Adobe recrie a classificação original, resultando em uma duplicata.

## Abordagem de regras de processamento

Crie uma [Regra de processamento](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) que mapeie `a.media.chapter.friendlyName` para uma eVar. Essa abordagem captura o nome amigável como um valor por ocorrência sem exigir manutenção de classificação.

A compensação é que você perde a relação garantida 1:1 entre o nome do capítulo e a dimensão pai [Capítulo](chapter.md). Se a sua implementação enviar valores inconsistentes para a mesma ID de capítulo em todos os eventos, vários nomes poderão aparecer sob o mesmo capítulo. A atualização de um valor se aplica somente aos dados daquele ponto em diante.

## Itens de dimensão

Cada item é o título literal do capítulo relatado em [início do capítulo](/help/implementation/events/chapters/chapter-start.md).
