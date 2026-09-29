---
title: Tipo de conteúdo
description: Relata o formato do fluxo (VOD, Ao vivo, Linear, podcast, música e assim por diante).
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
source-wordcount: '210'
ht-degree: 15%
---

# Tipo de conteúdo

>[!BEGINSHADEBOX]

*Esta página cobre a dimensão de relatório **Tipo de conteúdo**. Consulte [Tipo de conteúdo](/help/implementation/variables/core/content-type.md) para saber como coletar essa variável.*

>[!ENDSHADEBOX]

A dimensão **Tipo de conteúdo** informa o formato do fluxo (por exemplo, VOD, Live ou Linear para vídeo e música, podcast ou audiobook para áudio).

## Como essa dimensão é preenchida

O tipo de conteúdo é definido pelo reprodutor no início da sessão e transportado em cada evento. Não é derivado; o valor relatado corresponde ao que foi enviado durante a coleta.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.contentType` quando [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.contentType`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feeds de dados | `videocontenttype`, `post_videocontenttype` |
| Audience Manager | `c_contextdata.a.contentType` |

>[!IMPORTANT]
>
>Se o tipo de conteúdo não estiver definido ou estiver vazio, a dimensão relatará `missing_content_type` para a sessão. Use esse valor para encontrar implementações que precisam ser corrigidas.

## Itens de dimensão

Os valores definidos pela Adobe preenchem os segmentos e relatórios incorporados. Sequências personalizadas são aceitas, mas não corresponderão aos segmentos internos.

| Tipo de transmissão | Valores recomendados |
| --- | --- |
| Vídeo | `vod`, `live`, `linear`, `ugc`, `dvod` |
| Áudio | `song`, `podcast`, `audiobook`, `radio` |

## Segmentos recomendados

| Segmento | Regra |
| --- | --- |
| [!UICONTROL Conteúdo do VOD] | Tipo de conteúdo = `vod` |
| [!UICONTROL Conteúdo ao vivo] | Tipo de conteúdo = `live` |
| [!UICONTROL Conteúdo linear] | Tipo de conteúdo = `linear` |
