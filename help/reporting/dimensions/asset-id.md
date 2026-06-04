---
title: ID do ativo
description: Reporta um identificador estável do setor para o ativo de mídia subjacente.
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 2%

---


# ID do ativo

>[!BEGINSHADEBOX]

*Esta página aborda a **ID do ativo**dimensão de relatório. Consulte [ID do ativo](/help/implementation/variables/standard-metadata/asset-id.md) para saber como coletar essa variável.*

>[!ENDSHADEBOX]

A dimensão **ID do ativo** relata um identificador de setor estável para o ativo de mídia subjacente (normalmente um EIDR, TMS/Gracenote ou ID Rovi, mas as IDs proprietárias também são aceitas).

## Como essa dimensão é preenchida

A ID do ativo é definida pelo reprodutor no início da sessão.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics (regra de processamento) | Crie uma [Regra de processamento](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) que mapeie `a.media.asset` para uma eVar. |
| Adobe Analytics (classificação) | Classificação da dimensão [Conteúdo (ID)](content.md) — a Adobe cria automaticamente essa classificação quando os **[[!UICONTROL Metadados de vídeo]](/help/reporting/setup/analytics-reporting.md)** estão habilitados para o conjunto de relatórios. Você é responsável por preencher e manter os valores de classificação. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.assetID`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feeds de dados (regra de processamento) | `evar1`-`evar250`, `post_evar1`-`post_evar250` (a eVar para a qual sua regra de processamento mapeia `a.media.asset`) |
| Feeds de dados (classificação) | N/D — Os feeds de dados não aceitam classificações. |
| Audience Manager | `c_contextdata.a.media.asset` |

## Abordagem de classificação

O Adobe cria automaticamente a estrutura de classificação da ID de ativo quando os **[[!UICONTROL Metadados de vídeo]](/help/reporting/setup/analytics-reporting.md)** estão habilitados para o conjunto de relatórios. Você é responsável por preencher e manter a classificação usando [Conjuntos de classificações](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html).

Essa abordagem fornece um relacionamento :1 garantido entre cada ID de conteúdo e sua ID de ativo. As atualizações de classificação se aplicam retroativamente a todos os dados históricos dessa ID.

>[!IMPORTANT]
>
>Não altere o nome de classificação da ID de ativo. Renomeá-la pode fazer com que o Adobe recrie a classificação original, resultando em uma duplicata.

## Abordagem de regras de processamento

Crie uma [Regra de processamento](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) que mapeie `a.media.asset` para uma eVar. Essa abordagem captura a ID do ativo como um valor por ocorrência sem exigir manutenção de classificação.

A solução é que você perde o relacionamento 1:1 garantido entre a ID do ativo e a dimensão [Conteúdo (ID)](content.md) principal. Se a sua implementação enviar valores inconsistentes para a mesma ID de conteúdo em todos os eventos, várias IDs de ativos poderão aparecer no mesmo conteúdo. A atualização de um valor se aplica somente aos dados daquele ponto em diante.

## Itens de dimensão

Cada item é um valor de ID de ativo único reportado durante o período do relatório. Use um único identificador estável por ativo em todas as plataformas de distribuição para que o mesmo conteúdo seja acumulado até um único item de linha.
