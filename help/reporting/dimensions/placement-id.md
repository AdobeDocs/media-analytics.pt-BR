---
title: ID de posicionamento
description: Relata o identificador de posicionamento para cada anúncio.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 9%

---


# ID de posicionamento

>[!BEGINSHADEBOX]

*Esta página aborda a **ID de posicionamento**&#x200B;dimensão de relatório. Consulte [ID de posicionamento](/help/implementation/variables/ads/placement-id.md) para saber como coletar essa variável.*

>[!ENDSHADEBOX]

A dimensão **Identificação de posicionamento** informa o identificador de posicionamento de anúncios (normalmente um slot ou zona definida na plataforma do servidor de anúncios). Use a dimensão para comparar engajamento e conclusão entre slots de posicionamento.

## Como essa dimensão é preenchida

A ID de posicionamento é definida pelo reprodutor em cada evento `media.adStart`.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Crie uma [Regra de processamento](https://experienceleague.adobe.com/pt-br/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) que mapeie `a.media.ad.placement` para uma eVar. |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.placementID`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Feeds de dados | `evar1`-`evar250`, `post_evar1`-`post_evar250` (a eVar para a qual sua regra de processamento mapeia `a.media.ad.placement`) |

## Itens de dimensão

Cada item é o valor de posicionamento literal relatado em `media.adStart`.
