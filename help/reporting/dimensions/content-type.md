---
title: Tipo de conteúdo
description: Relata o formato do fluxo (VOD, Ao vivo, Linear, podcast, música e assim por diante).
feature: Dimensions
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 9%

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
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.contentType` quando [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.contentType`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/session-details-reporting) |
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
