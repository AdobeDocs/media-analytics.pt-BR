---
title: Canal de conteúdo
description: Informa a estação de distribuição, rede ou propriedade em que cada sessão foi reproduzida.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 6%

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
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.channel` quando [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.channel`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feeds de dados | `videochannel, post_videochannel` |

>[!IMPORTANT]
>
>Se o canal não estiver definido, a dimensão não será preenchida para essa sessão.

## Itens de dimensão

Cada item é a sequência literal definida no início da sessão. Qualquer sequência de caracteres é aceita. Valores típicos são um nome de rede, uma parte de um caminho de site ou um identificador de propriedade interno.
