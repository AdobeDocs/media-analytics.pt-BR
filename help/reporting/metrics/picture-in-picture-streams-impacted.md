---
title: Fluxos afetados pelo picture in picture
description: Conta as sessões em que o visualizador entrou no picture-in-picture pelo menos uma vez.
feature: Metrics
role: User, Admin
product_v2:
  - id: e55547f1-a1ff-40c6-8978-026e40ab7fa4
    internal-label: Analytics
feature_v2:
  - id: b3f03848-ae12-48b2-8aab-cad18567eb32
    internal-label: Metrics
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: beb51916dece77213e1b7346573c4377d62d2b2c
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 7%
---

# Fluxos afetados pelo picture in picture

>[!BEGINSHADEBOX]

*Esta página aborda a métrica de relatório **Fluxos afetados pela imagem na imagem**. Consulte [Picture in picture](/help/implementation/variables/player-state/picture-in-picture.md) para saber como coletar essa variável.*

>[!ENDSHADEBOX]

A métrica **Fluxos afetados pela métrica picture in picture** conta sessões em que o visualizador inseriu a reprodução picture in picture pelo menos uma vez. A métrica é um booliano em nível de sessão; várias entradas picture-in-picture na mesma contagem de sessão de um fluxo afetado. Para o volume total de entrada picture-in-picture, use [contagem de picture-in-picture](picture-in-picture-count.md).

## Como essa métrica é calculada

O back-end de mídia define esse sinalizador na primeira vez que um evento de início de estado picture-in-picture é recebido durante a sessão. A métrica é relatada na chamada de fechamento.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.states.pictureinpicture.set` quando o [[!UICONTROL Rastreamento do Estado do Player]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.states[]`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/media-reporting-details) entrada onde `name = "pictureInPicture"`, campo `isSet` |
| Feeds de dados | `event_list`, `post_event_list` (consulte a pesquisa de [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.states.pictureinpicture.set` |
