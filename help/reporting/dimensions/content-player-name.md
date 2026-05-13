---
title: Nome do reprodutor de conteúdo
description: Informa qual player renderizou cada sessão de mídia.
feature: Dimensions
role: User, Admin
source-git-commit: 186437a8669d2375caa9056dadd367ad7135f652
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 5%

---


# Nome do reprodutor de conteúdo

>[!BEGINSHADEBOX]

*Esta página aborda a **Nome do reprodutor de conteúdo**&#x200B;dimensão de relatório. Consulte [Nome do player de conteúdo](/help/implementation/variables/core/content-player-name.md) para saber como coletar essa variável.*

>[!ENDSHADEBOX]

A dimensão **Nome do player de conteúdo** informa qual player renderizou cada sessão de mídia (por exemplo, `HTML5 Player`, `Brightcove` ou `Roku Player`). Use-o para comparar engajamento, conclusão e qualidade entre os players na mesma propriedade.

## Como essa dimensão é preenchida

O nome do player é definido pelo player no início da sessão e persiste pela duração da sessão. O valor é enviado em cada evento e relatado no Adobe Analytics e no Customer Journey Analytics.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.playerName` quando [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.playerName`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feeds de dados | `videoplayername, post_videoplayername` |

>[!IMPORTANT]
>
>Se o nome do player não estiver definido, a dimensão não será preenchida para essa sessão. As sessões sem um nome de player não podem ser detalhadas por player nos relatórios.

## Itens de dimensão

Cada item é a sequência literal definida no início da sessão. Use um nome estável e distinto por player para que os dados de players diferentes não sejam recolhidos em um único item de linha.
