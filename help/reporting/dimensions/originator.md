---
title: Originador
description: Informa o criador ou estúdio de produção do conteúdo.
feature: Dimensions
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 2%

---


# Originador

>[!BEGINSHADEBOX]

*Esta página abrange a dimensão de relatório **Originador**. Consulte [Originador](/help/implementation/variables/standard-metadata/originator.md) para saber como coletar essa variável.*

>[!ENDSHADEBOX]

A dimensão **Originador** informa o criador ou estúdio de produção do conteúdo (por exemplo, `"Warner Brothers"` ou `"Sony"`). Use-a para comparar o engajamento entre proprietários de conteúdo ou titulares de direitos.

## Como essa dimensão é preenchida

O Originador é definido pelo reprodutor no início da sessão.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics (regra de processamento) | Crie uma [Regra de processamento](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) que mapeie `a.media.originator` para uma eVar. |
| Adobe Analytics (classificação) | Classificação da dimensão [Conteúdo (ID)](content.md) — a Adobe cria automaticamente essa classificação quando os **[[!UICONTROL Metadados de vídeo]](/help/reporting/media-reports-enable.md)** estão habilitados para o conjunto de relatórios. Você é responsável por preencher e manter os valores de classificação. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.originator`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feeds de dados (regra de processamento) | `evar1`-`evar250`, `post_evar1`-`post_evar250` (a eVar para a qual sua regra de processamento mapeia `a.media.originator`) |
| Feeds de dados (classificação) | N/D — Os feeds de dados não aceitam classificações. |
| Audience Manager | `c_contextdata.a.media.originator` |

## Abordagem de classificação

O Adobe cria a estrutura de classificação Originador automaticamente quando os **[[!UICONTROL Metadados de vídeo]](/help/reporting/media-reports-enable.md)** estão habilitados para o conjunto de relatórios. Você é responsável por preencher e manter a classificação usando [Conjuntos de classificações](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html).

Essa abordagem fornece uma relação garantida de :1 entre cada ID de conteúdo e seu originador. As atualizações de classificação se aplicam retroativamente a todos os dados históricos dessa ID.

>[!IMPORTANT]
>
>Não altere o nome de classificação do Originador. Renomeá-la pode fazer com que o Adobe recrie a classificação original, resultando em uma duplicata.

## Abordagem de regras de processamento

Crie uma [Regra de processamento](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) que mapeie `a.media.originator` para uma eVar. Essa abordagem captura o originador como um valor por ocorrência sem exigir manutenção de classificação.

A conclusão é que você perde a relação 1:1 garantida entre o originador e a dimensão [Conteúdo (ID)](content.md) principal. Se sua implementação enviar valores inconsistentes para a mesma ID de conteúdo em todos os eventos, vários originadores poderão aparecer no mesmo conteúdo. A atualização de um valor se aplica somente aos dados daquele ponto em diante.

## Itens de dimensão

Cada item é o valor literal do originador relatado no início da sessão. Use um nome estável e distinto por estúdio para que o engajamento não seja recolhido entre entidades não relacionadas.
