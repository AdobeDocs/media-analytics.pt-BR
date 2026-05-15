---
title: URL da arte
description: Relata o URL do ativo de cada criativo de anúncio.
feature: Dimensions
role: User, Admin
source-git-commit: 41cea9e0a166549f2f4b1cfbceb52ba2b16bf543
workflow-type: tm+mt
source-wordcount: '152'
ht-degree: 10%

---


# URL da arte

>[!BEGINSHADEBOX]

*Esta página abrange a **URL do Creative**&#x200B;dimensão de relatório. Consulte [URL do Creative](/help/implementation/variables/ads/creative-url.md) para saber como coletar essa variável.*

>[!ENDSHADEBOX]

A dimensão **URL do Creative** informa a URL do ativo de cada anúncio criativo. Use a dimensão quando o próprio URL for significativo para a análise (por exemplo, distinguir caminhos CDN ou versões criativas).

## Como essa dimensão é preenchida

A URL do Creative é definida pelo reprodutor a cada evento [ad start](/help/implementation/events/ads/ad-start.md).

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Crie uma [Regra de processamento](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/manage-report-suites/edit-report-suite/report-suite-general/processing-rules/pr-overview) que mapeie `a.media.ad.creativeURL` para uma eVar. |
| Customer Journey Analytics | [`mediaReporting.advertisingDetails.creativeURL`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Feeds de dados | `evar1`-`evar250`, `post_evar1`-`post_evar250` (a eVar para a qual sua regra de processamento mapeia `a.media.ad.creativeURL`) |
| Audience Manager | `c_contextdata.a.media.ad.creativeURL` |

## Itens de dimensão

Cada item é a cadeia de caracteres de URL literal informada em [ad start](/help/implementation/events/ads/ad-start.md).
