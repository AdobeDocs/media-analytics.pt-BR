---
title: ID de posicionamento
description: Relata o identificador de posicionamento para cada anúncio.
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
source-wordcount: '151'
ht-degree: 10%
---

# ID de posicionamento

>[!BEGINSHADEBOX]

*Esta página aborda a **ID de posicionamento**&#x200B;dimensão de relatório. Consulte [ID de posicionamento](/help/implementation/variables/ads/placement-id.md) para saber como coletar essa variável.*

>[!ENDSHADEBOX]

A dimensão **Identificação de posicionamento** informa o identificador de posicionamento de anúncios (normalmente um slot ou zona definida na plataforma do servidor de anúncios). Use a dimensão para comparar engajamento e conclusão entre slots de posicionamento.

## Como essa dimensão é preenchida

A ID de posicionamento é definida pelo reprodutor em cada evento [ad start](/help/implementation/events/ads/ad-start.md).

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Crie uma [Regra de processamento](https://experienceleague.adobe.com/pt-br/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) que mapeie `a.media.ad.placement` para uma eVar. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.placementID`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Feeds de dados | `evar1`-`evar250`, `post_evar1`-`post_evar250` (a eVar para a qual sua regra de processamento mapeia `a.media.ad.placement`) |
| Audience Manager | `c_contextdata.a.media.ad.placement` |

## Itens de dimensão

Cada item é o valor de posicionamento literal relatado em [início do anúncio](/help/implementation/events/ads/ad-start.md).
