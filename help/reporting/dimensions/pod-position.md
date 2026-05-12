---
title: Posição do pod
description: Relata o deslocamento de cada ad break no conteúdo.
feature: Dimensions
role: User, Admin
source-git-commit: 415d20722965d510458d3c09004b6991b05ac264
workflow-type: tm+mt
source-wordcount: '393'
ht-degree: 1%

---


# Posição do pod

>[!BEGINSHADEBOX]

*Esta página aborda a **Posição do pod**dimensão de relatório. Consulte [Hora de início do ad break](/help/implementation/variables/ads/ad-break-start-time.md) para saber como coletar essa variável.*

>[!ENDSHADEBOX]

A dimensão **Posição do pod** informa o deslocamento de cada ad break dentro do conteúdo, em segundos. Uma exibição anterior tem a posição `0`; as versões intermediárias têm posições correspondentes à hora de início do indicador de reprodução.

## Como essa dimensão é preenchida

A posição do pod é definida com base no valor de [Tempo de início de quebra de anúncio](/help/implementation/variables/ads/ad-break-start-time.md) definido pelo reprodutor em `media.adBreakStart`.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics (regra de processamento) | Crie uma [Regra de processamento](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) que mapeie `a.media.ad.podSecond` para uma eVar. |
| Adobe Analytics (classificação) | Classificação da dimensão [Pod de anúncio](ad-pod.md) — a Adobe cria automaticamente essa classificação quando o **[[!UICONTROL Anúncios de mídia]](/help/reporting/media-reports-enable.md)** está habilitado para o conjunto de relatórios. Você é responsável por preencher e manter os valores de classificação. |
| Customer Journey Analytics | [`mediaReporting.advertisingPodDetails.offset`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-pod-details-reporting) |
| Feeds de dados (regra de processamento) | `evar1`-`evar250`, `post_evar1`-`post_evar250` (a eVar para a qual sua regra de processamento mapeia `a.media.ad.podSecond`) |
| Feeds de dados (classificação) | N/D — Os feeds de dados não aceitam classificações. |

## Abordagem de classificação

O Adobe cria a estrutura de classificação Posição do pod automaticamente quando **[[!UICONTROL Anúncios de mídia]](/help/reporting/media-reports-enable.md)** está habilitado para o conjunto de relatórios. Você é responsável por preencher e manter a classificação usando [Conjuntos de classificações](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html).

Essa abordagem fornece uma relação garantida de :1 entre cada ID de pod de anúncio e sua posição. As atualizações de classificação se aplicam retroativamente a todos os dados históricos dessa ID.

>[!IMPORTANT]
>
>Não altere o nome de classificação da posição do pod. Renomeá-la pode fazer com que o Adobe recrie a classificação original, resultando em uma duplicata.

## Abordagem de regras de processamento

Crie uma [Regra de processamento](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) que mapeie `a.media.ad.podSecond` para uma eVar. Essa abordagem captura a posição do pod como um valor por ocorrência sem exigir manutenção de classificação.

A compensação é que você perde a relação garantida 1:1 entre a posição do pod e a dimensão pai [pod de anúncio](ad-pod.md). Se sua implementação enviar valores inconsistentes para a mesma ID de pod nos eventos, várias posições poderão ser exibidas no mesmo pod de anúncio. A atualização de um valor se aplica somente aos dados daquele ponto em diante.

## Itens de dimensão

Cada item é o valor de deslocamento inteiro (em segundos) informado em `media.adBreakStart`.
