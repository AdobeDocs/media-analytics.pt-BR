---
title: Classificação de conteúdo
description: Reporta a classificação de público-alvo conforme definido pelas Diretrizes de controle parental da TV ou por um sistema de classificação regional.
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
source-wordcount: '400'
ht-degree: 2%
---

# Classificação de conteúdo

>[!BEGINSHADEBOX]

*Esta página aborda a dimensão de relatório **Classificação de conteúdo**. Consulte [Classificação de conteúdo](/help/implementation/variables/standard-metadata/content-rating.md) para saber como coletar essa variável.*

>[!ENDSHADEBOX]

A dimensão **Classificação de conteúdo** informa a classificação de público-alvo de cada sessão. Use-a para comparar o engajamento e a carga de anúncios entre os níveis de classificação.

## Como essa dimensão é preenchida

A classificação de conteúdo é definida pelo reprodutor no início da sessão.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics (regra de processamento) | Crie uma [Regra de processamento](https://experienceleague.adobe.com/pt-br/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) que mapeie `a.media.rating` para uma eVar. |
| Adobe Analytics (classificação) | Classificação da dimensão [Conteúdo (ID)](content.md). O Adobe cria automaticamente essa classificação quando os **[[!UICONTROL Metadados de vídeo]](/help/reporting/setup/analytics-reporting.md)** estão habilitados para o conjunto de relatórios. Você é responsável por preencher e manter os valores de classificação. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.rating`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feeds de dados (regra de processamento) | `evar1`-`evar250`, `post_evar1`-`post_evar250` (a eVar para a qual sua regra de processamento mapeia `a.media.rating`) |
| Feeds de dados (classificação) | N/D — Os feeds de dados não aceitam classificações. |
| Audience Manager | `c_contextdata.a.media.rating` |

## Abordagem de classificação

O Adobe cria a estrutura de classificação de classificação de conteúdo automaticamente quando os **[[!UICONTROL Metadados de vídeo]](/help/reporting/setup/analytics-reporting.md)** estão habilitados para o conjunto de relatórios. Você é responsável por preencher e manter a classificação usando [Conjuntos de classificações](https://experienceleague.adobe.com/en/docs/analytics/components/classifications/sets/overview.html).

Essa abordagem fornece uma relação garantida 1:1 entre cada ID de conteúdo e sua classificação. As atualizações de classificação se aplicam retroativamente a todos os dados históricos dessa ID.

>[!IMPORTANT]
>
>Não altere o nome da classificação de classificação de conteúdo. Renomeá-la pode fazer com que o Adobe recrie a classificação original, resultando em uma duplicata.

## Abordagem de regras de processamento

Crie uma [Regra de processamento](https://experienceleague.adobe.com/pt-br/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) que mapeie `a.media.rating` para uma eVar. Essa abordagem captura a classificação de conteúdo como um valor por ocorrência sem exigir manutenção de classificação.

A solução é que você perde a relação 1:1 garantida entre a classificação de conteúdo e a dimensão [Conteúdo (ID)](content.md) principal. Se a sua implementação enviar valores inconsistentes para a mesma ID de conteúdo em todos os eventos, várias classificações poderão aparecer sob o mesmo conteúdo. A atualização de um valor se aplica somente aos dados daquele ponto em diante.

## Itens de dimensão

Cada item é o valor de classificação literal relatado no início da sessão (por exemplo, `"TVY"`, `"TVG"`, `"TVPG"`, `"TVMA"`). Mantenha um conjunto fixo de valores por sistema de classificação para evitar a fragmentação de itens de linha.
