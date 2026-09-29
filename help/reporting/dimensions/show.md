---
title: Programa
description: Reporta o programa ou o nome de série do conteúdo de vídeo que faz parte de uma série.
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
source-wordcount: '158'
ht-degree: 10%
---

# Programa

>[!BEGINSHADEBOX]

*Esta página abrange a **Mostrar**&#x200B;dimensão de relatório. Consulte [Programa](/help/implementation/variables/standard-metadata/show.md) para saber como coletar essa variável.*

>[!ENDSHADEBOX]

A dimensão **Mostrar** informa o nome do programa ou da série. Episódios de várias temporadas se acumulam no mesmo item da linha de exibição, então, use-o para comparar o engajamento durante toda a vida útil de uma série.

## Como essa dimensão é preenchida

Mostrar é definido pelo reprodutor no início da sessão quando o conteúdo faz parte de uma série.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.show` quando os [[!UICONTROL Metadados de vídeo]](/help/reporting/setup/analytics-reporting.md) estão habilitados. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.show`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feeds de dados | `videoshow`, `post_videoshow` |
| Audience Manager | `c_contextdata.a.media.show` |

## Itens de dimensão

Cada item é o nome de exibição literal relatado no início da sessão (por exemplo, `"Blinding Light"`). Use nomes estáveis e distintos para cada exibição, de modo que os dados não sejam recolhidos em programas não relacionados que compartilham uma palavra.
