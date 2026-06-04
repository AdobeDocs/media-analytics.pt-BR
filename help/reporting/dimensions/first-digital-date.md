---
title: Primeira data digital
description: Relata a data em que o conteúdo apareceu pela primeira vez em uma plataforma digital.
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 1%

---


# Primeira data digital

>[!BEGINSHADEBOX]

*Esta página aborda a **Primeira data digital**dimensão de relatório. Consulte [Primeira data digital](/help/implementation/variables/standard-metadata/first-digital-date.md) para saber como coletar essa variável.*

>[!ENDSHADEBOX]

A dimensão **Primeira data digital** informa a data em que o conteúdo apareceu pela primeira vez em uma plataforma digital. Use-o juntamente com a [Primeira data de transmissão](first-air-date.md) para comparar o tempo de lançamento digital com a transmissão original.

## Como essa dimensão é preenchida

A primeira data digital é definida pelo reprodutor no início da sessão.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics (regra de processamento) | Crie uma [Regra de processamento](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) que mapeie `a.media.digitalDate` para uma eVar. |
| Adobe Analytics (classificação) | Classificação da dimensão [Conteúdo (ID)](content.md) — a Adobe cria automaticamente essa classificação quando os **[[!UICONTROL Metadados de vídeo]](/help/reporting/setup/analytics-reporting.md)** estão habilitados para o conjunto de relatórios. Você é responsável por preencher e manter os valores de classificação. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.firstDigitalDate`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feeds de dados (regra de processamento) | `evar1`-`evar250`, `post_evar1`-`post_evar250` (a eVar para a qual sua regra de processamento mapeia `a.media.digitalDate`) |
| Feeds de dados (classificação) | N/D — Os feeds de dados não aceitam classificações. |
| Audience Manager | `c_contextdata.a.media.digitalDate` |

## Abordagem de classificação

O Adobe cria a primeira estrutura de classificação de data digital automaticamente quando os **[[!UICONTROL Metadados de vídeo]](/help/reporting/setup/analytics-reporting.md)** estão habilitados para o conjunto de relatórios. Você é responsável por preencher e manter a classificação usando [Conjuntos de classificações](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html).

Essa abordagem fornece uma relação garantida de :1 entre cada ID de conteúdo e sua primeira data digital. As atualizações de classificação se aplicam retroativamente a todos os dados históricos dessa ID.

>[!IMPORTANT]
>
>Não altere o nome da Primeira classificação de data digital. Renomeá-la pode fazer com que o Adobe recrie a classificação original, resultando em uma duplicata.

## Abordagem de regras de processamento

Crie uma [Regra de processamento](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) que mapeie `a.media.digitalDate` para uma eVar. Essa abordagem captura a primeira data digital como um valor por ocorrência sem exigir manutenção de classificação.

A solução é que você perde a relação garantida 1:1 entre a primeira data digital e a dimensão pai [Conteúdo (ID)](content.md). Se sua implementação enviar valores inconsistentes para a mesma ID de conteúdo em todos os eventos, várias primeiras datas digitais poderão aparecer sob o mesmo conteúdo. A atualização de um valor se aplica somente aos dados daquele ponto em diante.

## Itens de dimensão

Cada item é a sequência de data literal relatada no início da sessão. Use um formato consistente em todas as implementações. A Adobe recomenda `YYYY-MM-DD`.
