---
title: Marcadores de progresso
description: Conte as sessões cujo indicador de reprodução ultrapassou cada um dos cinco limites fixos (10%, 25%, 50%, 75% e 95%).
feature: Metrics
role: User, Admin
source-git-commit: d223e36dcf7a906a3184f3602addbbb58c20ce13
workflow-type: tm+mt
source-wordcount: '542'
ht-degree: 9%

---


# Marcadores de progresso

Os **Marcadores de progresso** são cinco métricas separadas que contam sessões cujo indicador de reprodução ultrapassou cada um dos cinco limites fixos (10%, 25%, 50%, 75% e 95% da duração do conteúdo). Use-as para representar a lista suspensa no tempo de execução do conteúdo; emparelhe com [Início do conteúdo](content-starts.md) para calcular o compartilhamento de sessões iniciadas que atingiram cada marco.

Cada marcador é acionado uma vez por sessão e não é acionado novamente na busca de retorno. Os marcadores ignorados ao buscar para a frente não são contados (por exemplo, um visualizador que salta de 5% a 60% aciona os marcadores 10%, 25% e 50%, todos de uma só vez).

## Como cada marcador é calculado

O back-end de mídia avalia o indicador de reprodução relatado em relação à [Duração do conteúdo](../dimensions/content-length.md) após cada evento. Quando o indicador de reprodução ultrapassa um limite pela primeira vez, o sinalizador correspondente é definido para o restante da sessão. Todos os cinco marcadores são relatados na chamada de fechamento. As sessões que nunca produzem um evento de reprodução no conteúdo principal (como [Quedas antes do início](/help/reporting/metrics/drops-before-start.md)) nunca avançam o indicador de reprodução além de qualquer limite, portanto, nenhum marcador é definido.

>[!IMPORTANT]
>
>Os marcadores de progresso exigem um [Tamanho do conteúdo](/help/reporting/dimensions/content-length.md) diferente de zero e relatórios precisos de indicador de reprodução. Se o comprimento do conteúdo for indefinido, zero ou incorreto, os marcadores poderão ser acionados na hora errada ou não serão acionados.

### Marcador de progresso em 10% {#progress-10}

Acionado quando o indicador de reprodução atinge pela primeira vez 10% da duração do Conteúdo.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.progress10` quando [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.hasProgress10`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feeds de dados | `event_list`, `post_event_list` (consulte a pesquisa de [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.progress10` |

### Marcador de progresso em 25% {#progress-25}

Acionado quando o indicador de reprodução atinge pela primeira vez 25% da duração do Conteúdo.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.progress25` quando [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.hasProgress25`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feeds de dados | `event_list`, `post_event_list` (consulte a pesquisa de [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.progress25` |

### Marcador de progresso em 50% {#progress-50}

Acionado quando o indicador de reprodução atinge pela primeira vez 50% da duração do Conteúdo.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.progress50` quando [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.hasProgress50`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feeds de dados | `event_list`, `post_event_list` (consulte a pesquisa de [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.progress50` |

### Marcador de progresso em 75% {#progress-75}

Acionado quando o indicador de reprodução atinge pela primeira vez 75% da duração do Conteúdo.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.progress75` quando [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.hasProgress75`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feeds de dados | `event_list`, `post_event_list` (consulte a pesquisa de [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.progress75` |

### Marcador de progresso em 95% {#progress-95}

Acionado quando o indicador de reprodução atinge pela primeira vez 95% da duração do Conteúdo.

| Sistema de relatório | Origem |
| --- | --- |
| Adobe Analytics | Coletado automaticamente dos dados de contexto `a.media.progress95` quando [[!UICONTROL Media Core]](/help/reporting/setup/analytics-reporting.md) está habilitado. |
| Customer Journey Analytics | [`xdm.mediaReporting.sessionDetails.hasProgress95`](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/data-types/session-details-reporting) |
| Feeds de dados | `event_list`, `post_event_list` (consulte a pesquisa de [`event.tsv`](https://experienceleague.adobe.com/en/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-contents#lookup-files)) |
| Audience Manager | `c_contextdata.a.media.progress95` |
