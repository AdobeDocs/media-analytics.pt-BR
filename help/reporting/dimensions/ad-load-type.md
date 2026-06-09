---
title: Carregamentos de anúncios
description: Relata o tipo de carregamento de anúncio usado para cada sessão de mídia de transmissão.
feature: Dimensions
role: User, Admin
source-git-commit: e392a66367cbdd8ada2432a5d3762e805dae676c
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 7%

---


# Carregamentos de anúncios

>[!BEGINSHADEBOX]

*Esta página abrange a **Dimensão de relatório de carregamentos de anúncios**. Consulte [Tipo de carregamento do anúncio](/help/implementation/variables/standard-metadata/ad-load-type.md) para saber como coletar essa variável.*

>[!ENDSHADEBOX]

A dimensão **Anúncio carregado** relata o tipo de anúncio carregado no início de cada sessão de streaming de mídia. O valor é definido pelo cliente, permitindo que as organizações classifiquem as sessões por seu mecanismo de entrega de anúncios (por exemplo, `"linear"`, `"dynamic"` ou `"programmatic"`).

## Como essa dimensão é preenchida

O tipo de carregamento do anúncio é definido pelo reprodutor no início da sessão.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.adLoad` quando [[!UICONTROL Streaming de Mídia]](/help/reporting/setup/analytics-reporting.md) está configurado. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.adLoad`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feeds de dados | `videoadload`, `post_videoadload` |
| Audience Manager | `c_contextdata.a.media.adLoad` |

## Itens de dimensão

Cada item é a cadeia de caracteres do tipo literal e carga definida no início da sessão. Os valores não estão restritos a uma enumeração padrão. Defina uma taxonomia consistente em suas implementações para que os valores sejam acumulados de forma previsível nos relatórios.
