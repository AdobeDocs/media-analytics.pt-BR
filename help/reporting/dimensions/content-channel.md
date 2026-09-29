---
title: Canal de conteúdo
description: Informa a estação de distribuição, rede ou propriedade em que cada sessão foi reproduzida.
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
source-wordcount: '163'
ht-degree: 8%
---

# Canal de conteúdo

>[!BEGINSHADEBOX]

*Esta página cobre a dimensão de relatório **Canal de conteúdo**. Consulte [Canal de conteúdo](/help/implementation/variables/core/content-channel.md) para saber como coletar essa variável.*

>[!ENDSHADEBOX]

A dimensão **Canal de conteúdo** informa a estação de distribuição, a rede ou a propriedade em que cada sessão foi reproduzida. Use-a para dividir a reprodução por rede ou seção de uma propriedade.

## Como essa dimensão é preenchida

O canal é definido pelo reprodutor no início da sessão e persiste pela duração da sessão.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.channel` quando [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.channel`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feeds de dados | `videochannel`, `post_videochannel` |
| Audience Manager | `c_contextdata.a.media.channel` |

>[!IMPORTANT]
>
>Se o canal não estiver definido, a dimensão não será preenchida para essa sessão.

## Itens de dimensão

Cada item é a sequência literal definida no início da sessão. Qualquer sequência de caracteres é aceita. Valores típicos são um nome de rede, uma parte de um caminho de site ou um identificador de propriedade interno.
