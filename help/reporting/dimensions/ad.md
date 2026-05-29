---
title: Publicidade
description: Relata cada anúncio exclusivo reproduzido, digitado pela ID do anúncio.
feature: Dimensions
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '186'
ht-degree: 7%

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
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.ad.name` quando o [[!UICONTROL Media Ads]](/help/reporting/media-reports-enable.md) está habilitado. Persiste durante a visita. |
| Customer Journey Analytics | [`xdm.mediaReporting.advertisingDetails.name`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/advertising-details-reporting) |
| Feeds de dados | `videoad`, `post_videoad` |
| Audience Manager | `c_contextdata.a.media.ad.name` |

>[!IMPORTANT]
>
>A ID do anúncio é obrigatória. Se não estiver definido ou estiver vazio, o anúncio é descartado dos relatórios de anúncio de mídia de transmissão.

## Itens de dimensão

Cada item é um identificador de anúncio único reportado em [início do anúncio](/help/implementation/events/ads/ad-start.md). Use um identificador estável por criativo para que o mesmo anúncio seja acumulado até um único item de linha nas sessões.
