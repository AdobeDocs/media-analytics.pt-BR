---
title: Nome do pod
description: Relata o nome amigável de cada ad break. Colete-a no Adobe Analytics usando uma classificação ou uma regra de processamento personalizada.
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 1%

---


# Nome do pod

>[!BEGINSHADEBOX]

*Esta página aborda a dimensão de relatório **Nome do pod**. Consulte [Nome do ad break](/help/implementation/variables/ads/ad-break-name.md) para saber como coletar essa variável.*

>[!ENDSHADEBOX]

A dimensão **Pod name** informa o nome amigável de cada ad break (por exemplo, `"pre-roll"`, `"mid-roll-1"`). No Customer Journey Analytics, é uma dimensão discreta preenchida diretamente da variável de implementação. No Adobe Analytics, ela está disponível por meio de duas abordagens: uma classificação da dimensão [Pod de anúncio](ad-pod.md) ou uma eVar preenchida com uma regra de processamento.

## Como essa dimensão é preenchida

O nome do pod é originário do valor [Ad break name](/help/implementation/variables/ads/ad-break-name.md) que o player define em [ad break start](/help/implementation/events/ads/ad-break-start.md).

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics (regra de processamento) | Crie uma [Regra de processamento](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) que mapeie `a.media.ad.podFriendlyName` para uma eVar. |
| Adobe Analytics (classificação) | Classificação da dimensão Pod de anúncio — A Adobe cria automaticamente essa classificação quando o **[[!UICONTROL Media Ads]](/help/reporting/setup/analytics-reporting.md)** está habilitado para o conjunto de relatórios. Você é responsável por preencher e manter os valores de classificação. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingPodDetails.friendlyName`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-pod-details-reporting) |
| Feeds de dados (regra de processamento) | `evar1`-`evar250`, `post_evar1`-`post_evar250` (a eVar para a qual sua regra de processamento mapeia `a.media.ad.podFriendlyName`) |
| Feeds de dados (classificação) | N/D — Os feeds de dados não aceitam classificações. |
| Audience Manager | `c_contextdata.a.media.ad.podFriendlyName` |

## Abordagem de classificação

O Adobe cria automaticamente a estrutura de classificação Nome do pod quando **[[!UICONTROL Anúncios de mídia]](/help/reporting/setup/analytics-reporting.md)** está habilitado para o conjunto de relatórios. Você é responsável por preencher e manter a classificação usando [Conjuntos de classificações](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html).

Essa abordagem fornece uma relação 1:1 garantida entre cada ID de pod e seu nome amigável. As atualizações de classificação se aplicam retroativamente a todos os dados históricos dessa ID.

>[!IMPORTANT]
>
>Não altere o nome de classificação do nome do pod. Renomeá-la pode fazer com que o Adobe recrie a classificação original, resultando em uma duplicata.

## Abordagem de regras de processamento

Crie uma [Regra de processamento](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) que mapeie `a.media.ad.podFriendlyName` para uma eVar. Essa abordagem captura o nome amigável como um valor por ocorrência sem exigir manutenção de classificação.

A conclusão é que você perde a relação garantida 1:1 entre o nome do pod e a dimensão pai [pod de anúncio](ad-pod.md). Se sua implementação enviar valores inconsistentes para a mesma ID de pod nos eventos, vários nomes poderão aparecer no mesmo pod de anúncio. A atualização de um valor se aplica somente aos dados daquele ponto em diante.

## Itens de dimensão

Cada item é o nome de ad break literal relatado em [início de ad break](/help/implementation/events/ads/ad-break-start.md).
