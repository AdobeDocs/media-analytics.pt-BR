---
title: ID de criação
description: Relata o identificador criativo do anúncio.
feature: Dimensions
role: User, Admin
source-git-commit: 415d20722965d510458d3c09004b6991b05ac264
workflow-type: tm+mt
source-wordcount: '374'
ht-degree: 2%

---


# ID de criação

>[!BEGINSHADEBOX]

*Esta página aborda a **Creative ID**&#x200B;dimensão de relatório. Consulte [Creative ID](/help/implementation/variables/ads/creative-id.md) para saber como coletar essa variável.*

>[!ENDSHADEBOX]

A dimensão **Creative ID** informa o identificador criativo do anúncio. Use a dimensão para acumular engajamento em anúncios que compartilham um criativo.

## Como essa dimensão é preenchida

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics (regra de processamento) | Crie uma [Regra de processamento](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) que mapeie `a.media.ad.creative` para uma eVar. |
| Adobe Analytics (classificação) | Classificação da dimensão [Anúncio](ad.md) — a Adobe cria automaticamente essa classificação quando o **[[!UICONTROL Anúncios de mídia]](/help/reporting/media-reports-enable.md)** está habilitado para o conjunto de relatórios. Você é responsável por preencher e manter os valores de classificação. |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.creativeID`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Feeds de dados (regra de processamento) | `evar1`-`evar250`, `post_evar1`-`post_evar250` (a eVar para a qual sua regra de processamento mapeia `a.media.ad.creative`) |
| Feeds de dados (classificação) | N/D — Os feeds de dados não aceitam classificações. |

## Abordagem de classificação

O Adobe cria a estrutura de classificação da Creative ID automaticamente quando o **[[!UICONTROL Anúncios de mídia]](/help/reporting/media-reports-enable.md)** está habilitado para o conjunto de relatórios. Você é responsável por preencher e manter a classificação usando [Conjuntos de classificações](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html).

Essa abordagem fornece uma relação garantida do :1 entre cada ID de anúncio e sua ID criativa. As atualizações de classificação se aplicam retroativamente a todos os dados históricos dessa ID.

>[!IMPORTANT]
>
>Não altere o nome de classificação da Creative ID. Renomeá-la pode fazer com que o Adobe recrie a classificação original, resultando em uma duplicata.

## Abordagem de regras de processamento

Crie uma [Regra de processamento](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) que mapeie `a.media.ad.creative` para uma eVar. Essa abordagem captura a ID criativa como um valor por ocorrência sem exigir manutenção de classificação.

A conclusão é que você perde a relação garantida 1:1 entre a ID criativa e a dimensão pai [Anúncio](ad.md). Se a sua implementação enviar valores inconsistentes para a mesma ID de anúncio em todos os eventos, várias IDs criativas poderão aparecer sob o mesmo anúncio. A atualização de um valor se aplica somente aos dados daquele ponto em diante.

## Itens de dimensão

Cada item é uma ID criativa exclusiva. Use um identificador estável por criativo para que o mesmo criativo acumule até um único item da linha em campanhas.
