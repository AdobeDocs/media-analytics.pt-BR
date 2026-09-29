---
title: Publicidade
description: Relata cada anúncio exclusivo reproduzido, digitado pela ID do anúncio.
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
source-wordcount: '188'
ht-degree: 8%
---

# Publicidade

>[!BEGINSHADEBOX]

*Esta página cobre a dimensão de relatório **Anúncio**. Consulte [ID do anúncio](/help/implementation/variables/ads/ad-id.md) para saber como coletar essa variável.*

>[!ENDSHADEBOX]

A dimensão **Anúncio** relata cada anúncio exclusivo reproduzido, digitado pela ID do anúncio definida em [início do anúncio](/help/implementation/events/ads/ad-start.md). A dimensão é o detalhamento principal para relatórios de anúncios e a chave de junção para classificações no nível do anúncio, como Nome do anúncio, Comprimento do anúncio e ID da Creative.

## Como essa dimensão é preenchida

O anúncio é definido pelo reprodutor em cada evento [início do anúncio](/help/implementation/events/ads/ad-start.md) como um identificador estável para o anúncio.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.ad.name` quando o [[!UICONTROL Media Ads]](/help/reporting/setup/analytics-reporting.md) está habilitado. Persiste durante a visita. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.name`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Feeds de dados | `videoad`, `post_videoad` |
| Audience Manager | `c_contextdata.a.media.ad.name` |

>[!IMPORTANT]
>
>A ID do anúncio é obrigatória. Se não estiver definido ou estiver vazio, o anúncio é descartado dos relatórios de anúncio de mídia de transmissão.

## Itens de dimensão

Cada item é um identificador de anúncio único reportado em [início do anúncio](/help/implementation/events/ads/ad-start.md). Use um identificador estável por criativo para que o mesmo anúncio seja acumulado até um único item de linha nas sessões.
