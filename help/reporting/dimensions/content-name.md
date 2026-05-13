---
title: Nome do conteúdo
description: Relata o título legível de cada sessão de mídia.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '158'
ht-degree: 8%

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
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.friendlyName` quando [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.friendlyName`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feeds de dados | `videoname, post_videoname` |

>[!NOTE]
>
>No Adobe Analytics, este valor também corresponde a uma classificação de **Nome do vídeo** na dimensão [Conteúdo](content.md). Você é responsável por preencher e manter essa classificação separadamente. O Customer Journey Analytics usa essa dimensão diretamente.

>[!IMPORTANT]
>
>Se o nome do conteúdo não for definido, a dimensão será despreenchida para essa sessão.

## Itens de dimensão

Cada item é o título literal relatado no início da sessão (por exemplo, `"Blinding Light"`).
