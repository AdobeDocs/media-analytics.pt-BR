---
title: ID do site
description: Informa o identificador de site de anúncio para cada anúncio.
feature: Dimensions
role: User, Admin
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '150'
ht-degree: 10%

---


# ID do site

>[!BEGINSHADEBOX]

*Esta página aborda a **dimensão de relatório de ID do Site**. Consulte [ID do Site](/help/implementation/variables/ads/site-id.md) para saber como coletar essa variável.*

>[!ENDSHADEBOX]

A dimensão **ID do Site** informa o identificador de site de anúncio (normalmente uma ID da sua plataforma de servidor de anúncios). Use a dimensão para dividir o envolvimento por site de posicionamento de anúncio.

## Como essa dimensão é preenchida

A ID do site é definida pelo reprodutor a cada evento [ad start](/help/implementation/events/ads/ad-start.md).

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Crie uma [Regra de processamento](https://experienceleague.adobe.com/pt-br/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) que mapeie `a.media.ad.site` para uma eVar. |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.siteID`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Feeds de dados | `evar1`-`evar250`, `post_evar1`-`post_evar250` (a eVar para a qual sua regra de processamento mapeia `a.media.ad.site`) |
| Audience Manager | `c_contextdata.a.media.ad.site` |

## Itens de dimensão

Cada item é o valor de ID de site literal relatado em [início do anúncio](/help/implementation/events/ads/ad-start.md).
