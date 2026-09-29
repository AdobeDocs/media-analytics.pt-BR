---
title: Nome do reprodutor de conteúdo
description: Informa qual player renderizou cada sessão de mídia.
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
source-wordcount: '196'
ht-degree: 7%
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
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.playerName` quando [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.playerName`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feeds de dados | `videoplayername`, `post_videoplayername` |
| Audience Manager | `c_contextdata.a.media.playerName` |

>[!IMPORTANT]
>
>Se o nome do player não estiver definido, a dimensão não será preenchida para essa sessão. As sessões sem um nome de player não podem ser detalhadas por player nos relatórios.

## Itens de dimensão

Cada item é a sequência literal definida no início da sessão. Use um nome estável e distinto por player para que os dados de players diferentes não sejam recolhidos em um único item de linha.
