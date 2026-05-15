---
title: Programa
description: Reporta o programa ou o nome de série do conteúdo de vídeo que faz parte de uma série.
feature: Dimensions
role: User, Admin
source-git-commit: 034d7736c2f6e15592f4f6a0313c78275c4fea50
workflow-type: tm+mt
source-wordcount: '156'
ht-degree: 8%

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
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.show` quando os [[!UICONTROL Metadados de vídeo]](/help/reporting/media-reports-enable.md) estão habilitados. |
| Customer Journey Analytics | [`mediaReporting.sessionDetails.show`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feeds de dados | `videoshow`, `post_videoshow` |
| Audience Manager | `c_contextdata.a.media.show` |

## Itens de dimensão

Cada item é o nome de exibição literal relatado no início da sessão (por exemplo, `"Blinding Light"`). Use nomes estáveis e distintos para cada exibição, de modo que os dados não sejam recolhidos em programas não relacionados que compartilham uma palavra.
