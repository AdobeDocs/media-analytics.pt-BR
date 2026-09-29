---
title: Nome do conteúdo
description: Relata o título legível de cada sessão de mídia.
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
source-wordcount: '162'
ht-degree: 11%
---

# Nome do conteúdo

>[!BEGINSHADEBOX]

*Esta página abrange a dimensão de relatório **Nome do conteúdo**. Consulte [Nome do conteúdo](/help/implementation/variables/core/content-name.md) para saber como coletar essa variável.*

>[!ENDSHADEBOX]

A dimensão **Nome do conteúdo** informa o título legível de cada sessão de mídia.

## Como essa dimensão é preenchida

O nome amigável é definido pelo reprodutor no início da sessão. O valor relatado corresponde ao que foi enviado.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.friendlyName` quando [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.friendlyName`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feeds de dados | `videoname`, `post_videoname` |
| Audience Manager | `c_contextdata.a.media.friendlyName` |

>[!NOTE]
>
>No Adobe Analytics, este valor também corresponde a uma classificação de **Nome do vídeo** na dimensão [Conteúdo](content.md). Você é responsável por preencher e manter essa classificação separadamente. O Customer Journey Analytics usa essa dimensão diretamente.

>[!IMPORTANT]
>
>Se o nome do conteúdo não for definido, a dimensão será despreenchida para essa sessão.

## Itens de dimensão

Cada item é o título literal relatado no início da sessão (por exemplo, `"Blinding Light"`).
