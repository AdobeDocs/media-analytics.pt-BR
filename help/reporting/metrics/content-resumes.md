---
title: Resumo de conteúdo
description: Conta as sessões que retomaram uma reprodução interrompida anteriormente.
feature: Metrics
role: User, Admin
source-git-commit: 031ecfceee8b2f200fd217c8b53232ff100a7002
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 9%

---


# Resumo de conteúdo

>[!BEGINSHADEBOX]

*Esta página aborda a métrica de relatórios **Resumo do conteúdo**. Consulte [Resumo do conteúdo](/help/implementation/variables/core/content-resumes.md) para saber como coletar essa variável.*

>[!ENDSHADEBOX]

A métrica **Resumo do conteúdo** conta sessões que retomaram uma reprodução interrompida anteriormente. Ele é incrementado quando o reprodutor sinaliza uma sessão como um currículo em `sessionStart` (por exemplo, depois de um buffer, pausa ou paralisação exceder 30 minutos). Use-a para separar novas sessões originais das sessões de continuação para o mesmo visualizador e ativo.

## Como essa métrica é calculada

O back-end de mídia define esse sinalizador quando `xdm.mediaCollection.sessionDetails.hasResume` é `true` no evento [início de sessão](/help/implementation/events/session/session-start.md). O reprodutor deve sinalizar explicitamente a sessão como um currículo. A métrica é relatada na chamada de fechamento.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.resume` quando [[!UICONTROL Media Core]](/help/reporting/media-reports-enable.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.hasResume`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feeds de dados | `event_list`, `post_event_list` (consulte a pesquisa de [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | N/D |
