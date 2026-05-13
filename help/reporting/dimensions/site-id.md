---
title: ID do site
description: Informa o identificador de site de anúncio para cada anúncio.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 9%

---


# ID do site

>[!BEGINSHADEBOX]

*Esta página aborda a **dimensão de relatório de ID do Site**. Consulte [ID do Site](/help/implementation/variables/ads/site-id.md) para saber como coletar essa variável.*

>[!ENDSHADEBOX]

A dimensão **ID do Site** informa o identificador de site de anúncio (normalmente uma ID da sua plataforma de servidor de anúncios). Use a dimensão para dividir o envolvimento por site de posicionamento de anúncio.

## Como essa dimensão é preenchida

A ID do site é definida pelo reprodutor em cada evento `media.adStart`.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Crie uma [Regra de processamento](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) que mapeie `a.media.ad.site` para uma eVar. |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.siteID`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Feeds de dados | `evar1`-`evar250`, `post_evar1`-`post_evar250` (a eVar para a qual sua regra de processamento mapeia `a.media.ad.site`) |

## Itens de dimensão

Cada item é o valor de ID de site literal relatado em `media.adStart`.
