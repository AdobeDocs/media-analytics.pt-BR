---
title: Episódio
description: Reporta o número do episódio em uma temporada.
feature: Dimensions
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 10%

---


# Episódio

>[!BEGINSHADEBOX]

*Esta página cobre a dimensão de relatório **Episódio**. Consulte [Episódio](/help/implementation/variables/standard-metadata/episode.md) para saber como coletar essa variável.*

>[!ENDSHADEBOX]

A dimensão **Episódio** informa o número do episódio em uma temporada. Use-o junto com o [Show](show.md) e a [Temporada](season.md) para cancelar o engajamento no nível de episódio individual.

## Como essa dimensão é preenchida

O episódio é definido pelo reprodutor no início da sessão.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.episode` quando os [[!UICONTROL Metadados de vídeo]](/help/reporting/setup/analytics-reporting.md) estão habilitados. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.episode`](https://experienceleague.adobe.com/pt-br/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feeds de dados | `videoepisode`, `post_videoepisode` |
| Audience Manager | `c_contextdata.a.media.episode` |

## Itens de dimensão

Cada item é o valor literal do episódio relatado no início da sessão (normalmente um número inteiro como `"13"`). Os números de episódio por si só não são únicos em todas as estações; emparelhe com Temporada para separações inequívocas.
